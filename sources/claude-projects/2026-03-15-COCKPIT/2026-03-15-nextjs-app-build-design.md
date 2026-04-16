---
title: 2026-03-15-nextjs-app-build-design.md
project: COCKPIT
doc_uuid: 114918db-d021-483a-8069-1c73b2e5bd42
source: claude-project-doc
type: source
---

# OSA Connect — Next.js App Build: Design Spec
**Date:** 2026-03-15
**Author:** Solo founder (airline pilot)
**Status:** Approved
**Scope:** Full Next.js application implementing the 8-stage trip request flow (49 states) with customer-facing flow, admin surface, and semi-automated (human-in-the-loop) brokerage model.

---

## Context

OSA Connect is a private charter brokerage. The marketing website (`site/index.html`) is complete and brand-compliant. A full UX research package (personas, journey maps, competitive benchmarks, JTBD) and a complete developer handoff spec (`design/12-trip-request-handoff.md`) with 49-state machine (`design/11-trip-request-state-machine.md`) exist and are the source of truth for all interaction and visual decisions.

**Brokerage model for v1:** Semi-automated. Customers submit requests via the app. The founder sources aircraft manually and enters quote data via an admin surface. The customer-facing UX presents polished, real-time status updates throughout.

**Constraints:** Solo founder with a day job. Greenfield backend. No timeline pressure to take live bookings — build it right first.

---

## 1. Architecture

### Stack

| Layer | Choice | Rationale |
|---|---|---|
| Framework | Next.js 14 App Router | RSC for data-fetching pages; client components only where interactivity requires it |
| Database + Auth + Realtime | Supabase | PostgreSQL for state machine, Auth for customers + admin role, Realtime for live status updates, Storage for PDFs |
| Email | Resend | Transactional email (acknowledgment, quote, confirmation, flight brief) |
| Deploy | Vercel | Zero-config Next.js, preview deployments per PR |

### Two Surfaces, One Codebase

| Surface | Route prefix | Who accesses it |
|---|---|---|
| Marketing site | `/` | Public |
| Trip request flow | `/request` | Customers (authenticated) |
| Trip status tracker | `/trips/[id]` | Customers (authenticated) |
| Admin dashboard | `/admin` | Founder only (Supabase admin role) |

### State Machine Architecture

The 49 states from `design/11-trip-request-state-machine.md` map to a `status` enum on the `trip_requests` table. State transitions are Next.js Server Actions. Supabase Realtime pushes status changes to the customer's `/trips/[id]` page immediately — no polling, no refresh.

**Who advances state:**
- Customer actions (Stage 5 accept, Stage 6 confirm modal) → Server Action → database write → Realtime push
- Admin actions (acknowledge, send quote, confirm with operator, deliver invoice) → Server Action → database write → Realtime push
- System (session expiry, network state) → client-side detection → global state overlay

---

## 2. Data Model

### `trip_requests` — Primary state machine table

```sql
id                uuid PRIMARY KEY DEFAULT gen_random_uuid()
status            text NOT NULL  -- enum: all 49 state IDs from spec
created_at        timestamptz DEFAULT now()
updated_at        timestamptz DEFAULT now()
customer_id       uuid REFERENCES auth.users
booking_for       text  -- null = self; populated if EA booking for principal

-- Stage 1: customer-entered
origin            text
destination       text
depart_at         timestamptz
return_at         timestamptz  -- nullable (one-way)
pax_count         int
aircraft_class    text  -- 'Light' | 'Midsize' | 'Super-Mid' | 'Heavy'
catering_notes    text
special_requests  text

-- Stage 4: admin-entered (quote)
quote_base        numeric
quote_fees        numeric
quote_total       numeric
quote_aircraft    text
quote_operator    text
quote_expires_at  timestamptz
quote_locked      boolean DEFAULT false

-- Stage 7: admin-entered (operator confirmation)
fbo_origin        text
fbo_destination   text
tail_number       text
confirmed_at      timestamptz

-- Stage 8: admin-entered (post-flight)
invoice_total     numeric
invoice_matches   boolean
flight_brief_url  text  -- Supabase Storage URL
```

**Design decision:** No separate `quotes` table for v1. One quote per request; quote fields live on the request row. Extract to a `quotes` table in v2 when multi-quote presentation (Stage 4 multiple options) is needed.

### `state_transitions` — Append-only audit log

```sql
id            uuid PRIMARY KEY DEFAULT gen_random_uuid()
request_id    uuid REFERENCES trip_requests
from_status   text
to_status     text
actor         text  -- 'customer' | 'admin' | 'system'
note          text  -- optional admin note
created_at    timestamptz DEFAULT now()
```

Never updated — only inserted. Full audit trail for every request. Also serves as the invoice-to-quote match record (Tier 2 requirement from research synthesis).

### `traveler_profiles` — Pre-fill and retention layer

```sql
id                uuid REFERENCES auth.users PRIMARY KEY
preferred_class   text
fbo_preferences   jsonb  -- { region: fbo_name }
catering_defaults text
frequent_pax      jsonb  -- [{ name, title }]
saved_routes      jsonb  -- [{ origin, destination, label }]
```

Foundation for Stage 1 pre-fill and one-tap rebooking from Stage 8 (Tier 1 retention driver from research).

---

## 3. Customer-Facing Flow

All 8 stages. Entry point is `/request`; post-submission the customer lives at `/trips/[id]`.

### Stage 1 — `/request` — Trip Submission
Single-page multi-step form (5 steps: route → dates → pax + class → catering/notes → review). URL does not change; state lives in a client component. Pre-fills from `traveler_profiles` on load. On submit: creates `trip_requests` row at `S1.SUBMITTED`, fires acknowledgment email via Resend, redirects to `/trips/[id]`.

All states from `S1.IDLE` through `S1.SUBMITTED` implemented per state machine spec, including the full submit path: `S1.SUBMITTING` → `S1.SUBMIT_SLOW` (at 3s) → escalation (at 8s) → `S1.SUBMISSION_FAILED` (at 15s). Each threshold has distinct copy and a "Request by phone" ghost button fallback. `S1.DUPLICATE_DETECTED` intercept must also be implemented. See `design/11-trip-request-state-machine.md` Stage 1 for exact copy and UI signals at each threshold.

The Stage 1 form component must include a `localStorage` draft-save hook from the start (keyed by customer ID). This stub is required in Milestone 2 so that `G.SESSION_EXPIRED` draft restoration (Milestone 7) can wire in without reopening the form component.

### Stage 2 — `/trips/[id]` at `S2.*` — Acknowledgment
Status page with 8-stage progress tracker (`--osa-orange` active stage). Content: "Request received — we're sourcing aircraft now." + request summary card + estimated response window. Supabase Realtime subscription open — page updates live when status advances. No customer action required.

### Stage 3 — `/trips/[id]` at `S3.*` — Sourcing (internal only)
No new customer action. Progress tracker advances. MoT 1 timer displayed (`--osa-salmon` → `--osa-orange` as target window approaches). Content: "Sourcing aircraft — we'll have pricing for you shortly."

### Stage 4 — `/trips/[id]` at `S4.*` — Quote Presentation
Quote card appears when admin enters data and advances status. Displays: aircraft details, operator, all-in pricing breakdown (base + fees + total), price-lock badge (`--osa-purple`), quote expiry timer. Single CTA: "Review and accept →". Triggers live via Realtime when admin sends quote — customer does not need to refresh.

**v1 scope note:** The state machine defines `S4.MULTI_QUOTE` (side-by-side cards, comparison table, "OSA Recommended" badge). This state requires a separate `quotes` table and is deferred to v2. In v1, Stage 4 always renders a single quote card (`S4.SINGLE_QUOTE` path only). `S4.MULTI_QUOTE` is excluded from Milestone 7's "all 49 states" target.

### Stage 5 — `/trips/[id]` at `S5.*` — Quote Review
Expanded quote view: full aircraft spec, operator name, FBO details, catering confirmation, line-by-line pricing. Primary action: "Accept this flight" (advances to S6). Edge case: if Claire's booking exceeds the org spend threshold, the EA policy block intercept fires (`G.EA_POLICY_BLOCK`) before S6. No "request changes" action exists in Stage 5 — the state machine defines no S5→S3 transition. Accept triggers confirmation modal with dark gray (`--bg-gravity`) background and orange CTA.

### Stage 6 — `/trips/[id]` at `S6.*` — Accepted, Pending Operator
Gravity screen. Coolvetica headline: "Confirmed." Secondary copy: operator confirmation in progress. Dark background persists during wait state.

### Stage 7 — `/trips/[id]` at `S7.*` — Confirmed (MoT 2)
Hard commit screen. Coolvetica: "Your flight is confirmed." Full confirmation package: tail number, FBO (origin + destination), departure time, operator contact. Three export actions: download PDF (Supabase Storage), add to calendar (ICS), copy shareable trip card. Replaces screenshot-as-confirmation antipattern identified in research.

### Stage 8 — `/trips/[id]` at `S8.*` — Flight Brief + Post-Flight
Pre-departure: handler contacts, FBO instructions, weather note, tail reconfirmed. Post-flight (after admin marks wheels-down): Coolvetica "Trip complete." Invoice delivered with line-by-line quote comparison. Rebook CTA pre-fills Stage 1 from this trip's data.

### Global States (`G.*`)
Implemented as non-blocking banners or full-screen overlays per severity:
- `G.NETWORK_ERROR` / `G.NETWORK_RESTORED` — yellow/blue fixed top banner, auto-retry every 5s
- `G.SESSION_EXPIRED` — full-screen overlay, draft saved to localStorage, restored on re-auth
- `G.EA_POLICY_BLOCK` — intercept modal with approval chain
- `G.MAINTENANCE` — full-page dark background with ETA

All global states implemented per `design/11-trip-request-state-machine.md` for copy and behavior.

**Token arbitration note:** The state machine references `--osa-bg-dark` for full-page dark backgrounds (`G.MAINTENANCE`, Stage 6 gravity screen). This token is not defined in `design/12-trip-request-handoff.md`. Use `--bg-gravity` (defined as `var(--osa-dark)` in the handoff token list) for all full-page dark backgrounds. The state machine's `--osa-bg-dark` references are errors — the handoff token list is authoritative.

---

## 4. Admin Surface

Route prefix: `/admin`. Protected by Supabase Auth (admin role). Redirects unauthenticated users to `/`. No brand treatment required — functional ops tool only.

### `/admin` — Request Dashboard
Table of all `trip_requests` sorted by `updated_at` descending. Columns: request ID (mono), customer name, route, depart date, status badge (color-coded by stage), time in current state. Filterable by status. Row click → request detail.

### `/admin/requests/[id]` — Request Detail
Split layout. Left panel: full request data + `state_transitions` audit log. Right panel: action surface, changes based on current status.

**Action panel by stage:**

| Status | Admin action |
|---|---|
| `S1.SUBMITTED` | "Acknowledge" — one click, no data, advances to S2 |
| `S2.*` | "Mark as Sourcing" — optional internal note, advances to S3 |
| `S3.*` | "Send Quote" — aircraft, tail, operator, base, fees, total, expiry. Advances to S4. Customer sees quote instantly via Realtime. |
| `S4.*` / `S5.*` | Read-only. "Nudge customer" sends reminder email via Resend. |
| `S6.*` | "Confirm with Operator" — FBO origin/destination, tail reconfirmation, confirmed departure. Advances to S7. |
| `S7.*` | Edit FBO/tail if operator changes. On save: customer's `/trips/[id]` page shows an inline diff card highlighting the changed field(s) in `--diff-highlight` (`color-mix(in srgb, var(--osa-blue) 27%, transparent)`) with a "Changes to your flight" heading and a dismiss action. No state machine transition — request stays at `S7.*`. This satisfies Tier 1 item #7 from research synthesis (proactive disruption alerts). |
| `S8.IN_FLIGHT` | "Mark wheels-down" — advances to post-flight. |
| `S8.POST_FLIGHT` | "Deliver invoice" — final total, line items, upload flight brief PDF. |

All state transitions are Server Actions with optimistic UI. No page reloads.

### `/admin/customers/[id]` — Customer Profile
Read-only. `traveler_profile` + full booking history. Lookup tool for operator calls.

---

## 5. Delivery Sequence

Seven milestones. Each is a complete vertical slice — testable and deployable before the next begins.

### Milestone 1 — Foundation
**Build:** Next.js project, Supabase schema + auth, Vercel deploy.
**Done when:** Admin login works. Customer accounts work. Schema deployed.

### Milestone 2 — Request in, acknowledgment out
**Build:** Stage 1 form (all S1 states including submit timeout chain and duplicate detection), Stage 2 status page, admin dashboard list + "Acknowledge" action, Resend acknowledgment email.
**Done when:** Customer submits request → you see it in dashboard → you acknowledge → customer sees live update + email.
**Why first after foundation:** Proves the entire product plumbing (form → DB → Realtime → admin action → customer update) before building any additional stage.
**Note:** The Stage 1 form component must include the `localStorage` draft-save hook in this milestone, even though `G.SESSION_EXPIRED` full overlay ships in Milestone 7. Stub it now; wire it fully later.

### Milestone 3 — Quote delivery
**Build:** Stage 3 status page, Stage 4 quote display, admin quote entry form, Resend quote email.
**Done when:** You enter a quote → customer's page transforms to show pricing and accept CTA instantly.
**Unlock:** Product is technically quotable. Real requests could be taken after this milestone.

### Milestone 4 — Booking (launch-ready)
**Build:** Stage 5 review, Stage 6 acceptance + gravity screen, Stage 7 confirmation package, admin operator confirmation form, Resend confirmation email, PDF + ICS exports.
**Done when:** Customer accepts quote → you confirm → customer gets hard confirmation with tail, FBO, departure, PDF, and calendar invite.
**Unlock:** Stages 1–7 complete. Product is bookable end-to-end. Launch-ready state.

### Milestone 5 — Post-flight
**Build:** Stage 8 flight brief, admin wheels-down action, invoice delivery, post-flight invoice-to-quote comparison.
**Done when:** Full 8-stage loop closes. All three Moments of Truth covered.

### Milestone 6 — Retention layer
**Build:** Traveler profile pre-fill on Stage 1, saved routes, one-tap rebooking from Stage 8.
**Done when:** Returning customers recognized. Preferences pre-populated. Repeat routes surface as one-tap rebook.

### Milestone 7 — Polish
**Build:** All global states (G.*), full mobile responsive pass, accessibility audit.
**Done when:** All 49 states implemented per spec. Production-hardened.

---

## Design Rules

1. **Milestone discipline:** Do not start Milestone N+1 until Milestone N's vertical slice is complete and testable. No building forward over rough edges.
2. **No multi-quote table until v2.** Quote fields stay on `trip_requests` until multi-quote presentation is needed.
3. **Brand source of truth is `BRAND.md`.** All color, typography, and spacing decisions reference `BRAND.md` and `design/12-trip-request-handoff.md` — no deviation.
4. **State machine source of truth is `design/11-trip-request-state-machine.md`.** Do not add states, copy, or transitions without updating that document first.
5. **Admin surface has no brand requirements.** Functional over polished. Do not spend design time on the admin UI.
6. **Coolvetica is used in exactly 5 places.** As specified in `design/12-trip-request-handoff.md` section 2. No additions without design sign-off.
7. **`--osa-bg-dark` is not a valid token.** Any reference to `--osa-bg-dark` in the state machine document is an error. Use `--bg-gravity` for full-page dark backgrounds. The handoff token list (`design/12-trip-request-handoff.md` section 1) is the authoritative CSS dictionary.

---

## References

- Brand: `BRAND.md`
- State machine: `design/11-trip-request-state-machine.md`
- Developer handoff: `design/12-trip-request-handoff.md`
- Research synthesis: `research/08-synthesis-final.md`
- Personas: `research/01-personas.md`
- Competitive benchmark: `research/10-competitive-benchmark.md`

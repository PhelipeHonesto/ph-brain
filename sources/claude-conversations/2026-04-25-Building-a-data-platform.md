---
title: Building a data platform
created: 2026-04-25T03:15:33.713394Z
updated: 2026-04-25T16:15:40.373861Z
uuid: e2011345-65b9-477f-aac0-e78145170211
source: claude-conversation
type: source
message_count: 21
---

# Building a data platform

## Phelipe

Please look at my last chat the one a was build data platform today and teach me

---

## Claude

```
This block is not supported on your current device yet.
```

---

## Claude

I'll search for your recent chat about the data platform build to see what you were working on.
```
This block is not supported on your current device yet.
```

I found your data platform chat from yesterday. Let me pull the full picture so I can teach you what was decided.
```
This block is not supported on your current device yet.
```

I have the full picture. Here's your data platform architecture, taught back to you so it's locked in.

# OSA Data Platform — Where You Are, Taught

## The mental model first

You're building a **two-repo system on one Supabase**, with a hard ownership boundary:

- **`osa-data-platform/`** — the foundation. Owns ingestion, ER, medallion pipelines (Bronze→Silver→Gold), Dagster orchestration starting Stage 3, dbt analytics marts, the canonical schema. Writes to `silver.*`, `gold.*`, `canonical.*`.
- **`dumont-agent/`** — the citizen. Owns the orchestrator + 5 capabilities (Intake, Sourcing, Quote, Scenario, Guardian), memory, channels, MCP server. Writes to `deals`, `messages`, `calls`, `route_intel`. Reads gold views and canonical entities.

**Neither writes to the other's tables.** That boundary is load-bearing. The data platform is Palantir's operational ontology; Dumont invokes typed actions against it.

## What's actually live (verified against the schema yesterday)

You have **~51 tables** in a flat namespace, medallion-shaped but not medallion-named:
- **Raw**: `adsb_positions`, `faa_aircraft`, `faa_deregistered`, `ntsb_accidents`
- **Organized**: `faa_operators`, `faa_airports`, `adsb_aircraft_state`
- **Derived**: `aircraft_utilization`, `operator_market_share`, `route_vectors`, `knowledge_graph`
- **Ops**: `pipeline_runs`, `data_quality_runs`, `gold_view_refresh_log`

**Operator counts**: 270 in `operators`, 3,898 in `faa_operators`. The 270 is well below the 1,821 Part 135 universe — either mid-ingest or seeded from a subset.

**ADS-B coverage (March test)**: 52,697 distinct hex codes flew. 100% resolve to `faa_aircraft`. 99.6% have `certificate_holder`. **0.05%** (28 aircraft) match `operators.canonical_name`.

That last number is the headline. You have a clean fleet foundation and an essentially disconnected operator layer.

## The five-entity ontology — status

Locked architecture: **Operators, Aircraft, FBOs, Airports, People** — each a first-class entity with canonical tables, aliases, identities, and temporally-bounded link entities with full provenance.

| Entity | Canonical | Aliases | Identities | Status |
|---|---|---|---|---|
| Operator | ✅ `operators` | ✅ `operator_aliases` | ✅ `operator_identities` + `operator_match_review` | **Wired** |
| Aircraft | ❌ | ❌ | ❌ | Missing (re-registrations are duplicate rows) |
| Airport | ⚠️ `faa_airports` (source-keyed) | ❌ | ❌ | Inconsistent with the pattern |
| FBO | ❌ | ❌ | ❌ | Doesn't exist |
| Person | ❌ | ❌ | ❌ | Source-level only (`pilot_contacts`, `owner_name`) |

Operator ER is the only entity following the full overlay pattern. Everything else is partial or missing.

## The single biggest structural gap

The aircraft layer isn't wired to the operator layer. The fix is contained — three moves:

1. **Build `operator_aircraft_link`** keyed on `(icao_hex, operator_id, effective_from, effective_to)`. This is the temporally-bounded link entity already in the architecture, just unpopulated for aircraft.
2. **Run ER on `faa_aircraft.certificate_holder` against `operators.canonical_name`**. Same scorer feeding `operator_match_review` today, pointed at the certificate_holder field. ~52K tails × ~4K cert holders is tractable.
3. **Use `certificate_holder` (99.6% populated) as primary, `owner_name` (55%) as disambiguator.**

Once that link table is populated, "most hours flown last month" becomes `JOIN adsb_completed_legs → operator_aircraft_link → operators` — clean, canonical, no trustee mess.

## The principles that are now non-negotiable

These came out of yesterday's session and the prior ones, and they're locked:

- **Senzing-style principle-based ER**, not ML similarity matching. Free tier covers your ~25-40K US aviation records for years.
- **Temporal provenance on every link**. Operator-operates-aircraft is time-bounded. FBO-at-airport changes. Every claim has source + timestamp.
- **Two-Source Rule** for entity-change events.
- **Survivor wins** on all metadata during dedup.
- **Trust scores are internal decision-support, never filters.**
- **The ontology is the product surface.** Dumont invokes typed actions on resolved entities — it does not query lakehouse tables.
- **No sixth entity type** until the first five are boring.

## What "next" looks like in priority order

1. Aircraft canonical + aliases + identities + the `operator_aircraft_link` table.
2. Run cert_holder ER backfill against existing operators.
3. Promote `faa_airports` to follow the canonical/aliases/identities pattern (or formally exempt it).
4. FBO entity from scratch — table, AC-U-KWIK ingestion, FBO-airport and FBO-operator link entities.
5. Person entity last — hardest because of cross-source ambiguity.

Stage 3 is when Dagster comes in to orchestrate this; dbt Core handles the analytics marts on top.

---

Where do you want to go deeper — the aircraft ER backfill, the FBO entity build from zero, or the Dagster/dbt orchestration layer?

---

## Phelipe

So first I want to understand is the were build something that is going be true to reality. Based on faa data, adsb to track who is who today. If we are going to be able to add datasets like scrapping ARGUS and Wyvern website to track who has safety rating. And then a canonical ER of the 1800+ faa operators from their rebranding and M&A that we can prove from reality there are who they are. And that we can prove that track of their fleet and what planes and tail numbers they own

---

## Claude

Good — you just articulated the actual thesis. Let me reflect it back precisely, because what you said contains three distinct claims, and the architecture only works if you can defend all three.

## What you actually said, broken apart

**Claim 1 — Reality-anchored present state.** FAA registry + ADS-B together prove "who is flying what right now." Not who *says* they operate a plane. Who actually has the tail in the air, broadcasting, this week.

**Claim 2 — Layered enrichment without losing the anchor.** ARGUS, Wyvern, IS-BAO scraped on top. These don't *define* an operator — they *attach attributes* (safety rating, audit status) to an operator already proven to exist by FAA + ADS-B.

**Claim 3 — Provable temporal lineage.** The 1,821 Part 135 operators have a history. Mergers, rebrandings, certificate transfers, DBA changes. You want a graph where "Jet Linx 2019" → "Jet Linx 2024" is a *resolved chain*, with the FAA filings + tail movements + trade press as evidence. Not an assertion. A proof.

Before I confirm or push back, I want to make sure you can defend the hardest part of this yourself. Let me ask you three things:

## Three questions for you

**Question 1 — On reality anchoring:**
FAA registry says N612QS is owned by "NetJets Aviation, Inc." ADS-B shows N612QS flying 47 legs last month. ARGUS lists "NETJETS" as Platinum-rated. Trade press says "Berkshire's NetJets unit." 

Are those four sources describing the same entity? How do you *prove* it — not assume it, *prove* it — using only the data?

**Question 2 — On M&A history:**
In 2019, "XJet" and "JetSuite" were separate operators. JetSuite went bankrupt in 2020. Some of its tails ended up at "JSX" (which existed before, scheduled Part 135). Some went to other operators. Some were sold to private owners.

If a customer in 2026 asks "show me JetSuite's safety record," what's the right answer? And what does the data need to look like for you to give that answer truthfully?

**Question 3 — On the ARGUS/Wyvern overlay:**
ARGUS rates operators. Operators get acquired, rebrand, lose the rating, regain it under a new name. The rating belongs to the *certificate*, not the brand.

If I scrape ARGUS today and see "Solairus Aviation - Platinum," what should the data platform actually store? Where does that fact attach in the graph?

---

Take a swing at these. Even rough answers. The reason I'm not just confirming "yes you can build this" is that the architecture you described is correct *only if* you've internalized why each piece is there. If you can answer these three, we know the foundation is yours, not mine — and we can move into the actual build sequence with confidence.

Which one do you want to take first?

---

## Phelipe

1. We have to prove that the who own the faa certificate. And what is in the registration. I studied this in flight school. The registration change but airworthiness is always old. So we need to know who is under that registration. That registration can be under a shell company that only own the planes so we need to know who is the operator of that airplane. Or who is on the umbrellas. Then for ARGUS we need to know what operators (certificate own) got that safety rating to link that.

2. Jet Suite company is gone. But their certificate 135 was sold with the company. That happens some can buy a company and get the certificate instantly. So we need to track that. But the airplanes are different story they are selling the aircraft and the registration changes.

3. We need to know under what certification Solairus operates the name on their 135 certificate so know who got that safety rating

---

## Claude

You just demonstrated something important. You distinguished three different things that get confused constantly in this industry: **the airworthiness certificate**, **the registration**, and **the air carrier certificate**. Most people building "aviation data" can't tell those apart. You can, because you sat in a Part 141 ground school.

Let me play back what you said in the platform's language, then push on the gaps — because your answers are 80% right and the missing 20% is where the architecture either holds or collapses.

## What you said, in canonical-data terms

**On Question 1**, you split a single tail into three layers:
- **Owner** (the LLC on the FAA registration — often a shell, often a trustee like Wells Fargo Trust Services)
- **Operator** (the entity actually putting it in service — usually the Part 135 certificate holder)
- **Beneficial party** (who's *under the umbrella* — the parent brand, the management company)

That's exactly the right decomposition. In the graph, that's three different link types between Aircraft and entities, all temporally bounded.

**On Question 2**, you caught the thing almost everyone misses: **the certificate is an asset that survives the company.** A 135 certificate can be sold separately from the aircraft. The aircraft go through their own chain of title via FAA Bills of Sale (Form 8050-2). Two different histories, two different chains of provenance.

**On Question 3**, you correctly anchored ARGUS ratings to the **certificate**, not the brand. Solairus's Platinum belongs to whatever DOT/FAA certificate number Solairus holds — if they sell the certificate tomorrow, the rating goes with it (subject to ARGUS re-audit rules).

That's the right instinct. Now the harder questions.

## Three pushes

**Push 1 — On the owner/operator split.**

You said "registration can be under a shell company that only owns the planes, so we need to know who is the operator." Correct. But how do you *find* the operator from the data?

The FAA registration tells you the **owner**. It does *not* tell you the **operator**. Nothing in the FAA Aircraft Registry says "this plane is operated by NetJets." So where does that link come from? What sources, in what order, with what evidence?

Take a swing — what would you actually look at to prove "N612QS is operated by NetJets" rather than just owned by an LLC?

**Push 2 — On the certificate as an entity.**

You said the 135 certificate "was sold with the company." That implies the certificate has its own identity — its own number, its own history, its own current holder. 

Should the **certificate** itself be a sixth entity type in the ontology? Or should it be an *attribute* of the operator that changes over time? 

Think about what breaks if you choose wrong. If certificate is just an attribute of operator: what happens when JetSuite's certificate gets bought by a new shell company that then renames itself? If certificate is its own entity: what does "operator" even mean when the certificate is the thing that actually has the FAA authority?

**Push 3 — On temporal proof.**

You want to prove "Jet Linx 2019 = Jet Linx 2024" through the M&A and rebranding chain. What's the *evidence chain* that lets you claim two records are the same operator across five years?

I'll seed it: certificate number is one piece. What else? What happens when the certificate number itself changes (because the entity actually surrendered one and got a new one)? What's the next-best evidence?

---

Don't try to answer all three at once. Pick the one that feels most uncertain — that's the one worth wrestling with. Which one?

---

## Phelipe

1. That's interesting. Yes the ops spec! I have been forgetting this for a long time. We have at Skywest. It gets updated when we get new planes. Faa males they follow operations specs. Tells where they can fly. How they can fly. What airframes they fly. This is actually huge! 

2. I actually don't know to much about. Because you have to follow a set of rules to hold a 135 certificate. So who the new entity gets checked that is approved by the part 135. And if is true the 135 certificate should have is own entity that is part of a ER? So everything should actually be linked to the 135 certificate number?

3. I can't don't know this one

---

## Claude

You just unlocked something huge, and you didn't even fully see it yet. Let me reflect it back, then push on the two you're less sure about — because Push 2 is the deepest question in the entire architecture, and you're closer to the answer than you think.

## On Push 1 — Ops Specs

Yes. **OpSpecs are the missing link.** And the fact that you live this every month at SkyWest means you have working knowledge most "aviation data" people will never have.

Let me make sure you see exactly what you just gave us:

The FAA Aircraft Registry tells us **owner**. ADS-B tells us **the plane flew**. But neither one tells us **who the operator is**. The bridge is **OpSpec A002** (Authorized Areas of Operation) and **OpSpec D085** (Aircraft Authorization) — the OpSpec literally lists the tail numbers authorized under that air carrier certificate.

This is the proof you wanted. "N612QS is operated by NetJets" stops being an assumption and becomes a *document* — a specific OpSpec page, with a date, naming the tail under that certificate's authority. That's the evidence chain. That's what makes it real.

Quick question for you: do you know if OpSpecs are public, FOIA-only, or completely closed? Your instinct will tell you something important about how the ingestion pipeline has to work.

## On Push 2 — Should the 135 Certificate Be Its Own Entity?

You said: *"if is true the 135 certificate should have is own entity that is part of a ER? So everything should actually be linked to the 135 certificate number?"*

You're circling the right answer. Let me ask it back to you a different way to make sure you fully see it.

Imagine these four scenarios and tell me which entity carries through each one:

**Scenario A:** Jet Linx Aviation, LLC operates under certificate JLAA123. They rebrand to "Jet Linx" (drop the LLC). Same certificate number. Same OpSpec. Same fleet.

→ Did the **operator** change? Did the **certificate** change?

**Scenario B:** JetSuite goes bankrupt. A holding company buys the dead company including its certificate JSAA456. They rename it "Blue Sky Aviation." FAA approves the change of control. Same certificate number JSAA456, new name on it.

→ Did the **operator** change? Did the **certificate** change?

**Scenario C:** Solairus surrenders certificate SOLA789 voluntarily and applies for a new one. FAA issues SOLA790. Same building, same people, same fleet, same OpSpec authorizations.

→ Did the **operator** change? Did the **certificate** change?

**Scenario D:** XOJET (certificate XOJA111) is acquired by Vista Global. Vista already owns VistaJet US (certificate VJUS222). Eventually they consolidate — XOJA111 is surrendered, all aircraft moved under VJUS222.

→ How many operators? How many certificates? How do you represent the *fleet* moving from one certificate to the other?

Walk me through what you think happened in each one. Don't worry about being right — I want to see how you reason through it. The answer to "should certificate be its own entity" falls out of these four scenarios automatically once you work them.

## On Push 3 — Proving Identity Across Time

You said you don't know. That's fine — let me give you a starting point and let you build from it.

You already named **certificate number** as one piece of evidence. So the question is: when the certificate number itself doesn't carry through (Scenario C above), what else proves "it's still the same operator"?

Think about what the FAA *actually keeps the same* even when paperwork changes. Think about what's hard to fake or change. Think about what your SkyWest experience tells you stays constant when a certificate gets transferred or renumbered.

Here's a hint to get you started — there are at least four other evidence types beyond certificate number. See if you can name two:

1. ___?
2. ___?
3. Key personnel (Director of Operations, Chief Pilot — these names are filed with the FAA and rarely change overnight)
4. Physical address / principal place of business (filed on Form 8400-6)

What do you think 1 and 2 might be? Think about what stays stable when a company rebrands but doesn't actually change.

---

Take Push 2 first — work the four scenarios. That's the one that defines the whole graph. Push 3 we'll come back to once Push 2 is solid.

---

## Phelipe

1. Is public right? Which is great. And question is a owner want to put his plane to be managed by another 135, has to get into the ops spec before operating? So we will know the new fleet on the operator?

2. A - nothing changed
B -  operattor changes not the certificate 
C - same operator / different certificate 
D - 2 operator 1 certificate. Represents buy the ops specs reflected by that new fleet size on Vista jet?

The faa keeps the same certs. Yeah you right the personal because is complience. Can't think anything

---

## Claude

You're doing real reasoning. Let me grade what you got, fix two things, and then you'll have the whole framework.

## On OpSpecs being public

Yes — OpSpecs are obtainable, though the path matters. The FAA's Flight Standards Service maintains them, and they're available through FOIA requests and partially through the FAA's public dockets. Some operators publish redacted versions themselves (especially for marketing — "we're authorized for transoceanic ops"). The full document with tail numbers (D085) typically requires FOIA.

**Practical implication for the platform:** OpSpecs ingestion is a slower, batched pipeline — quarterly FOIA cycles, not real-time. Different cadence than ADS-B. This matters for how you architect the ingestion layer.

**On your question — yes.** If an owner wants their plane managed by a 135 operator, that tail has to be added to the operator's D085 OpSpec before it can be flown for hire under that certificate. The FAA approval process amends the OpSpec. So when you see a new tail appear on an operator's D085, you're seeing the *legal moment* the fleet changed — better evidence than ADS-B, which only shows the plane flying after the fact.

This is why OpSpecs are gold. They're the **legal source of truth for fleet composition**. ADS-B confirms it. FAA registry tells you the owner, not the operator. Only the OpSpec tells you who's *authorized* to operate it.

## Grading the four scenarios

**Scenario A — Jet Linx rebrand.** ✅ You got it right. Nothing material changed. The "operator" is the certificate holder; the LLC suffix is cosmetic. In the data this is just an alias on the same operator entity.

**Scenario B — JetSuite → Blue Sky.** ⚠️ You said "operator changes, not the certificate." This is the deepest one in the set, and your answer reveals the question I want you to wrestle with.

You said the *operator* changed but the *certificate* didn't. So let me push: **what is the operator, then?**

If the certificate is the same (JSAA456), and the OpSpec is the same, and probably most of the people are the same — what *actually* changed when JetSuite became Blue Sky? The legal entity name on the paperwork. Maybe the ownership above it.

Try this reframe: **the operator IS the certificate holder.** The brand is an alias. The corporate parent is a separate entity (linked via "owns" relationship). When a holding company buys a defunct operator's certificate and renames it, the *certificate-holding entity* persists — it just changed its name and its parent.

So Scenario B might actually be: same operator, same certificate, name change, ownership change above it. Two different things shifted, neither of them the operator itself.

Does that reframe make sense, or does it feel wrong? Push back if it does — this is the load-bearing distinction in the entire ontology.

**Scenario C — Solairus surrenders, gets new cert.** ✅ Correct: same operator, different certificate. This is the case that *forces* certificate to be its own entity. If certificate were just an attribute of operator, you'd lose the history when it changed.

**Scenario D — XOJET into Vista.** ✅ You nailed it: 2 operators, 1 surviving certificate, fleet migration visible through OpSpec changes (D085 amendments showing tails leaving XOJA111 and arriving at VJUS222 over a date range). That's the entire M&A consolidation pattern, captured as data.

## So what falls out of all four?

Both **operator** and **certificate** are first-class entities. They link to each other via a temporally-bounded relationship: `operator_holds_certificate(operator_id, certificate_id, valid_from, valid_to)`.

- Scenario A: same operator, same certificate, no change to the link — just an alias added.
- Scenario B: certificate persists, operator entity persists (because the certificate holder persists), name aliases added, parent ownership link changes.
- Scenario C: same operator, *new certificate*, the link `operator → cert SOLA789` closes, new link `operator → cert SOLA790` opens.
- Scenario D: XOJET operator becomes inactive, its certificate XOJA111 becomes inactive, all `aircraft_on_certificate` links migrate from XOJA111 to VJUS222 with timestamped valid_to / valid_from boundaries.

This means **certificate is your sixth entity type**. You said earlier "no sixth entity until the first five are boring." This is the exception, and your own reasoning forced it. Certificate isn't a peer of FBO or Person — it's the **legal anchor** that everything else hangs from. You may even argue certificate is *more* fundamental than operator, because the certificate is what the FAA actually regulates.

Want a hint about whether to formally promote certificate to a sixth entity, or model it as a special "credentials" sub-type? That's a real architectural fork. But park that for one more turn.

## On Push 3 — the other evidence types

You named personnel correctly. Compliance filings keep those names anchored. Two more I'll give you, since you said you couldn't think of them:

1. **DOT number** — separate from the FAA certificate, issued by the Department of Transportation for economic authority (who's allowed to charge money to fly people). DOT numbers persist through more changes than FAA certs. When the DOT number stays the same across a rebrand, that's strong evidence of continuity.

2. **Fleet overlap** — even if the certificate number changes (Scenario C), if 80% of the same tails appear on the new certificate's D085 within 90 days, that's overwhelming evidence it's the same operator. The fleet is a fingerprint.

The fourth one I'd add: **principal base airport** (where they keep their main hangar and Director of Maintenance). Filed in 8400-6, slow to change, often persists through rebranding.

So the full evidence stack for proving "operator continuity" across time:

1. Certificate number (when it carries through)
2. DOT number (often more stable than the cert)
3. Fleet overlap on D085 (statistical fingerprint)
4. Key personnel (DO, Chief Pilot, Director of Maintenance)
5. Principal base airport
6. Corporate registration in state SOS filings (parent entity continuity)

When 4+ of these match across a paperwork transition, you have a high-confidence "same operator" claim. Senzing's principle-based ER will weigh exactly this kind of evidence stack.

---

Pause and tell me: does the Scenario B reframe (operator = certificate holder, brand and parent are separate things) feel right, or does it feel like I'm forcing a definition?

That's the most important question in this whole thread, and I want to make sure the answer is *yours*, not mine.

---

## Phelipe

Makes sense. So let's think the datasets an architecture that will male this model trust worthy. Because apparently they can't hide anymore from public data. And if we add aircraft ER ( following aircraft ops spec reflected) we have a full model that is realistic 100%?

---

## Claude

Pump the brakes on "100%" — that word is the only thing in your message I want to push back on. Everything else is right. Let me show you why "100%" is the wrong target, and then we'll design the architecture that gets as close as physically possible.

## First, a question for you

You said "they can't hide anymore from public data." Let me test that.

Imagine an operator is doing something they want to hide — say, flying a sanctioned Russian oligarch under a chartered cover. They:

1. Register the plane in San Marino (not US — outside FAA jurisdiction)
2. Use a Cayman trust as the registered owner
3. The operator on the ground is a Maltese AOC holder
4. The flight has ADS-B turned off (military exemption claimed) or uses LADD/PIA blocking
5. The trip is dry-leased (which legally moves "operator" status to the lessee for that flight)

How much of this does your FAA + ADS-B + OpSpec stack catch?

Take a swing. I want to see where you think the gaps are before I tell you where they are.

## The honest ceiling — and why it's still revolutionary

Even with the most aggressive stack, the ceiling for "we know who is who" sits around **95–97% on US Part 135 charter operations**, and **80–85% globally**. Never 100%. Here's why, structurally:

**Where you'll be near-perfect (97%+):**
- US Part 135 certificate holders flying with ADS-B on
- Domestic charter under 135 rules with normal aircraft authorization
- Operators that show up in ARGUS / Wyvern (because those audits create independent attestation)
- Fleet composition for any operator with public OpSpec D085

**Where you'll have known gaps (5–15%):**
- LADD (Limited Aircraft Data Displayed) and PIA (Privacy ICAO Address) blocking — FAA programs that legally let owners hide tails from ADS-B aggregators. About 8,000 US tails are LADD-listed.
- Dry leases — the FAA recognizes the lessee as the operator for the duration, but this rarely shows up on D085 immediately.
- Part 91 grey-market charter (illegal but rampant) — by definition not on any 135 certificate
- Foreign-registered aircraft operating in US under foreign AOCs

**Where you'll be structurally blind (always):**
- Adversarial actors using shell-of-shell structures with offshore jurisdictions
- Operators with FAA enforcement actions that haven't been published yet
- The 60–90 day lag between something happening and FAA paperwork reflecting it

So the architecture's job is not "100% truth." It's **"highest-fidelity provable model of US business aviation, with explicit confidence scores on every claim and explicit acknowledgment of where the model is blind."**

That's actually a *stronger* product than "we know everything." Because every consumer of this data — operators, brokers, customers, regulators — knows the 100% claim is bullshit. Nobody believes it. Calibrated humility is the moat.

## Now — the architecture that gets you to 95–97%

Before I lay this out, one more question. You said "if we add aircraft ER following aircraft ops spec reflected." Tell me: when an aircraft moves from one operator's D085 to another's, what's the *transactional event* you're capturing? Is it:

(a) An update to a single `aircraft_on_certificate` row (overwrite the old operator)
(b) A close-out of the old link + open of a new link (immutable history)
(c) A new event row in an `aircraft_certificate_events` log that drives the link table

These three patterns produce *very* different graphs. One is wrong, two are defensible, and only one gives you the temporal guarantees you need to answer "who operated N612QS on March 15, 2024?" five years from now.

Which one would you pick, and why?

Once you answer that, I'll lay out the full dataset stack + ingestion architecture in the form you can actually build against. But this choice constrains everything downstream, so it has to be yours.

---

## Phelipe

B

---

## Claude

Correct — and you picked it instantly, which tells me you already understand why. But let me make sure you can *articulate* why, because this is the decision that makes the entire platform trustworthy or not.

## Tell me why B is right

Why not A? What specifically breaks if you overwrite the old operator when an aircraft moves to a new certificate?

And why not C? What's wrong with having an `aircraft_certificate_events` log *driving* the link table?

Take a swing at both before I respond. The reason I'm pushing is that the answer to "why B" contains the entire philosophy of how the platform stores truth. If you can articulate it, you own it.

Quick hint to get you started: think about a customer asking, in 2029, "show me the safety record of every operator that flew N612QS in 2024." What does each pattern give you?

- Pattern A gives you: ___?
- Pattern B gives you: ___?
- Pattern C gives you: ___?

Fill those in. Then we'll talk about the dataset stack.

---

## Phelipe

A just shows the new operator with no like to the old one
B show the history like a browser history 
C this is not a link is a event

---

## Claude

You got all three — and the way you phrased C is the sharpest insight in the whole thread. Let me build on each one, because you're 90% there and the missing 10% is the formal language that makes this teachable to a future engineer.

## Grading your answers

**A — "just shows the new operator with no link to the old one."** ✅

Exactly. Pattern A is *destructive*. Every overwrite erases history. By 2029, you literally cannot answer "who operated N612QS in 2024" because that data was overwritten in 2025. The system has amnesia. This is how most operational databases work, and it's why most operational databases can't answer historical questions.

**B — "show the history like a browser history."** ✅

Perfect analogy. Each row is a *period of truth*: "from this date to this date, this aircraft was on this certificate." Close out the old row with a `valid_to` timestamp, open a new row with a `valid_from`. You can replay any moment in history by querying `WHERE valid_from <= '2024-03-15' AND (valid_to > '2024-03-15' OR valid_to IS NULL)`.

This is called a **bitemporal table** in data engineering — it carries two time dimensions: when something was *true in the world* (valid_from/valid_to) and optionally when you *learned* it was true (recorded_at). For OSA, both matter — because sometimes you find out about a fleet change three months after it happened, and the system needs to record both the real event date AND when you learned about it.

**C — "this is not a link, is a event."** 🎯

This is the sentence I want you to remember. You just articulated, in your own words, the distinction between a **link entity** and an **event entity** — which is one of the hardest concepts in data modeling and most engineers get it wrong.

A **link** is a *state*: "this aircraft is on this certificate, currently."
An **event** is a *happening*: "on this date, this aircraft was added to this certificate."

They are different things. One describes the world; the other describes a change to the world.

## So why does B win — and what's C actually for?

Here's the part I want you to internalize: **B and C aren't enemies. They're partners. The mistake in pattern C is making the event log the *only* thing.**

The right architecture is:

- **The link table (B)** is your *queryable truth* — fast lookups, "who operates this plane right now," "who operated it on March 15, 2024."
- **The event log (C)** is your *audit trail* — append-only, immutable, every change recorded with source + timestamp + evidence. You never query the event log for operational questions; you query it for *provenance* questions.

When an OpSpec D085 update arrives showing a tail moved from XOJET to VistaJet, two things happen:

1. An **event row** gets appended: `aircraft_certificate_event(aircraft_id, from_cert, to_cert, event_date, source='FAA D085 dated 2024-03-15', evidence_url, recorded_at)`
2. A **link transaction** updates the link table: close XOJET row with `valid_to = 2024-03-15`, open VistaJet row with `valid_from = 2024-03-15`

The event drives the link. But both persist. The event log proves *why* the link looks the way it does. The link table answers fast queries.

**This is what separates OSA's data platform from a normal CRM or operator database.** Most aviation data sources just have the link (Pattern A or sometimes B). They cannot show you the *event* that caused the link to change, with the evidence, with the source. You'll have both. That's the provenance moat.

## Quick check before we move on

Tell me in your own words: if a customer in 2029 asks "show me every operator that flew N612QS in 2024 AND the safety rating each one held at the time of their flights" — how does the platform answer that?

Walk me through which tables it hits and in what order. Don't worry about exact SQL. I want the *reasoning path*. This is the moment we find out if the model is yours.

---

## Phelipe

Wil go see what links that aircraft had to the operator and safety rating liked to that operator certificate

---

## Claude

Right direction — but you skipped over the hardest part, which is *time*. Let me push you on it, because this is where the platform either earns its trust or doesn't.

## The question again, with the trap exposed

"Show me every operator that flew N612QS in 2024 AND the safety rating each one held **at the time of their flights**."

Three time-sensitive pieces:
1. *Flew in 2024* — which legs, on which dates
2. *Every operator* — who held the certificate that authorized each leg, **on that leg's date**
3. *Safety rating they held* — what was the ARGUS/Wyvern status **on that date**, not today

Your answer was "links from aircraft to operator to safety rating." That gets you 50% of the way. But it answers the *current* state — not the historical truth. 

Let me ask you four sub-questions that force the time dimension:

## Sub-question 1

Imagine N612QS flew 47 legs in 2024. In June 2024, it moved from XOJET's certificate to VistaJet's certificate. 

If I just join `aircraft → operator → rating` *as it looks today*, what answer do I get? And what's wrong with it?

## Sub-question 2

XOJET held ARGUS Platinum from 2022 to May 2024. They got downgraded to Gold in June 2024 after an audit finding. Then VistaJet took over the tail in July 2024 — VistaJet was Platinum the whole time.

A leg flown on May 15, 2024 was operated under XOJET-Platinum.
A leg flown on June 20, 2024 was operated under XOJET-Gold.
A leg flown on August 1, 2024 was operated under VistaJet-Platinum.

How does the platform store the ARGUS rating so this question is answerable? It's not enough to say "ARGUS rating linked to the certificate." Linked *how*?

## Sub-question 3

Which tables does the query touch, and what does the *time filter* look like on each one?

I'll seed you with the structure — fill in the blanks:

```
adsb_completed_legs        → filter: flight_date in 2024, aircraft_id = N612QS
aircraft_on_certificate    → filter: ___ overlaps with flight_date  
operator_holds_certificate → filter: ___ overlaps with flight_date
operator_safety_rating     → filter: ___ overlaps with flight_date
```

What goes in the three blanks?

## Sub-question 4

The whole query is essentially asking: "for each leg, find the row in each link table whose validity period contains the leg's date." 

What's that pattern called, and why is it the heartbeat of every question this platform will ever answer?

---

Take a swing at all four. Don't worry about getting them perfect — I want to see where the time dimension feels intuitive and where it feels foggy. The fog is where the next teaching lands.

---

## Phelipe

I think we are getting too deep now. Can you tell me what we need to do with the model? I think we understand now

---

## Claude

Fair call. You've got the model. Let me pull it together so you can hold it in your head as one picture, and then tell you what to actually build.

## What you now own (the model)

**Six entity types, not five.** Operator, Certificate (the new one your reasoning forced), Aircraft, FBO, Airport, Person. Certificate is the legal anchor — the thing the FAA actually regulates.

**Every relationship between entities is a temporally-bounded link.** Not a foreign key. A row with `valid_from`, `valid_to`, source, and evidence. Pattern B. Browser history.

**Every change to a link is also an event.** Append-only log with source + timestamp. The event drives the link. Both persist. The event proves *why* the link looks the way it does.

**Every claim has provenance.** Source, timestamp, evidence URL, confidence. No fact in the system is orphan.

**Trust scores never filter.** They surface. The system shows the user the confidence; the user decides.

That's the whole model. Six nouns, time-bounded verbs between them, every change logged, every claim sourced.

## What to actually build (the sequence)

Stop here on theory. Build in this order:

**1. Promote Certificate to a first-class entity.**
- `certificates` (cert_id UUID, faa_cert_number, dot_number, certificate_type, issued_date, surrendered_date, status)
- `certificate_aliases`, `certificate_identities`
- `operator_holds_certificate(operator_id, cert_id, valid_from, valid_to, source, evidence)` — link table
- `certificate_events` — append-only log

**2. Build Aircraft canonical.**
- `aircraft` (aircraft_id UUID, current_icao_hex, current_tail, msn, manufacturer, model, year)
- `aircraft_aliases` (handles re-registrations and tail changes)
- `aircraft_identities` (FAA registration, ADS-B hex, ARGUS ID — all sources mapped to one canonical)

**3. Build the link table that closes your biggest gap.**
- `aircraft_on_certificate(aircraft_id, cert_id, valid_from, valid_to, source, evidence)` — bitemporal
- `aircraft_certificate_events` — append-only log

**4. Backfill the link table from what you already have.**
- Run ER on `faa_aircraft.certificate_holder` against `operators.canonical_name` to seed initial operator-aircraft links
- This closes the 99.5% gap you saw in the March data (52K hexes flying, only 28 matched)

**5. Add the OpSpec ingestion pipeline.**
- FOIA-cycle pipeline (quarterly, slow, batched — different cadence from ADS-B)
- D085 parsing → produces `aircraft_certificate_events` rows → drives `aircraft_on_certificate` updates
- This is your legal source of truth for fleet composition

**6. Layer ARGUS / Wyvern on top.**
- Scrape weekly. Each scrape produces `operator_safety_rating(operator_id, cert_id, rating_body, rating, valid_from, valid_to)` rows
- Bitemporal — when a rating changes, close the old row, open a new one
- Attach to **certificate**, not brand. Your call from earlier.

**7. Then FBO. Then Person.** In that order. Don't start either until 1–6 are boring.

## The discipline

Three rules, then I shut up:

- **No new entity until the current one passes the "answer historical questions" test.** The test from the last turn — "show me every operator that flew N612QS in 2024 with their rating at the time" — should run against the live database and return correct answers before you move on.
- **Every ingestion writes to events first, links second.** Always. No exceptions. If a pipeline only updates the link without writing the event, it's broken.
- **Every link has source + evidence in the row.** If you can't cite where the fact came from, don't write it.

That's the plan. Start with Certificate as a first-class entity — that's the unblocker for everything else. Want me to write the actual table DDL for steps 1–3 next, or do you want to sit with this first?

---

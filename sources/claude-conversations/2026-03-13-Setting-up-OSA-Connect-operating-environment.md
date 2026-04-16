---
title: Setting up OSA Connect operating environment
created: 2026-03-13T21:15:09.564877Z
updated: 2026-03-14T08:02:51.090511Z
uuid: 73c1fb9b-ce38-4383-9a6b-39ca4fb17923
source: claude-conversation
type: source
message_count: 16
---

# Setting up OSA Connect operating environment

## Phelipe

You have full context on OSA Connect from the project files. I want to set up my primary operating environment here.
First, confirm what you know about OSA — the business model, the three-entity structure, the stage-gate framework, and where I am in Year 1 — so I know you're grounded in the right documents.
Then build me the persistent OSA CRM with all four tables from the Operating System: Pipeline, Contacts, Trip Log, and Operators. It should save across sessions using persistent storage. Design it to OSA's exact field specifications from the Implementation Assets document already in this project.
Once that's running, I want to work through the 8 open decisions from the Implementation Assets so the system is actually ready to use on day one.

---

## Claude

I'll start by pulling the key project documents to ground myself, then build your CRM.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me pull the actual Implementation Assets and Execution Memo files directly to get the exact field specs and the 8 open decisions.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me read the Operating System and Execution Memo for the three-entity structure and stage-gate framework.
```
This block is not supported on your current device yet.
```

Good. I now have the full picture. Let me read the frontend design skill, then build the CRM.
```
This block is not supported on your current device yet.
```

Now I have everything I need. Here's what I know, and then I'll build the CRM.

---

## OSA Connect — Context Confirmation

**Business model:** On-demand private jet charter brokerage. You source aircraft from Part 135 operator networks, present options with markup, coordinate bookings, and manage end-to-end trip execution. No aircraft ownership.

**Entity structure:** Three layers — (1) **Orange Sunshine Aviation** is the parent/holding entity, (2) **OSA Connect** is the client-facing charter brokerage sub-brand, (3) **the operator network** is the supply side (Part 135 certificate holders you source from). OSA Connect sits between demand-side clients and supply-side operators, earning margin on the spread.

**Stage-gate framework (from the Operating System):** Every trip moves through 8 pipeline stages with hard exit criteria and SLAs: INQUIRY (15-min response) → QUOTING (options in 4h) → OPTIONS SENT (follow up at 4h) → NEGOTIATING (reply in 2h) → CONFIRMED (agreement in 2h) → BOOKED (operator confirm in 4h) → COMPLETED (post-flight in 24h) → LOST (log reason, 90-day re-engage). Each gate has required fields that must be filled before advancement.

**Year 1 position:** Pre-revenue. Aviation lawyer secured for charter agreement. Tech stack identified (Google Workspace, HubSpot/Notion, Airtable). Brand identity designed (orange/purple system). Operator network and CRM not yet built. 8 implementation decisions remain open.

**The 5 databases from the Implementation Assets:** Trips, Clients, Quotes, Operators, Tasks — each with exact properties, types, select options, views, and relationship structures.

---

Now I'll build your persistent CRM. Given the Implementation Assets specify 5 databases (Trips, Clients, Quotes, Operators, Tasks), I'm building all five — the four you mentioned map to the Operating System's core tables, and Quotes is the critical bridge between Trips and Operators. Every field, select option, and relationship follows the exact specs from the document.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Your CRM is live with all 5 databases from the Implementation Assets, using persistent storage that saves across sessions. Every field, select option, pipeline stage, and relationship follows the exact specs from the document.

---

Now let's work through the **8 open decisions** so this system is ready for day one. I'll frame each one with a recommended answer, my reasoning, and what you'd need to change if you disagree.
```
This block is not supported on your current device yet.
```

While you're thinking on those first three, here's the reasoning behind my recommended defaults for each:

**Decision 1 (Margin):** I'd recommend **12% floor, 15% target**. At 10% you're leaving money on the table for the risk you're absorbing. At 15% minimum you'll lose competitive quotes early when you're building trust. 12% floor gives you room to stay competitive on price-sensitive deals while 15% target on standard bookings protects your economics. Heavy jets and multi-leg trips often support higher margins (18–20%) because coordination complexity is higher.

**Decision 2 (Payment):** I'd recommend **100% upfront** for Year 1. You don't have the cash reserves to float operator deposits while waiting on client balances. Most established brokers eventually move to 50/50, but that's after they have working capital and client trust history. 100% upfront also eliminates the single biggest operational risk — a client canceling after you've already committed funds to the operator.

**Decision 3 (Cancellation):** I'd recommend **deferring to your lawyer's template** with the 75%/50%/100% structure as your stated preference. The cancellation terms need to mirror what operators impose on you (which varies), so your lawyer should build in back-to-back protection. Your terms to the client should always be at least as strict as the operator's terms to you.

Once you select those three, I'll send decisions 4–8 (the tooling, workflow, and operational ones).

---

## Phelipe

same again. I have research standard policies around the industry

---

## Claude

Good — if you've benchmarked industry standards, let's lock these in fast. Here are decisions 4–8:
```
This block is not supported on your current device yet.
```

And the final two:
```
This block is not supported on your current device yet.
```

My recommended defaults while you decide:

**Decision 4:** Skip automation for now. You're pre-revenue with zero inbound volume. Manual entry into the CRM takes 90 seconds per inquiry and keeps you close to every deal. Automate when you're handling 10+ inquiries per week.

**Decision 5:** This Claude CRM as your operating layer, HubSpot later. HubSpot's free tier is solid but setting it up properly takes a full day you don't need to spend yet. The persistent CRM here matches your exact field specs and is usable right now. When deal flow justifies it, migrate to HubSpot with the same pipeline stages and field structure.

**Decision 6:** Tail # only — never expose operator name. This is standard broker practice. Disclosing the operator lets clients go direct on the next trip and cut you out. The tail number gives the client everything they need operationally (FAA lookup, safety verification) without exposing your supply chain.

**Decision 7:** PDF attached to email. It looks professional, is easy to forward to passengers, and creates a paper trail. The formatted email body is a nice backup for urgency, but the PDF is the primary deliverable.

**Decision 8:** Operator default, you escalate if needed. Most Part 135 operators have catering relationships and handle it as part of the charter. You relay the client's preferences, the operator arranges it, and you confirm it's handled during the T-24 pre-flight check. Only escalate to FBO catering or independent sourcing if the operator can't accommodate the request.

Once you lock in all 8, I'll produce a single-page decisions document you can reference and we'll move to your next priority.

---

## Phelipe

WOW good question. I wanna be truthful. we will have contract to protect us from scammy ways to go behind us. so idk what would be the most fair and advantages way to deal with this, also idk industies standard

---

## Claude

Good instinct — this is one of the most important structural decisions in brokerage. Let me give you the real picture.
```
This block is not supported on your current device yet.
```

This changes everything about the decision. Here's the real answer:

**You are legally required to disclose the operator's identity.** This isn't a business preference — it's federal regulation.

Under 14 CFR Part 295, effective February 14, 2019, air charter brokers must make certain compulsory disclosures to the charterer, including the name of the direct air carrier who will be in operational control of the aircraft.

Specifically, brokers are required to make three compulsory disclosures: the corporate name of the direct air carrier in operational control, the capacity in which the broker is acting (indirect air carrier, agent of charterer, or agent of carrier), and the existence or absence of liability insurance held by the broker.

The timing question is the important nuance for your workflow. The DOT confirmed that an air charter broker may contract with a customer before knowing the identity of the direct air carrier, and must disclose the carrier's identity within a reasonable time after the information becomes available. So you can sign the charter agreement before you've locked the operator, then disclose once confirmed.

And here's the enforcement reality: if the disclosure is not made within a reasonable amount of time, the charterer is entitled to cancel and receive a full refund.

**So here's how this actually plays out for OSA Connect:**

Your charter agreement (which your aviation lawyer is drafting) needs to include the Part 295 disclosure language. The Trip Packet should include the operator name and tail number once the booking is confirmed. This is non-negotiable from a compliance standpoint.

The concern about clients going direct is real but manageable. Your protection comes from three things: (1) your charter agreement should include a non-circumvention clause, (2) your value proposition is the sourcing, coordination, and disruption handling — not just the operator name, and (3) clients who go direct lose the broker layer of protection and take on operational risk themselves. Most serious charter clients don't want that.
```
This block is not supported on your current device yet.
```

My recommendation is option 3 — disclose at booking plus the non-circumvention clause. It keeps you fully compliant, transparent (which builds trust), and contractually protected. Flag this specific requirement to your aviation lawyer so the charter agreement template includes both the Part 295 disclosure section and the non-circumvention language.

---

## Phelipe

again learn with you here. we are learn from industry standards and build our way or deal. i view 3 very good way to comply with the law and protect us and the client or their is a way to do the same and get competition adavatage? we dont wanna be scammy we wanna build trust

---

## Claude

That's the right mindset. Let me dig into how the best brokers actually handle this — the ones who turn the disclosure requirement into a trust advantage rather than just checking a compliance box.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's the competitive landscape on this decision, and where the real advantage lives.

**The industry reality:** Most brokers treat operator disclosure as a compliance checkbox — they drop the operator name into a contract clause and move on. Some older-school brokers still try to obscure operator identity as long as possible, which is now both illegal and a trust killer. The best brokers have flipped this entirely.

Here's the key insight from Paramount Business Jets, one of the most respected brokerages: they provide clients with a complete ARGUS TripCHEQ safety report, Wyvern Pass report, or an in-house safety report on the crew and aircraft for every flight. Air Charter Advisors takes a similar approach — as a Premium Wyvern Broker Member, they have direct access to comprehensive safety reports, which they use to enhance due diligence and provide an extra layer of transparency on every flight they arrange.

The circumvention fear is real but overstated. The disclosure may open brokers to client circumvention, since clients could conceivably cancel with their broker and book with operators themselves, avoiding commissions. But in practice, clients who value private aviation want a broker who feels like a trusted advisor — someone anticipating their needs, solving problems before they know there's an issue, and ensuring every flight is smooth. Clients who would go direct after learning the operator name were never going to be loyal repeat clients anyway.

And here's what sets the bad actors apart: some charter brokers claim to fly their own aircraft in an attempt to gain a competitive advantage, deliberately misrepresenting the nature of their business by concealing information about the actual operator, deceiving their clients and even risking their safety. That's the opposite of where you want to be.

**The competitive advantage play for OSA Connect is this:** Don't just disclose the operator name because the law says you have to. Go further. Build a "Flight Safety Brief" that you include with every Trip Packet — it contains the operator name, their Part 135 certificate status, their ARGUS or Wyvern rating, the aircraft tail number, and a note that you personally vetted this operator. Most brokers hand over a name in fine print. You hand over a professional safety brief that says "I checked everything so you don't have to."

That does three things at once: (1) full Part 295 compliance, (2) positions you as the broker who takes safety more seriously than anyone else (which is credible because you're actually a pilot), and (3) makes your value so visible that going direct feels like losing your safety net.

Your protection against circumvention then comes from four layers: the non-circumvention clause in your charter agreement, the ongoing service value you demonstrate, your disruption recovery capability (if a plane breaks, the client needs you to source a replacement in hours — operators don't do that for direct clients), and the fact that operators give better pricing and priority to brokers who send consistent volume.
```
This block is not supported on your current device yet.
```

Take your time on this one. The Safety Brief approach is something your aviation lawyer should also weigh in on — there may be specific language they'd want included (or excluded) from a liability perspective. But directionally, the "radical transparency as competitive advantage" play is how the best modern brokerages are winning.

---

## Phelipe

Q: Decision 6 (final) — Operator Disclosure Policy for OSA Connect:
A: Full transparency + Safety Brief + non-circumvention clause (recommended)

---

## Claude

Strong choice. That's the right call for a brokerage built on trust, and your pilot background makes the Safety Brief credible in a way most brokers can't pull off.

I'll build the Flight Safety Brief template as a deliverable once we close out all 8 decisions. For now, Decision 6 is locked:

**Decision 6 — LOCKED:** Full transparency. Every Trip Packet includes a Flight Safety Brief (operator name, Part 135 status, ARGUS/Wyvern rating, tail number, broker vetting note). Charter agreement includes non-circumvention clause. Your aviation lawyer reviews both.

Now we're waiting on your selections for Decisions 1–5, 7, and 8 from the earlier prompts. While those are pending, here's a quick status of where we stand:

| Decision | Status |
|---|---|
| 1. Margin policy | Awaiting your pick |
| 2. Payment split | Awaiting your pick |
| 3. Cancellation terms | Awaiting your pick |
| 4. Form-to-CRM automation | Awaiting your pick |
| 5. Primary CRM system | Awaiting your pick |
| 6. Operator disclosure | **LOCKED — Full transparency + Safety Brief + non-circumvention** |
| 7. Trip Packet format | Awaiting your pick |
| 8. Catering sourcing | Awaiting your pick |

Go ahead and select from those earlier prompts whenever you're ready. Once all 8 are locked I'll produce three deliverables: a one-page Decisions Reference doc, the Flight Safety Brief template, and your updated Trip Packet with the Safety Brief integrated — all ready for your lawyer to review.

---

## Phelipe

put a pin really quick on that and come back to me on that after you do this update that i will prompt you.
I need to update the CRM Contacts section. Two things:
1. Add contact type categories to the Contacts tab if they don't exist yet. The three categories are:
- Client — someone booking or inquiring about trips
- Operator/Partner — someone in the industry with a service or business relationship
- Network — someone who engaged or connected but no clear business path yet
2. Add the first contact:
- Name: Jack Rosenberg
- Category: Network
- Location: Colorado
- Business: Aircraft detailing
- Source: LinkedIn inbound — responded to Loud Hawk newsletter post (Edition 1)
- Date added: March 13, 2026
- Notes: Reached out after first newsletter post. Said he loves the vision and does aircraft detailing in CO. Potential future Operator/Partner if a service relationship develops.
Make sure the contact type category is filterable so I can sort by Client, Operator/Partner, or Network later.

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me see the ClientsTab filter area and the ClientForm to know exactly what to update:
```
This block is not supported on your current device yet.
```

Good. I can see the current structure. The existing `CLIENT_TYPES` field (UHNW, Corporate, etc.) is about the *client profile* — that's a different axis from the *contact category* you're describing. I need to add a new `contactCategory` field that sits above the existing type system. Let me make the edits:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now add the `contactCategory` field and `dateAdded` field to the ClientForm, and add "LinkedIn-Inbound" to the lead sources:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now update the Save button label and the modal title references in the main app for clients:
```
This block is not supported on your current device yet.
```

Now I need to seed Jack Rosenberg's record. Let me add a seed function that runs on first load:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me also update the tab label from "Contacts" count to include the new contact, and fix the "New Contact" button label in the tabs:
```
This block is not supported on your current device yet.
```

Good — the tabs definition dynamically reads counts, so Jack will show up automatically. Let me verify the final file compiles correctly by checking the structure:
```
This block is not supported on your current device yet.
```

Looks good. Let me present the updated file:
```
This block is not supported on your current device yet.
```

CRM updated. Here's what changed:

**New field — Contact Category** with three filterable options: Client, Operator/Partner, Network. This sits above the existing Client Type field (UHNW, Corporate, etc.), so you have two layers: *who they are to you* (category) and *what kind of client they are* (type). The Contacts tab now has filter pills at the top so you can toggle between All, Client, Operator/Partner, and Network views with counts.

**New field — Date Added** so you can track when contacts entered the system.

**New lead source — LinkedIn-Inbound** added to the source options alongside the existing Referral, Cold-Outreach, Inbound-Web, and Partner.

**First contact seeded — Jack Rosenberg** is in there with all his details: Network category, Colorado, aircraft detailing business, LinkedIn-Inbound source from Loud Hawk Edition 1, March 13 2026, and your notes about the potential to upgrade him to Operator/Partner.

Click into the Contacts tab and you should see him. The filter pills will show "All 1 | Client 0 | Operator/Partner 0 | Network 1." When he becomes a service partner, just click his record and change the category — the filter counts update automatically.

Ready to come back to the remaining 7 open decisions whenever you are.

---

## Phelipe

Quick housekeeping patch on the OSA Connect Operating System document.
Update the Document Suite Reference and any governing-base references so they point to version-agnostic language:
- Replace any reference to "Execution Operating Memo v4" with "current OSA Execution Memo"
- Replace any reference to "Strategic Roadmap v2" with "current OSA Strategic Roadmap"
This ensures the Connect OS doesn't go stale when future versions of the memo or roadmap are produced.
Also confirm that the post-trip follow-up standard in the Connect OS is "within 24 hours of scheduled landing" (it should already be — just verify).
Do not change anything else.

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Good, I can see all the exact strings. The file is plain text (markdown-like), not binary docx. Let me make the targeted replacements:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me verify there are no remaining versioned references and confirm the post-flight timing:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

All post-flight references confirmed. Let me check line 779 to make sure it's consistent:
```
This block is not supported on your current device yet.
```

That line 779 is about referral follow-up, not post-flight — separate context, correctly reads "within 24 hours" for contacting a referred lead. Not a post-flight reference, so no issue.

Now copy to outputs:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Done. Here's what changed and what was verified:

**4 replacements made:**
- "Governing Base: OSA Execution Operating Memo v4" → "Governing Base: current OSA Execution Memo"
- Intro paragraph reference updated to match
- Document Suite Reference table: Execution Memo entry now reads "current OSA Execution Memo"
- Document Suite Reference table: Strategic Roadmap entry now reads "current OSA Strategic Roadmap"

**Zero versioned references remain** — confirmed with a full-file search for "Memo v4", "Memo v3", "Roadmap v2", "Roadmap v1". All clean.

**Post-flight timing verified:** The standard appears in four distinct locations throughout the document, and all consistently read "within 24 hours of scheduled landing." No changes needed.

**Nothing else was touched.** Ready to come back to the remaining 7 open decisions whenever you are.

---

## Phelipe

can you add the visual branding into this. is ahrd to read

---

## Claude

Let me look at the brand assets to understand the visual system, then rebuild this as a properly formatted Word document.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me read the full document content so I can rebuild it properly:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now I have the complete document. Let me get the logo image dimensions and build the branded docx:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now I'll build the branded document. This is a large file so I'll create it in sections:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

This is now a fully branded Word document with the complete OSA visual identity applied throughout. Here's what's in there:

**Cover page** with your OSA Connect color logo, document title, and governing base reference (version-agnostic, as patched earlier).

**Brand system throughout:** OSA orange (#E8621A) for accent borders, headings dividers, step numbers, and note callouts. OSA purple (#5B2D8E) for sub-headings and category badges. Dark (#1A1A2E) for table headers and primary text. Professional table formatting with color-coded qualification matrices (green/amber/red), branded email template boxes with orange left-border, and checkbox-style checklists for the operator vetting tool.

**Headers and footers** on every page with "OSA CONNECT | OPERATING SYSTEM" and orange underline.

**All 9 tools** fully formatted with proper table structures, step tables, email templates in styled boxes, and the note callouts with orange sidebar.

**All content identical** to the patched version — the version-agnostic references are in place, and post-trip follow-up still reads "within 24 hours of scheduled landing" in all locations.

Ready to come back to the remaining 7 open decisions whenever you are.

---

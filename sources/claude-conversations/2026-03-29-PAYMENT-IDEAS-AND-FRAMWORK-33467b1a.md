---
title: PAYMENT IDEAS AND FRAMWORK
created: 2026-03-29T22:53:35.237845Z
updated: 2026-04-02T02:35:45.657800Z
uuid: 33467b1a-3dbd-40c1-9a89-8852a806571d
source: claude-conversation
type: source
message_count: 16
---

# PAYMENT IDEAS AND FRAMWORK

*Summary: **Conversation Overview**

The person is building OSA (a private aviation charter brokerage platform) and is working through the legal, contractual, and payment infrastructure needed to operate as a Part 295 charter broker. The conversation covered three interconnected topics: finding NBAA charter broker contract templates, assessing the safety of using public contract examples, and mapping out the payment architecture for charter broker and operator relationships.

On contracts, Claude searched for NBAA templates and found that NBAA does not publish standalone contract templates — only best practices guides and member resources. Claude identified several publicly available broker agreements (Fly Louie, BlackBird, Global Jet Concept) as structural references, with Fly Louie flagged as the closest match for OSA's agent-of-customer model. The person confirmed they want to operate as agent of the customer under Part 295, not as an indirect air carrier. Claude advised that an aviation attorney review any final agreement and estimated $3–5K for proper legal drafting.

On payment architecture, the conversation built on prior sessions involving a Mercury API workflow and ADS-B trigger concepts. Claude clarified that ADS-B triggers are a Phase 2+ feature — the industry standard is operators get paid before the aircraft moves, and net-30 terms only exist for high-volume established broker relationships. The person confirmed they want to operate at Tier 2 from Day 1 (Mercury intermediary: client pays into Mercury, operator paid same day before flight). The conversation then focused on making this flow as frictionless as possible: generating branded payment pages with wire/ACH details, using Mercury webhooks to auto-match incoming payments to deals, auto-notifying operators when funds are secured, and using Mercury's API to initiate outbound operator payments with one manual approval step retained as a safety net. The person dismissed a follow-up question about where to go deeper and the conversation ended there.

**Tool Knowledge**

Claude used web search and conversation search tools throughout. Conversation search using the query "Mercury API payment workflow" and "ADS-B triggers funds payment" successfully retrieved relevant prior session content. Web search for "NBAA charter broker template contracts" and "air charter broker agreement template sample PDF" returned useful results, while "charter operator net 30 payment terms broker credit" required a follow-up search with "private charter operator payment terms established broker net 30 credit account aviation" to surface more specific industry context. Searching for prior chat content by topic keyword rather than exact phrasing proved effective for retrieving relevant session material.*

## Phelipe

Can you find NBAA charter broker templates contracts?

---

## Claude

The user is asking me to find NBAA (National Business Aviation Association) charter broker template contracts. Let me search for this.
```
This block is not supported on your current device yet.
```

The search results show NBAA has best practices guides and regulatory guidance, but not specific template contracts. Let me search more specifically for template contracts.
```
This block is not supported on your current device yet.
```

NBAA doesn't appear to publish actual template contracts for charter brokers. They publish best practices guides, consumer guides, and regulatory guidance, but the actual contract templates seem to be members-only or don't exist as downloadable templates. Let me search for charter broker contract templates more broadly.
```
This block is not supported on your current device yet.
```

Good findings. NBAA doesn't publish standalone contract templates - they publish best practices guides that are members-only. But I found several real-world charter broker agreement examples. Let me give Phelipe a clear summary.Phelipe, here's what I found:

**NBAA doesn't publish standalone contract templates.** What they offer are best practices guides and regulatory guidance that inform what your contracts should contain. The key resources:

1. **NBAA Best Practices for Air Charter Brokering** (updated Aug 2024) — covers the four broker capacity types: agent of the customer, agent of the air carrier, broker as middleman, and broker as indirect air carrier, along with terms and conditions guidance and insurance considerations. This is the closest thing to a "template framework" from NBAA. The PDF is at: https://nbaa.org/wp-content/uploads/2024/07/NBAA-Best-Practices-for-Air-Charter-Brokering.pdf

2. **Aircraft Charter Consumer Guide** — members-only, provides tools you can customize to pre-screen operators and obtain competitive quotes.

Both are behind the NBAA member paywall for the full versions.

**Real contract examples I found publicly:**

- **Fly Louie's Brokerage Agreement** (flylouie.com/brokerage-agreement) — structured as agent of the client, with clear language that the broker does not own or operate any aircraft. Good reference for OSA's "agent of customer" model.

- **BlackBird's Charter Agreement** (flyblackbird.com/aircraft-charter-agreement) — positions the broker as an indirect air carrier sourcing single entity charters, with the Part 135 operator furnishing the actual transportation.

- **Global Jet Concept's Brokerage Agreement** (globaljet.aero) — detailed international broker agreement structured with the broker acting as agent of and on behalf of the client.

- **Law Insider** (lawinsider.com/contracts/tagged/aircraft-charter-agreement) — aggregates filed charter agreements from SEC filings you can study.

**For OSA specifically:** Since you're operating as agent of the customer (not IAC), the Fly Louie template is probably the closest structural match. The key Part 295 disclosures you need baked into any agreement are: your capacity as broker, that you're not the direct air carrier, total charter cost, third-party fees, and carrier identity before contract execution. Want me to pull any of these full agreements for a deeper look?

---

## Phelipe

Is it safe?

---

## Claude

The user is asking "Is it safe?" - this is ambiguous. They could be asking about:

1. Whether it's safe/legal to use these public contract templates as a basis for OSA's contracts
2. Whether operating as a charter broker is safe from a liability perspective
3. Something else

Given the context of our conversation about charter broker contracts and OSA, I think they're asking whether it's safe to use these templates/structure their brokerage agreements this way - or whether operating as a broker (vs. holding a Part 135 certificate) is safe from a legal/liability standpoint.

Let me ask for clarification since this is ambiguous.Could you clarify what you mean? A few ways I could take that:

- Is it **legally safe** to model OSA's contracts off these public examples?
- Is the **agent-of-customer broker structure** safe from a liability standpoint?
- Is operating as a **Part 295 broker without a Part 135 certificate** safe/compliant?

Which angle are you getting at?

---

## Phelipe

1 and 2

---

## Claude

Phelipe is asking about two things:
1. Is it legally safe to model OSA's contracts off these public examples?
2. Is the agent-of-customer broker structure safe from a liability standpoint?

Let me give him a direct, practical answer on both. I'm not a lawyer so I need to caveat that, but I can share what's generally understood in the industry.**1. Modeling contracts off public examples**

Using publicly available agreements as structural references is standard practice — every aviation attorney does this. The risk isn't in studying them, it's in copy-pasting without adapting to your specific legal structure. The Fly Louie and BlackBird agreements are filed publicly or posted as terms of service, so referencing their structure is fine. That said, you absolutely need an aviation attorney to draft or review your final agreement before you use it with clients. Part 295 has specific disclosure requirements, and a generic template won't cover state-level consumer protection nuances or your specific liability allocation. A contract that's 90% right but misses one disclosure requirement puts your DOT registration at risk.

**2. Agent-of-customer liability exposure**

This is actually the lowest-liability broker structure of the four NBAA categories, and it's the right call for OSA's stage. As agent of the customer, you're arranging transportation on the client's behalf — the contractual relationship for carriage is between the client and the Part 135 operator. Your liability is limited to your performance as broker (sourcing, vetting, disclosure), not the operation of the flight.

The key risks to manage are: making representations about safety or aircraft quality that go beyond what the operator warrants (creates broker liability), failing to vet the operator's certificate/insurance/safety record (negligence exposure), and using language like "our fleet" or "our aircraft" that could make DOT treat you as holding yourself out as a carrier.

Your ATP credibility is a double-edged sword here — it's a massive trust signal, but it could also raise the standard of care expected of you as a broker if something goes wrong. An attorney can help you draft language that leverages your expertise without creating implied warranties.

Bottom line: get an aviation attorney who knows Part 295. Budget $3-5K for a proper broker agreement and client-facing terms. It's one of the few things worth spending real money on before your first deal. I'm not a lawyer, so treat all of the above as directional, not legal advice.

---

## Phelipe

Go on the last chat. And explain payment architecture for charter and operator

---

## Claude

The user wants me to find the last chat and explain the payment architecture for charter and operator. Let me search for recent chats first.
```
This block is not supported on your current device yet.
```

The user wants me to go to the last chat and explain the payment architecture for charter broker and operator. Let me search for more specific content about payment architecture in that conversation.Here's the link to your last chat: [GLUING ALL OSA CONNECT](https://claude.ai/chat/21f6ab35-7a10-4cba-b7fa-cc4923883aef)

Now, the payment architecture for charter broker ↔ operator — here's how the money actually flows:

**Standard Charter Payment Flow (How it works today)**

Client pays the broker the full charter price. The broker holds those funds (ideally in escrow or a trust account — this is a Part 295 best practice), then pays the operator the agreed-upon rate minus the broker's margin. Typical broker markup is 8-15% on top of the operator's quoted price, though some brokers work on a flat commission disclosed to the client.

There are three common structures:

**A) Broker collects, pays operator** — Most common. Client pays broker → broker takes margin → broker pays operator before or after the flight. Risk sits with the operator if the broker doesn't pay. This is where OSA starts.

**B) Split payment** — Client pays the operator directly for the flight cost, and pays the broker a separate fee. More transparent, but clunkier. Some high-end brokers use this.

**C) Indirect Air Carrier (IAC)** — Broker buys the charter capacity from the operator, then resells it to the client at markup. Broker assumes more liability and regulatory burden. Not where you want to be at Day 1.

**The OSA Strategic Play (from your last session)**

The insight was that by combining real-time operator schedule access (Aviapages/Leon/FL3XX) with payment rails (Brex partner-bank model), you collapse the entire RFQ-negotiate-invoice-pay cycle into a single pre-validated, pre-funded booking. The operator sees a confirm/decline notification where the money is already secured. Nobody has built this combination — being the broker AND owning the payment rails AND having live schedule visibility.

But the grounded sequence is: close 5-10 deals manually via phone calls first (structure A above), prove the unit economics, then layer the payment infrastructure on top of real transaction data. Want to dig into any layer deeper?

---

## Phelipe

I want to understand what is the standard. What we can do with the workflow. What we can do with relationships.
Because we were talking ads-b triggers for funds

---

## Claude

Phelipe wants to understand the standard payment workflow in charter brokerage, then what OSA can innovate on top of it, and he's referencing a prior conversation about ADS-B triggers for funds. Let me search for that ADS-B conversation.
```
This block is not supported on your current device yet.
```

Great, I found the relevant conversations. Let me synthesize this into a clear breakdown of: 1) the industry standard, 2) workflow innovations OSA can build, 3) relationship-based innovations, and specifically the ADS-B trigger concept.Good — this is all connected across your sessions. Let me lay it out in three layers.

**LAYER 1: THE INDUSTRY STANDARD (how it works today)**

Client requests a trip → broker calls 3-5 operators → operators quote back (usually 2-24 hours) → broker marks up 8-15% → client approves and pays broker via wire or credit card → broker pays operator via wire before or after the flight → flight happens → done.

The money flow is messy. Most brokers collect from the client, then wire the operator separately. The timing is inconsistent — some operators demand full payment 48-72 hours before departure, some accept net-30. There's no standard trigger for when the operator gets paid. It's all manual, relationship-dependent, and the broker carries all the float risk. If a client pays by credit card and the broker wires the operator, and then the client does a chargeback — the broker is out the full amount because wires are irreversible.

**LAYER 2: THE WORKFLOW INNOVATION (what OSA can build)**

This is the ADS-B trigger architecture from your earlier sessions. The flow becomes:

Client pays into escrow (Stripe Connect holds the funds, not OSA) → flight is confirmed → ADS-B data detects wheels-up → escrow automatically releases operator payment minus broker commission → everyone gets paid simultaneously upon verified departure.

Three things this solves that nobody else has solved:

First, **chargeback protection**. The client's credit card payment sits in Stripe's escrow. The operator gets paid via ACH/wire from the escrow — a separate transaction. If the client disputes after the flight, you have ADS-B tracking data proving departure, route, and arrival plus a signed digital charter agreement. The dispute is between the platform and the card company, not between the broker and operator.

Second, **trust elimination**. The operator doesn't have to trust the broker to pay. The money is already secured before wheels-up. The client doesn't have to trust the broker with $40K sitting in a personal business account. It's in Stripe's regulated escrow. The broker doesn't carry float risk because they never hold the funds.

Third, **speed**. No invoicing. No net-30. No chasing payments. Departure = payment. Automatically.

**LAYER 3: THE RELATIONSHIP PLAY (what changes with operator partnerships)**

This is where the layers compound. With your first 5-10 operators you close by phone (ATP credibility, direct relationship), you're proving the payment model manually — maybe even starting with pass-through where the client pays the operator directly and you invoice your fee separately. Zero risk.

But once an operator has done 3-5 deals through OSA and trusts the system, you migrate them onto the escrow rails. Now they're a "connected account" on Stripe Connect. Their schedule data (eventually via Leon/FL3XX/Aviapages) feeds into your sourcing pipeline. Their payment releases are automated via ADS-B triggers.

The relationship progression looks like:

**Deal 1-3:** Pass-through. Client pays operator directly. You invoice brokerage fee separately. Operator learns you bring real clients and you're not wasting their time.

**Deal 4-10:** Escrow. Client pays into Stripe. Operator sees funds are secured before they even position the aircraft. Release on wheels-up. Operator starts to prefer you over brokers who pay net-30 on a handshake.

**Deal 10+:** Schedule integration. Operator gives you API access or shares availability proactively. You can quote in minutes instead of hours because you already know what's available. Combined with the payment guarantee, the operator's workflow collapses to: notification → confirm → fly → money hits account.

That's the "Stripe for private aviation" position — you're not just the broker, you're the financial and operational infrastructure that operators can't easily leave because the payment certainty and speed is better than anything else in the market.

The phasing from your last session still holds: manual first, attorney trust account or Stripe escrow at 20+ deals, licensed payment infrastructure evaluation at 100+. The ADS-B trigger is the unlock that turns a standard escrow into something structurally new. Want to go deeper on any of these layers?

---

## Phelipe

Look last chat. We had mercury api workflow.
I can't do ads-b on the beginning right? Who they allow net 30?

---

## Claude

Phelipe is asking me to look at the last chat for the Mercury API workflow discussion, and he has two questions:
1. He can't do ADS-B triggers at the beginning, right?
2. Who allows net-30 payment terms?

Let me search for the Mercury API discussion.
```
This block is not supported on your current device yet.
```

Now I have the full context. Let me answer his two questions:

1. He can't do ADS-B triggers at the beginning - correct, and the standard is operators get paid BEFORE the plane moves
2. Who allows net-30 terms?

Let me also search for net-30 in charter to give him a proper answer.
```
This block is not supported on your current device yet.
```

Now let me search specifically for charter aviation payment terms - who gets net 30 in this industry.
```
This block is not supported on your current device yet.
```

Let me now synthesize all of this into a clear answer about:
1. ADS-B triggers - correct, can't do that at the beginning
2. Net-30 in charter - who gets it and how it works
3. The Mercury API workflow from the last chat
4. What OSA can do with workflow and relationshipsOkay, found the Mercury workflow from your last chat. Let me lay this out properly.

**You're right — ADS-B triggers are a Phase 2+ feature.** At Day 1 you don't have the integration built, you don't have the volume to justify it, and frankly operators would look at you sideways if you pitched "we pay on wheels-up" because that's not how the industry works. Operators get paid BEFORE the plane moves. That's the standard.

**THE ACTUAL PAYMENT STANDARD IN CHARTER:**

The typical timeline is: client confirms the trip → full payment due immediately or within 24-48 hours of confirmation → operator receives payment (or confirmation that funds are secured) before they commit crew, fuel, and aircraft → flight operates.

From Fly Louie's actual terms: full payment for each flight is due upon confirmation by the client of a specific itinerary and price quote, and payments must be received in order for the broker to enter into a charter contract with the carrier. PrivateFly operates similarly — the charter price is paid at the time and in the amount specified in the charter contract.

There is no net-30 in standard charter brokerage for individual flights. It's pay-before-you-fly, full stop. The operator won't position the aircraft without secured funds.

**WHO GETS NET-30 (and why it matters for OSA):**

Net-30 exists in charter, but only in two specific contexts:

First, **established broker-operator relationships at volume.** If Air Charter Service or Sentient books 50 flights a month with an operator, that operator might extend net-30 terms to the brokerage because the relationship is proven, the volume is consistent, and the risk of non-payment is low. This is essentially trade credit — the operator is saying "I trust you to pay within 30 days because you always have." The operator would run a credit check on the brokerage, evaluate their payment history, and set a credit limit.

Second, **corporate accounts.** Fortune 500 companies that charter frequently sometimes negotiate net-30 or net-60 terms with brokers or operators directly. The broker floats the operator payment and invoices the corporate client on terms. The broker carries the float risk.

**Neither applies to OSA on Day 1.** You have no track record, no volume, no credit history as a broker. Every deal will be prepaid.

**THE MERCURY WORKFLOW (from your last chat):**

The architecture you mapped out was:

Client confirms trip → your Connect app generates wire instructions to your Mercury account → client wires full amount → Mercury webhook fires notifying your system → your system matches the wire to the deal → status updates to "funds_received" → you confirm with the operator → your system calls Mercury's API to send the operator's portion → status updates to "operator_paid" → flight operates.

Mercury is the pipe. Your code is the escrow logic. You're tracking which dollars belong to which deal in your system, even though legally it's all in one Mercury account.

**THE RELATIONSHIP PROGRESSION (what changes everything):**

Here's where it gets strategic. Think of it in tiers:

**Tier 1 — Stranger (Deals 1-3 with a new operator):**
Pass-through. Client pays operator directly. You invoice your brokerage fee separately. The operator has zero risk. You have zero float exposure. You're proving you bring real, qualified clients.

**Tier 2 — Acquaintance (Deals 4-10):**
Mercury intermediary. Client pays into your Mercury account. You pay the operator within 24 hours of receiving funds, before the flight. The operator sees you always pay on time. You're building a payment track record.

**Tier 3 — Trusted Partner (Deals 10-20):**
Same Mercury flow, but now the operator starts giving you preferential pricing, holding aircraft for you on verbal confirmation before the wire clears, maybe even giving you 48-72 hours post-flight to settle. This is earned, not asked for. It happens naturally when you've paid on time 10+ times.

**Tier 4 — Credit Relationship (20+ deals, volume):**
Now you can have the net-30 conversation. The operator knows your payment history. You might say: "We're doing 8-10 deals a month with you. Can we settle weekly instead of per-trip?" This is where your margin improves because you collect from clients immediately but settle with operators on a cycle. The float is yours.

**Tier 5 — The ADS-B Play (50+ deals, infrastructure built):**
Now the ADS-B trigger makes sense, but it's flipped from what you originally imagined. It's not "operator gets paid on wheels-up" — that's slower than the standard. Instead, ADS-B becomes your **verification and reconciliation layer**: confirming the flight actually operated as booked, auto-closing the deal in your system, triggering the commission calculation, and generating the post-flight settlement report. At this tier, the operator is already on net-7 or weekly settlement. ADS-B just automates the proof-of-service.

**The real insight:** ADS-B isn't a payment trigger. It's an **audit trigger**. It proves the service was delivered, which protects you in disputes, chargebacks, and reconciliation. That's more valuable than using it to release funds.

Want to map the Mercury API calls for Tier 1 and Tier 2 specifically?

---

## Phelipe

I can do tier 2 day one. I am looking how can I make this as frictionless as possible

---

## Claude

Phelipe wants to do Tier 2 from day one - Mercury intermediary where client pays into his Mercury account and he pays the operator. He wants to make it as frictionless as possible.

Let me think about what "frictionless" means in this context:
- For the client: easy to pay, clear instructions, fast confirmation
- For the operator: fast payment, certainty of funds, minimal back-and-forth
- For Phelipe: minimal manual steps, automated notifications, clean reconciliation

The key friction points in the current charter payment flow are:
1. Client has to manually wire (wire instructions, bank details, etc.)


2. Phelipe has to manually check if wire arrived
3. Phelipe has to manually confirm with operator
4. Phelipe has to manually send operator payment
5. Reconciliation is manual

Mercury's API can automate most of the backend steps - checking for incoming payments, notifying him, and triggering operator payouts. But the real bottleneck is getting the client to pay in the first place. Wires are cumbersome, credit cards expose him to chargebacks, and ACH takes too long. I need to figure out what payment methods Mercury actually supports that could make this seamless for clients.You can. The question is where the friction actually lives. Let me break it down by who feels it.

**CLIENT FRICTION (the deal-killer):**

The worst part of the current charter experience is the payment moment. Client says yes to a $30K quote, then you say "great, here are our wire instructions" and hand them a routing number and account number. Now they have to call their bank, or log into their bank portal, set up a new payee, type in numbers, wait for verification. That's 20-45 minutes of hassle right at the moment of highest excitement. Every minute of friction is a chance for them to cool off.

What you can do on Day 1 with Mercury:

Mercury gives you a routing and account number. But instead of emailing raw wire instructions, your Connect app generates a clean payment page — branded OSA, shows the trip summary (KTEB → KPBI, Citation X, March 31), the total, and the wire details formatted for easy copy-paste. Add a "Pay by ACH" option alongside wire. ACH is free on Mercury, settles in 1-2 business days, and the client can initiate it from their bank without calling anyone. For repeat clients, they save your Mercury details once and it's one-click from their bank going forward.

**OPERATOR FRICTION (the trust-killer):**

The operator's friction is uncertainty. "Did the broker actually collect? When am I getting paid?" Every hour they're waiting to hear about payment is an hour they might release that aircraft to another broker.

With Mercury's API, the moment the client's wire or ACH hits your account, your system can automatically send the operator a notification: "Funds secured for [trip]. Your payment of $26,500 will be sent within 2 hours." Then your system calls Mercury's API to initiate the outbound wire to the operator. The operator sees money in their account same day or next morning.

Your pitch to operators becomes: "You'll have confirmation of secured funds within hours of booking, and payment in your account before the crew even starts their duty day."

**YOUR FRICTION (the scaling-killer):**

The manual steps that eat your time: checking if the wire arrived, matching it to the right deal, calculating the operator portion vs your commission, initiating the outbound payment, updating statuses. Mercury's webhooks handle the first two automatically. Your pipeline handles the math. Mercury's API handles the outbound. You're left with one manual step: reviewing and approving the outbound payment before it fires. Keep that manual approval for your first 20 deals. It's your safety net.

**The Day 1 flow, made as tight as possible:**

Client says yes → your system auto-generates a branded payment page with wire/ACH details and trip summary → client pays → Mercury webhook fires → your system matches payment to deal, updates status to "funded," auto-notifies the operator that funds are secured → you review and approve the outbound payment → Mercury API sends operator their portion → status updates to "operator paid" → done.

Total manual touchpoints for you: one. The approval click.

Total time for client: however long their bank takes to send a wire or ACH.

Total time for operator to see money: same day for wire, next day for ACH.
```
This block is not supported on your current device yet.
```

Waiting for Phelipe's response.

---

## Phelipe

[User dismissed — do not proceed, wait for next instruction]

---

## Claude

The user dismissed the question. I'll wait for their next message.Standing by.

---

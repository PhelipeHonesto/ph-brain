---
title: Services as the next software frontier
created: 2026-03-17T18:18:13.457230Z
updated: 2026-03-17T18:56:20.112284Z
uuid: b727887c-b20a-4c3e-b952-6b99128ab9c7
source: claude-conversation
type: source
message_count: 4
---

# Services as the next software frontier

## Phelipe

https://sequoiacap.com/article/services-the-new-software/
Give the summary

---

## Claude

Let me fetch that article for you.
```
This block is not supported on your current device yet.
```

Here's the summary:

**Sequoia's thesis (by Julien Bek, March 5, 2026):** The next trillion-dollar company won't sell AI tools — it will sell the *work itself*. For every dollar spent on software, six are spent on services, and AI is now good enough to capture that services budget directly.

The core framework distinguishes between **intelligence** (rule-based tasks AI can already do autonomously) and **judgement** (experience-driven decisions that still need humans). Software engineering crossed the AI-autonomy threshold first because it's primarily intelligence work, but every profession is next.

Two models are emerging: **copilots** (sell the tool to the professional, like Harvey for lawyers) and **autopilots** (sell the outcome directly to the buyer, like Crosby drafting NDAs for companies instead of law firms). Autopilots capture the work budget from day one, which dwarfs the tool budget.

The **playbook** for autopilot startups: start where outsourcing already exists. If a task is already outsourced, the company has accepted external delivery, there's an existing budget line, and the buyer is already purchasing an outcome. Replacing an outsourcing contract is a vendor swap; replacing headcount is a reorg.

The article then maps specific verticals by readiness, including insurance brokerage ($140-200B), accounting ($50-80B, with a structural talent shortage accelerating adoption), healthcare revenue cycle, claims adjusting, tax, transactional legal, IT managed services, supply chain, recruitment ($200B+), and management consulting ($300-400B, though mostly judgement-heavy and hardest to automate).

The punchline: 2025's fastest-growing AI companies were copilots; in 2026 many will try to become autopilots, but they face the innovator's dilemma — selling the work means cutting their own customers out of doing it. That's the opening for pure-play autopilot startups.

This maps directly to what you're building with OSA, Phelipe. Charter brokerage is a services business where the client is buying an outcome (a flight), not a tool. OSA Connect is essentially an autopilot play in a fragmented, outsourced-heavy market — right in Sequoia's sweet spot on that opportunity map.

---

## Phelipe

What could we do be build tho? Following this strategy

---

## Claude

Good question. Let me think through this against OSA's actual position.

The Sequoia framework says: find the outsourced, intelligence-heavy task in your vertical, nail distribution, then expand toward insourced judgement work as you compound data.

In private aviation, here's how that maps:

**The outsourced intelligence work (your wedge):**
Charter brokerage is *already* the outsourced layer. Companies and individuals don't build in-house flight departments until they're flying 200+ hours/year. Below that threshold, they outsource to brokers. The broker's core job is intelligence work: matching trip requirements to available aircraft, collecting quotes from operators, comparing price/safety/availability, and handling logistics. That's exactly the type of work AI can systematically outperform humans on — especially at speed and breadth of operator coverage.

**What OSA could build as the autopilot:**
Instead of positioning OSA Connect as a brokerage tool (copilot for brokers), you position it as the thing that *does the brokerage* for the end client. The client inputs a trip, and OSA delivers a vetted, priced, safety-scored option. No human broker in the middle making phone calls — the system does the intelligence work (operator matching, pricing logic, safety screening via your Safety Brief framework, availability checking) and you apply the judgement layer (final vetting, relationship calls, edge cases).

The concrete build sequence following Sequoia's playbook would look something like:

**Phase 1 — Automate the intelligence layer of brokerage.** Build the quoting engine inside OSA Connect so that a trip request automatically matches against your operator database, pulls in safety/insurance/fleet data, and generates a ranked shortlist with pricing. Right now that's manual outreach. Making it systematic is the unlock. The Safety Brief (Decision 6) becomes your proprietary data moat — every quote you process builds a deeper operator intelligence layer that no competitor has.

**Phase 2 — Sell the outcome, not the service.** Your distribution is Loud Hawk. Instead of Loud Hawk driving leads to "talk to a broker," it drives leads to "get your trip quoted in minutes." The buyer is purchasing the flight, not hiring a broker. That's the autopilot framing.

**Phase 3 — Expand into judgement territory.** As you accumulate trip data, operator performance data, pricing patterns, and client preferences, you start handling the harder stuff: fleet management advisory, aircraft acquisition timing recommendations, the transition-to-ownership analysis for clients crossing the 200-hour threshold. That's where OSA Aircraft comes in as the natural upsell — and it's the judgement-heavy work that's much harder to compete with.

**The structural advantage you already have:**
The Blackout Aviation failure points you mapped are basically the risks of running a *copilot* brokerage (narrow avatar, commoditized offer, no product control). The autopilot framing solves most of them. Your Safety Brief de-commoditizes. Loud Hawk solves CAC. The Embraer/Brazil cross-border niche gives you a defensible starting wedge where your judgement (dual citizenship, operational knowledge, family ties) compounds into proprietary data that's genuinely hard to replicate.

The one open question this sharpens: the payment/compliance infrastructure (your candidate Decision 7) isn't just a risk mitigation item — in the autopilot model, it's *core infrastructure*. If you're selling the outcome, you own the transaction end to end, which makes the "never pay irreversible supplier money with reversible client money" rule even more critical to solve cleanly before scaling.

Does this track with where your head's at, or are you thinking about a different angle?

---

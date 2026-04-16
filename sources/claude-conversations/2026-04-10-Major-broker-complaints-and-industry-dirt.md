---
title: Major broker complaints and industry dirt
created: 2026-04-10T19:52:28.368594Z
updated: 2026-04-10T20:41:14.310685Z
uuid: 113c1f4b-7b3e-4959-bbe4-325b3919561c
source: claude-conversation
type: source
message_count: 32
---

# Major broker complaints and industry dirt

*Summary: **Conversation Overview**

Phelipe is building OSA (Orange Sunshine Aero), a zero-commission private jet charter marketplace with an AI layer called Dumont, and engaged Claude in deep competitive intelligence research across multiple dimensions. The session covered broker complaints and industry dirt, pricing transparency mechanics, app landscape analysis, user acquisition strategy, and a breakthrough product idea. Phelipe's working vocabulary includes terms like Thompson Sampling, Guardian agent, Quote Agent, clean holds, Loud Hawk (his content brand), ATP credential, Avinode, Part 135, FBO, ADS-B, and beachhead customers (post-raise founders doing 2-8 trips/year).

The research revealed that Paramount Business Jets is the most credible transparency competitor, showing actual operator wholesale cost plus a disclosed 10-16% tiered management fee on every invoice — a model Paramount has operated since 2010. This makes transparency a weak differentiator for OSA against Paramount specifically, shifting the competitive angle to cost structure (2% vs 10-16%) and AI-driven speed. Other major brokers like Wheels Up, Victor, and JetLux have significant legal, financial, and reputational vulnerabilities documented across securities lawsuits, administration proceedings, and fraud cases. FlyHouse was flagged as the most dangerous direct competitor given its reverse-auction model, funding, and IPO ambitions. Elevate Jet was identified as the best current app in the space, built on 30 years of proprietary data with an AI called Ruby, though they're still hiring their first dedicated UX designer and lack price calendars, margin transparency, and social features. XO leads on raw download volume at 2 million-plus.

For UX inspiration, Phelipe was directed to study Wise for the booking/pricing flow, Mercury for aesthetic fit with his beachhead customer, Google Flights for the price calendar pattern, Carvana/Carfax for trust reporting, and OpenTable for the clean hold concept. The session concluded with Phelipe generating an original product idea: a tool where users upload any broker quote, invoice, or email as a PDF or screenshot, and an AI reverse-engineers the probable operator cost versus broker markup, building trust through radical transparency while simultaneously collecting real market pricing data at scale. Claude confirmed this is technically feasible using LLM document parsing against OSA's pricing model, legally sound since users voluntarily share their own documents, and strategically powerful as a data flywheel that trains Thompson Sampling with real competitor pricing data contributed by users. The build sequence proposed starts with a free web tool requiring no account, progresses to account creation for quote history, then moves into the app with push notifications and a savings dashboard.*

## Phelipe

Can you look i to reddit or forum and see what is main complaint of big brokers players. Like paramount and ACS ? Can you find dirty in them or the top 10 brokers?

---

## Claude

Phelipe wants competitive intelligence on major charter brokers - complaints, issues, dirty laundry.
```
This block is not supported on your current device yet.
```

Paramount looks clean. Let me search for complaints and negatives about the bigger players.
```
This block is not supported on your current device yet.
```

Let me search more specifically for complaints about the top brokers like ACS (Air Charter Service), PrivateFly, Victor, Magellan Jets, etc.
```
This block is not supported on your current device yet.
```

Let me search for more specific complaints about top brokers - markup issues, transparency problems, etc.
```
This block is not supported on your current device yet.
```

Let me search for the most common customer complaints and industry-level dirt.
```
This block is not supported on your current device yet.
```

Let me search for Wheels Up complaints and Directional Aviation/Tuvoli/PrivateFly issues specifically.
```
This block is not supported on your current device yet.
```

Good, I have a lot of material now. Let me compile the key findings for Phelipe.Phelipe, here's what I found across Glassdoor, Trustpilot, industry publications, and legal filings. No Reddit goldmine specifically, but plenty of real dirt:

**Air Charter Service (ACS)**
- Glassdoor reviews flag sexual harassment happening daily with no punishment even when HR knows, and a culture described as "toxic" with "no work life balance" — essentially 24/7/365. Employees report very low base pay, no commission for six months, getting snapped at for having conversations, and management playing favorites regardless of work quality.
- Client-side: clean publicly. Their complaints are internal culture, not customer-facing scandals. But the employee churn and culture issues tell you something about how deals get handled behind the scenes.

**Wheels Up — the big cautionary tale**
- Lost $555 million in 2022 on ~$1.5B revenue. Members held roughly $1 billion in unused flight credits when bankruptcy rumors hit. Founder/CEO Kenny Dichter stepped aside amid CNBC reports the company was consulting bankruptcy advisors.
- Hit with a securities class action alleging materially false financial statements — understating net losses and overstating goodwill.
- Sued FlyExclusive for $33.6–$37.5M after FlyExclusive terminated their fleet agreement on July 4th weekend eve, alleging Wheels Up was insolvent and in default on payments.
- Customers in forums called them "a horrible company" and said they deserved bankruptcy.

**Victor (Fly Victor)**
- Clive Jackson promised transparent pricing with capped 10% markups, but the company accumulated over $50 million in losses. Parent company entered administration (UK bankruptcy equivalent), then underwent a management buyout.
- Got sued for $30 million in a RICO lawsuit over the privatejet.com domain deal. Jackson himself acknowledged the industry problem: brokers daisy-chain, so a single client inquiry generates 9 quote requests and 13 phone calls.

**JetSuite**
- Had backing from JetBlue and Qatar Airways, was growing fast, then Covid hit. Went through Chapter 11 and SuiteKey customers lost $50 million in deposits.

**JetLux (Tomer Osovitzki)**
- Broker arrested for credit card fraud — allegedly manipulated approval systems to push unauthorized charges. Government alleged $1.3 million in fraudulent charges. Was named in a lawsuit by Silver Air suing the Kardashians for $225K in unpaid charter bills.

**Private Jet Charter (UK — Hugh Courtenay)**
- Ran a "pay twice" scam: client pays in full, then right before the flight the broker claims they couldn't transfer the money and asks the client to pay the operator directly. First payment never returned. When exposed, they just rebranded under a new company name with the same logo.

**Industry-wide structural complaints (the real OSA ammunition):**

1. **Hidden fees everywhere.** The main customer concerns are being overcharged and strict cancellation terms. De-icing, fuel surcharges, crew overnight fees, repositioning — all appear post-quote.

2. **Bait-and-switch jet cards.** Some brokers advertise guaranteed-rate jet cards on their websites but don't actually sell them — it's just for SEO to get phones ringing, then they push dynamic pricing.

3. **No price transparency.** Brokers are "multipliers" who make money whenever they can, and clients often accept quotes without enough comparisons in a non-transparent market.

4. **Grey charters / illegal operators.** Proliferated during COVID — uncertified Part 91 aircraft flying commercial flights without proper insurance, maintenance, or pilot qualifications.

5. **Broker daisy-chaining.** Victor's own founder admitted clients go through multiple brokers generating redundant quote requests — massive inefficiency that inflates costs.

**What Paramount does RIGHT (your main named competitor):**
Paramount is annoyingly clean. 325+ Trustpilot reviews at 5 stars, Glassdoor reviews praising the CEO. They claim to reject 73% of legal operators and show "wholesale" pricing. They're the hardest to attack directly.

**Your OSA angle from all this:**
The structural complaints — opacity, hidden fees, broker conflicts, daisy-chaining, bait-and-switch pricing — are exactly what your zero-commission marketplace and pre-calculated Quote Agent solve. The trust deficit is massive and the incumbents are either scandal-ridden (Wheels Up, Victor, JetLux) or opaque by design (ACS, most traditional brokers). "Vetted by an airline pilot" hits different when the industry's trust layer is this thin.

Want me to compile this into a competitive intelligence doc for OSA-Brain?

---

## Phelipe

They show wholesale which means they are transparent?

---

## Claude

Phelipe is questioning whether Paramount showing "wholesale" pricing actually means transparency.No. Showing "wholesale" is a marketing move, not real transparency.

Here's the problem: when Paramount says they show you the "wholesale" cost, they're showing you *their* buy price from the operator — but you have no way to verify that's actually what the operator quoted them. They control both numbers. The "wholesale" price could already include margin baked in before they show it to you, and then they add their disclosed fee on top.

True transparency would mean the client sees the operator's actual quote directly — which is what OSA's model does with the Quote Agent pre-calculating the real price and Guardian validating the mission before a single call goes out.

Paramount's model is still: operator quotes Paramount → Paramount presents "wholesale" to client → client trusts Paramount's word on what wholesale means → Paramount adds their fee. The client never touches Avinode. The client never sees the raw operator quote. It's transparency theater.

It's like a car dealer saying "I'll show you the invoice price" — that invoice price already has holdback and dealer incentives baked in that you'll never see.

OSA's structural advantage: you're building a system where the price intelligence layer (Thompson Sampling) and the zero-commission marketplace model eliminate the *incentive* to hide margin. That's the difference between claiming transparency and having a structure where opacity literally can't exist.

---

## Phelipe

Wait to they show their operator price?

---

## Claude

Phelipe is asking whether Paramount actually shows the operator's price to the client. Let me look back at what the search results said.

From the search results, the Paramount website said reviewers mention PBJ shows them the "wholesale" cost. But I don't have concrete details on exactly what they disclose. Let me be honest about what I actually know vs. what I assumed.Honestly, I'm not 100% sure from what I found. The search results said reviewers mention Paramount shows the "wholesale" cost, but the exact mechanics — whether that means the literal operator quote or just a lower-looking number they label "wholesale" — wasn't clear.

Let me dig deeper.
```
This block is not supported on your current device yet.
```

Now I have the full picture on Paramount's model.OK so I was wrong to dismiss them. Paramount actually does show the operator's price.

Since 2010, Paramount has shown every detail of the flight — including the broker markup and the operator wholesale price to the broker — fully transparent to the client. Their SVP said publicly: "No broker I know of reveals their true markup, except for PBJ. The typical markup by brokers in the industry is 15-30%. We offer wholesale pricing plus a 10 to 11% fixed management fee."

They gave a concrete example: a Gulfstream IV London to New York typically sells retail at $60-70K but the broker buys it for as little as $40K. Most brokers including ACS provide a single "all-in" price where profit margin is undisclosed.

So Paramount is genuinely doing what you assumed nobody was doing. Their model: competitive bidding among operators → pass through the winning operator's wholesale price → add a fixed 10-16% management fee on top, disclosed on the invoice.

**What this means for OSA:**

Paramount already occupies the "transparency" lane. They've been doing it since 2010. Your differentiator against them isn't transparency — they beat you to it. Your differentiators are:

1. **Zero commission vs. their 10-16% fee.** OSA's 2% payment processing is structurally cheaper.
2. **AI pre-calculation vs. their human bidding.** Their "competitive bidding" still requires brokers to manually call operators. Your Quote Agent does this at machine speed.
3. **Marketplace vs. broker model.** They're still the intermediary. OSA lets operators and clients connect with less friction.
4. **Pilot-level domain expertise baked into the AI**, not just a human advisor on the phone.

But don't position against Paramount on transparency — they'll eat you alive on credibility there with 20 years of track record. Position on cost structure and speed. Their model is transparent but still *expensive*.

---

## Phelipe

Can you find new news quotes on reddit or forum from them?

---

## Claude

Searching for reddit/forum discussions about these brokers.
```
This block is not supported on your current device yet.
```

No Reddit results. Let me try searching Reddit directly.
```
This block is not supported on your current device yet.
```

No results. Let me try differently.
```
This block is not supported on your current device yet.
```

Reddit is just not producing results for this niche. Let me try one more search.
```
This block is not supported on your current device yet.
```

Found FlyerTalk and PPRuNe forum content. Let me share what's useful.Honest answer: Reddit has almost nothing on charter broker complaints — the private jet customer base doesn't hang out there. But I found gold on **FlyerTalk** and **PPRuNe** (Professional Pilots Rumour Network), which are the actual forums where this audience lives.

**FlyerTalk (charter customers):**

One customer said: "When I first began to charter I would shop around with several brokers to try and obtain the best price. It was a surprise to me just how many different prices there were for the same aircraft." He added he still wonders "how much commission he is adding on the trips, and how much I would save if I was able to receive the quotes at NET price."

That's your customer pain point in their own words — they *know* they're not seeing net price and it bugs them, but they accept it because shopping around takes too much time.

Other FlyerTalk highlights: A broker confirmed standard markup is around 10% with about 5% standard deviation either way. Users noted Sentient Jet sends "1,000,000 emails" but "the rates don't make sense," and XO's Citation X coast-to-coast went from $19K to almost $30K.

**PPRuNe (operators/pilots):**

This is where the real industry frustration lives. An operator trying to approach a UK broker was told: "We never disclose fees as they are unique to each booking and private to us! No broker will ever disclose this!"

A pilot/industry person responded with the kill shot: "Estate agent — full disclosure/regulated. Travel agent — full disclosure/regulated. Insurance broker — full disclosure/regulated. Stock broker — full disclosure/regulated. It's about time that brokers woke up... Isn't it a bit mad that anyone can start a small company, call themselves Private Jet Flights 4U Ltd, and sell a $200K charter without any regulation, industry oversight or qualification, yet you can't sell a £50 seat on a scheduled flight without an ATOL licence?"

**NBAA Conference (March 2026 — literally last week):**

Industry panelists said digital platforms can be misleading — some show customer ratings of aircraft, but "a closer inspection reveals the same reviews posted repeatedly to make it appear like a genuine rating system."

A broker in the audience admitted he lost a million-dollar charter client after recommending a low-price operator. He warned the client about reliability issues, but the client lost trust when the operator failed to perform.

**Bottom line for OSA content:** FlyerTalk and PPRuNe are where your beachhead customers lurk, not Reddit. The pain points are consistent: price opacity, broker markup mystery, no way to verify net operator pricing, and zero regulation of who can call themselves a broker. That PPRuNe quote about regulation is basically an argument for OSA's existence.

---

## Phelipe

Can you find quotes from paramount like the invoice?

---

## Claude

Phelipe wants to see actual Paramount invoices or screenshots showing their transparent pricing breakdown.
```
This block is not supported on your current device yet.
```

No actual invoice screenshots found. Let me summarize what's confirmed.No actual invoice screenshot exists publicly — they wouldn't post that with client data. But here's exactly what the invoice structure looks like based on all confirmed sources:

**Paramount's invoice line items (confirmed):**

On every invoice, you see exactly what the operator is being paid and exactly what PBJ is earning.

Their invoices break down the operator price — every quote shows the actual operator cost plus their fixed management fee.

**The exact markup tiers (confirmed by Private Jet Card Comparisons):**

Black Tier ($1M deposit): wholesale + 10% or $1,000 minimum, capped at $30,000 for trips over $300K.

Emerald ($100K deposit): wholesale + 16% or $1,600 minimum. Gold ($250K deposit): wholesale + 14% or $1,400 minimum. Platinum ($500K deposit): wholesale + 12% or $1,200 minimum.

**So a real-world example would look like:**

- Operator wholesale quote: $40,000
- PBJ management fee (Emerald tier, 16%): $6,400
- **Client pays: $46,400**

Versus industry norm where you'd just see: **$52,000** with no breakdown.

**The key thing for OSA:** Even with this transparency, Paramount is still charging 10-16% on top. On a $40K flight that's $4,000-$6,400 in broker fees. OSA's 2% payment processing on $40K = $800. That's a 5-8x cost difference on every single flight — and you can show the same operator price transparency Paramount does, but without the management fee layer.

The question you should be asking operators: "Would you rather give 10-16% to Paramount or 0% to OSA and get clean holds with 70%+ conversion rates?" That's the operator-side pitch that Paramount can't match.

---

## Phelipe

Can you find invoices of any top 10 brokers?

---

## Claude

Let me search for actual invoice examples/screenshots from any major charter brokers.
```
This block is not supported on your current device yet.
```

Let me try to find evoJets which claims to have sample invoices.
```
This block is not supported on your current device yet.
```

Let me fetch evoJets page properly.
```
This block is not supported on your current device yet.
```

Got the evoJets sample invoice. But notably, it does NOT show broker markup as a line item.Here's what I found — and this is the key insight:

**evoJets published a sample invoice** (LA to Aspen roundtrip, midsize jet):

- Flight Time (5hrs @ $3,400/hr): $17,000
- Fuel Surcharge: $550
- Crew Fees: $600
- Landing Fees: $750
- Subtotal: $18,900
- Federal Excise Tax (7.5%): $1,417.50
- **Total: $20,317.50**

Notice what's **missing**? The broker's commission. It's baked into the hourly rate or hidden somewhere else. There's no line that says "evoJets fee: $X." That's the standard industry invoice — it looks transparent because it itemizes operational costs, but the broker margin is invisible.

Business Jet Traveler confirmed this directly: "Don't expect line-item invoices from all of them. 'We prefer not to give a breakdown because we want to keep it simple,' said one charter company CEO."

**No broker besides Paramount publicly shows their actual margin as a separate line item.** Every other "transparent" invoice I found itemizes flight time, fuel, landing fees, crew, FET — but the broker spread is embedded in the hourly rate. The client sees $3,400/hr but has no idea if the operator quoted $2,900/hr and the broker pocketed $500/hr.

This is actually huge for your positioning. The entire industry's version of "transparency" is itemizing *operational* costs while hiding the *brokerage* cost. Even evoJets, which literally markets "sample invoices with detailed price breakouts," doesn't show their cut.

**OSA content angle:** Screenshot that evoJets invoice, put it next to what an OSA invoice would look like (operator cost + 2% payment processing, clearly separated), and let the visual do the talking. That's a Loud Hawk post that writes itself.

---

## Phelipe

What are the pure brokers with app?

---

## Claude

Quick answer from what I already know plus a fast search.
```
This block is not supported on your current device yet.
```

Good. Let me compile the pure brokers with apps.Here's the landscape of **pure brokers (own zero aircraft) with booking apps** as of early 2026:

**The new wave (startups):**

- **FlyHouse** — Reverse auction model where operators bid against each other and price drops over 60 minutes. Claims 30-second booking. Built on acquisition of JetASAP. Raising at $500M pre-money valuation, projecting $2.64B revenue, planning IPO within 2-3 years. Has FriendShare seat-splitting feature.

- **Elevate Jet** — AI-powered instant pricing across six aircraft categories. Launched Feb 2026. Uses AI to manage real-time expenses, multicity itineraries, and aircraft feasibility — flags hidden complexities upfront. Backed by Private Jet Services Group.

- **Jettly** — Marketplace/broker with app, emphasizes empty legs and price comparison.

- **Levo.aero** — Another new entrant in the instant booking space.

- **FlyUSA** — App with real-time pricing. Operates both as broker and has its own AOC (Part 135 certificate), so hybrid model.

**Established players with apps (hybrid broker/operator):**

- **XO** (Vista Global) — Largest scale app. Pure broker for third-party fleet + access to Vista's owned fleet. 2,200+ aircraft.
- **Wheels Up** — App-first, but also operates owned fleet. Post-Delta rescue.
- **Victor** — App with transparent pricing claims, post-administration management buyout.

**What none of them have:**

- Zero-commission model
- Pre-calculated pricing before contacting operators
- Pilot-level domain expertise in the AI layer
- Hold conversion rate as the core operator value prop

Doug Gollan of Private Jet Card Comparisons noted: "The best brokers could do the same thing in about an hour, with more specific details about the aircraft." The apps are solving speed, not trust or cost structure.

**FlyHouse is your closest comp and most dangerous competitor.** Their reverse auction is similar to your competitive bidding concept, and they're well-funded. But they're still taking a broker cut and their "Airbnb for jets" framing is operator-centric, not client-fiduciary. OSA's clean hold model with 70%+ conversion is a fundamentally different value prop to operators than FlyHouse's auction chaos.

---

## Phelipe

What is the main thing nbaa gives?

---

## Claude

Quick factual question about NBAA.
```
This block is not supported on your current device yet.
```

Simple answer.The three big things NBAA gives:

1. **Lobbying/advocacy** — They're the leading organization in Washington advocating for business aviation before Congress, government agencies, courts, and international forums. Airport access, airspace protection, fighting user fees and taxes. This is the core product.

2. **Events/networking** — NBAA-BACE (the big annual convention), Schedulers & Dispatchers Conference (where all the broker/operator deal flow happens), regional forums. 11,000 member companies worldwide.

3. **Operational resources** — They maintain a desk at the FAA's Air Traffic Control System Command Center, provide safety education, airspace alerts, tax guidance, and a member directory with 200+ product/service categories.

For OSA specifically, the Schedulers & Dispatchers Conference is where your operator relationships get built. That's where brokers and operators meet face-to-face. The March 2026 one in Cleveland that generated all those quotes I found earlier — that's the room you eventually need to be in.

---

## Phelipe

Who has the best app?

---

## Claude

Let me search for comparisons of private jet booking apps.
```
This block is not supported on your current device yet.
```

Let me give a quick ranking.Based on everything reviewed:

**XO wins on scale and polish.** Largest bookable network (2,400+ aircraft), shared-seat pricing, instant booking technology described as "best-in-class." Backed by Vista Global's deep pockets. The benchmark app everyone else is chasing.

**Elevate Jet wins on intelligence.** It passed tests other apps fail — wouldn't let you book a jet into Santa Monica (runway too short for charter jets), and only showed nonstop-capable aircraft for Hawaii. Uses AI to evaluate whether a jet can actually fly a given route by accounting for fuel, range, crew limits, and airport constraints. This is the closest to what OSA's Dumont pipeline should feel like to a user.

**FlyHouse wins on concept/buzz.** Reverse auction, FriendShare seat-splitting, 30-second booking. But industry insiders are skeptical — one source said to meet 2026 revenue targets they'd need major acquisitions. More sizzle than steak right now.

**Everyone else is mediocre.** Jettly, PrivateFly, Victor — functional but not differentiated. Wheels Up's app is fine but the brand is damaged.

**For OSA's roadmap:** Elevate Jet is the design/UX comp to study. Their AI feasibility layer (can this jet actually fly this route?) is what your Guardian agent does. But none of these apps solve the fundamental problem: they're all still taking a broker cut and none show the operator's actual price. The app is the wrapper — OSA's structural advantage is what's inside.

---

## Phelipe

Who do you think designed elevate jets app?

---

## Claude

Let me search quickly.
```
This block is not supported on your current device yet.
```

They built it in-house.Built in-house. The app is powered by "Ruby," their proprietary agentic AI, built on 30 years of operational data. Greg Raiff (founder/CEO) emphasizes it was built by an aviation company, not a tech company — no outside investment, no private equity.

Their tech team is based in **Plano, TX** and reports to a CTO. They're currently hiring a UX/UI designer — Figma, React/Vue, HTML/CSS/JS — to own end-to-end design across web, internal apps, and customer-facing products. The fact they're hiring now tells you the app is still early and they're iterating.

Tech stack from the job posting: Figma for design, React or Vue for frontend, ClickUp for project management, GitHub, UserTesting/Maze/Hotjar for UX research.

Key detail: Raiff said "the biggest challenge in applying AI to private aviation is ensuring the technology serves the business and not the other way around. We measure success not in technology metrics, but in outcomes: booking conversion, client satisfaction, and the speed and accuracy of the booking experience."

That's basically your Dumont philosophy stated by a competitor. The difference: they have 30 years of data and zero outside capital. You have zero data but a structurally better economic model (2% vs their undisclosed broker margin) and pilot-level domain expertise baked into the AI rather than retrofitted onto a legacy broker operation.

---

## Phelipe

If yu had say what company would kill in the game of this app who would be? Like zillow ramp stripe idk think the guys or companies that would make the app really sticky
Zach Wilson’s core argument maps cleanly to what you’re building with Dumont.
The key takeaway: don’t dump everything into the agent’s context. Instead, pre-compute purpose-built data slices — “customer_churn_last_28days” in his example, or in your case something like “operator_quote_history_KJOT_midsize” — so the agent picks the right pre-aggregated dataset for each task rather than reasoning over raw everything.
His “action-oriented architecture” diagram (image 2) is basically what you’re already designing: data flows in, LLM acts on it in near-real-time, decision happens in minutes not months. That’s the Quote Agent pre-calculating prices instead of waiting for Avinode RFQ round-trips.
The practical implication for OSA: as you build out Dumont’s orchestrator pattern, design your data layer around question-specific contexts from the start. Operator reliability scores, route pricing histories, aircraft availability windows — each as a named, scoped dataset the orchestrator can select from, not one massive table it has to parse every time.
511 likes, 56 comments, Business Insider reposting — this framing is resonating. Worth noting Zach’s content style too: strong opening hook, clear problem→solution arc, visual diagrams. Very aligned with the Loud Hawk editorial approach you’re building.

---

## Claude

Phelipe is asking which existing tech company or team could build a killer private aviation booking app - thinking about the DNA/talent that would make it sticky. He's thinking about companies like Zillow (real estate marketplace), Ramp (fintech/cards), Stripe (payments infrastructure).

Let me think about this practically.Great question. Here's who would absolutely murder this if they decided to build it:

**Ramp** — This is the scariest fit. They already own the corporate card and expense layer for exactly the companies whose founders are your beachhead customers. They know who's spending $30K+ on travel. They have the payment infrastructure, the spend intelligence, the employer-employee trust relationship. If Ramp built a charter booking layer on top of their card product, they'd have distribution + payments + data flywheel from day one. Their DNA is "show you where you're overpaying" — that's literally OSA's pitch.

**Stripe** — They wouldn't build the app, but whoever builds on Stripe Connect for the payment infrastructure between client → platform → operator has a massive advantage. Stripe's marketplace payout rails are purpose-built for the three-party flow you need. They're the picks-and-shovels play.

**Faire** — Wholesale marketplace connecting brands to retailers. Their DNA is exactly "show the wholesale price, transparent markup, let buyers compare." Transpose that to operators and charter clients and you have OSA's marketplace model.

**Robinhood/Public** — They democratized access to something previously opaque and gatekept by intermediaries. The UX philosophy of making complex financial products feel simple is what the charter app needs. Their controversial insight was: remove the commission. Sound familiar?

**Zillow** — The Zestimate concept maps directly to your Thompson Sampling pricing intelligence. Pre-computed price estimates for any route before you even talk to anyone. That's your Quote Agent.

**The actual answer though?** The company that kills this is the one that combines **Ramp's spend intelligence + Faire's wholesale transparency + Robinhood's zero-commission model + Zillow's pre-computed pricing**. That's literally what you're building with OSA.

Re: Zach Wilson's architecture — his point about pre-computed data slices is exactly right for Dumont. Don't make the Quote Agent reason over every operator in Avinode every time. Build scoped datasets: `route_pricing_TEB_OPF_midsize_30d`, `operator_reliability_score_XYZ_air`, `aircraft_availability_window_N123AB`. The orchestrator picks the right slice, the agent acts on it. That's how you get sub-minute quotes instead of the industry's 2-hour broker loop.

The stickiness comes from the data flywheel: every completed deal makes the pricing intelligence better, which makes quotes faster and more accurate, which drives more deals. That's the Zillow Zestimate effect applied to charter pricing. No incumbent has this because none of them are capturing structured deal data at the transaction layer.

---

## Phelipe

I wanna know who to "copy" to design the best UX for private charter brokerage app

---

## Claude

Phelipe wants UX inspiration for OSA's app. Let me think about which apps have the best UX patterns that map to charter brokerage needs, rather than searching broadly.The apps to study, mapped to the specific UX problem each solves for you:

**For the quote/pricing experience:**
- **Google Flights** — The price calendar, the "track prices" toggle, the way it shows you alternatives ("$200 cheaper if you fly Tuesday"). Your Quote Agent output should feel like this. Pre-computed, visual, instant.
- **Robinhood** — How they make a complex financial transaction feel like one tap. The confetti moment. Charter booking confirmation should feel this clean.

**For the trust/transparency layer:**
- **Carfax/Carvana** — Vehicle history report before you buy. That's your Guardian safety report. Operator rating, aircraft tail number history, crew credentials — presented like a Carfax report the client can read in 30 seconds.
- **Wise (TransferWise)** — The way they show "here's the real exchange rate, here's our fee, here's what your bank would charge." That exact pattern is how you show operator wholesale price + OSA's 2% vs what a traditional broker would charge. Side-by-side cost transparency.

**For the marketplace/operator relationship:**
- **Faire** — How they present wholesale products to retailers. Clean cards, trust badges, reorder simplicity. That's your operator catalog.
- **OpenTable** — Restaurant availability in real-time with confirmed bookings. Your clean hold concept is basically OpenTable for jets — confirmed slot, not a tentative inquiry.

**For the overall app shell and feel:**
- **Mercury (banking)** — Clean, premium fintech for startups. Your beachhead customer (post-raise founder) already uses Mercury. Match their aesthetic expectations. Dark mode, minimal, data-forward.
- **Amex Centurion/Platinum app** — How luxury financial services feel on mobile. Not flashy, just confident and competent.

**For the content/education layer (Loud Hawk integration):**
- **Coinbase Learn** — How they embed education into a transaction app. Your first-time charter client needs "what's a midsize jet vs super-mid" explained without feeling stupid.

**The one to actually reverse-engineer pixel by pixel:**
- **Wise.** Their transfer flow is your booking flow. Origin → destination → amount → "here's the real price breakdown" → confirm → track. Every screen maps. And their brand positioning ("the old way is broken, we show you the truth") is basically OSA's positioning translated to fintech.

Go download Wise right now and do a fake transfer. That's your app.

---

## Phelipe

Analysis of elevate jets app

---

## Claude

Let me search for more details about the Elevate Jet app UX, screenshots, reviews.
```
This block is not supported on your current device yet.
```

Good, I have a comprehensive picture of Elevate Jet's app. Let me synthesize.Here's the breakdown:

**What they got right:**

- **Feasibility-first AI.** Won't let you book a jet into Santa Monica (runway too short) or show non-nonstop aircraft for Hawaii. Other apps fail these tests. This is the Guardian agent concept — don't let the client book something that physically can't work.

- **300-point checklist stored per client.** Catering preferences, timing sensitivities, privacy expectations, onboard amenities — all stored for future bookings. This is smart retention design. Second booking is faster than first.

- **Flight grading system.** Evaluates crew performance, FBO quality, aircraft condition, cabin design. Basically a quality score per flight option — something no other app surfaces.

- **No membership required.** No onboarding friction, works for first-time users. Smart for acquisition.

- **"Aman or Four Seasons" aesthetic.** Doug Gollan described the design as luxury hospitality-grade.

**What they got wrong / gaps:**

- **No price calendar.** Unlike competitors, there's no calendar to view price variations by date. Huge miss. Google Flights proved this is the #1 feature for price-sensitive bookers. Your beachhead customer (post-raise founder doing 2-8 trips/year) absolutely wants to see "fly Tuesday instead of Friday, save $4K."

- **100% cancellation penalty on one-way.** Unless you put $100K on account. That's brutal for first-time users and kills trust.

- **No price transparency on margin.** They show "transparent pricing" but nowhere do they show the operator wholesale cost vs their markup. It's Paramount-lite transparency — itemized costs, hidden margin.

- **Still a broker.** The app is a prettier front door to the same broker model. Ruby prices the flight, but the economic structure underneath is traditional markup.

- **Targeting 10K users by year end.** CMO told press they're aiming for 10,000 active users by end of 2026. That's tiny. Tells you adoption is early.

- **No social/community layer.** FlyHouse has FriendShare. Elevate has nothing. For your beachhead (founders who know each other), a social booking feature would be sticky.

- **React/JS app, still hiring their first dedicated UX designer.** The app shipped before they had a full-time UX person. That means V1 was likely built by engineers with design taste, not design-led. It'll get better but it's not design-mature yet.

**What OSA should steal:**

1. The feasibility check (your Guardian already does this)
2. The 300-point preference storage (build this into Dumont's client memory layer)
3. The flight grading system (your operator reliability scores)
4. The "no membership required" zero-friction entry

**What OSA should beat them on:**

1. Price calendar (Google Flights pattern)
2. Actual margin transparency (Wise pattern — "here's operator cost, here's our 2%")
3. Cancellation terms that don't punish first-timers
4. Pre-computed pricing via Thompson Sampling so quotes are instant without needing to be "guaranteed at inflated levels"

Elevate is the best app in the space right now, but it's a luxury wrapper on a traditional broker. OSA's opportunity is to be the Wise to their traditional bank.

---

## Phelipe

Who has the most amount of users?

---

## Claude

XO likely has the most users based on what I already found - they mentioned 2 million downloads. Let me confirm.From what's already in the research:

**XO** — More than 2 million downloads. Not even close. Backed by Vista Global's infrastructure and marketing spend.

Everyone else is way behind:

- **Wheels Up** — ~12,000 members (but shrinking, down from peak)
- **FlyHouse** — 2,300 aircraft listed, user count not disclosed but early
- **Elevate Jet** — Targeting 10,000 active users by end of 2026, meaning they're well below that now
- **Jettly** — Not disclosed
- **Victor** — Had 175,000 registered names and 3,000 unique booking customers before their administration/restructuring

XO wins by a landslide because Vista Global (parent) spent billions acquiring companies and funneling users into one app. Downloads ≠ active bookers though — most of those 2M probably opened it once to browse prices. The actual booking conversion is likely a tiny fraction.

The real question for OSA isn't user count — it's deal volume. A platform with 500 users doing 8 trips/year each at 70%+ hold conversion is more valuable than XO's 2M downloads with unknown conversion. That's the marketplace density play you're building toward.

---

## Phelipe

How to acquire app user like a freak? With quality. What campaign. Organic that would make everyone wanna download load. Look at past chats for our calculators and index that could be embedded so we get people using as much as possible with a easy conversion

---

## Claude

Phelipe wants me to look at past chats for calculators and tools they've discussed, then build a user acquisition strategy around them.
```
This block is not supported on your current device yet.
```

Good, found the calculator discussion. Let me search for more.
```
This block is not supported on your current device yet.
```

Good. Let me search for more specific past chats about the tools/calculators.
```
This block is not supported on your current device yet.
```

Now I have the full picture. Let me synthesize a killer acquisition strategy using the tools/calculators from past chats as the app download funnel.OK, I've got the full map from our past sessions. Here's the play:

**The core insight: your website tools ARE the app funnel.**

You don't market the app. You market the tools. The tools create the habit. The habit creates the download.

**The Acquisition Stack (in build order):**

**Layer 1 — Free web tools that capture intent (no app needed)**

These live on orangesunshine.io, rank in Google, and collect emails:

1. **Charter Cost Calculator** — Origin, destination, date, pax count → instant price range with the Wise-style breakdown ("operator cost: $18,500 / typical broker markup: $2,700 / OSA: $370"). Every competitor has a version but none show the markup split. CTA: "Get exact pricing in the app"

2. **Charter vs Commercial Calculator** — From your Innovation Thesis (#66). Input hourly rate, team size, trips/year → shows the productivity math. "Your team loses $72,000/year flying commercial on this route." CTA: "See what charter actually costs for your routes"

3. **Runway Analyzer** — "Can a Phenom 300 land at Aspen?" No good tool exists for this. Pilots know, clients don't. Your ATP credential makes this content untouchable. CTA: "A pilot checks every flight. Get a quote."

4. **Aircraft Comparison Tool** — Side-by-side specs, cabin photos, range maps. "Phenom 300 vs Citation Latitude" gets searched and nobody has a great interactive version.

**Layer 2 — Gated tools that require account (email or app)**

5. **Route Price Index** — Your ADS-B heat map data turned into a consumer product. "Chicago to Aspen averages $38K in January, $29K in March. Best day to book: Tuesday." This is the Zillow Zestimate for charter. Nobody has this. Gate it behind email.

6. **Deal Alert / Price Watch** — "Set an alert for TEB→PBI under $22K." Requires the app. This is the Google Flights price tracking feature. Once someone sets an alert, they're checking the app regularly.

7. **Empty Leg Tracker** — Real-time repositioning flights on your operator network. This is the #1 reason casual charter shoppers download any app. Gate it behind app download.

**Layer 3 — App-only features that create the habit loop**

8. **Quote History + Savings Dashboard** — Every quote you've gotten, what you paid, what a traditional broker would have charged. "You've saved $14,200 across 3 flights." This is Robinhood's portfolio view for charter.

9. **Flight Brief** — The Guardian safety report + trip details + weather + FBO info packaged as a beautiful pre-flight briefing. Push notification 24hr before departure. This is the "open the app" trigger.

10. **Pilot's Notes** — Your personal operational commentary on each route. "Approach into ASE is challenging, here's what your crew will deal with." Nobody else can write this. It's content that makes the app feel like having a pilot friend.

**The Funnel Math:**

```
Web tools (SEO) → 20K monthly visitors (month 5-6)
    ↓ 3% email capture = 600 emails/month
    ↓ 10% download app = 60 app installs/month
    
Route pages (SEO) → 15K monthly visitors (month 5-6)  
    ↓ 2% quote request = 300 leads/month
    ↓ 5% download app = 15 app installs/month

LinkedIn/Loud Hawk → 5K monthly visitors
    ↓ 5% email = 250/month
    ↓ 15% download app = 37/month

Total: ~112 app installs/month by month 6
```

That's modest. Here's how you go nuclear:

**The Viral Mechanic — "What's Your Broker Actually Charging You?"**

Build a one-page tool: input any charter quote you've received from any broker. OSA's pricing engine reverse-engineers the probable operator cost and shows the estimated markup. Share button generates a card: "I just found out my broker marked up my last flight 28%. Check yours."

This is the tool that spreads. Founders share it in group chats. It goes on Twitter/X. It's inherently viral because it reveals something people suspected but couldn't prove. Every share is an OSA brand impression. Every use captures a lead who just learned they're being overcharged.

**The quality filter:** you're not getting random downloads. Every person who uses these tools self-selects as someone who charters or is considering chartering. That's why 100 quality app users who actually book flights beats XO's 2M downloads of people who opened it once to look at prices they can't afford.

**Build sequence:**
- Week 1-2: Charter Cost Calculator (web, React component)
- Week 3-4: Aircraft Comparison Tool (web)
- Week 5-6: "What's Your Broker Charging" viral tool
- Month 3: App shell with Deal Alerts + Empty Leg Tracker
- Month 4: Full app with Quote History + Flight Brief

The tools drive the downloads. The downloads aren't the goal — the bookings are. But every tool earns trust before asking for a transaction.

---

## Phelipe

Dude if we make a tool where people can drop their pdf, email, invoice into the an ai chat like we do here. And reverse engineer to say the markup. We earn trust ( transparency- now everyone knows) and we also get quote data from everyone! Is that feasible?

---

## Claude

This is a brilliant idea. Let me think about feasibility.That's the single best idea you've had for OSA. Full stop.

**Why this is genius:**

1. **You get their data.** Every uploaded quote is a real operator price, real route, real date, real broker markup. That's the training data for Thompson Sampling that would take you years to build through your own deals. Users literally hand you the market intelligence for free.

2. **You earn trust by showing the truth.** The user uploads a quote, your AI says "the operator probably charged $19,200, your broker added ~$5,800 (30%). Industry average markup on this route is 18-25%." They're furious at their broker and grateful to you.

3. **The CTA writes itself.** "Want this same flight at 2% instead of 30%? Get an OSA quote." You just converted a competitor's customer using the competitor's own quote as the sales tool.

4. **It's a data moat.** Every quote uploaded makes your pricing model smarter, which makes your estimates more accurate, which makes more people trust the tool, which gets more uploads. Classic data flywheel.

**Feasibility — 100% yes.**

The AI piece is straightforward. Charter quotes and invoices follow predictable formats: aircraft type, route, flight time, hourly rate, fuel, landing fees, FET, total. Claude or any LLM can parse a PDF/image/email and extract those fields with high accuracy. Then you run it against your pricing model:

```
User uploads: TEB→PBI, Citation X, $42,000 total
AI extracts: 2.5hr flight, Citation X
Your model calculates: 
  - Estimated operator cost: $28,000-32,000
  - Fuel: ~$4,200
  - Fees: ~$2,800  
  - Probable operator total: ~$31,000-33,000
  - Broker markup: ~$9,000-11,000 (26-35%)
  - OSA would charge: $33,000 + 2% = $33,660
  - You'd save: ~$8,340
```

**How to build it:**

Phase 1 (week 1): Simple web page. Upload PDF/screenshot/paste text. Claude API parses it, returns the breakdown. No account needed. Free. Shareable result card.

Phase 2 (month 1): Add account creation to save quote history. "Upload all your quotes, see your total overpayment this year." Now you have a registered user.

Phase 3 (month 2): Move it into the app. Push notification: "You uploaded 4 quotes last month. You overpaid an estimated $23,400. Want us to requote these trips?"

**The data you collect per upload:**
- Route (origin/destination)
- Aircraft type
- Date/season
- Total price
- Line item breakdown (if available)
- Broker name (from the letterhead/email)
- Which broker is most expensive on which routes

After 1,000 uploads you have the most comprehensive broker markup database in private aviation. Nobody has this. Not Avinode, not ARGUS, not Private Jet Card Comparisons. You'd know exactly what every major broker charges on every major route.

**The legal question:** can you do this? Yes. The user owns their quote. They're sharing it voluntarily. You're providing analysis of a document they gave you. No different than uploading a medical bill to a cost comparison site. Just make your privacy policy clear about data usage.

**The viral loop:** User uploads quote → sees they overpaid → shares screenshot → friend uploads their quote → repeat. The anger at being overcharged IS the sharing mechanism.

**Name it something sticky.** Not "quote analyzer." Something like **"Fair Flight Check"** or **"Quote X-Ray"** or honestly just **"The Markup Calculator"** — dead simple, everyone knows what it does.

Build this before anything else. This is your Robinhood moment — the tool that makes the industry's dirty secret visible to everyone.

---

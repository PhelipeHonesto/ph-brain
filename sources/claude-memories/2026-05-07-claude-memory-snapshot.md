---
title: Claude Memory Snapshot
exported_date: 2026-05-07
source: claude-memories
type: source
---

# Claude Memory Snapshot

*This is Claude's accumulated memory about Phelipe as of the export date. It represents synthesized context across past conversations.*

**Work context**

Phelipe is the solo founder of Orange Sunshine Aviation (OSA), a bootstrapped AI-native private aviation platform, building part-time while flying the Embraer E175 as a First Officer at SkyWest Airlines. He holds an ATP certificate with CFI/CFII/MEI ratings and an E175 type rating, has no college degree, and holds dual US-Brazilian citizenship. OSA encompasses multiple brands: Loud Hawk (independent aviation intelligence publication), OSA Connect (AI-native charter brokerage), OSA Aircraft (aircraft transactions), OSA Management, and OSA Capital.

**Personal context**

Phelipe grew up in São José dos Campos, Brazil, with deep family roots in aviation (both parents worked at Embraer; his brother Ygor is pursuing cybersecurity). He is based in Illinois and communicates in a direct, fast-paced style — often short bursts — preferring harsh honest assessments over diplomatic framing, and pushing back readily when responses are imprecise or over-engineered. He thinks best by talking and building, and works in short, intense sessions around his flight schedule.

**Top of mind**

Phelipe is deep in Chicago real estate strategy — working through neighborhood selection (Avondale, Albany Park, Belmont Cragin, Portage Park), multifamily underwriting, Cook County tax mechanics, and a hybrid direct-ownership-plus-LP-syndication model. He is also refining OSA's long-term wealth architecture: OSA as the cash-flow engine, real estate as the passive income floor, and angel investing as the upside layer, with the OSA Real Estate Holdings subsidiary strategy as a mechanism to deploy retained corporate earnings into property without dividend taxation. Entity structure decisions are active, including why S-Corp is wrong for OSA and the relevant FINRA licensing path (SIE now, Series 65 at Year 5–7). On the OSA data platform, Phase 2 LLM-augmented entity resolution recently passed its evaluation gate (zero false matches), with the aircraft-to-operator linkage fix — building an `operator_aircraft_link` table and running ER on ~52K tails — identified as the critical next infrastructure step.

**Brief history**

*Recent months*

OSA's data platform has been the primary build focus: FAA-grounded entity resolution for US Part 135 operators, a 352-record ER queue, Firecrawl-based ingestion, and a Supabase Postgres backend with pgvector installed. The MCP server stack is fully operational (dumont-intelligence, ph-brain, osa-data-platform) and connected to Claude Desktop. A live MCP data investigation surfaced four critical gaps: operator_type is 98% null, 74 pending ER reviews with zero reviewed, no cert-class column in faa_operators, and aircraft-to-operator linkage at 0.05% complete. The competitive positioning thesis is crystallized: OSA will be the first commercial aviation intelligence platform combining canonical operator/aircraft entity resolution, ADS-B real-time observation, and provenance-grounded multi-modal RAG for buyer-side charter intelligence — with the Zillow parallel as the strategic playbook (publish free intelligence to win SEO and brokerage distribution, monetize through brokerage and payment processing rather than data subscriptions).

PH-Brain, Phelipe's personal intelligence substrate, is fully operational: Voyage-3-large embeddings at 2048 dimensions, HNSW indexing, hybrid semantic + tsvector search, MCP-exposed to Claude Desktop, and regularly updated via Claude export pipeline. The OSA brand system and website prototype work was also active, with Claude Design used for OSA homepage iteration toward Area 17 / Swiss International Typographic Style aesthetic, and a comprehensive brand system document produced.

Agent framework research covered OpenClaw, Hermes (Nous Research), and their tradeoffs for OSA use cases. Key architectural decisions: the human audit loop in memory engineering is load-bearing (not a scaffold), the OSA data platform follows a four-tier model (S3 Glacier → S3 Parquet → Supabase Postgres → pgvector), and Dagster adopted for orchestration starting Stage 3. LinkedIn excluded from all data sources (ToS, non-negotiable).

OSA's go-to-market foundations were established: beachhead customer is post-raise founders doing 2–8 charter trips/year; real competitive alternative is commercial travel (not other brokers); LinkedIn and Loud Hawk newsletter are P0 channels; NBAA is a non-negotiable conference; the founder advisory program (5–10 high-leverage founders at break-even economics) is the highest-leverage early distribution play. PMF survey designed for post-raise founders with post-trip trigger mechanics.

*Earlier context*

OSA Connect's Dumont agent system was built and deployed to Railway, combining a voice SDR (Vapi + ElevenLabs + Deepgram) with Claude Haiku as the natural language layer. The five-engine OSA platform architecture was locked: OSA Connect, OSA ACMI, OSA Cargo, OSA Aircraft, and OSA Pay (yield-bearing client accounts, 2% payment processing, credit lines). OSA Pay's zero-commission / payment-rail monetization model was validated against Toast, Robinhood, Stripe, and DoorDash analogues. The strategic north star: brokerage is the wedge, zero-commission marketplace is the customer acquisition channel, payment infrastructure with compounding network effects is the actual business.

Programmatic SEO engine built: 50+ route pages live at orangesunshineaviation.com, dynamic sitemap, drip publishing automation via GitHub Actions, and a comprehensive content intelligence layer (writing-guide.md, aircraft-scoring.md, CLAUDE.md, CI/CD pipeline). OSA Charter Index established as the Zillow Zestimate model — transparency is the product, calibration improves with deal volume (±20% launch → ±5% at 500+ deals), with Wise-style Cost Anatomy breakdowns on every route page.

OSA's legal and operational infrastructure was resolved: Delaware C-Corp via Every.io, Mercury banking, DOT Part 295 registration, four-policy insurance stack (GL, E&O, Cyber, Tech E&O/AI Liability), and client/operator agreements via General Legal. Entity is Orange Sunshine Aviation; domain is orangesunshine.com; "OSA" is internal shorthand.

*Long-term background*

OSA originated ~9 months before the earliest conversations, with a pivot to the charter brokerage model roughly 40 days before the March 2026 sessions following market validation. Phelipe spent roughly three years in Denver in hospitality and restaurant operations before entering aviation. His Brazilian roots and family aviation background (Embraer, São José dos Campos) are foundational to his founder-market fit narrative. The core strategic bet established early: OSA as Apple (owns client demand, delivers outcomes) vs. Hamilton AI as Microsoft (sells tools to operators). Loud Hawk was conceived from the start as the editorial gravity well generating zero-CAC audience that converts to brokerage clients — modeled on the Michelin Guide / Morningstar independence framework.
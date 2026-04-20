---
title: Claude Memory Snapshot
exported_date: 2026-04-19
source: claude-memories
type: source
---

# Claude Memory Snapshot

*This is Claude's accumulated memory about Phelipe as of the export date. It represents synthesized context across past conversations.*

**Work context**

Phelipe is the solo founder and CEO of Orange Sunshine Aviation (OSA), a multi-brand AI-native private aviation platform he is building part-time while flying the Embraer E175 as a First Officer at SkyWest Airlines. He holds an ATP certificate with E175 type rating and CFI/CFII/MEI ratings, has no college degree, and has dual US-Brazilian citizenship. OSA's brands include Loud Hawk (independent aviation editorial/media), OSA Connect (AI-powered charter brokerage), OSA Aircraft (acquisition advisory and buy/sell), OSA Management, and OSA Capital — with the latter two kept out of investor and public-facing materials for now.

**Personal context**

Phelipe is based in Illinois, works in short, intense sessions around a reserve flight schedule, and thinks best by talking and building rather than writing. He communicates in a direct, fast-paced style and pushes back on diplomatic hedging — preferring honest, blunt assessments and concrete analogies. He has a strong Brazilian cultural background and dual citizenship.

**Top of mind**

Phelipe is deep in the infrastructure and intelligence layers of OSA, having recently completed a major PostgreSQL migration (SQLite → Supabase) for the Dumont platform, built 15K+ pgvector route embeddings, and established a full three-layer medallion data architecture (S3 raw → Supabase organized → analytics derived). He is actively researching OSA's payment infrastructure positioning (OSA Pay: yield-bearing client accounts, real-time ADS-B-triggered operator settlement, 2% processing) and exploring a closing coordination dashboard opportunity for OSA Aircraft within the aircraft sales escrow ecosystem. The website redesign for the OSA playground repo is underway using an Area 17-inspired design direction (big type, near-monochrome, OSA brand colors: Orange #E74B1D, Near Black #1A1A1A, Cream #F5F0E8).

**Brief history**

*Recent months*

Phelipe completed a comprehensive organic growth and content strategy for OSA and his personal founder brand, landing on LinkedIn and Loud Hawk newsletter as P0 channels, programmatic route pages as P0 for SEO, and a "document the build" content production model (voice memos → AI draft → review). The HAWK multi-agent content system (Scout, Writer, Designer, Conductor, Analyst + Memory Layer) was architected as the content engine, designed to eventually transfer to a future Brand and Content Strategist hire. The beachhead customer is locked as post-raise founders doing 2–8 charter trips per year, frustrated by wasted travel days; the real competitive alternative is commercial first class, not legacy brokers. The buyer-facing category frame is "time infrastructure."

OSA's core product architecture is stable: Dumont is a single intelligent orchestrator agent (not a five-agent pipeline externally) handling Intake, Sourcing, Quote, Scenario, and Guardian functions. OSA Pay is the real long-term business — a zero-commission marketplace monetized via 2% payment processing, with yield-bearing client accounts (Brex/Column N.A. model), credit lines, and real-time operator settlement. The Ghost Positioning Spread (using ADS-B to identify pre-positioned aircraft and eliminate phantom deadhead costs) is the core economic thesis. The Charter Index follows a Zillow Zestimate model: transparency is the product, not precision — current ~12–20% error margin is acceptable, calibrating to ±5% at 500+ deals. Route pages include a Wise-style "Cost Anatomy" breakdown.

The Dumont agent was deployed to Railway (replacing ngrok permanently), integrated with Vapi for voice (ElevenLabs + Deepgram Nova-3), and uses Claude Haiku as the SDR conversation layer. The OSA programmatic SEO site (Next.js, Vercel) reached 40+ route pages across four city hubs with a GitHub Actions drip automation (3 routes per 12 hours from queue). A full intelligence layer was built: writing-guide.md, aircraft-scoring.md, CLAUDE.md, and a Zod validation pipeline with CI/CD. The OSA-Brain Obsidian vault was built as Phelipe's founder second brain and OSA's institutional memory, with 140+ processed conversations, slash command system, and a dual-pipeline architecture (Inbox for Phelipe's output, Raw for external world input).

MCP stack for Claude Code includes Paper, MaxiBestOf (`https://maxibestof.one/mcp-server`), Refero (`https://api.refero.design/mcp`), and Figma via claude.ai connectors only. Key lesson: local-scoped MCPs must be re-added when switching project directories; Paper requires full remove-and-re-add after every restart.

*Earlier context*

OSA's strategic architecture was fully crystallized: charter brokerage as the wedge, zero-commission marketplace as the customer acquisition channel, and payment infrastructure with compounding network effects as the actual business. Six network effects were mapped for OSA Pay. The full five-engine platform was locked: OSA Connect, OSA ACMI (post-seed), OSA Cargo, OSA Aircraft, and OSA Pay. Aircraft transaction advisory was elevated as a high-LTV accelerant ($275–435K in fees per large aircraft sale vs. $3–5K on a charter deal).

Competitive intelligence was built on Hamilton AI ($7.5M seed, operator-side SaaS, assessed as the "Microsoft" to OSA's "Apple"), FlyHouse (most dangerous direct competitor, reverse-auction model), Paramount Business Jets (transparency competitor, 10–16% disclosed fee), and Aviapages (proved demand for free charter tools, no AI or payment layer). The OSA vs. JETNET data strategy was mapped: free public sources (FAA registry, ADS-B community forks, UCC filings, state records) achieve ~68% of JETNET's accuracy on Day 1, scaling to ~91% by Year 5. Aircraft profile pages (Zillow/Carfax model for 170K+ US-registered aircraft) were identified as a category-defining SEO and data moat opportunity.

Positioning was stress-tested against April Dunford, Chris Walker, and Dave Gerhardt frameworks. Key decisions: outcome ownership language (one vetted result delivered, not a list of options), greenfield customer strategy (no incumbent to displace), and "intelligent pricing vs. dynamic pricing" as a key differentiator (Thompson Sampling optimizes for deal closure and gets smarter with every transaction). The investor narrative arc was built: broken market seen from the cockpit → competitors solving the wrong problem → outcome ownership product → payment infrastructure as the real business → founder-market fit.

Pre-seed hiring plan: CTO (equity-heavy, full technical build), Operator Relations (tech person who learns aviation), Brand and Content Strategist (demand engine), Sales Rep (Paramount model, base + commission). Legal infrastructure: Delaware C-Corp via Every.io, General Legal for broker agreements (~$1K), four-policy insurance stack (GL, E&O, Cyber, Tech E&O/AI Liability). Domain: orangesunshineaviation.com (committed, brand cohesion priority).

*Long-term background*

OSA has been in development for approximately 9+ months, with a pivot to the AI-native charter brokerage model roughly 40 days before late March 2026 following market validation. The founding insight — combining ADS-B data, FAA registry intelligence, physics-based pricing, and an ATP pilot's domain expertise into a neutral intelligence layer — remains the north star. The corporate aircraft acquisition thesis (OBBBA 2025 100% bonus depreciation + sale-leaseback + charter revenue offset) was developed as a core OSA Aircraft value proposition. The brand architecture was simplified Jobs-1997-style: OSA as master brand, sub-brands as wordmarks only, Loud Hawk as the sole independently positioned publication with its own visual identity (Deep Purple #432a7a + shared OSA Orange thread). Typography system: Coolvetica + Lexend. Loud Hawk is OSA's zero-CAC content gravity well and the editorial independence is a strategic asset, not a distraction.

**Other instructions**

- When helping with OSA marketing and positioning, blend frameworks from April Dunford (category positioning), Chris Walker (demand creation / dark social), and Dave Gerhardt (founder-led brand building).
- OSA Charter Index follows a Zillow Zestimate model — transparency is the product, not precision. Current ~12–20% error margin is acceptable. Calibration path: ±20% launch → ±12% at 50 deals → ±8% at 200 deals → ±5% at 500+. Route pages include Wise-style "Cost Anatomy" breakdown.
- Building philosophy: build for quality and architectural correctness, not artificial deadlines. Do not pressure Phelipe with launch timelines. When he says to stop with dates, respect it completely.
- Phelipe has no college degree and is not pursuing one. Do not reference any academic affiliation.
- Phelipe is not pursuing YC. Do not frame milestones or priorities around YC batch deadlines. OSA's roadmap is driven by the plan, infrastructure architecture, and thesis.
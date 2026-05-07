---
title: Data modeling fundamentals and entity resolution
created: 2026-04-19T01:16:45.494010Z
updated: 2026-04-19T03:08:38.636651Z
uuid: 4490716e-4118-46de-bc88-fb18545c84fa
source: claude-conversation
type: source
message_count: 6
---

# Data modeling fundamentals and entity resolution

*Summary: **Conversation Overview**

The person is building a business called OSA (with related projects including Dumont Intelligence, OSA Connect, OSA Pay, OSA Aircraft, and Loud Hawk) and is actively developing an AI context system they call OSA-Brain. The conversation covered two connected learning sessions. In the first, the person asked for a comprehensive explanation of data modeling concepts including Master Data Management, Entity Resolution, record linkage, identity graphs, dimensional modeling, Kimball methodology, and Lakehouse Bronze/Silver/Gold architecture. Claude provided detailed explanations connecting each concept to the person's specific use case — aviation data, aircraft identity resolution, operator tracking, and beneficial ownership graphs — and mapped the concepts to a proposed Bronze/Silver/Gold pipeline built on Postgres with Type 2 slowly-changing dimensions.

In the second part of the conversation, the person shared industry research about context engineering emerging as a key AI discipline in 2026, referencing sources including Datafold predictions, Jensen Huang's CES statement, Gartner analysis, Phil Schmid's five-layer framework, and Meta's engineering blog post about their 59-file tribal knowledge system. The person noted that their existing OSA-Brain system — comprising 140 conversation summaries, CLAUDE.md files, lessons.md, and workflow documentation — appeared to match this pattern. Claude confirmed the partial match but drew a clear distinction: the person has built the raw materials but not yet the discipline of compression, retrieval routing, critic passes, or automated refresh that defines mature context engineering practice.

The person then asked Claude to research context engineering comprehensively and explain it from scratch, expressing that the concept was still confusing and asking whether it was simply "a set of md files to create context for the agent so it can operate better." Claude corrected this mental model directly, explaining that context engineering is the discipline of deciding what information the model sees on every single inference call, with markdown files being only one of many mechanisms. The explanation covered the technical reality of context windows, the phenomenon of context rot, the four core operations (write, select, compress, isolate), a five-tier progression from basic prompt engineering to self-maintaining context infrastructure, and research findings that poorly constructed context files actively degrade performance and increase costs. Claude recommended a specific reading list in priority order: Anthropic's context engineering post, LangChain's agent context guide, the Manus lessons post, Meta's tribal knowledge post, and HumanLayer's CLAUDE.md guide. The session ended with Claude offering to apply context engineering discipline to a specific piece of the person's existing setup as a concrete next step.*

## Phelipe

i want to learn more and understant about data modeling.
"Master Data Management" (MDM) — the umbrella term. Big enterprise word for this.
"Entity Resolution" (ER) — the specific problem of deciding which records refer to the same real-world entity.
"Record linkage" — academic term, same thing.
"Identity graph" — when the resolution goes deeper (people, households, devices). Used heavily in adtech.
"Dimensional modeling" / "Kimball methodology" — the broader data warehousing framework. Operators would be a Type 2 slowly-changing dimension.
"Lakehouse architecture" (Bronze/Silver/Gold) — modern cloud data platform shape. Bronze = raw scrape, Silver = cleaned, Gold = canonical.

```
Databricks has excellent writing on this. Airbnb published a classic blog post ("Unified Metadata"). Uber, Netflix, Palantir all have public talks about their implementations.

```

---

## Claude

This is a great instinct — these concepts are exactly the right scaffolding for what you're already building with Dumont Intelligence. Let me walk you through how they actually fit together, because the way they're usually taught makes them sound like separate universes when they're really one stack.

## The core problem, stated plainly

You have messy data coming in from many sources. Same real-world thing shows up with different names, different IDs, different attributes, at different times. You want a clean view.

Every term on your list is attacking some slice of that problem. Let me map them to your world.

## Entity Resolution (ER) — the atomic problem

This is the one you're already doing, whether you call it that or not.

You're staring at FAA registry data, ADS-B squawks, UCC filings, LinkedIn scrapes. "N123AB" in one system is "N-123-AB" in another is a tail number with a trailing space somewhere else. The aircraft that flew KMDW→KTEB at 14:32 UTC and the aircraft registered to Acme Holdings LLC — same jet? Different jet?

ER is the discipline of answering that. It breaks into three steps:

**Blocking** — you can't compare every record to every other record (170,000 aircraft × 170,000 = 29 billion comparisons). You block on something cheap — first three chars of tail number, or ICAO hex — to get candidate pairs down to a manageable set.

**Matching** — for each candidate pair, score how likely they're the same entity. Classic approach is Fellegi-Sunter probabilistic matching (1969, still the foundation). Modern approach is ML — train a model on labeled pairs. Splink (open source, from the UK Ministry of Justice) is the best library for this and it'll map directly onto your use case.

**Clustering** — matches are pairwise but entities aren't. If A matches B and B matches C but A doesn't match C, what do you do? Graph algorithms (connected components, usually) resolve the cluster.

**Record linkage** is literally the same thing. Statisticians called it record linkage starting in the 1940s (Halbert Dunn coined it). Computer scientists rediscovered it in the 90s and called it entity resolution. Same problem, two tribes.

## Master Data Management (MDM) — the organizational wrapper

MDM is what enterprises call it when ER becomes a program instead of a project. It adds governance (who owns the canonical record?), stewardship (who resolves ambiguous matches?), and distribution (how do downstream systems get the golden record?).

For OSA right now, you don't need MDM as a discipline. You need ER as a capability. MDM matters when you have 40 systems writing to the same entity and need political structure around whose version wins. Worth knowing the term because you'll hear it, but don't build MDM infrastructure — build ER pipelines and call them that.

The one MDM concept worth stealing immediately is **the golden record** — the single canonical version of an entity that you compute from all sources. For an aircraft, your golden record is: tail number + ICAO hex + make/model/serial + current operator + current owner + base airport. Every source contributes, none is authoritative on its own.

## Identity graph — ER plus relationships

Identity graph is ER where you care about the edges between entities as much as the entities themselves. Adtech built this out because they needed to answer: this cookie, this device ID, this email, this household — same person? Same buyer unit?

For you, the identity graph is the killer concept. Aircraft → Operator → Management Company → Beneficial Owner → LinkedIn profile → Founder → Company. Each of those is an entity, each edge is a relationship with its own metadata (when did this operator start managing this aircraft, when did this LLC acquire it, etc).

The moment you model this as a graph instead of a bunch of joined tables, a lot of your intelligence queries become trivial. "Show me all aircraft controlled by post-Series-A founders in the Midwest" is a graph traversal. In flat tables it's a nightmare.

You won't necessarily use a graph database (Neo4j, Dgraph) — Postgres with proper relational modeling handles this fine up to surprising scale. But you should think in graph terms even when implementing in SQL.

## Dimensional modeling / Kimball — how to store the resolved data

Ralph Kimball's book (*The Data Warehouse Toolkit*, 1996, still the bible) gives you the vocabulary for how to shape resolved data for analytics.

Two shapes: **facts** (things that happened, usually with timestamps — a flight, a quote, a payment) and **dimensions** (things that exist and have attributes — an aircraft, an operator, a customer, an airport).

Facts are tall and narrow, dimensions are short and wide. A flight fact has maybe 15 columns but millions of rows. An operator dimension has 200 columns and 3,000 rows.

**Slowly Changing Dimensions** is the concept you flagged. When an operator changes its name, or an aircraft changes hands, or a founder's company raises a round — the dimension changed. How do you record that?

- Type 1: overwrite. You lose history.
- Type 2: add a new row with effective_from / effective_to dates. You keep history.
- Type 3: add a new column (previous_name). Rarely worth it.

For OSA intelligence, almost everything is Type 2. You care about who owned N123AB in 2023 vs 2026 because that's market intelligence. Every operator record, aircraft registration, beneficial ownership chain — Type 2.

The canonical pattern: every dimension row has `valid_from`, `valid_to`, `is_current` columns. Your queries filter by `is_current = true` for "right now" questions, or join on the timestamp for "at the time of this flight, who owned this aircraft" questions.

## Lakehouse / Bronze-Silver-Gold — the pipeline shape

This is how modern data platforms organize the flow from raw to refined. Databricks popularized the terminology; the pattern is older.

**Bronze** — raw ingested data, immutable, append-only. Exactly what the source gave you, with ingestion timestamp. Your S3 Glacier ADS-B archive is textbook Bronze. FAA registry snapshots go here untouched. Never delete, never update.

**Silver** — cleaned, deduplicated, conformed to common schemas. Tail numbers normalized. Dates parsed. Obvious garbage filtered. Joined to reference data where useful. This is where ER happens — Silver is where "N123AB" and "N-123-AB" become one entity.

**Gold** — business-ready aggregates and canonical entities. Your golden records live here. Your route-level intelligence tables live here. Your aircraft profile page reads from Gold. Gold is optimized for the specific queries your product and analytics actually run.

The rule that matters: Bronze is sacred. If Silver or Gold is wrong, you can always rebuild from Bronze. If Bronze is corrupted, you're rescraping from source. This is why you never transform in place — the transformation is code, the data is history.

## How this maps onto Dumont / OSA

You're already doing pieces of this. Let me sketch what a mature version looks like:

**Bronze layer:** raw ADS-B positions, FAA registry snapshots (monthly), UCC filing scrapes, AvBuyer/Controller listings, LinkedIn enrichment pulls. Each source lands in its own table/bucket with ingestion metadata. Append-only.

**Silver layer (this is where ER lives):**
- `aircraft_resolved` — one row per real-world aircraft, with the golden record. Sourced by matching FAA tail/serial against ICAO hex against ADS-B observations.
- `operator_resolved` — one row per operating entity. Matches the FAA registered owner against UCC debtor names against state corp records. This is brutal — "Acme Aviation LLC" and "ACME AVIATION, L.L.C." and "Acme Aviation Holdings" need ER.
- `person_resolved` — beneficial owners, founders, executives, linked via LinkedIn and state filings.
- All Type 2. Everything has valid_from / valid_to.

**Gold layer:**
- `aircraft_profile` — the denormalized read model for your public pages. Built from Silver, refreshed on schedule.
- `route_intelligence` — your KMDW→KTEB-style aggregates. Facts (flights) rolled up by origin-destination pair, with operator mix, price estimates, frequency.
- `ghost_inventory` — the push-notification product. Facts with short TTL.

**Identity graph overlay:** the relationships between entities in Silver form a graph. Aircraft–operator edges (with Type 2 history). Operator–beneficial-owner edges. Person–company edges. Store in Postgres with proper foreign keys and a couple of recursive CTEs and you have a working identity graph without a graph database.

## What to read and watch

The sources you listed are the right ones — Kimball's book is non-negotiable if you want the dimensional modeling vocabulary burned into your bones, and the Databricks writing on lakehouse and medallion architecture is the clearest modern treatment.

A few I'd add:

- **Splink documentation** (moj-analytical-services/splink on GitHub). The clearest practical intro to probabilistic ER I've seen. You can run their tutorials against your own data in an afternoon.
- **Peter Christen, *Data Matching*** (Springer, 2012). The textbook on ER. Dense but complete.
- **Max Beauchemin's blog, particularly "The Rise of the Data Engineer" and "Functional Data Engineering."** Max was at Airbnb, wrote Airflow and Superset, and his writing is where the modern pipeline-as-code philosophy got articulated.
- **dbt's documentation on incremental models and snapshots.** dbt's `snapshot` feature is literally Type 2 SCD implemented for you. Whether or not you use dbt, reading how they model it will clarify your thinking.

## One thing I'd push back on

Don't let the enterprise vocabulary seduce you into building enterprise infrastructure. MDM programs, formal data governance committees, master data stewards — these exist because companies with 10,000 employees and 40-year-old systems have political coordination problems. You don't.

What you need is tight, well-modeled ER pipelines with Type 2 history, a clean Bronze/Silver/Gold separation in Postgres (or Postgres + S3 for Bronze), and an identity graph you query through SQL. That's it. The aircraft profile page, the route intelligence, the ghost inventory alerts — they all fall out of that stack.

The vocabulary is worth having because it lets you read the right papers and hire well later. The infrastructure should stay exactly as big as your product requires and not one step bigger.

Want me to sketch the actual schema for `aircraft_resolved` and its Type 2 history tables? That'd be a concrete next step — you could compare it against what you have in Supabase right now and see where the model needs to tighten up.

---

## Phelipe

From the Datafold 2026 predictions:
"Per Indeed Hiring Lab's 2026 report, data and analytics postings declined 15.2% year-over-year through October 2025, and overall tech postings dropped 8.5%. Taking this at face value, it suggests that data jobs are taking twice the hit from AI than an average tech job."
And from Jensen Huang at CES 2026:
"The bottleneck is shifting from compute to context management."
2. Context engineering — this is the actual meta-skill
Gartner called this "the breakout AI capability of 2026." Every major source confirms it. It's not just prompt engineering — it's the discipline of designing the full information environment for AI agents.

```
Context engineering layers (Phil Schmid, Google DeepMind):
1. System instructions
2. Memory (short-term + long-term)
3. Retrieved data (RAG results)
4. Tool definitions  
5. Conversation state / tool outputs

Operations:
- Context Offloading — move info out of prompt, into external systems
- Context Reduction — compress/summarize to prevent "context rot"
```

OSA-Brain is already context engineering. The 140 conversation summaries you've built, the lesson files, the semantic understanding of the business — that's exactly what the industry is calling "context engineering."
What Meta did (from Facebook Engineering blog, April 6, 2026):
"A swarm of 50+ specialized AI agents that systematically read every file and produced 59 concise context files encoding tribal knowledge... AI agents now have structured navigation guides for 100% of our code modules... preliminary tests show 40% fewer AI agent tool calls per task."
Your CLAUDE.md, lessons.md, and the WORKFLOW.md system you built ARE this pattern. You stumbled into industry best practice.

lets explore this. i need to learn more about and from the latest updates

---

## Claude

Good instinct to pull on this thread — you're sitting on something the industry just named, and the naming matters because it tells you what to optimize for next. Let me ground this in what's actually being published right now, then connect it to what you've already built.
```
This block is not supported on your current device yet.
```

Let me also pull the Meta engineering piece specifically, because that's the pattern most directly applicable to what you've built with OSA-Brain:
```
This block is not supported on your current device yet.
```

Good — this gives me a clean picture of the field as it actually stands this month. Let me synthesize.

## The core claim, stated precisely

You're not wrong that OSA-Brain is context engineering. But the precise framing is sharper than "the thing I stumbled into is the thing the industry is building." The honest version:

**You've built the raw materials. The industry has named the operating system that runs on top.**

Your 140 conversation summaries, lesson files, workflow docs — those are the *artifacts* context engineering produces. The discipline the field is codifying right now is about how to **curate, compress, retrieve, and refresh** those artifacts programmatically as first-class infrastructure. That gap is the interesting part. Let me unpack what's actually being published.

## What "context engineering" means in 2026

Anthropic's definition, which the rest of the field has largely adopted: context engineering is the set of strategies for curating and maintaining the optimal set of tokens during LLM inference — including all the information that lands there outside of the prompts. Prompt engineering was about *what you write*. Context engineering is about *the full information environment* the model sees when it acts.

Phil Schmid's five-layer model (system instructions, memory, retrieved data, tool definitions, conversation state) is the cleanest scaffolding, but every major lab converged on roughly the same four operations. LangChain frames them as write, select, compress, isolate. Anthropic frames them as curation, retrieval, compression, offloading. Towards Data Science calls them offloading, retrieval, isolation, reduction. Same four moves, different vocabularies.

The shift that makes this a real discipline and not rebranded prompt engineering: context is now treated as a compiled view over a richer stateful system, not a mutable string buffer. Sessions, memory, and files are the sources; flows and processors are the compiler pipeline; the working context is the view you ship to the LLM for a single invocation. That reframe is the whole thing — it's the move from "stuff everything into the prompt" to "context is a pipeline with an architecture."

## The Meta paper, read carefully

The Meta pre-compute engine is worth studying in detail because it's the cleanest large-scale implementation of the pattern you've been building in miniature. A few specifics worth pulling out:

Meta used a large-context-window model and task orchestration to structure the work in phases, with three final critics running integration tests — 50+ specialized tasks orchestrated in a single session. The five questions each analyst answered per module were the core framework. The five questions matter. They're what separates useful context files from documentation theater:

1. What does this module do / configure?
2. What are common patterns?
3. What are non-obvious gotchas (hidden field renames, silent failure modes)?
4. What are its dependencies?
5. What undocumented conventions does it follow?

Question 5 is where the real value lives. Meta found 50+ non-obvious patterns like hidden intermediate naming conventions where one pipeline stage outputs a temporary field name that a downstream stage renames — reference the wrong one and code generation silently fails. None of this had been written down before.

The "compass, not encyclopedia" principle is the part most people miss. Each context file is roughly 25-35 lines, about 1,000 tokens, with quick commands, key files, non-obvious patterns, and cross-references — zero fluff. All 59 files together consume less than 0.1% of a modern model's context window.

That last number is the one worth tattooing somewhere. The entire tribal knowledge of a 4,100-file, three-repo, multi-language system compressed into less than 0.1% of available context. The discipline is aggressive compression with high-signal preservation, not comprehensive documentation.

And the crucial, underappreciated part: the system self-refreshes every few weeks, validating file paths, identifying coverage gaps, re-running critic agents, and auto-fixing issues. Context that decays is worse than no context at all.

## Where OSA-Brain actually stands relative to this

Let me be direct with you because your framing risks overstating the match.

**What you have that maps cleanly:**
- CLAUDE.md and per-project instruction files → equivalent to Meta's module-level context files
- OSA-Brain's 140 conversation summaries → raw source material, more like Bronze than Silver
- Lessons.md, frameworks, unsell angles → closest thing to the "non-obvious patterns" layer
- Slash command system → equivalent to Meta's orchestration layer, in primitive form
- The Karpathy llm-wiki raw/ immutable directory → Bronze layer in data-lake terms

**What you don't have yet that the discipline calls for:**
- **The compass-not-encyclopedia discipline.** Your summaries aren't ruthlessly compressed. They're narrative, which is useful for you as a founder but inefficient as agent context. The Meta equivalent would be a 30-line file per OSA engine — OSA Connect, OSA Pay, OSA Aircraft, Dumont, Loud Hawk — each answering the five questions.
- **Automated refresh.** Meta's system re-runs critics every few weeks. Yours is manual. Context decay is real — a summary from 4 months ago referencing a platform decision that's since reversed is actively harmful.
- **Critic agents.** Meta ran three rounds of independent critic passes, which moved quality scores from 3.65 to 4.20/5.0. Your multi-AI audit loop for programmatic SEO (Claude + Gemini + ChatGPT) is the same pattern but you haven't applied it to OSA-Brain itself.
- **Measurement.** Meta measured tool-call reduction (~40%) and task time compression (two days → 30 minutes). You have no baseline, so you can't tell whether a given change to OSA-Brain is helping or hurting.

## The four operations, applied to your setup

**Write (offloading).** You're doing this. Voice memos → summaries → Obsidian vault. The question is what you're writing. Right now you're writing long-form narrative. The discipline says: also write short-form, agent-readable compasses. One per engine, one per agent, one per major decision. 25-35 lines each. This is the single highest-leverage change you can make this weekend.

**Select (retrieval).** You're doing this poorly, and it's not your fault — the tooling is still primitive. You have 140 summaries and no structured way to say "for this task, load exactly these three." Meta built a routing layer. Yours right now is "Claude searches semantically and hopes." A middle-ground move: add a top-level `INDEX.md` that says "for OSA Connect questions, load X, Y, Z. For Dumont data pipeline questions, load A, B, C." The routing doesn't have to be AI — it can be a dumb lookup table that you maintain.

**Compress (reduction).** Good context engineering usually comes down to finding the smallest possible set of high signal tokens that give the LLM the highest probability of producing a good outcome. You haven't done any compression. The 140 summaries are probably 3-5x longer than they need to be for agent consumption. The founder-facing version can stay long; the agent-facing version should be brutal.

**Isolate.** The mistake is to assume more agents means more shared context. Dumping a giant shared transcript into every sub-agent often creates the opposite of specialisation — every agent reading everything, inheriting everyone else's mistakes, and paying the same context bill over and over. Your HAWK design (Scout, Writer, Designer, Conductor, Analyst with a shared Memory Layer) needs this lens applied hard. The shared Memory Layer should probably be much smaller than your instinct is telling you. Each agent should get a narrow slice, not the full vault.

## The warning nobody's saying loud enough

One finding from the Meta paper that's easy to miss: recent academic research found that AI-generated context files actually decreased agent success rates on well-known open-source Python repositories. In that scenario, context files are redundant noise. Our codebase is the opposite: proprietary config-as-code with tribal knowledge that exists nowhere in any model's training data.

This is the test. Context engineering pays off when your domain contains knowledge the model doesn't have. For OSA, this is true for:
- OSA's business model specifics (zero commission, OSA Pay thesis, the five engines)
- Aviation-specific tribal knowledge (FAR Part 135 vs Part 91, ADS-B data quirks, operator behavioral patterns)
- Your personal decision history and reasoning patterns
- Dumont's specific schema and data model

It is **not** true — and context files actively hurt — for:
- General programming questions
- General aviation facts the model already knows
- Generic marketing or positioning frameworks

So a principle to steal from Meta: only write context files for things the model couldn't figure out on its own from a quick read of your repo. If it could, you're adding noise.

## The meta-point about the job market data

The Datafold prediction you quoted — data/analytics postings down 15.2% YoY vs 8.5% for tech broadly — is the backdrop that makes this discipline matter. The jobs getting eaten fastest are the ones that translated business questions into SQL and back. The jobs getting created are the ones that architect the context systems that let agents do that translation reliably.

You don't need to be a data engineer. You need to be the person who architected the information environment that lets agents do data engineering against your domain. That's the shift. OSA-Brain is the start of that for you, and the path from where you are to where Meta is isn't complicated in concept — it's just discipline applied to compression, critics, and refresh cycles.

## What I'd actually do next

If I were you, and you wanted to act on this:

First, pick one agent that matters and run the Meta five-question framework on its context. Dumont Intelligence is the obvious candidate because you already use it agentically and the tribal knowledge is dense. Produce one 30-line compass file answering the five questions for Dumont specifically. Measure: does a fresh Claude session with that compass complete a typical Dumont task in fewer turns than without it? If yes, replicate. If no, tighten.

Second, kill or consolidate half of your 140 summaries. The founder-value ones stay in a human-readable archive. The agent-value ones get rewritten as compasses. You will resist this because the summaries feel valuable. They are — for you. They are not, in current form, efficient context for an agent.

Third, set a monthly critic pass. One day, once a month. You + Claude + one other model read every compass file, flag stale references, verify paths and decisions are current, produce a diff. Put it on the calendar. Meta built a cron job for this; you can do it manually for a year before it's worth automating.

Want me to take a crack at drafting the five-question compass for Dumont Intelligence as a concrete example of what the compressed form should look like? That would be the fastest way to see whether this framing actually works on your data, and it'd give you a template to apply to the other engines.

---

## Phelipe

research first all you can find about context enginnering. this is still a little confusing form e. what i understand this is a set of the md files to create context for the agent so he can operate better?

---

## Claude

Good — this is worth getting right, because the mental model matters more than the specific tactics. Let me pull the primary sources comprehensively before I explain it cleanly.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I have enough to give you the clean, grounded explanation. Let me reset the whole frame because your current mental model ("a set of md files to help the agent operate better") is capturing a symptom, not the system.

## Start here: what context actually is

The word "context" has a specific technical meaning that matters. When you talk to Claude, the model doesn't "know" anything mid-conversation — it doesn't remember your last message, it doesn't remember who you are, it doesn't remember what project you're working on. On every single call, the entire situation gets packaged up and sent to the model as one big block of text. That block is the context.

Context refers to the set of tokens included when sampling from a large-language model. The engineering problem at hand is optimizing the utility of those tokens against the inherent constraints of LLMs in order to consistently achieve a desired outcome.

The context window is finite. For Claude right now it's around 200K tokens — call it 500 pages of text. Everything has to fit in that window: the system prompt, your message, the conversation history, any files the agent has read, tool definitions, tool outputs, memory, retrieved documents. Everything.

And here's the part that's not intuitive until you internalize it: **more context is not better. More context is usually worse.**

Research from Chroma called this "context rot." Transformer attention is quadratic. A context of 100,000 tokens requires exponentially more processing than 10,000. And according to Anthropic's research, models suffer from "context rot" — as token volume increases, accuracy in recalling any specific piece of information decreases. Microsoft and Salesforce published a paper called "LLMs Get Lost in Multi-Turn Conversation" showing accuracy can drop ~40% after just one turn of bloat.

So the actual problem is: the model has a limited attention budget, and every token you put in the context competes with every other token for that attention. Your job is to decide what the model sees.

## That's what context engineering is

Context engineering refers to the set of strategies for curating and maintaining the optimal set of tokens (information) during LLM inference, including all the other information that may land there outside of the prompts.

The sharp version of the definition that the whole field has converged on: good context engineering means finding the smallest possible set of high-signal tokens that maximize the likelihood of some desired outcome.

Read that twice. It's the whole discipline in one sentence. **Smallest possible set. Highest signal. Right now, for this specific task.**

Andrej Karpathy's phrasing, which gets quoted everywhere: "Context engineering is the delicate art and science of filling the context window with just the right information for the next step."

Bharani Subramaniam at Thoughtworks: "Context engineering is curating what the model sees so that you get a better result."

All the same idea. The agent is not a person you're briefing. It's a machine with a working memory limit, and you're deciding what goes in that working memory every turn.

## So where do the markdown files come in?

This is where your current mental model is partially right but mostly inside-out.

Markdown files are **one mechanism** for putting information into the context. They're popular because they're human-readable, version-controllable, and tool-agnostic. CLAUDE.md, AGENTS.md, SKILL.md, Cursor rules, Windsurf rules — all variations on the same idea: static text files that get loaded into the context at certain moments.

But the markdown files are not context engineering. They're one of many levers. The full picture has five layers of stuff that can go into context:

1. **System instructions** — the standing orders (often CLAUDE.md sits here)
2. **Memory** — short-term (this session) and long-term (across sessions)
3. **Retrieved data** — stuff pulled in from databases, search, vector stores (RAG)
4. **Tool definitions** — descriptions of what tools the agent can call
5. **Conversation state and tool outputs** — the running history of what's happened

Context engineering is the discipline of orchestrating all five. Markdown files are most visible in layer 1, but the real work happens across all layers.

## The four operations that define the discipline

Every serious writeup has converged on roughly the same four moves. LangChain named them cleanest:

**Write** — save information *outside* the context window so the agent can retrieve it later. Scratchpads, notes, external memory, files on disk. The idea is that you don't force everything into the window; you let the agent write things down for later.

**Select** — pull information *into* the context window at the right moment. This is where retrieval, RAG, and "read the relevant file" live. Good selection means the agent gets what it needs for this task, and nothing else.

**Compress** — when context gets full, summarize or trim to preserve what matters and drop what doesn't. Anthropic calls this "compaction." When a conversation nears the context limit, the agent passes its own history to the model with a prompt to summarize and compress the most critical details, like architectural decisions or unresolved bugs. It then starts a new, clean context window with only this summary, freeing up tokens.

**Isolate** — split work across multiple agents or sessions so one subtask's context doesn't contaminate another's. Subagents with their own context windows. Fresh sessions for unrelated tasks. The `/clear` command.

Those four operations are the whole toolkit. Every technique you'll read about is an implementation of one of them.

## Now the markdown files make sense

A CLAUDE.md file is a specific implementation of the *Write* and *Select* operations combined. You write your project's conventions once into a file; the agent loads them when it starts working on that project.

But here's what most people get wrong, and what you need to understand if you're going to do this well:

**CLAUDE.md loads into the context on every single message in that project.** Every token in that file takes up space that could otherwise hold relevant work. Every conversation starts with this context already loaded, which sounds useful but cuts both ways.

This is why the advice from people who actually run this in production is brutal about size:

- Target: under 300 lines. Focus on what Claude would get wrong without the file.
- Start with a single file; split it into subdirectories when it exceeds 150-200 lines.
- Meta's compass files, as you saw in my last message, are 25–35 lines each, ~1,000 tokens.

And the HumanLayer team found something even more important: Claude code injects a system reminder with your CLAUDE.md file: "IMPORTANT: this context may or may not be relevant to your tasks. You should not respond to this context unless it is highly relevant to your task." As a result, Claude will ignore the contents of your CLAUDE.md if it decides that it is not relevant to its current task. The more information you have in the file that's not universally applicable to the tasks you have it working on, the more likely it is that Claude will ignore your instructions.

Stuff your CLAUDE.md with too much, and the agent will quietly ignore *all of it*.

And there's a harder finding: The ETH Zurich study found that LLM-generated context files reduced task success rates by approximately 3% on average, increased inference costs by over 20%, and required 2-4 additional reasoning steps. Human-curated files provided a marginal 4% performance gain, but still incurred the same token overhead.

A bad context file is worse than no context file. It costs you money, slows the agent down, and makes it perform *worse*. This is the opposite of most people's intuition.

## The mental model to replace yours with

Don't think "markdown files to help the agent." Think like this:

**The context window is the agent's working memory for the next single action it takes. You are the architect of that working memory. Your job on every turn is to get the right small amount of information into that window and keep the wrong information out.**

The markdown files are one tool for loading information in. Skills are another (they lazy-load only when relevant). Subagents are another (they work in their own isolated window). RAG is another (it pulls things in on demand). Compaction is another (it trims history when the window fills). Memory systems are another (they persist across sessions).

The skill you're building — context engineering — is knowing which tool to reach for in which situation, and doing that with discipline about how many tokens you're spending for how much benefit.

## What this looks like as a progression

Tier 1 — Prompt engineering: you type a better question, you get a better answer. One-shot. What most people still do.

Tier 2 — Basic context files: you add a CLAUDE.md or AGENTS.md so the agent knows your project basics without re-explaining. Most people who "do context engineering" stop here.

Tier 3 — Layered context: you have a small root context file for universal project stuff, plus sub-directory context files that load only when the agent enters that area, plus skills that load only when relevant, plus specs written before specific tasks. You're actively managing what's in the window at any moment.

Tier 4 — Multi-agent with isolation: you have specialized subagents (security reviewer, data analyst, writer) each with their own context window and their own tools, coordinated by a lead agent. Each agent sees only what's relevant to its slice.

Tier 5 — Self-maintaining context infrastructure: like Meta's pre-compute engine — a system that generates and refreshes its own context files, with critic agents checking quality, automated refresh cycles, measurement of whether changes help or hurt.

Most serious teams in 2026 are living at Tier 3 and reaching for Tier 4. Meta is the public example of Tier 5.

## To directly answer your question

"Is this a set of md files to create context for the agent so it can operate better?"

Not quite. It's the *discipline of deciding what the agent sees on every turn, why, and when to change it*. Markdown files are one common implementation of that discipline, but they're the tool, not the skill.

The skill itself is developing taste for:

- What information this specific task needs
- What information would actively hurt if included
- Where information should live (in the prompt? a file loaded always? a file loaded on demand? a retrievable memory? a separate subagent's context?)
- When to compress, when to throw away, when to start fresh
- How to measure whether a change helped or hurt

The reason the field matters right now is that models have gotten good enough that the bottleneck moved. A year ago, the bottleneck was the model's reasoning. Now the model can reason fine — the bottleneck is whether you fed it the right information in the right shape at the right time. That's why Jensen said the bottleneck shifted from compute to context management, and why teams shipping real agents in 2026 spend most of their engineering time here.

## How to actually learn it

If you want to go deep and build real intuition, I'd read in this order. All short, all authoritative:

1. Anthropic's "Effective context engineering for AI agents" (on anthropic.com/engineering). This is the canonical reference and the shortest path to the full mental model.
2. LangChain's "Context Engineering for Agents." Clean write/select/compress/isolate taxonomy.
3. The Manus "Lessons from Building Manus" post. This is the most honest in-the-trenches account — they rebuilt their framework four times.
4. Meta's "How Meta Used AI to Map Tribal Knowledge" engineering post. The production-scale example.
5. The HumanLayer "Writing a good CLAUDE.md" post. The single best practical guide to the most common artifact you'll produce.

That's maybe two hours of reading total, and it'll give you the working vocabulary the whole industry is using.

Want me to take one concrete piece of your current setup — say your CLAUDE.md for one OSA project, or the OSA-Brain vault structure — and walk through what context engineering discipline would actually change about it? That's usually when this clicks from "interesting concept" to "oh, I see exactly what I've been doing wrong."

---

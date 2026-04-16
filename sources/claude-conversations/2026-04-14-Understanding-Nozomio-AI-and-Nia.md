---
title: Understanding Nozomio AI and Nia
created: 2026-04-14T14:17:17.799641Z
updated: 2026-04-14T16:28:02.505323Z
uuid: c0d91ff6-e545-4cd7-9f09-5c1a7f7c68eb
source: claude-conversation
type: source
message_count: 22
---

# Understanding Nozomio AI and Nia

*Summary: **Conversation Overview**

The person is building OSA (a private aviation platform) and working on an AI agent system called Dumont, which handles charter sourcing and operator intelligence. The conversation began with the person asking about Nozomio AI and its flagship product Nia — a live-indexed retrieval layer for coding agents that provides continuously updated context from codebases, documentation, and external sources. Claude explained the distinction between static memory files (like CLAUDE.md, memory.md, intelligence.md) and Nia's live crawling approach, which keeps agent knowledge current without manual maintenance.

The person pushed back several times on not fully grasping the concept, prompting progressively simpler explanations. The analogy that landed was: "Claude Code knows what you told it. Nia knows what's true right now." The person then asked whether OSA could build Nia internally, which Claude reframed — OSA already has the components of a Nia-equivalent (Ghost Positioning Spread, Charter Index, Aviapages integration), and what's missing is a Supabase + pgvector retrieval layer with a freshness crawler. The person clarified they meant building Nia as a standalone product, which Claude advised against given Nozomio's head start and OSA's focus, instead reframing the real opportunity as building the aviation-specific intelligence layer — indexing a private market nobody has indexed before, which is a data moat Nia could never replicate.

The conversation also covered a GitHub repo (andrej-karpathy-skills) — a pre-built CLAUDE.md template based on Karpathy's LLM coding principles — with Claude providing a one-line curl install command and recommending it for OSA's Next.js and SEO repos. Finally, the person asked about Multica, an open-source project management platform where AI agents function as assignable teammates with compounding skills, which Claude connected directly to OSA's HAWK multi-agent architecture (Scout, Writer, Designer, Conductor, Analyst). The person communicates in short, direct questions and responds to pushback with continued questioning until the concept clicks — preferring honest assessments over hype, and concrete OSA-specific relevance over abstract explanations.*

## Phelipe

What is the nozomio ai? Explain to me

---

## Claude

Let me search for "nozomio ai" to find out what it is.
```
This block is not supported on your current device yet.
```

Good info. Let me summarize Nozomio clearly.**Nozomio** (also called Nozomio Labs) is a YC-backed applied AI research lab. Here's the breakdown:

**What it is:** An applied product and research lab building the future of context for AI. Their flagship product is called **Nia**.

**What Nia does:** Nia is a search and index API that continuously provides context from docs, research papers, datasets, codebases, and more — so AI agents never rely on stale data.

**The core problem it solves:** Language models can write code better than most humans, but they often destroy codebases due to poor context management and understanding. Nia fixes this by giving coding agents (like Cursor or Claude Code) accurate, up-to-date context — reducing hallucinations.

**How it works technically:** Nia acts as a context augmentation layer for AI agents, indexing entire codebases, documentation, and web pages. This enhances the agents' understanding and reduces the number of tokens required by up to three times, making the process more efficient and cost-effective.

**The founder:** Arlan Rakhmetzhanov, an 18-year-old who joined Y Combinator's Summer 2025 batch, raised an $850K pre-seed from London's LocalGlobe while still a teenager. He later announced a $6.2M round.

**TL;DR for OSA relevance:** It's an MCP-compatible context layer for coding agents. If you're running Dumont or any agentic workflows via Claude Code, Nia is the type of tool that keeps your agents from hallucinating outdated API docs or stale codebase state. Worth watching.

---

## Phelipe

Wait why is so good? Claude code can't do that?

---

## Claude

Phelipe is asking why Nia is valuable if Claude Code already exists. Let me explain the distinction clearly.Good question. Claude Code can write and edit code extremely well — but it has a fundamental limitation: **its context window is finite and static**.

Here's the gap Nia fills:

**The problem with coding agents alone:**
- When you point Claude Code at a large codebase, it can only "see" what fits in the context window at once
- It has no live access to external docs (e.g., latest Stripe API, updated Next.js docs, your custom internal docs)
- If a library updated last month, Claude Code doesn't know — it hallucinates the old behavior

**What Nia adds:**
- It continuously indexes your repos, docs sites, and research papers in the background
- When your coding agent needs context, Nia retrieves only the *most relevant* chunks — instead of dumping everything into the context window
- Result: less token waste, more accurate answers, fewer hallucinations on external APIs

**The analogy:** Claude Code is the pilot. Nia is the dispatcher feeding it the right charts, NOTAMs, and weather at the right moment — instead of the pilot having to memorize every possible route in existence.

**Why Claude Code alone can't do this:** It's not a knowledge retrieval system. It's a reasoning + coding system. These are different layers. Nia sits *underneath* the agent as a live, always-updated knowledge layer.

That said — for most solo builds, Claude Code + well-maintained `CLAUDE.md` files gets you 80% there. Nia matters most when you're dealing with fast-moving external APIs or massive codebases with multiple repos. For OSA's current scale, probably not urgent.

---

## Phelipe

What. Agents have memory.md and intelligence.md. I am not getting how important and dirruptive it is

---

## Claude

Phelipe is pushing back — he's saying agents already have memory files (like CLAUDE.md, memory.md, intelligence.md). He wants to understand what's truly disruptive about Nia beyond what those files already provide.

Let me think about this clearly.

The key distinction is:

1. **Static files** (CLAUDE.md, memory.md) = you manually write and update them. They're snapshots. They don't update themselves. If Next.js releases a new version, your CLAUDE.md doesn't know.

2. **Nia** = a continuously running crawler/indexer that watches docs, repos, papers, and feeds the agent *live, semantically-retrieved* context on demand.


The real disruption is that Nia provides living, auto-updating knowledge at retrieval time rather than static snapshots — it scales where CLAUDE.md breaks down at enterprise scale with multiple repos and thousands of files. It's like the difference between a pilot flying with a six-month-old chart versus one receiving live ATC data. For Dumont agents specifically, instead of manually maintaining operator intelligence files, Nia would automatically surface the latest aircraft availability, current FBO pricing, and real-time weather without anyone touching a markdown file.Fair pushback. Here's the real distinction:

**Your memory.md / CLAUDE.md = a snapshot you wrote manually.**

- You update it when you remember to
- It only knows what *you* put in it
- It doesn't scale — imagine 10 repos, 50 external APIs, docs sites that update weekly

**Nia = a live crawler running 24/7 in the background.**

- It indexes external sources automatically — framework docs, research papers, third-party APIs, your entire codebase
- When the agent needs context, it *retrieves semantically* — not just keyword match, but "what's actually relevant to this task right now"
- Nobody writes anything. It just stays current.

**The real disruption:** It decouples *knowledge* from *context window size.* Right now, the more you want your agent to know, the more tokens you burn. Nia's retrieval layer means the agent only pulls what it needs, when it needs it — at a fraction of the token cost.

**OSA parallel to make it click:** Your Dumont agents have CLAUDE.md with operator intelligence. But that file is written by you. Imagine if Dumont automatically indexed every operator's fleet page, every FBO pricing update, every aircraft availability signal — without you touching a markdown file. That's what Nia is doing for codebases.

The disruption isn't "agents with better notes." It's **agents that never have stale knowledge at any scale, with no human maintenance cost.** That's a different category entirely.

---

## Phelipe

Not getting it

---

## Claude

He's not getting it. Let me think about the simplest possible way to explain this.

The core insight: right now, AI agents are smart but blind to anything they weren't trained on or told explicitly. Nia is like giving them a live library they can query at any moment.

Let me try a really simple, concrete explanation.Okay. Forget tech. One sentence:

**Claude Code knows what you told it. Nia knows what's true right now.**

---

Concrete example:

Next.js releases a new version. Something changes in how App Router works.

- Claude Code still codes the **old way** — because that's what it learned
- Your CLAUDE.md still says the **old way** — because you didn't update it
- Nia already **crawled the new docs** and gives the agent the correct, current behavior automatically

You shipped a bug because your agent was working off outdated truth. That's the problem.

---

**The disruption:** Every coding agent today — Cursor, Claude Code, Copilot — is flying with a map printed 6 months ago. Nia gives them a live GPS.

At scale, with dozens of external dependencies all moving simultaneously, this isn't a nice-to-have. Your agent is only as good as the knowledge it has access to. Stale knowledge = wrong code = bugs in production.

That's why it's disruptive. Not a feature. A new layer of the stack that didn't exist before.

---

## Phelipe

You think this is actually relevant? Is that big?

---

## Claude

Phelipe is asking for my honest take on whether Nia/Nozomio is actually a big deal or not. Let me give him a direct, honest assessment.Honest take? **Relevant, yes. Category-defining, unclear.**

The problem is real. Stale context kills agents at scale. But:

**Reasons it might be big:**
- Every company building with AI agents has this problem
- It's infrastructure — infrastructure companies get massive if they become the default
- YC + $6.2M early means smart people believe it
- MCP adoption is exploding, and Nia plugs in cleanly

**Reasons to be skeptical:**
- OpenAI, Anthropic, Google are all building better native retrieval into their models — the problem Nia solves might get absorbed into the base layer
- It's a *workflow* tool, not a *platform* — hard to build a moat when the underlying models keep improving
- The CLAUDE.md + good discipline approach solves 80% of the problem for most teams right now

**Real answer:** It's a smart wedge for today's agent limitations. Whether it's a lasting independent company or gets acqui-hired by Anthropic/Google in 2 years — that's the actual question.

Think of it like early database caching tools. Real problem, real solution — but eventually the databases just got faster and absorbed most of the use case.

**For OSA specifically:** Zero relevance right now. You're not running agents at a scale where this matters. File it under "watch, don't act."

---

## Phelipe

Can look at this?

---

## Claude

The image shows a Reel about "Index-free code search" - "Regex is cooked." This is about semantic/AI-powered code search that doesn't need regex patterns. It's from a Neovim plugin called fff.nvim by dmtrKovalenko.

This is actually related to the Nozomio conversation - it's the same space. AI-powered code search vs traditional regex search.Yeah. This is actually the same conversation we were just having — just a different angle.

**What this is:** A Neovim plugin ("fff") that lets you search your codebase using natural language instead of regex. You describe what you're looking for, it finds it semantically.

**Why it matters in context:** This is the *developer-facing* version of the same idea Nia is solving at the *agent* level.

- Regex = find exact string patterns
- This = find code by *meaning* ("where do we handle auth errors?" instead of `grep -r "auth.*error"`)

**The thread connecting all of this:**

Regex → keyword search → semantic search → Nia's live-indexed retrieval for agents

Each step is the same disruption: stop searching by *syntax*, start searching by *intent*.

**Is this big?** The plugin itself, probably not. But it's a signal that the whole code search layer is getting rebuilt on top of embeddings and semantic retrieval. That's real.

Nozomio is betting that this same shift happens at the *agent infrastructure* level — not just for humans searching code, but for agents that need to *know* codebases autonomously.

Same wave, different surfboard.

---

## Phelipe

Can we build nia for us?

---

## Claude

Phelipe is asking if we can build a Nia-equivalent for OSA. Let me think about what that means in OSA's context.

Nia for OSA would be: a live-indexed retrieval layer that feeds Dumont agents with current, accurate context — operator fleet data, FBO pricing, aircraft availability, route data, etc. — instead of relying on static files.

Let me think about what OSA actually needs and whether this is buildable.Yes. And honestly you're already halfway there without realizing it.

**What Nia for OSA looks like:**

Instead of indexing codebases and docs, you're indexing **aviation intelligence** — and feeding it to Dumont agents in real time.

The sources:
- Operator fleet pages (ADS-B position data)
- FBO pricing and availability
- Aircraft specs and performance data
- Route pricing signals (Aviapages + your own transaction history)
- FAA registry changes
- Weather / NOTAMs for positioning logic

**What you already have:**
- Dumont's Ghost Positioning Spread = ADS-B-based live retrieval
- OSA Charter Index = a pricing knowledge layer
- The Aviapages API integration

That's Nia. You just haven't framed it that way.

**What's missing to complete it:**
- A proper embeddings layer so agents retrieve by *meaning* not just lookup
- A crawler that keeps operator data fresh automatically
- A retrieval API that any Dumont agent can call mid-task

**The real question:** Do you build this now or after first revenue?

My honest take — **after first revenue.** Right now your bottleneck is deals, not agent intelligence. But architecturally, you should design Dumont's sourcing layer *knowing* this is where it goes. Don't hardcode what should be retrieved dynamically.

You're not building Nia. You're building **Nia for private aviation.** That's actually a moat.

---

## Phelipe

Is basically putting in a supabase with vector?

---

## Claude

Yes, essentially. Let me explain simply.Yes. That's 80% of it.

**The core:**
- Supabase with pgvector extension
- Embed your data (operator profiles, aircraft specs, route pricing, FBO info) into vectors
- Agent queries by meaning → retrieves most relevant chunks → passes to Claude as context

**The other 20%:**
- A crawler that re-indexes when data changes (so it stays fresh — that's the actual Nia innovation)
- A ranking layer that picks the *best* chunks, not just similar ones
- Rate limiting + cost control so agents don't over-retrieve

**For Dumont specifically:**

```
Operator asks for NYC → Aspen
↓
Dumont calls retrieval layer
↓
pgvector returns: 3 operators with Aspen experience, 
current positioning of relevant aircraft, 
historical pricing on that route
↓
Claude reasons on fresh, relevant context only
```

Instead of Claude trying to remember everything or you manually maintaining markdown files.

**Build order when you're ready:**
1. Supabase + pgvector — 1 day
2. Embed your existing route + operator data — 1 day
3. Hook it into Dumont's sourcing agent — 1-2 days
4. Add the crawler for freshness — that's the hard part

Total: a weekend sprint post-revenue. You already have the data. You just need the retrieval layer on top of it.

---

## Phelipe

I am saying nia

---

## Claude

Phelipe is asking if they can build Nia itself — as a product, not just for internal OSA use. Let me think about this carefully.Got it. You're saying — build Nia. As a product. Not just for OSA internally.

**Honest take:**

You could. The technical barrier is low. Supabase + pgvector + a crawler + an MCP server = Nia functionally.

But.

**Why you shouldn't:**

- Nozomio already has it, has YC, has $6.2M, has distribution
- It's a developer tool — completely different GTM than OSA
- You'd be splitting focus at the worst possible time
- Your moat in aviation is *domain knowledge* — not retrieval infrastructure

**The real insight you're having:**

You don't want to *build* Nia. You want to build the **aviation equivalent of Nia** — a live intelligence layer for private aviation that no coding tool could ever replicate. Operator positioning, route pricing, fleet availability, FBO intel — all fresh, all semantic, all feeding Dumont.

That's not a feature. That's actually a **data business.**

And nobody has it. Because nobody has the transaction history to train it. You will.

That's worth more than Nia. Nia indexes public docs. You'd be indexing a private market that's never been indexed before.

**That's the actual bet.** Not building Nia. Building what Nia would be if it understood private aviation.

---

## Phelipe

https://github.com/forrestchang/andrej-karpathy-skills
how to use this?

---

## Claude

```
This block is not supported on your current device yet.
```

This is a CLAUDE.md template based on Karpathy's observations about LLM coding pitfalls. Simple to explain and use.This is a pre-built `CLAUDE.md` file based on Karpathy's observations about how LLMs screw up when coding. Four principles baked in.

**To use it — one command in your project root:**

```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpthy-skills/main/CLAUDE.md
```

If you already have a CLAUDE.md (like OSA does), append instead:

```bash
echo "" >> CLAUDE.md
curl https://raw.githubusercontent.com/forrestchang/andrej-karpthy-skills/main/CLAUDE.md >> CLAUDE.md
```

**What it does for you:**

The four rules it enforces on Claude Code:

1. **Think before coding** — stops Claude from silently picking wrong assumptions and running with them
2. **Simplicity first** — stops 1000-line solutions when 100 would do
3. **Surgical changes** — stops Claude from "improving" code it shouldn't touch
4. **Goal-driven execution** — give it success criteria, let it loop until verified

**For OSA:** Drop this into your Next.js repo and your programmatic SEO project. It directly fixes the thing where Claude Code goes and refactors stuff you didn't ask it to touch. You've probably hit that already.

Takes 30 seconds to install. Worth it.

---

## Phelipe

how multica works?

---

## Claude

The user is asking about "multica." Let me search for this.
```
This block is not supported on your current device yet.
```

Got it. Multica is an open-source project management platform for human + agent teams.**Multica = project management where agents are actual teammates, not just tools.**

The core idea: for decades, software teams have been single-threaded — one engineer, one task. AI agents change that. Multica brings time-sharing back, but the "users" multiplexing the system are both humans and autonomous agents.

**How it works practically:**

Assign issues to an agent like you'd assign to a colleague — they pick up the work, write code, report blockers, and update statuses autonomously. No more copy-pasting prompts. No more babysitting runs. Agents show up on the board, participate in conversations, and compound reusable skills over time.

**The problem it solves:** When you throw a complex development task at a group of agents, they frequently fall into self-indulgent chaos. You don't know who's working on what, or whether any of them are stuck. Even worse, today Agent A figures out the AWS deployment, but tomorrow Agent B takes over and steps on exactly the same pitfalls — no experience accumulation.

**Key differentiator — Skills that compound:** Agents don't just execute tasks, they build reusable skills over time. Every task makes the next one faster.

**To install:**
```bash
curl -fsSL https://raw.githubusercontent.com/multica-ai/multica/main/scripts/install.sh | bash
multica setup
```

**OSA relevance:** This is literally what HAWK is. Scout, Writer, Designer, Conductor, Analyst — each as an assignable agent with a profile, task history, and compounding skills. Multica is the open-source infrastructure layer for exactly that architecture. Worth watching closely.

---

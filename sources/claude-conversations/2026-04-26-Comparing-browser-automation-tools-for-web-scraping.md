---
title: Comparing browser automation tools for web scraping
created: 2026-04-26T11:47:53.605053Z
updated: 2026-04-26T17:04:24.673924Z
uuid: 98359fba-099a-4734-9d55-b5a4142b037a
source: claude-conversation
type: source
message_count: 65
---

# Comparing browser automation tools for web scraping

## Phelipe

Is this better then playwrights?

---

## Claude

Quick honest take: I can't tell from the screenshot alone. The repo's tagline ("headless browser for AI agents and web scraping") suggests it's positioned as a Playwright/Puppeteer alternative, but 5.4k stars and a v0.1.1 release from 23 hours ago means it's very early. Let me actually look it up.
```
This block is not supported on your current device yet.
```

Honest answer: **no, not better — different.** Obscura isn't really a Playwright competitor. It's a Rust-based headless browser engine that Playwright can drive via CDP. So you'd usually use them *together*, not pick one.

Here's the actual shape of it:

**What Obscura is:** a 70 MB single-binary headless browser (V8 + CDP) written by a 16-year-old. Replaces *headless Chrome*, not Playwright. Playwright/Puppeteer connects to it the same way they'd connect to Chrome.

**Where it wins:** memory footprint (30 MB vs Chrome's 200+ MB), startup time, and built-in stealth/anti-fingerprinting without paying Browserbase. Good for cheap scraping at scale on small VPSes.

**Where Playwright still wins:** mature ecosystem, multi-browser (Firefox/WebKit, not just Chromium), better waiting semantics, huge community, battle-tested for testing. Obscura is v0.1.1 from yesterday — single maintainer, no track record.

**Caveats worth knowing:**
- The 5.4k stars in 23 hours is suspicious. Real OSS adoption doesn't move that fast. Could be HN frontpage, could be inflated.
- Vendor-published benchmarks. Validate on your own targets.
- Stealth mode helps with fingerprinting but won't beat IP reputation blocks.

**For OSA Connect specifically** — if you're scraping operator sites or jet listings, this isn't a Playwright replacement decision. The question is whether you want to swap Chrome for Obscura *under* Playwright to cut server costs. At your current scale, not worth the risk on a v0.1.1 project. Revisit when you're running real volume and Chrome memory is actually the bottleneck.

---

## Phelipe

What about this from google

---

## Claude

Let me look at this one — Google publishing "Agent Skills" is interesting context.
```
This block is not supported on your current device yet.
```

Different category entirely — this isn't a tool you'd compare to Playwright. It's the same concept as the Anthropic skills system you're already using (the SKILL.md files in your OSA-Brain stack). Google launched their official Agent Skills repository at Cloud Next 2026 to equip AI agents with condensed, real-time expertise for Google Cloud products like BigQuery, GKE, and the Gemini API, avoiding context bloat.

**What it actually is:** packaged instructions for coding agents (Gemini CLI, Claude Code, Cursor, Antigravity) to use Google Cloud products correctly. They follow the open Agent Skills specification and work across multiple agent hosts including GitHub Copilot, Claude Code, Cursor, Codex, and Gemini CLI.

**Why this matters for you:** the Agent Skills format is becoming a real standard. There are now 1000+ agent skills from official dev teams — Anthropic, Google Labs, Vercel, Stripe, Cloudflare, Netlify, Trail of Bits, Sentry, Figma — all using the same SKILL.md spec. Your OSA-Brain Obsidian vault and Claude slash commands are already in this paradigm; the ecosystem is converging on it.

**Concrete relevance to OSA:**
1. If you ever touch Google Cloud (BigQuery for Charter Index data, Vertex AI for Dumont fallback), `google/skills` makes Claude Code dramatically more accurate at writing that code without you babysitting it.
2. The portable spec means skills you build for your own Claude Code workflows (HAWK agents, OSA Connect codebase conventions, route page generation) can be packaged the same way and ride on whatever agent host you use later.
3. GitHub now ships gh skill install/update with content-addressed change detection and version pinning — so internal OSA skills could live in a private repo with proper supply-chain controls. That's relevant when you eventually hire the CTO and Brand & Content Strategist and need to transfer tacit knowledge as enforced workflow, not docs.

Not urgent. But worth knowing the format you've been using ad-hoc is now the industry standard, and it's where the tooling is consolidating fast.

---

## Phelipe

Explain CLI. And what would be the advantage on context compared to MCP

---

## Claude

## What CLI means

CLI = Command Line Interface. A program you run by typing commands in a terminal instead of clicking buttons in a GUI.

When you type `git push` or `npm install` or `obscura fetch https://...` — that's a CLI. The program takes text input (commands + arguments + flags), does work, prints text output. No windows, no mouse.

In the agent world, "CLI tools" means tools your AI agent invokes by running shell commands. Claude Code itself is a CLI. `gh` (GitHub) is a CLI. `gcloud` is a CLI. The agent literally types `gh issue list --repo osa/connect` the same way you would.

---

## CLI vs MCP — the context tradeoff

This is the actually interesting question. Both let an agent talk to external systems. The difference is **how much context they burn**.

**MCP (Model Context Protocol):**
- Tools are loaded into the model's context window upfront
- Each tool = a JSON schema describing its name, parameters, types, descriptions
- A typical MCP server exposes 10–50 tools. Big ones (Gmail, Asana, Salesforce) can expose 100+
- All those schemas sit in context whether you use them or not
- Tool calls return structured JSON the model parses

**CLI:**
- The agent runs `gh --help` or reads a SKILL.md once when it needs the tool
- Output is plain text, often human-readable
- Only the specific command + output occupies context
- The "interface" lives on disk (man pages, --help, skills), not in context

### Where CLI wins on context

**1. Lazy loading.** With MCP, if you connect Gmail + Calendar + Drive + Asana + Slack, you might burn 15–30k tokens on tool schemas before the model writes a single word. With CLI, the agent reads `gh --help` only when it needs GitHub. Other tools cost zero until used.

**2. Compression.** CLI output is often denser than MCP JSON. `gh pr list` returns a clean table; the equivalent MCP response is verbose JSON with field names repeated on every row. On a 50-PR list that's a 3–5x difference.

**3. Composability.** Agents can pipe: `gh pr list --json title,author | jq '.[] | select(.author.login=="phelipe")'`. One context-cheap operation does work that would be three MCP calls + parsing.

**4. Skill packaging.** Google's skills repo, Anthropic's skills — they teach an agent *how to use a CLI*, not what the API surface is. The SKILL.md is loaded once, then the agent operates with normal commands. This is why the Agent Skills standard exploded: it's CLI-shaped, not MCP-shaped.

### Where MCP wins

**1. Auth and state.** MCP servers handle OAuth, token refresh, session state. CLI tools either need the user logged in already or ship their own auth.

**2. Structured returns.** When you genuinely need typed data (parse this calendar event, extract these fields), MCP's JSON is easier than regex-ing CLI output.

**3. Discoverability.** MCP tools advertise themselves. The model sees them and knows what's possible. CLI requires the agent to know to look.

**4. Non-developer surfaces.** SaaS tools without CLIs (most of them) only expose MCP or REST. You can't `gh`-equivalent your way through Notion or Linear without their CLI existing.

---

## The practical pattern emerging

The high-leverage setup right now: **MCP for connected services, CLI + Skills for everything else, especially infrastructure and code.**

For OSA specifically: keep MCP for Gmail/Calendar/Drive/Dumont. But your Next.js route page pipeline, GitHub Actions, Railway deploys, Obsidian vault operations, HAWK agent system — those should be CLI + skills, not MCP. Cheaper context, faster iteration, portable across whatever agent host you use next year.

The reason Anthropic shipped skills and Google followed within months: MCP-everything bloats context faster than models can grow. Skills + CLI is how this scales.

---

## Phelipe

Okay so we have 3 thing. Skills, CLI amd MCP this are part of tools of context engineering?

---

## Claude

Yes — exactly right. They're all context engineering primitives, but they solve different parts of the same problem: **how do you get the right information and capabilities into the model's context at the right time, without bloat?**

Here's the cleaner mental model:

## The three primitives

**Skills = knowledge / how-to**
Static instructions the agent reads when relevant. "When you do X, follow this process." Loaded on-demand from disk. No execution, just guidance. Your OSA writing-guide.md, aircraft-scoring.md, CLAUDE.md — those are skills.

**CLI = capability via shell**
Commands the agent executes. The interface is the program itself + its --help. Agent learns it once (often via a skill), then uses it. Output is text. Cheap context, composable, works offline.

**MCP = capability via protocol**
Tools advertised through a standardized API. Schemas sit in context. Auth and state handled by the server. Best for connected SaaS where you need structured data and OAuth.

## How they layer

Think of it as a stack, not three competing options:

```
Skills        ← teach the agent how to think/work (process, conventions)
   ↓
CLI + MCP     ← give the agent capabilities (do things, fetch data)
   ↓
Files/Memory  ← persistent state the agent reads and writes
```

A well-designed agent workflow uses all three:

- **Skill** says "when generating a route page, follow writing-guide.md, score aircraft via aircraft-scoring.md, then commit via gh CLI"
- **CLI** (`gh`, `git`, `npm`) does the actual work
- **MCP** (Gmail, Calendar) handles the connected-service slice

## The bigger frame: context engineering

Context engineering is the discipline of deciding **what goes into the model's context window, when, and in what form**. It's the successor to "prompt engineering" — prompts are one input, but context is the whole picture: system prompt + skills loaded + tool schemas + conversation history + retrieved files + tool outputs.

The four levers you actually pull:

1. **Selection** — what to include (which skills, which tools, which past chats)
2. **Compression** — how to represent it densely (CLI text vs MCP JSON, summaries vs full docs)
3. **Timing** — when to load it (upfront vs on-demand, eager vs lazy)
4. **Persistence** — what survives across turns (memory, files, vault entries)

Skills, CLI, and MCP are tools. Context engineering is the practice of using them well.

## Why this matters for OSA

You're already doing context engineering — that's what your OSA-Brain vault, slash command system, and CLAUDE.md files are. The Dumont pipeline, HAWK agent design, the export workflow — all of it is context engineering.

The shift worth internalizing: **your moat isn't the agents, it's the context system feeding them.** Anyone can spin up Claude Code. Few people have a structured second brain + skill library + CLI workflows that make every session start at 80% productivity instead of 0%. That compounds.

---

## Phelipe

What about plugs ins and hooks?

---

## Claude

Good — these round out the picture. Plugins and hooks are the **execution-layer primitives**, while skills/CLI/MCP are the capability layer.

## Hooks

**What they are:** scripts that run automatically at specific points in an agent's lifecycle. Event-driven. The agent doesn't decide to run them — they fire on triggers.

**Claude Code hooks** (the most concrete example):
- `PreToolUse` — runs before any tool call. Can block it.
- `PostToolUse` — runs after a tool succeeds. Can validate or transform output.
- `UserPromptSubmit` — runs when you send a message. Can inject context.
- `Stop` — runs when the agent finishes. Can verify work is complete.
- `SessionStart` — runs when a session opens. Can load state.

**Why they matter for context engineering:**

Hooks let you enforce determinism around the model's non-determinism. The model is probabilistic; hooks are not. So you wrap the model in deterministic guardrails.

Concrete examples:
- `PreToolUse` hook that blocks `rm -rf` or any push to `main` without tests passing
- `PostToolUse` hook that runs `prettier` after every file edit, so the model never has to remember to format
- `UserPromptSubmit` hook that auto-injects current git branch + recent commits, so the model always knows the state of the repo
- `Stop` hook that runs the test suite and refuses to let the agent claim "done" until it's green

Hooks are the **anti-rationalization layer**. The model can talk itself into skipping tests. A hook can't.

## Plugins

**What they are:** packaged bundles that combine the other primitives — skills + commands + hooks + MCP servers + agent personas — distributed as a single installable unit.

Think of a plugin as "a complete capability pack for a specific job." Instead of you wiring up a skill, three CLI tools, an MCP server, and four hooks individually, someone packages it and you `gh skill install` or equivalent.

**A real plugin might contain:**
- `skills/` — how-to docs (process, conventions)
- `commands/` — slash commands you can invoke (`/deploy`, `/review`)
- `hooks/` — event handlers (auto-format, block bad commits)
- `agents/` — specialist personas the main agent can delegate to
- `mcp.json` — MCP server config the plugin needs

Anthropic, Google, Stripe, Vercel — they're all shipping plugins now. The ecosystem is converging on this format because it's the only way to distribute opinionated workflows without forcing users to manually wire everything.

## The full stack

Layered cleanly:

```
Plugins         ← distribution unit (bundles everything below)
   ↓
Hooks           ← deterministic guardrails around model behavior
Skills          ← how-to knowledge, loaded on demand
CLI + MCP       ← capabilities (execute, fetch, transact)
   ↓
Files/Memory    ← persistent state
```

## The mental model that ties it all together

The model is a **reasoning engine** that's smart but unreliable. Context engineering is the discipline of compensating for that unreliability with structure:

- **Skills** make the model competent at specific tasks (knowledge it doesn't have to derive)
- **CLI/MCP** give the model hands (capabilities to act in the world)
- **Hooks** prevent the model from doing dumb things (enforced rules it can't override)
- **Plugins** package the above into reusable units (so you're not rebuilding from scratch every time)
- **Memory/files** give the model continuity across sessions (state that survives)

## Concrete relevance for OSA

Your HAWK system is fundamentally a plugin in waiting. Right now it's described as five agents (Scout, Writer, Designer, Conductor, Analyst). What that actually means in this stack:

- **Skills:** writing-guide.md (Writer), aircraft-scoring.md (Scout), brand visual system (Designer), analytics interpretation (Analyst), workflow orchestration (Conductor)
- **CLI:** voice-memo intake → transcription → vault commit → publish pipeline
- **MCP:** LinkedIn posting, newsletter sender, analytics fetchers when those connect
- **Hooks:** PreToolUse to enforce never publishing without Conductor review; PostToolUse to auto-tag and file by topic
- **Plugin:** the whole thing packaged so when you hire the Brand & Content Strategist, they `install hawk` and inherit a working system instead of reading docs

The framing shift: HAWK isn't "five agents." HAWK is a **context-engineered plugin** that ships the institutional memory of your content operation. That's what makes it transferable. That's what makes it a moat.

---

## Phelipe

Are we missing anything?

---

## Claude

Yeah — there are a few more primitives worth knowing. The full picture isn't just six things; it's closer to ten. Here's what we haven't covered:

## What we're missing

**1. Subagents / agent delegation**
The main agent spawns specialized subagents with their own context windows. Each subagent has a focused job (e.g., "research this topic," "review this code") and returns a summary. Lets the main agent stay clean while delegates do heavy work in parallel. Claude Code calls these subagents; OpenAI calls them "agents" in their SDK; the pattern is the same. This is how HAWK's five-role system actually executes — Conductor is the main agent, the others are subagents.

**2. Slash commands**
User-invoked shortcuts that inject a structured prompt + context. `/review`, `/deploy`, `/route-page`. Different from skills (skills are passive knowledge; slash commands are active triggers). You already have these in your OSA-Brain vault. The distinction: skills tell the agent *how*, slash commands tell the agent *go*.

**3. Output styles / response formats**
Constrained response shapes the model must follow. JSON mode, structured outputs, XML tags, custom schemas. Critical for any agent step that feeds another agent — unstructured prose doesn't compose, structured output does. HAWK passing data between agents needs this.

**4. RAG (Retrieval-Augmented Generation)**
Vector search over a corpus, results injected into context at query time. Different from skills (skills are curated and static; RAG is dynamic over large document sets). Useful when your knowledge base is too big to load wholesale. Your Obsidian vault could be RAG'd once it crosses ~500 notes.

**5. Memory systems**
Persistent state that survives across sessions. Different flavors:
- **Episodic** — what happened last time (your monthly Claude chat exports)
- **Semantic** — facts about the user/project (what's in your userMemories now)
- **Procedural** — learned workflows ("Phelipe always wants X before Y")

You already have all three running, just informally.

**6. Evals**
Automated tests for agent behavior. Run a battery of prompts, score outputs against expected results, track regressions. Without evals, you can't tell if a skill update made the agent better or worse — you're flying blind. This is the unsexy primitive that separates hobbyist agents from production ones.

**7. Guardrails / classifiers**
Lightweight models that screen inputs and outputs. Different from hooks (hooks are rule-based; guardrails are model-based). Used for safety, off-topic detection, PII redaction. Less relevant for OSA right now but matters once Dumont is talking to real prospects unsupervised.

**8. Observability / tracing**
Logging every tool call, token count, latency, cost per session. You can't optimize what you can't see. Langfuse, LangSmith, Arize — the category exists because debugging agents without traces is brutal.

## The complete stack

```
Evals + Observability    ← measure and debug everything below
   ↓
Plugins                  ← distribution
   ↓
Subagents                ← parallel specialized execution
Slash commands           ← user-invoked triggers
Hooks                    ← deterministic guardrails
Skills                   ← how-to knowledge
Output styles            ← response shape contracts
   ↓
CLI + MCP                ← capabilities (act, fetch)
RAG                      ← dynamic retrieval over large corpora
Guardrails               ← input/output safety screens
   ↓
Memory + Files           ← persistent state across sessions
```

## What's actually missing from OSA right now

You have most of this informally. The two real gaps:

**Evals.** You're iterating on HAWK, on Dumont, on route page generation — without a way to measure whether changes improve quality. This is the next discipline to add. Doesn't need to be sophisticated. Even a 20-prompt regression test you run before shipping changes to a skill would prevent silent quality drift.

**Observability.** Dumont in production with Vapi + ElevenLabs + Deepgram + Railway — when something goes wrong on a real call, can you trace exactly which step broke and why? If not, you're going to learn the hard way the first time it matters.

Everything else in the stack you're either using or have a clear path to. Those two are blind spots worth closing before scale forces them.

---

## Phelipe

Is this harness engineering?

---

## Claude

Close, but not quite. The terms overlap and people use them loosely, so let me draw the line cleanly.

## Context engineering vs harness engineering

**Context engineering** is about *what the model sees*. Selection, compression, timing, persistence of information. The discipline answers: "Given a finite context window and an unreliable reasoning engine, what should be in front of the model right now?"

**Harness engineering** is about *the system around the model*. The runtime, the loops, the orchestration, the safety layer. The discipline answers: "How do I take a model that produces text and turn it into a system that reliably does work in the real world?"

The harness is the cage the model runs in. Context is what gets fed through the bars.

## What's in each

**Context engineering scope:**
- Skills (what knowledge loads when)
- RAG (what to retrieve)
- Memory (what persists)
- Output styles (response shape)
- Prompt structure
- Token budget management

**Harness engineering scope:**
- The agent loop itself (plan → act → observe → repeat)
- Tool execution layer (CLI, MCP, function calls)
- Hooks and interrupts
- Subagent orchestration and delegation
- Error handling and retries
- State machines
- Sandboxing and permissions
- Observability and tracing
- Eval infrastructure

The full stack I drew you is actually **both disciplines combined**. Skills/RAG/memory/output-styles are context engineering. Hooks/subagents/CLI-execution/evals/observability are harness engineering. Plugins are a packaging format that bundles both.

## Why the distinction matters

A team can be excellent at one and bad at the other.

- **Great context, weak harness:** beautiful skills and prompts, but the agent crashes on retries, can't recover from tool failures, has no observability. Demos well, breaks in production.
- **Great harness, weak context:** rock-solid runtime with sandboxing, traces, evals — but the agent does mediocre work because the skills are thin and memory is unstructured. Reliable but unimpressive.

You need both. The high-leverage builders right now are people who treat them as one combined discipline, which is why "context engineering" gets used as shorthand for the whole thing even though it's technically narrower.

## Concrete framing for OSA

- **OSA-Brain vault, CLAUDE.md, writing-guide.md, slash commands, monthly export workflow** → context engineering
- **HAWK's five-agent orchestration, Dumont's Vapi+ElevenLabs+Deepgram pipeline, GitHub Actions drip-publishing, hooks that would gate route-page commits, the eval suite you don't have yet, Railway observability** → harness engineering
- **The whole HAWK plugin you're building** → both, packaged together

If you want a one-line internal mental model: **context engineering tells the model what to think about; harness engineering makes sure it actually ships.**

The reason this distinction matters strategically: when you eventually hire your CTO, you'll want them strong on harness. When you hire the Brand & Content Strategist, you want them strong on context. Different skills, different hires, both required.

---

## Phelipe

Let's think o  our data plataform. What kinda of context engineering and harness engineering we should think about

---

## Claude

Good question to be sitting with now, before you have data flooding in. Let me think through this properly — first the shape of the platform, then the engineering layers.

## What "data platform" actually means for OSA

You're not building one data platform. You're building an integrated data spine that has to serve four very different workloads:

1. **Operational** — Dumont intake, deal pipeline, operator quotes, payments
2. **Pricing intelligence** — Charter Index, route pages, calibration data, deal volume feedback loop
3. **Content intelligence** — HAWK inputs/outputs, Loud Hawk performance, dark social signals
4. **Strategic memory** — vault, conversations, decisions, frameworks (already partially live)

These have different latency, structure, and access patterns. If you build one monolithic context system trying to serve all four, it will be mediocre at all of them. If you build four siloed systems, you lose the compounding effect of cross-domain queries (which is where the actual moat lives).

The right shape: **one canonical data layer underneath, four context-engineered surfaces on top, with shared harness infrastructure.**

---

## Context engineering layer

The job here: when an agent (or you) asks a question, the right slice of data lands in context, in the right form, at the right density.

**1. Schema design as context design**

This is the most underrated decision. Your data tables aren't just storage — they're context primitives. A row is what the model will eventually see. So design tables for *agent legibility*, not just normalized correctness.

Concrete: a `deals` table where every row reads like a self-contained brief — origin, destination, aircraft, operator, quoted price, Charter Index estimate, variance, close status, days to close, client segment. An agent pulling 10 rows gets 10 useful contexts. If instead you have `deals` + `deal_legs` + `deal_pricing` + `deal_outcomes` normalized across four tables, every agent query becomes a join and a context bloat.

The principle: **denormalize for agent reads, even if it costs storage.** Storage is cheap, context isn't.

**2. Layered retrieval, not flat search**

You'll be tempted to throw everything in a vector DB and RAG it. Don't. Different data wants different retrieval:

- **Structured ops data** (deals, quotes, payments) → SQL with parameterized queries the agent constructs
- **Pricing data** (route benchmarks, calibration history) → SQL + materialized views the agent reads
- **Content corpus** (vault notes, past chats, articles) → hybrid search (BM25 + vectors) with metadata filters
- **Live signals** (LinkedIn analytics, GSC impressions, deal events) → time-series with windowed queries

Build a thin abstraction so the agent says "find me X" and the routing layer picks the right backend. Otherwise you'll RAG numerical data and SQL your prose, both badly.

**3. Memory hierarchy, explicit**

Right now your memory is informal — Obsidian vault + monthly Claude exports + my userMemories. As data volume grows, you need explicit tiers:

- **Hot** — current sprint, current deal, current week's content (loads every session)
- **Warm** — last 90 days, current quarter, this year's deals (loads on relevant query)
- **Cold** — full history, semantic search only (loads on explicit recall)

Each tier has different summarization. Hot stays raw. Warm gets weekly digests. Cold gets monthly + thematic summaries. The summarization is itself an agent job — Conductor-style — running on a schedule.

**4. Provenance and freshness as first-class fields**

Every data point an agent sees should carry: source, timestamp, confidence, last-verified. Especially for Charter Index where you're publishing benchmarks. An agent quoting a route price needs to know if the underlying data is from 30 deals or 3, from this quarter or last year. Otherwise it'll confidently cite stale numbers and you'll learn about it from a customer screenshot.

**5. Skills per data domain**

You'll need a skill for each major data surface:
- `querying-deals.md` — schema, common queries, edge cases
- `charter-index-methodology.md` — how prices are calculated, error margins, when to trust
- `vault-search.md` — taxonomy, tag conventions, where things live
- `analytics-interpretation.md` — what counts as signal vs noise on LinkedIn, GSC, newsletter

Without these, every agent session re-learns your data model badly.

---

## Harness engineering layer

The job here: the data platform runs reliably, every action is traceable, errors don't propagate silently, and humans can see what's happening.

**1. Pipeline orchestration**

Right now your data flow is mostly agentic and ad-hoc. As volume grows you need actual pipelines:

- **Scheduled** — Charter Index recalibration, vault summarization, content performance digests, deal cohort analysis
- **Event-driven** — new deal closed → update Charter Index + trigger content opportunity check + log to vault
- **On-demand** — agent queries that fan out to multiple sources

You don't need Airflow on day one. You do need to decide *now* whether you're using Railway cron + scripts, or Temporal, or Inngest, or something else. Switching later is painful.

My read: stay on Railway + simple cron + Postgres for as long as you can. Move to a real orchestrator (Temporal is the cleanest) when you have >20 scheduled jobs or any job whose failure has financial consequences.

**2. The dual-write problem**

The hardest harness problem you'll hit: your operational system (deals, payments) and your intelligence system (Charter Index, content insights) need to stay in sync without either becoming the bottleneck for the other.

The right pattern: **single source of truth in Postgres (or whatever transactional DB), event log of changes (CDC or app-level), downstream systems consume the event stream.** Charter Index recalibration runs off the event stream. HAWK content opportunity detection runs off the event stream. The vault gets updated off the event stream. Everything reads from one truth, reacts asynchronously.

Don't build sync writers. Don't try to keep three databases consistent in real-time. You will lose.

**3. Evals against your data**

This is where evals get teeth. Some examples for OSA:

- "Given these 50 historical deals, does Charter Index v2.1 have lower error than v2.0?" — regression test before deploying methodology changes
- "Given these 20 RFQs, does Dumont route them correctly to the right operator tier?" — regression test before changing routing logic
- "Given these 10 vault queries, does the retrieval surface return the right notes in top 5?" — regression test before reindexing

Each of these is an eval that should run on a schedule and gate deploys. Without them, every change to a methodology or skill is a hope.

**4. Observability with money attached**

Generic observability is fine for tech. For OSA, you want observability that surfaces *business* metrics, not just technical ones:

- Cost per Dumont call (Vapi + ElevenLabs + Deepgram + LLM tokens)
- Token spend per agent task type
- Charter Index error per route per quarter
- Time from RFQ → first quote → close
- Content piece → impression → reply → meeting → deal (full attribution chain)

If you can't see these, you can't optimize them. If you can, you can run the company off three dashboards.

**5. Sandboxing and permissions**

As agents get more capable, the blast radius of a bad action grows. You need permission tiers:

- **Read-only** — most agent operations
- **Write to staging/draft** — content generation, draft route pages, draft quotes
- **Write to production** — only with explicit human approval or hook-gated automation
- **Money movement** — never agent-autonomous, always human-in-loop

Build this in early. Retrofitting permissions onto a permissive system is brutal.

**6. The replay primitive**

Every agent action and every pipeline run should be replayable. Same input → same output (or same error). This sounds boring; it's actually the difference between a system you can debug and one you can't. Concretely: log inputs, log outputs, version the prompts and skills, snapshot the data state. When Dumont misroutes a deal in production, you should be able to replay that exact call and see why.

---

## What I'd actually do, in order

If I were sitting where you are with the platform decisions still mostly open:

1. **Lock the canonical data model** — what tables, what fields, what's denormalized for agent reads. This is a one-week design exercise that pays for two years.

2. **Pick the event stream pattern** — even if it's just append-only Postgres tables on day one. Establish the discipline that nothing writes directly without an event being logged.

3. **Build the memory hierarchy explicitly** — hot/warm/cold tiers with clear loading rules and summarization jobs. Write the skill for each.

4. **Stand up the eval harness before you need it** — even with three tests. The discipline of "no methodology change without an eval" is what separates Charter Index from being a marketing claim vs a real product.

5. **Wire observability with business metrics, not just system metrics** — so the dashboards you check daily are the same ones investors and a future CTO will check.

6. **Defer orchestration sophistication** — Railway + cron + Postgres is enough until it isn't. Don't pre-optimize toward Temporal/Inngest until you've felt the pain.

7. **Hooks for permission gates from day one** — even crude ones. `PreToolUse` hook that blocks any agent write to production tables without approval.

The thing to internalize: **the data platform isn't a feature, it's the substrate every product runs on.** Charter Index, Dumont, HAWK, OSA Connect, eventually OSA Pay — they're all surfaces over the same underlying data + context + harness stack. Get this right once, and every product gets faster and smarter for free. Get it wrong, and every product carries the same tax forever.

Want to go deeper on any of these layers? The data model design and the event stream pattern are the two I'd start with — they're upstream of everything else.

---

## Phelipe

Let's just think at the data plataform. Forget payments.

---

## Claude

Good — narrowing this. Pure data platform, no payment rails complicating it. Let me redo this with sharper focus.

## What the data platform actually is

Strip everything else away and the data platform has one job: **be the trustworthy substrate that every OSA product reads from and writes to.** Charter Index reads from it. Dumont logs to it. HAWK pulls signals from it. Route pages render from it. The vault syncs with it. Future products you haven't built yet plug into it.

If the data platform is right, every product gets faster and smarter for free. If it's wrong, every product carries the same tax forever.

So the design question isn't "what tools do we use" — it's "what are the canonical entities, who owns them, how do they flow, and how do agents read them efficiently."

---

## The four entity domains

Before context or harness, you need to be honest about *what data exists*. For OSA, four domains:

**1. Market data** — the world outside OSA
- Routes (origin/destination pairs, market depth, seasonality)
- Aircraft (tail numbers, types, ages, operators, locations)
- Operators (fleet, certifications, reputation, coverage)
- External pricing signals (charter quotes seen in market, fuel, positioning costs)

**2. Transactional data** — what happens in OSA's flow
- RFQs (requests for quotes, intake source, segment)
- Quotes (operator → OSA, OSA → client, with breakdown)
- Deals (closed, lost, fallen-through)
- Communications (Dumont calls, emails, follow-ups)

**3. Intelligence data** — what OSA learns
- Charter Index estimates (per route, per aircraft class, with confidence)
- Calibration history (estimate vs actual, error tracking)
- Client segments (post-raise founders, pattern matching, signals)
- Operator scoring (response rate, quote accuracy, follow-through)

**4. Content & knowledge data** — institutional memory
- Vault notes (decisions, frameworks, learnings)
- Content artifacts (LinkedIn posts, Loud Hawk issues, route pages)
- Performance signals (impressions, replies, dark social mentions)
- Conversation exports (Claude sessions, strategic discussions)

These are the four domains. Every product is a different cut over them. The data platform's job is to make all four queryable, joinable, and trustworthy.

---

## Context engineering for the data platform

**1. Entity-first schema, agent-legible**

The biggest decision: design tables as *self-describing entities*, not as normalized 3NF database orthodoxy. An agent pulling a single deal should get a row that tells the whole story without joins.

Bad: `deals` (id, rfq_id, status), `rfq_legs` (rfq_id, origin, dest), `deal_pricing` (deal_id, total, breakdown_json), `deal_operator` (deal_id, operator_id)... agent has to do four joins to understand one deal.

Good: `deals` table where each row carries the denormalized story — origin, destination, aircraft type, operator name, quoted price, Charter Index estimate at time of quote, variance, status, days-to-close, client segment, intake source. Joins still possible for analytics, but the row alone is *legible context*.

The principle: **storage is cheap, agent context is the constraint.** Optimize the schema for read-time legibility.

**2. The unified entity ID system**

You'll have the same operator referenced in market data, in deals, in scoring, in content. Same with aircraft, routes, clients. Pick a canonical ID convention now and enforce it everywhere. Sounds boring. Catastrophic if skipped.

Recommendation: human-readable IDs (`op_priester`, `acft_cl350_n123ab`, `route_kpwk_kteb`) instead of UUIDs where possible. Agents debug them faster, you read them in logs, no cognitive tax to remember mappings.

**3. The event log as the spine**

Below the entity tables, an append-only event log. Every state change in the system becomes an event:

- `rfq_received`, `quote_requested`, `quote_received`, `quote_sent`, `deal_closed`, `deal_lost`
- `index_recalibrated`, `operator_scored`, `route_updated`
- `content_published`, `content_performance_logged`

This log is the source of truth. Entity tables are *projections* over the log. Charter Index recalibration runs off the log. HAWK opportunity detection runs off the log. The vault auto-updates off the log.

Why this matters: it gives you replay (rebuild any entity table from history), audit (every change traceable), and **agent legibility for time** (an agent can ask "what changed in the last 24 hours" without you building a custom interface for every entity).

You don't need Kafka for this. Postgres with an `events` table, append-only, with proper indexing, is sufficient until you're processing thousands of events per second. You're not.

**4. Layered retrieval, four routing rules**

The agent doesn't pick the backend. The platform does, based on query type:

- Structured entity lookup (give me deal X, give me operator Y) → direct SQL
- Aggregations and analytics (deals last quarter, error by route) → SQL with materialized views
- Time-window queries (what changed, recent activity) → event log scan
- Semantic / unstructured (find vault notes about X, find content about Y) → vector search with metadata filters

Build a single `query()` interface the agents use. The router behind it picks the right backend. Agents don't think about retrieval mechanics; they think about questions.

**5. Memory tiers, explicit and summarized**

Already mentioned this but it's worth restating in pure-data-platform terms. Three tiers, three retention/summarization policies:

- **Hot (full fidelity)** — last 30 days of events, current quarter's deals, active RFQs, this month's content. Loads cheaply, agents see raw.
- **Warm (weekly summaries)** — last 12 months. Summarized into weekly digest entities. Agent sees the summary, can drill into raw if needed.
- **Cold (semantic only)** — beyond 12 months. Vector-indexed summaries, retrieved only on explicit query.

The summarization is itself a scheduled job. It runs weekly. It's eval'd. You version the summarization logic so when you improve it, you can re-summarize history.

**6. Provenance and freshness as schema requirements**

Every entity row carries: `created_at`, `updated_at`, `source`, `confidence`, `last_verified`. Every Charter Index estimate carries: `methodology_version`, `data_window`, `sample_size`, `error_margin`. Every operator score carries: `as_of`, `based_on_n_deals`.

Without this, agents will confidently cite stale or thin data. With this, the agent can say "Charter Index for KPWK→KTEB is $24,500 based on 18 deals in the last 90 days, ±14% confidence" — which is the actual product.

**7. Domain skills**

One skill per major data surface. Loaded on relevant queries:

- `data/querying-deals.md`
- `data/charter-index-methodology.md`
- `data/operator-scoring.md`
- `data/vault-retrieval.md`
- `data/event-log-conventions.md`

Each one: what's in this domain, common queries, edge cases, what to never do, how to interpret confidence/freshness.

---

## Harness engineering for the data platform

**1. Write paths, controlled**

Three classes of writes, three different harnesses:

- **Trusted automated writes** — pipeline jobs, structured agent outputs that pass validation. Schema-checked, then logged to event log + projected to entity table.
- **Agent-proposed writes** — anything an agent wants to write that isn't a known-safe operation. Goes to a staging table, requires review (human or eval-gated) before promotion.
- **Human writes** — UI or direct DB. Logged to event log same as automated.

The rule: **nothing writes to production entity tables without an event being logged.** Bypassing the event log breaks replay and audit. Make it physically hard to do.

**2. Validation as a hook layer**

`PreToolUse` hooks (or their equivalent in your data layer) on every write:

- Schema validation (Zod on the way in, before the event is appended)
- Referential integrity (operator exists, route is real)
- Business rule validation (quote breakdown sums to total, deal can't close without prior quote)
- Anomaly detection (price > 3σ from Charter Index → flag, don't auto-promote)

When validation fails, the write goes to a `quarantine` table with the error and the proposing agent/source. Humans triage. This is how you keep the data clean while still letting agents write.

**3. Scheduled jobs, declarative**

A small set of jobs run on schedule:

- Charter Index recalibration (nightly initially, then real-time as volume justifies)
- Memory tier promotion/summarization (weekly)
- Operator scoring update (after each deal closes + nightly aggregate)
- Materialized view refresh (hourly for dashboards)
- Vault sync (continuous or hourly)

Each job declared in one place, with: schedule, inputs, outputs, eval gate, alerting. Don't sprinkle cron across the codebase. One registry.

**4. Evals against the data layer**

The evals worth running on the data platform itself, not the products on top of it:

- **Schema integrity** — can I rebuild every entity table from the event log? Continuous test.
- **Charter Index regression** — given last 100 closed deals, does v(n) outperform v(n-1)? Gate on methodology changes.
- **Retrieval quality** — given a labeled set of vault queries, does the retrieval return the right notes in top-K? Gate on indexing changes.
- **Summarization fidelity** — given raw events from a week, does the weekly digest preserve the facts an agent needs? Periodic.
- **Anomaly detector** — does the validation layer catch known-bad writes? Adversarial test set.

Without these, every change is a hope. With these, the platform compounds quality over time.

**5. Observability tuned to data, not just compute**

Generic infra observability is fine. The data-specific signals to track:

- Event log throughput and lag
- Validation pass/fail rate per write source
- Charter Index error per route, trended over time
- Retrieval recall on the labeled eval set
- Memory tier promotion latency
- Schema drift detection (any table whose row shape has changed)

These are the signals that tell you the data platform is healthy. CPU and RAM tell you nothing.

**6. Replay as a first-class capability**

Every agent action and every pipeline run produces enough trace to replay. Same input + same data state + same code version → same output. This is non-negotiable for a system where agents are writing data; without it, debugging a bad write that went to production is forensics, not engineering.

Concretely: tag every write with the agent session ID, the prompt version, the skill version, the data state hash. When something's wrong, you reconstruct the exact context the agent had and run it again.

**7. Permission tiers, enforced at the platform level**

The data platform itself enforces:

- Read-only by default for all agent operations
- Write to staging by elevated agents
- Write to production only via validated event log writes
- Schema changes only via versioned migrations with explicit approval

This isn't a hook on a tool call. It's enforced in the data layer (row-level security, role-based access). Hooks at the agent level are belt-and-suspenders. The data layer is the suspenders.

---

## What I'd actually build first

Given you're solo, part-time, and need to not over-engineer:

**Phase 1: the spine**
- Postgres with the four entity domains as tables, denormalized for legibility
- Append-only `events` table as the spine
- Canonical ID convention enforced
- Provenance/freshness fields on every entity row
- A thin `query()` interface routing to SQL vs vector vs event-log

**Phase 2: the discipline**
- Validation layer (Zod schemas, business rules) on every write
- 3–5 evals running on schedule, gating changes
- One scheduled job: Charter Index recalibration off the event log
- Skills for each domain so agents query competently

**Phase 3: the leverage**
- Memory tier summarization jobs
- Materialized views for the dashboards you'll actually look at
- Replay capability with session-tagged writes
- Permission tiers at the database level

You can do Phase 1 in a focused week. Phase 2 in another. Phase 3 when volume forces it.

The temptation will be to skip the event log because "we don't need it yet." Resist this. It's the spine. Every piece of intelligence you build later — Charter Index calibration, operator scoring, content attribution — runs cleanly off an event log and miserably without one. Add it on day one. It's twenty lines of schema.

The other temptation: vector DB everything. Don't. SQL is correct for 80% of OSA's data. Vectors are only for the unstructured corpus (vault, content, transcripts). Routing is the win, not picking one backend.

Want to drill into the entity schema design specifically? That's the highest-leverage decision and the one I'd want to think through carefully before any code gets written.

---

## Phelipe

Look at our past chats for context. How can we keep build and add context engineering and harness engineering

---

## Claude

Let me pull what's actually been built and discussed before I answer this — your past chats have the operational detail that should anchor this.
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

Now I have enough. Let me give you a clean answer grounded in what's actually built.

---

## Where you actually are

You don't need to build a data platform from scratch — **you've been building it for months.** Let me reflect back the real state, then map context and harness moves onto it.

**What exists:**
- Supabase Postgres with ~45 data-platform tables (ADS-B, FAA, NTSB, operators, canonical, aircraft, route, knowledge_graph, etc.) and ~8 agent-state tables (deals, messages, calls, client_profiles)
- 152K+ completed ADS-B legs, 4,968 charter-class aircraft, 4,298 ghost candidates already materialized
- Dumont running on Railway (Vapi + ElevenLabs + Deepgram + Claude Haiku, ~575ms turn, $0.15/call)
- Mission Control dashboard at mc.orangesunshineaviation.com with chat, pipeline view, Loud Hawk tab
- OSA-Brain Obsidian vault with `/quickdump`, `/dump`, `/organize`, `/compile`, `/decay`, `/recall`, `/brief`, `/digest`, `/healthcheck`, `/operator`, `/decision`, `/debrief`
- The decision logged in `phase1-followups.md` to split `osa-data-platform` from `dumont-agent` post-build
- Dumont Intelligence MCP server, currently in dumont-agent, designed to move to osa-data-platform

That's the substrate. Now the question becomes: **how do we add context engineering and harness engineering discipline on top of what's already running, without slowing the build?**

---

## Context engineering moves

These are about making the data the agents see denser, more legible, and properly tiered.

**1. Lock the entity-legibility contract for the tables Dumont reads most**

Right now the 22K+ legs table works because you already backfilled `aircraft_class`. That was a context engineering fix you didn't name as one — you made each row self-describing so queries return useful context, not joins-to-nothing. Same pattern needs applying to:

- `operators` (must carry: ARGUS rating, Wyvern status, fleet count, response history, last-deal-date, in one row)
- `route_intelligence` (must carry: liquidity score, ghost probability, Charter Index estimate, sample size, last-calibrated, in one row)
- `deals` (must carry: full story — origin, destination, aircraft, operator, quoted vs index, variance, status, days-to-close, in one row)

Build it as a discipline: **before any new agent feature ships, check that the rows it reads are agent-legible without joins.**

**2. Materialized views as context primitives**

For the queries Dumont runs over and over (KTEB ghost candidates, KPWK super-mid availability, route X recent volume), build materialized views. Refresh on a schedule. The agent pulls from the view, not the raw tables. Faster, denser, predictable token cost.

This is the highest-leverage near-term move. You've got the raw data; you don't have the materialized layer yet.

**3. Provenance fields on Charter Index outputs**

Every Charter Index estimate Dumont surfaces needs to carry: methodology version, sample size, error margin, last calibrated. You already locked the calibration path (±20 → ±12 → ±8 → ±5). Now make it visible in every output. This is what separates "Dumont confidently quoted a stale price" from "Dumont said $24,500 ±14% based on 18 deals last 90 days."

This is a schema-level decision. Add the fields now. Backfill is cheap. Retrofitting later when you have a customer dispute is not.

**4. Memory tier promotion for Dumont's deal history**

Right now Dumont's deal_events log grows linearly. As deals accumulate, the agent's context cost grows with it. Build the three-tier discipline:

- Hot: last 30 days, raw events, full fidelity
- Warm: last 12 months, weekly summaries (a scheduled summarizer job)
- Cold: beyond 12 months, semantic-indexed only, retrieved on demand

The summarizer is itself an agent job. Conductor-style. Eval'd. Versioned. You can build it before you need it because the data is small now — perfect time to write the discipline while the cost of getting it wrong is zero.

**5. Domain skills in osa-data-platform repo**

When the data platform splits out, ship skills with it:

- `data/querying-deals.md`
- `data/charter-index-methodology.md`
- `data/operator-scoring.md`
- `data/ghost-candidates.md`
- `data/event-log-conventions.md`

Anyone (you, Claude Code, future CTO, Hermes if you wire it up) querying the platform reads these once and operates correctly. Without them, every session re-derives bad SQL from scratch.

**6. The MCP tool surface as context contract**

The Dumont Intelligence MCP server you're moving to osa-data-platform is the actual context interface. The tools it exposes ARE the context engineering decisions — what's queryable, what's denormalized, what's pre-aggregated. When you do the move, treat the tool surface as a v1 API. Don't expose raw SQL access. Expose entity-shaped, legibility-first tools: `get_operator_profile`, `find_ghost_candidates`, `get_route_intelligence`, `query_recent_deals`. Each one returns dense, self-describing rows.

---

## Harness engineering moves

These are about making sure the system runs reliably, every action is traceable, and errors don't propagate silently.

**1. The repo split itself is harness work**

The decision logged in `phase1-followups.md` to extract osa-data-platform from dumont-agent isn't just code organization — it's the harness boundary. Once data is behind an MCP interface, Dumont can't accidentally write directly to a table. The MCP tools enforce the contract. Bad writes hit the validation layer, not production.

This is the single highest-leverage harness move available. Sequence it after Phase 7 finishes so you don't break in-flight work, but it's the next major architectural step.

**2. Validation as a hook layer at the data platform**

Every write to canonical tables goes through validation:

- Zod schema check
- Referential integrity (operator exists, route is real)
- Business rule check (quote breakdown sums to total, deal can't close without prior quote)
- Anomaly detection (price > 3σ from Charter Index → quarantine)

Failed writes land in a `quarantine` table with the proposing agent + reason. You triage. This is how you let agents write to production without breaking trust.

**3. Eval suite gating the methodology you actually publish**

Charter Index will be a public-facing benchmark. Every methodology change needs to pass evals before it deploys:

- Given the last 100 closed deals, does v(n) outperform v(n-1) on error metric?
- Given a labeled set of operator queries, does the resolver return correct canonical entities top-1?
- Given known-bad writes (test set), does validation catch them?
- Given a labeled set of vault queries, does retrieval surface the right notes top-K?

Five tests, run on a schedule, gate deploys. This is the difference between "Charter Index improving over time" being a marketing claim vs a measurable product.

**4. Observability with business signals, not just system metrics**

Wire dashboards that show:

- Cost per Dumont call (Vapi + ElevenLabs + Deepgram + LLM tokens)
- Token spend per agent task type
- Charter Index error per route per quarter
- RFQ → first quote → close time
- Ghost positioning hit rate (predicted vs actual)
- Validation pass/fail rate per write source

These go on the same Mission Control dashboard you've already built. One view. The agent system is healthy when these numbers are.

**5. Replay capability tagged at the agent layer**

Every Dumont action and every pipeline run produces enough trace to replay: session ID, prompt version, skill version, data state hash. When something goes wrong on a real call, you reconstruct the exact context Dumont had and run it again to debug.

You're not at the volume where this is forced yet. You will be. Build the trace logging now while the system is small and you can verify it works.

**6. Permission tiers at the database, not just the agent**

Right now Dumont has full DB access because it's in the same repo. After the split:

- Read-only role for default agent operations
- Write-to-staging role for proposed updates
- Write-to-production role only via validated MCP tools
- Schema changes only via versioned migrations with explicit approval

Postgres row-level security is the right primitive. This is belt-and-suspenders against a bad agent action — even if the agent tries to do something stupid, the database refuses.

**7. The Conductor as a harness primitive, not a content agent**

HAWK's Conductor is named like a content role but it's actually a harness role — orchestrating Scout/Writer/Designer/Analyst, gating outputs, enforcing the workflow. Reframe Conductor in your own thinking as "the harness layer for HAWK." Same way Dumont's PIC pattern is the harness layer for the five capabilities.

This matters for the eventual hire: when you bring on a Brand & Content Strategist, what they inherit is the *content discipline* (skills, voice, process). What they don't touch is the harness (Conductor logic, eval gates, hooks). That separation is what makes the role transferable.

---

## The build sequence I'd recommend

Given you're solo, part-time, and don't pressure yourself with deadlines:

**Now (during Phase 7):**
- Add provenance fields to Charter Index outputs (schema-level, cheap)
- Backfill agent-legibility on operators table the way you did on legs
- Build 3 evals that gate Charter Index methodology changes

**Next (after Phase 7 finishes):**
- Execute the osa-data-platform / dumont-agent split per `phase1-followups.md`
- Move the Dumont Intelligence MCP server to osa-data-platform
- Lock the MCP tool surface as the v1 context contract
- Ship domain skills alongside the new repo

**Then (when volume forces it):**
- Materialized views for hot queries
- Memory tier summarization for deal history
- Validation/quarantine layer on writes
- Permission tiers via RLS
- Replay tagging on every agent action

**Continuously:**
- Observability dashboards with business metrics, expanding as new flows go live
- Eval suite growing with every new methodology or skill change

---

## The frame to internalize

You're not adding context engineering and harness engineering as new disciplines. **You've been doing both implicitly for months.** The vault structure is context engineering. The /organize and /decay slash commands are harness. The OSA-Brain CLAUDE.md is a skill. The Dumont MCP server is a context contract. The osa-data-platform split decision is a harness boundary.

The shift now is from implicit to explicit — naming what you're doing, building it as discipline, and making the moves transferable to the future CTO and Brand & Content Strategist who will inherit this.

The next person you hire shouldn't have to read 200 chat exports to understand how OSA's data system works. They should clone the repo, read 5 skill files, and operate. That's the goal of making this explicit.

---

## Phelipe

Forget dumont and hawk for now. Think data plataform for aviation. The operator ER, Aircraft ER, datasets and adsb ingestion

---

## Claude

Good. Pure data platform for aviation. Forget the agents, forget the products on top — just the substrate. Let me think through this carefully because this is the foundational work everything else depends on.

## What "the aviation data platform" actually is

You're building a canonical truth layer for U.S. private aviation. Four entity types, multiple source datasets, continuous ingestion. The job: ingest noisy, overlapping, sometimes contradictory data from many sources, resolve it into clean canonical entities, and expose those entities for query.

The entities, in order of complexity:

1. **Aircraft** — every airframe that exists, identified by tail number, ICAO hex, serial number
2. **Operators** — every Part 91 / 135 / 121 entity that flies aircraft
3. **Routes** — every origin/destination pair, with characteristics
4. **Events** — every state change in the world (a flight happened, an operator got certified, a tail changed hands)

These are not equally hard. Aircraft is the easiest because tail numbers are unique and the FAA registry is authoritative. Operators is the hardest because operators have multiple legal entities, DBAs, fleets they manage but don't own, and certificate types. Routes are derived. Events are append-only and easy if you get the schema right.

Let me work through each.

---

## Aircraft entity resolution

**The truth source:** FAA Aircraft Registry (`registry.faa.gov`). ~300K active US-registered aircraft. Updated monthly. This is the authoritative dataset. Everything else enriches it.

**The canonical key:** N-number (tail number). It's unique, stable, and human-legible. Use it as the primary identifier. ICAO hex is the secondary key (used by ADS-B). Serial number is the tertiary key (used when registration changes).

**Schema, agent-legible:**

```
aircraft (
  n_number              text PK,           -- N123AB
  icao_hex              text,              -- ABC123
  serial_number         text,
  manufacturer          text,              -- Embraer
  model                 text,              -- Phenom 300E
  type_code             text,              -- E55P (ICAO)
  aircraft_class        text,              -- light/midsize/super_mid/heavy/turboprop
  year_manufactured     int,
  registered_owner      text,              -- legal owner from FAA
  registered_owner_type text,              -- individual / corp / partnership / trust
  operator_canonical_id text,              -- resolved operator (FK)
  operator_confidence   numeric,           -- 0.0-1.0
  base_airport_icao     text,              -- inferred from ADS-B activity
  registration_status   text,              -- active / cancelled / expired
  last_seen_adsb        timestamptz,
  data_sources          text[],            -- ['faa', 'adsb', 'aviapages']
  created_at            timestamptz,
  updated_at            timestamptz
)
```

**Resolution problems:**

- **Owner ≠ operator.** FAA registers the legal owner. The operator is who flies it. A Delaware LLC owns the plane; NetJets operates it. Owner-to-operator resolution is a real problem and is half the value of the platform.

- **Trust registrations.** ~30% of business jets are owned by trusts (Bank of Utah Trustee, etc.). The trust hides the beneficial owner. You can't resolve it from FAA alone. You need ADS-B activity + operator certificates + sometimes manual triangulation.

- **Type codes are messy.** ICAO type code (`E55P`) ≠ manufacturer model (`Phenom 300E`) ≠ marketing name (`Phenom 300`). Build a `aircraft_types` reference table that maps all three and has the class designation. Don't store class on every aircraft row — derive it from type code via the lookup.

- **Hex codes change rarely but do change.** When a tail re-registers, the hex updates. Track this in event history.

**The operator resolution heuristic:**

Build a resolver that takes (n_number, owner_name, ADS-B base airport, ADS-B flight pattern) and returns the most likely operator. Layered approach:

1. If owner matches a known operator name fuzzy-string → use it (high confidence)
2. If aircraft is on a Part 135 certificate (DOT operator list) → use that operator (high confidence)
3. If aircraft consistently bases at a known operator's home airport → likely managed by them (medium confidence)
4. If aircraft is owned by a known trust → flag as "managed, operator unknown" (low confidence, manual review queue)

Store the resolution result with confidence. Re-resolve nightly as new data comes in.

---

## Operator entity resolution

**The truth sources, ranked:**

1. **FAA Part 135 certificate holders** (DOT/FAA datasets) — authoritative for who's certified to fly charter
2. **FAA Part 121 air carrier list** — for commercial
3. **ARGUS ratings** (Gold, Gold Plus, Platinum) — third-party safety rating, paid data
4. **Wyvern Wingman** — competing third-party safety rating, paid data
5. **NTSB accident database** — incidents per operator
6. **State business registrations** — DBAs and legal entities
7. **Operator websites** — for fleet listings, contact info, marketing
8. **Aviapages directory** — already-aggregated operator info, useful as a sanity check

**The canonical key:** This is where it gets hard. There's no single ID for operators. Options:

- FAA certificate number (when applicable) — stable, unique, but only for Part 135/121
- DOT number — broader but inconsistent
- Custom canonical ID (`op_priester_aviation`) — human-legible, you control it

Recommendation: custom canonical ID as primary key, with FAA cert number and DOT number as additional lookup fields. This lets you handle Part 91 fleets that don't have an FAA cert at all.

**Schema:**

```
operators (
  canonical_id          text PK,           -- op_priester_aviation
  legal_name            text,              -- Priester Aviation, LLC
  dba_names             text[],            -- ['Priester', 'Priester Aviation']
  faa_cert_number       text,              -- if Part 135/121
  faa_cert_type         text,              -- part_91 / part_135 / part_121
  dot_number            text,
  base_airport_icao     text,              -- KPWK
  fleet_size            int,               -- derived from aircraft table
  argus_rating          text,              -- gold / gold_plus / platinum / none
  wyvern_status         text,              -- wingman / registered / none
  is_safa_iosa          boolean,
  ntsb_incidents_5y     int,               -- derived
  contact_phone         text,
  contact_email         text,
  website               text,
  founded_year          int,
  data_sources          text[],
  data_confidence       numeric,
  last_verified         timestamptz,
  created_at            timestamptz,
  updated_at            timestamptz
)
```

**Resolution problems:**

- **Multiple legal entities.** Priester Aviation might be Priester Aviation LLC, Priester Aviation Holdings LLC, and PA Management Group LLC all rolling up to the same operational entity. Your canonical resolver needs to merge these. Build a `operator_aliases` table that maps every observed name variant to the canonical ID.

- **Managed vs owned fleet.** Most operators manage aircraft they don't own. The operator-to-aircraft relationship is many-to-many in reality, but you'll model it as one-to-many on the aircraft side (each aircraft has one current operator) and let history live in events.

- **Charter brokers ≠ operators.** A broker (like OSA) doesn't fly anything. Don't conflate. Have a separate `brokers` table or a `entity_type` field on a unified `aviation_entities` table.

- **Operators come and go.** Certificates lapse. Companies sell. Mark soft-delete via `status` field; never hard-delete. The historical fact that operator X flew aircraft Y in 2023 is valuable.

**The merge primitive:**

Build a `merge_operators(from_id, to_id)` function that:
1. Updates all aircraft pointing to `from_id` to point to `to_id`
2. Moves all aliases from `from_id` to `to_id`
3. Logs the merge as an event
4. Marks `from_id` as merged with a pointer to `to_id`

This is the operation you'll run constantly as you discover that "Priester Aviation" and "Priester Aviation LLC" are the same entity. Make it idempotent and reversible.

---

## Routes and route intelligence

**The canonical key:** `(origin_icao, destination_icao)`. Always store both directions separately — KTEB→KMIA and KMIA→KTEB are different routes with different demand patterns.

**Routes are derived, not ingested.** Every completed leg from ADS-B contributes to route intelligence. The route table is a materialized view over the legs table, plus enrichment.

**Schema:**

```
routes (
  origin_icao          text,
  destination_icao     text,
  PRIMARY KEY (origin_icao, destination_icao),

  distance_nm          numeric,           -- great circle, computed
  typical_flight_min   int,               -- median from ADS-B
  legs_30d             int,               -- last 30 days
  legs_90d             int,
  legs_365d            int,
  charter_legs_90d     int,               -- filtered to charter-class aircraft
  unique_aircraft_90d  int,
  unique_operators_90d int,

  charter_index_light     numeric,        -- $/hour estimate
  charter_index_midsize   numeric,
  charter_index_supermid  numeric,
  charter_index_heavy     numeric,
  charter_index_methodology_v text,
  charter_index_sample_size int,
  charter_index_error_pct  numeric,
  charter_index_calibrated_at timestamptz,

  liquidity_score      numeric,           -- 0-100
  ghost_probability    numeric,           -- 0-1
  seasonality_pattern  jsonb,             -- monthly multipliers
  
  last_recalculated    timestamptz
)
```

This table is rebuilt on a schedule from the legs table. Don't let agents write to it directly. It's a projection.

---

## Events: the spine

Every state change in the platform is an event. Append-only. This is the most important table in the entire system.

```
events (
  event_id             uuid PK,
  event_type           text,              -- aircraft_registered, operator_merged, leg_completed, charter_index_recalibrated, etc.
  entity_type          text,              -- aircraft / operator / route / leg
  entity_id            text,              -- the canonical ID of the affected entity
  payload              jsonb,              -- the actual change data
  source               text,              -- faa_registry / adsb_lol / opensky / manual / etc.
  source_record_id     text,               -- traceability back to source
  occurred_at          timestamptz,        -- when the change happened in the world
  ingested_at          timestamptz,        -- when we learned about it
  ingestion_run_id     uuid,               -- which ingestion job produced this
  confidence           numeric,
  schema_version       int                 -- so you can evolve payload shape
)
```

**Why this is non-negotiable:**

- Replay: rebuild any entity table from the event log
- Audit: every change traceable to a source and a timestamp
- Time travel: query "what did we believe about operator X on date Y"
- Debugging: when something looks wrong, the event log tells you why
- Calibration: Charter Index recalibration runs from `leg_completed` events filtered by date range

Your existing 152K legs and 22K events from ADS-B ingestion are already the start of this. The discipline to add: **everything that mutates an entity table also writes an event.** No exceptions. Make it physically hard to skip.

---

## ADS-B ingestion

You already have this working. Let me focus on the harness around it because that's where the fragility lives.

**Current state from past chats:**
- `adsb-history/traces` from globe_history GitHub repos, 65K trace files per day
- ~3.9M positions per day after 10x downsampling from 38M raw
- 22K completed legs materialized per day
- 4,968 charter-class aircraft per day
- Ingestion script: `npm run ingest:history [path]`, ~5 min for one day on MacBook
- ODbL 1.0 license, 3 years of data available (2023-2026)

**Gaps in the harness:**

1. **No incremental ingestion discipline.** You're running the full ingest manually. Build:
   - A daily cron that pulls the latest day from globe_history
   - An idempotent ingest (running twice on the same day produces the same result)
   - A progress tracker (`archive_progress` table you have) extended to `ingestion_runs` with start/end/rows/errors
   - A backfill script that fills gaps (any day missing from `archive_progress` gets pulled)

2. **No leg detection eval.** Your leg detector turns position streams into legs via airborne→ground transitions. How accurate is it? Build a small labeled set (50 legs you've manually verified) and run the detector against it on every change. Without this, you'll silently degrade detection quality and never know.

3. **No deduplication primitive.** ADS-B from `adsb.lol`, OpenSky, FlightAware all overlap. As you add sources, you'll get the same flight three times. Decide now: one canonical leg per (icao_hex, departure_time ± 5 min) — keep the highest-confidence source. Build the dedup logic before you add the second source.

4. **No data quality flags on legs.** Some legs have wrong origin (0 flight time means the detector misfired). Some have positions over the ocean for GA aircraft (probably wrong tail). Add a `quality_flags` jsonb to legs and a nightly job that flags anomalies. Filter them out of route intelligence.

5. **Aircraft state computation is implicit.** Your `adsb_aircraft_state` table tracks current state. But the logic for "is this aircraft currently airborne, idle, or in maintenance" is not formalized. Write it down as a state machine. Eval it on labeled examples.

---

## Source dataset map

Here's the full list of datasets the platform should know about, what they contribute, and where they fit:

**Aircraft truth:**
- FAA Aircraft Registry (monthly snapshot, ~300K aircraft)
- FAA MASTER file (more detail per aircraft)
- ICAO type code reference (static)

**Operator truth:**
- FAA Part 135 certificate holders
- FAA Part 121 air carrier list
- DOT operator database
- ARGUS / Wyvern (paid, when budget allows)
- State business registrations (when needed for entity resolution)

**Activity truth:**
- adsb.lol globe_history (3 years daily, primary)
- OpenSky Network (live, optional second source)
- FlightAware (paid, deferred)
- ADS-B Exchange (alternative, free)

**Safety truth:**
- NTSB accident database
- FAA enforcement actions
- FAA airworthiness directives

**Reference data:**
- Airport database (OurAirports.com is free, comprehensive)
- Runway data (FAA airport facility directory)
- FBO list (FBOs.com or paid alternative)
- Fuel pricing (paid, deferred)

**Market context:**
- Aviapages directory (free tier, validation only)
- ADS-B-derived charter movement counts (your own derived data)

**Don't ingest everything at once.** The discipline: start with the FAA registry + adsb.lol. Get those two clean and canonical. Then add Part 135 certificates. Then NTSB. Each new source = one ingestion job + one resolver pass + one eval set. Don't skip the eval.

---

## The repo structure for osa-data-platform

```
osa-data-platform/
├── README.md
├── CLAUDE.md
├── docs/
│   ├── architecture.md
│   ├── entity-resolution.md
│   ├── source-datasets.md
│   └── ingestion-runbook.md
├── skills/
│   ├── querying-aircraft.md
│   ├── querying-operators.md
│   ├── querying-routes.md
│   ├── charter-index-methodology.md
│   ├── event-log-conventions.md
│   └── entity-resolution-rules.md
├── migrations/                    # Postgres schema, versioned
├── src/
│   ├── ingestion/
│   │   ├── faa-registry/
│   │   ├── adsb-lol/
│   │   ├── opensky/
│   │   ├── ntsb/
│   │   └── shared/                # dedup, validation, event-writing
│   ├── resolvers/
│   │   ├── aircraft.ts
│   │   ├── operator.ts
│   │   └── shared/                # fuzzy matching, alias handling
│   ├── projections/               # materialized view rebuilders
│   │   ├── routes.ts
│   │   ├── operator-fleet.ts
│   │   └── charter-index.ts
│   ├── mcp/                       # the MCP server, tool surface
│   │   ├── tools/
│   │   │   ├── get-aircraft.ts
│   │   │   ├── get-operator.ts
│   │   │   ├── find-ghost-candidates.ts
│   │   │   ├── get-route-intelligence.ts
│   │   │   └── query-recent-legs.ts
│   │   └── server.ts
│   └── evals/
│       ├── leg-detection.eval.ts
│       ├── operator-resolution.eval.ts
│       ├── charter-index-regression.eval.ts
│       └── fixtures/
├── jobs/                          # scheduled work
│   ├── daily-adsb-ingest.ts
│   ├── monthly-faa-registry.ts
│   ├── nightly-resolver-pass.ts
│   ├── route-intelligence-rebuild.ts
│   └── charter-index-recalibration.ts
└── tests/
```

The discipline: **every entity has an ingester, a resolver, a projection, and an eval.** If one of those is missing, the entity isn't production-grade.

---

## Build sequence I'd recommend

You already have FAA + ADS-B + completed legs working. The platform exists. The work now is making it disciplined.

**Phase A: solidify what's running**
1. Add `events` table as the spine, retrofit existing ingesters to write events
2. Add provenance + confidence fields to aircraft and operator tables
3. Build the `merge_operators` and `merge_aircraft` primitives properly
4. Add data quality flags to legs and a nightly anomaly job

**Phase B: extract and harden**
1. Execute the `dumont-agent` → `osa-data-platform` split
2. Move the MCP server to the data platform repo
3. Lock the MCP tool surface as v1
4. Ship domain skills with the new repo

**Phase C: ingestion discipline**
1. Daily cron for adsb.lol with idempotent ingest
2. Monthly cron for FAA registry refresh
3. Backfill script for any missing days
4. Eval suite for leg detection, operator resolution, charter index

**Phase D: resolver intelligence**
1. Operator resolver with the layered heuristic (cert → owner match → base airport → trust flag)
2. Aircraft → operator confidence scoring
3. Manual review queue for low-confidence resolutions
4. Charter Index v2 calibration off the cleaned event log

**Phase E: new sources**
1. NTSB integration (safety scoring)
2. Part 135 certificate holders
3. ARGUS / Wyvern when budget allows
4. Each one through the same disciplined pipeline

Don't skip Phase A. Most platforms die not because they can't ingest more sources but because the substrate gets messy and every new source amplifies the mess.

---

## The frame

This data platform is the actual moat. Every product OSA ships is a different cut over this. Charter Index, route pages, Dumont, eventually OSA Aircraft, eventually OSA Pay — all of it reads from this.

Get it disciplined now, while the data is small and you can verify quality directly. Once you're at 10x current volume, the discipline you didn't build at this stage becomes impossibly expensive to retrofit. The right time to formalize entity resolution, event logging, and eval gating is when the data is small enough to inspect by hand. That's now.

Want to go deeper on any specific piece? The operator entity resolution is probably the highest-leverage to think through carefully — it's the hardest problem and the one with the most payoff.

---

## Phelipe

Is this legit?

---

## Claude

Let me look it up — moneyprinter.me, "by Roger," YC + General Catalyst + Capital One Ventures backing.
```
This block is not supported on your current device yet.
```

Yeah, it's a real company. Roger (aka ClawGTM / MoneyPrinter) is a YC S24 company. The founder previously built OctoShop to a $2M cash exit before college and bootstrapped TravelArrow to $1.7M ARR. Backed by YC, General Catalyst, and Capital One Ventures — that part checks out.

What it actually does: Roger is an AI sales rep — it deploys agent swarms across 300M profiles, live job listings, and custom scrapers to find leads, then crafts personalized messages across email and LinkedIn. Now they've added phone dialing as a third channel.

**Honest take, given OSA:**

The product is legitimate. The category is brutally crowded — there are now 50+ "AI SDR" tools and the differentiation between them is mostly marketing. The "paste your URL, print money" framing is the dominant aesthetic in the space right now (Clay, 11x, Artisan, Regie, all converging on the same pitch).

**Should you use it for OSA? Almost certainly not, and here's why:**

1. **Your beachhead is too narrow.** Post-raise founders doing 2–8 charter trips a year. There are maybe 5,000 of them in the US. AI SDR tools are built for high-volume, low-precision outbound — they spray. Your motion is the opposite: connector relationships, dark social, screenshot-worthy content, dream 500 list. Spray-and-pray will burn your domain reputation and put you in spam folders before you book a single meeting.

2. **You're the one selling AI-native aviation.** If you're caught using a generic AI SDR to send templated outreach about how OSA is different, that's a credibility tax you can't afford. Your founder-led brand is the moat for the first 50 deals.

3. **Conceptually, you're building Dumont — the domain-specific version of this.** Dumont with the data platform behind it is a vertical-specific Roger for charter aviation. You'd be paying a horizontal tool to do a worse version of what you're building.

4. **The economics don't work for your deal size.** AI SDR tools are priced for SMB SaaS where ACV is $5–50K and volume is the game. Your deal size is much higher per transaction, but volume is much lower. The unit economics that justify Roger's pricing don't map.

**Where it's interesting as research, not as a buy:**

The product page itself is a positioning study. "Paste your website. Print money." with social proof tickers showing live customer wins (Lumen Sales buying signal, Frontline AI 34% open rate, SideQuest GTM plan) is a textbook Dunford-shaped landing page — clear value, time-to-value visible (Lumen "61s," Harbor Health "5.9s"), specific outcomes attached to specific customers. The audio note button, the cassette aesthetic, the "by Roger" personal branding under "money printer" — all of that is worth studying for how OSA Connect's eventual landing page should feel.

So: legit product, not your tool, but a useful reference for landing page craft. Don't subscribe.

---

## Phelipe

Can we replicate this?

---

## Claude

Pause before answering that — let me make sure I'm answering the right question, because "replicate this" could mean three very different things.

## Three things you might mean

**1. Replicate the landing page aesthetic for OSA Connect's site**
The "paste your URL, print money" page craft. Bold serif/italic mix, cassette aesthetic, live ticker of customer wins, specific time-to-value numbers, audio note button, founder personal branding. That's a positioning + design exercise. Cheap and high-leverage.

**2. Build a generic AI SDR product like Roger**
A horizontal "paste your URL, we find buyers and message them" tool. Compete with Roger, 11x, Clay, Artisan, Regie. New product category, new business, distinct from OSA.

**3. Build a vertical AI SDR for charter aviation, internal to OSA**
Take the Roger pattern and apply it specifically to OSA's beachhead — your data platform identifies post-raise founders, Dumont reaches out across email/LinkedIn/phone, the system runs in the background while you fly trips at SkyWest. This is conceptually what Dumont becomes once it has the data platform behind it.

Which one are you actually asking about?
```
This block is not supported on your current device yet.
```

Pick one and I'll go deep. My honest read on each before you choose:

**Option 1** is the right move regardless of anything else. Roger's landing page is doing positioning work OSA Connect's eventual site needs to do. Worth studying and adapting.

**Option 2** is a bad idea for you. The category is bloodbath-crowded, your moat in aviation is precisely that you're not horizontal, and it would split your focus from the only thing that compounds — OSA's vertical depth.

**Option 3** is the most interesting question, and arguably what you've been building toward without naming it. Dumont + the data platform + the operator/aircraft/route entities + outbound across email/LinkedIn/phone targeting your specific ICP = a vertical Roger that nobody else can build because nobody else has the aviation data layer underneath. This is where the real conversation is.

---

## Phelipe

Q: Which 'replicate' do you mean?
A: Vertical AI SDR for OSA (Dumont evolution)

---

## Claude

Good. This is the right thing to be thinking about. Let me work through it carefully because there's a lot to get right.

## What you're actually proposing

Dumont today is an inbound voice agent with a 5-capability pipeline. It answers calls, qualifies trips, runs intake. The orchestrator is built. The data platform is being built behind it.

What you're proposing is the inverse motion: **outbound.** Dumont initiates contact with target prospects (post-raise founders), across multiple channels (email, LinkedIn, phone), using the data platform to identify buying signals (raised in last 90 days, traveling for fundraising/board meetings/site visits, currently flying commercial), and the existing reasoning layer to write personalized outreach that doesn't sound like a templated AI SDR.

The Roger pattern flipped vertical: instead of "paste any URL," it's "we already know the URL — every post-raise founder in your ICP." Instead of generic personalization, it's domain-specific personalization built on aviation data nobody else has.

This is real. Let me think through what makes it work, what kills it, and what the actual build looks like.

---

## Why this is uniquely possible for OSA

Three things compound:

**1. You have the data layer they don't have.** Roger searches LinkedIn and company websites. You have ADS-B + FAA + funding databases + your own deal history + route intelligence. When you reach out to a post-raise Series B founder in Chicago, you can reference: "Saw your team flew commercial KORD→KSFO last week — that's a 4.5-hour day. Here's what KPWK→KOAK on a Phenom 300 looks like for the same trip." That's not personalization a horizontal tool can do.

**2. Your channels include a real one nobody else has.** Email and LinkedIn are saturated. The phone channel — Dumont actually calling — is differentiated *only if it's good*. You already have that infrastructure (Vapi + ElevenLabs + Deepgram, ~575ms turn, $0.15/call). A founder who picks up a call from someone who clearly understands their travel pattern and offers concrete time savings is a different conversation than getting another "quick question?" email.

**3. The outbound reinforces the inbound product.** Every outbound conversation feeds the data platform — which post-raise founders pick up, what objections come up, what travel patterns convert. This makes Dumont smarter for *every* call, inbound or outbound. Roger doesn't have this loop because they don't own a transaction.

---

## What kills this if you build it wrong

**1. Becoming the thing you despise.** The reason "AI SDR" is a slur in 2026 is that the category trained an entire generation of buyers to hate templated outreach pretending to be personal. If your outbound feels like Apollo + ChatGPT, you've burned the founder-led trust that's your actual moat. The tolerance for AI-generated outreach in your ICP (sophisticated post-raise founders) is roughly zero.

**2. Volume thinking.** Roger's economics work at 10,000 sends per customer per month. Your deal size and ICP demand the opposite — maybe 50 truly targeted touches per month, each one researched well enough that the recipient doesn't realize an AI helped. If you build for volume, you've built the wrong product.

**3. Channel reputation damage.** Your domain (orangesunshine.com) and your phone numbers are non-renewable resources. One spam complaint, one mass send to a bad list, one wrong-number dial in volume, and you're rebuilding from zero. The data platform has to gate aggressively against bad sends, not enable more sends.

**4. The compliance cliff.** TCPA on phone calls. CAN-SPAM on email. LinkedIn's anti-automation rules. None of these are theoretical for outbound. Roger has a legal team. You don't, yet.

**5. Distraction from inbound.** You're 9 months in. Dumont's voice intake works. The data platform is mid-build. Adding an outbound surface before inbound has 50 deals through it would be classic founder ADHD — building the more interesting thing instead of finishing the working thing.

---

## The honest sequence

Here's how I'd actually think about it:

**Don't build outbound until inbound is closing deals.** Specifically: until you have 10 real deals through Dumont, you don't know what makes a conversation convert. Without that knowledge, your outbound personalization is guessing. You'd be optimizing the top of the funnel before you understand the bottom.

**The data platform work doesn't change.** Everything we discussed for the data platform — operators, aircraft, routes, events, ADS-B ingestion, entity resolution — happens regardless. The data layer for outbound is the same data layer for inbound. Just keep building.

**Start adding the outbound-specific entities only when ready.** When you do flip the switch, you'll need:
- A `prospects` entity (different from operators/aircraft) — companies and founders in your ICP
- A `signals` entity — funding events, hiring patterns, travel patterns from ADS-B
- A `touches` entity — outbound attempts across channels with full provenance
- A `conversations` entity — what the prospect said, where it went

But none of these get built until you've closed 10 inbound deals and know what works.

**The first version of "outbound" should be manual.** Before any automation, you (or eventually a Sales Rep hire) does this by hand for 30 days. You run a list of 50 post-raise founders, you research each one using the data platform, you reach out personally. You learn what works. *Then* you encode the patterns into Dumont.

This is the same logic as the Charter Index calibration path: ±20% at launch → ±5% at 500 deals. You don't ship the AI version of a process before you've manually proven the process converts.

---

## What "Vertical Dumont" actually looks like at v1

Assume you've done the manual phase, learned what converts, and you're ready to encode it. The minimum viable outbound system:

**Inputs (from the data platform):**
- New funding announcements (Crunchbase, PitchBook, or scraped) → identifies post-raise founders
- Founder location + company HQ + likely travel patterns
- Recent commercial flight indicators (LinkedIn check-ins, Twitter posts, ADS-B for any private flights they're already taking)
- Match against your ICP (Series A-C, $5M-$50M raised, founder-CEO, geography matches your hubs)

**The signal layer:**
- A `signals` table where each row is: "Company X, signal Y, observed Z time ago, confidence W"
- Examples: `raised_series_b_30d_ago`, `posted_about_business_travel_fatigue_7d_ago`, `team_size_grew_to_50_indicating_offsites`, `competitor_just_chartered_a_jet`
- Each signal has a decay function — fresh signals are more valuable than old ones

**The personalization engine:**
- For each prospect, Dumont generates a research brief: who they are, why now, what travel pattern likely matters, what specific route on what specific aircraft would save them what specific amount of time
- The brief is the basis for outreach, not the outreach itself
- A human (you, initially) reviews the brief and approves or rejects the prospect before any send

**The send layer:**
- Email first (lowest commitment, easiest to personalize at scale)
- LinkedIn DM as follow-up only if email gets opened but not replied
- Phone call only if both email and LinkedIn get engagement
- Each channel gated by the previous one's signals

**The intelligence loop:**
- Every send is tagged with the brief that produced it
- Every response (open, reply, meeting booked, not interested, hard no) feeds back into Dumont's understanding
- The data platform learns which signals predict which conversion patterns
- Over time, Dumont gets better at picking which 50 prospects this week are worth touching

---

## What this is NOT

**Not a generic AI SDR product you sell.** This is internal infrastructure for OSA. You're not competing with Roger. You're building the vertical version that only works because of OSA's specific data and ICP.

**Not a volume play.** 50 high-quality touches per month, each with a researched brief, beats 5,000 templated sends every time for your ICP.

**Not a replacement for founder-led brand.** This works *because* of the dark social, Loud Hawk, LinkedIn presence you're already building. The outbound lands warmer because the prospect has heard of OSA. Without the brand layer, this is just spam with better data.

**Not the next thing you build.** It's the thing you build after inbound has 10–50 deals through it and you understand what converts.

---

## The honest answer to "can we replicate this"

Yes, and better — but only if you're disciplined about *when*. Roger gets to be horizontal because they have no other product. You have a transaction product (charter brokerage) whose unit economics improve with every deal closed inbound. Your outbound system, built right, is more defensible than Roger because it sits on a data moat they can't replicate. Built wrong, it's a distraction that burns your channels and brand.

The work to do *now*:
1. Keep building the data platform — every entity we discussed is dual-use for inbound and outbound
2. Get inbound to 10 real deals through Dumont before you touch outbound
3. When you start, do it manually for 30 days before you automate

The work *not* to do now:
1. Don't build a `prospects` table or a signals layer yet
2. Don't buy any AI SDR tools to bridge the gap
3. Don't start outbound to validate inbound — that's the ADHD move

When you're ready to start, I'd want to think through the prospect entity and the signals layer with the same depth we just did for operators and aircraft. They're different beasts and they deserve their own design session.

For now: keep your head down on the data platform and inbound conversion. The outbound version of this will be more powerful in 6 months than it would be if you started today.

---

## Phelipe

What is data governance?

---

## Claude

Good question to be asking, especially given everything we've been discussing about your data platform.

## What data governance is

Data governance is the set of rules, processes, and accountability that control **how data is created, accessed, changed, and used** across an organization. It answers questions like:

- Who is allowed to read this data? Who can change it?
- Where did this data come from, and can we trust it?
- What happens when two sources disagree?
- How do we know it's still accurate?
- If something goes wrong, who is responsible?
- Can we prove to regulators (or customers, or investors) that we're handling data correctly?

Think of it as the operating manual for your data — the policies that turn a pile of databases into a system you can actually rely on.

## The five pillars, in plain terms

**1. Ownership.** Every dataset has a person or team responsible for it. The operator entity is owned by someone. The aircraft entity is owned by someone. When the data goes wrong, you know who fixes it.

**2. Quality.** Rules about what counts as valid data. Tail numbers must match FAA format. Operator names must resolve to a canonical entity. Charter Index estimates must carry confidence and sample size. Bad data gets caught at write time, not discovered three months later.

**3. Access control.** Who can read what, who can write what. Read-only by default. Production writes require approval. Schema changes require migrations. The data layer enforces this, not the application.

**4. Lineage and provenance.** For any data point, you can trace where it came from, when it arrived, what transformations happened to it, and what it produced downstream. Your event log is the start of this.

**5. Lifecycle.** What happens when data ages, gets corrected, gets deleted, or gets archived. Cold tier promotion. Quarantine handling. Retention policies.

## Why it matters

Without governance, every dataset eventually becomes a swamp. Three people add the same operator under three different names. A schema change breaks a downstream report nobody knew existed. An agent writes bad data into production and you can't trace which agent or when. A customer asks "where did this number come from" and nobody can answer.

The Carly Taylor post is selling Collibra's product — a heavyweight enterprise data governance platform that big companies use because they have hundreds of analysts, dozens of databases, and regulators breathing down their neck. The post correctly identifies that traditional governance is brittle (one team, manual rules, ignored when inconvenient), and pitches AI to automate it. That's mostly a Fortune 500 problem. Collibra costs hundreds of thousands of dollars a year. Not your problem yet.

## What governance looks like for OSA right now

You don't need Collibra. You don't need a data governance team. You need *governance discipline baked into the platform itself* — which is most of what we've been discussing without naming it.

Translating the five pillars to your scale:

**Ownership:** You own everything. When you hire a CTO, the CTO inherits ownership of the data platform. When you hire the Brand & Content Strategist, they inherit ownership of the content corpus. Document this in the repo READMEs.

**Quality:** This is the validation layer we discussed — Zod schemas on every write, business rule checks, anomaly detection, quarantine table for bad writes. Already on the roadmap.

**Access control:** Postgres row-level security with read/staging/production tiers. Already on the roadmap.

**Lineage and provenance:** The event log. Provenance fields on every entity (`source`, `confidence`, `last_verified`). Already on the roadmap.

**Lifecycle:** Memory tiering (hot/warm/cold), summarization jobs, soft-deletes never hard-deletes. Already on the roadmap.

## The frame to internalize

What Collibra sells to enterprises is the same discipline you'd build into your platform from day one — except they're retrofitting it onto sprawling, undisciplined data estates that grew up without governance. You have the rare opportunity to build governance *into the substrate* instead of bolting it on later.

Three rules that get you 80% there as a solo founder:

1. **Nothing writes without going through an event.** No raw SQL inserts to canonical tables. Every change is a logged event with source, timestamp, and confidence.

2. **Every entity row is self-describing.** Provenance, freshness, and confidence are required fields, not optional. An agent reading the row knows whether to trust it.

3. **Every production write is validated.** Schema check, business rule check, anomaly check. Failures go to quarantine, not production.

Build those three into the data platform, and you have governance without ever buying a governance product. When you eventually hire a CTO and they ask "what's our data governance posture?" — those three rules are your answer, and they're stronger than what most Series B companies have.

The post is a useful reminder that this matters. The product they're selling is not for you. The discipline they're describing absolutely is.

---

## Phelipe

Can you find this reasearch paper

---

## Claude

Let me find it.
```
This block is not supported on your current device yet.
```

Found it. Here's the actual paper, plus a couple of small corrections to the LinkedIn post.

## The paper

**Title:** Recursive Language Models  
**Authors:** Alex L. Zhang, Omar Khattab, et al. (MIT CSAIL)  
**arXiv:** [2512.24601](https://arxiv.org/abs/2512.24601) (December 31, 2025, v2 January 28, 2026)  
**Author's blog (excellent walkthrough):** [alexzhang13.github.io/blog/2025/rlm/](https://alexzhang13.github.io/blog/2025/rlm/)  
**Code:** [github.com/alexzhang13/rlm-minimal](https://github.com/alexzhang13/rlm-minimal)

## What it actually does

RLMs are a general inference paradigm that treats long prompts as part of an external environment and allows the LLM to programmatically examine, decompose, and recursively call itself over snippets of the prompt.

In plain terms: instead of stuffing a huge document into the model's context window, you put the document in a Python variable, and the model writes code to inspect, slice, and search it. When it finds relevant snippets, it makes recursive sub-calls to itself (or a cheaper model) on just those pieces.

The architecture typically involves two agents — a "root language model" like GPT-5 that orchestrates by writing code and managing data flow, and a faster cheaper "recursive language model" that processes the specific text snippets isolated by the code. Because the prompt resides in the environment's memory rather than the model's context window, the system can handle inputs far larger than the model's training limit.

## A few corrections to the LinkedIn post

The post is roughly right but loose on a few details:

**"58.00 vs. 0.04" benchmark numbers** — the post is mangling these. On BrowseComp-Plus the corpus ranges from about 6M to 11M tokens, which is 2 orders of magnitude beyond the 272k token context window of GPT-5. RLM with GPT-5 achieves around 91.33 accuracy with an average cost of 0.99 USD per query. Standard models scoring near 0% on the 10M-token benchmark is real; the specific "58 vs 0.04" framing isn't quite accurate.

**"No summarization, no deletion of nuance"** — partly true, partly oversold. The system avoids forced upfront summarization, but the recursive sub-calls absolutely *can* summarize subsections when that's the right strategy. The point is the model decides what to compress and when, not that nothing ever gets compressed.

**"Eliminates the need for RAG"** — overstated. RLMs are an alternative scaffold to RAG for long-context reasoning, not a replacement for retrieval over corpora that don't fit in any context. The paper compares against RAG-style baselines and beats them on these specific tasks; it doesn't make vector retrieval obsolete.

## Why this is interesting for OSA

This is directly relevant to the data platform conversation we just had. RLMs are essentially **the architectural pattern of the agent writing code to query its environment, rather than the environment being shoved into context.**

That's the same principle behind:
- The MCP tool surface you're building (agent calls `get_operator_profile` rather than receiving the whole operators table)
- Memory tiering (agent retrieves from cold tier on demand rather than loading all history)
- The "agents query SQL via tools" pattern over "agents read raw tables in context"

The RLM paper is a more aggressive version of the same idea — and it validates the architectural direction. By treating massive text inputs as an environment that models can program against, RLMs sidestep the fundamental scaling limits of monolithic context. That's the same bet you're making: don't try to load everything; build a queryable substrate the agent navigates.

The author's blog post is the best version of this — clearer than the paper, much clearer than the LinkedIn post. Worth 20 minutes if you want to see how the paradigm maps onto what you're building.

---

## Phelipe

Can you reasearxh how people are using agentic ai and frameworks in data

---

## Claude

Good question — this is the frontier worth understanding because it's directly upstream of how OSA's data platform should work. Let me actually research this.
```
This block is not supported on your current device yet.
```

Good signal. Let me get one more angle — the actual frameworks teams are using.
```
This block is not supported on your current device yet.
```

I have enough now. Let me synthesize this for OSA.

---

## How agentic AI is actually being used in data — the 2026 reality

There are three distinct waves happening simultaneously. Most coverage conflates them. Pulling them apart:

### Wave 1: Agentic data engineering (the pipelines themselves)

The shift everyone's announcing in 2026: **data pipelines are becoming agents instead of scripts.** Traditional pipelines follow fixed instructions; engineers define workflows, schedule jobs, fix failures manually. Agentic pipelines reason, plan, act, and learn without constant intervention.

The three flagship products: **Databricks Genie Code** (launched March 2026), **Snowflake Cortex Code**, and **Qlik Agentic Data Engineering**. Databricks reports Genie Code more than doubled the success rate of leading coding agents on real-world data science tasks (32.1% to 77.1%).

What these systems actually do:
- **Ingestion agents** — autonomously pull from APIs, files, streaming sources; handle schema drift; recover from failures
- **Transformation agents** — generate SQL, dbt models, feature engineering; optimize based on usage patterns
- **Quality agents** — detect anomalies, validate inputs, quarantine bad records
- **Governance agents** — enforce access controls, maintain lineage, ensure compliance
- **Orchestration agents** — coordinate the above, resolve conflicts when a quality agent flags something while a transformation agent is mid-execution

The pattern: a quality agent may flag an issue while a transformation agent is mid-execution. The orchestrator decides whether to pause, reroute, or continue processing based on impact and policy. This multi-agent architecture enables parallel execution, faster recovery, and higher system resilience.

### Wave 2: Active metadata as the new substrate

This is the most important shift and the most underdiscussed. "If data was the oil of the 2010s, metadata is the oil of the 2020s." Successful data engineers in 2026 understand that investing in metadata is not overhead — it's the core value proposition.

The concept: agents need *context about the data*, not just the data itself. A well-constructed knowledge graph can answer questions like "What data do we have about customer behavior?" not by simple keyword matching, but by understanding that customer behavior might be reflected in transaction tables, clickstream logs, support tickets, and survey responses — even if none of them explicitly mention "customer behavior."

The four context types they're calling out:

1. **Temporal context** — when was this created, when was it last updated, what was the state of the world at the time
2. **Relational context** — how does this data relate to other datasets, what joins are meaningful
3. **Quality context** — how reliable is this data, what are known issues or limitations
4. **Provenance context** — where did this come from, what transformations happened, who/what touched it

This maps almost exactly to what we discussed for OSA's data platform: provenance fields, freshness fields, confidence scores, the event log. The frontier of data engineering in 2026 is converging on the architecture you're already building, just with bigger company budgets behind it.

### Wave 3: Agents as database citizens

In Databricks's Lakebase service, AI agents now create roughly 4x more databases than human users. Agents are prolific creators of database environments — spinning up instances for experiments, branching for testing, and discarding them when done.

This is wild and has implications. Telemetry from Lakebase production environments shows that on average, each database project has ~10 branches and some databases with nested branches reaching depths of over 500 iterations. Database infrastructure is being redesigned for ephemeral, branch-heavy, agent-driven workflows. Postgres-compatible systems with O(1) branching are becoming the default substrate.

For OSA: when you eventually need staging environments for data platform work, this is the architecture pattern to adopt — branch the production database for the agent to test against, then merge or discard. Cheap, safe, fast.

---

## The framework landscape — what teams are actually using

Three frameworks dominate production. Picking one is a 4-month commitment. OpenAI Agents SDK treats agents as imperative handoff chains, LangGraph models them as explicit state machines over a graph, and CrewAI composes them as role-driven crews with declarative tasks. The mental model you adopt will outlive any single project. Migrating tool definitions, memory schemas, and observability plumbing between frameworks routinely consumes an engineer for a quarter.

**LangGraph** — graph-based, stateful, explicit control flow. For complex, branching workflows with conditional routing, retry logic, and human checkpoints, nothing comes close. Best observability via LangSmith. Steepest learning curve. LangGraph's MCP integration is the deepest because MCP tools become first-class graph nodes with full streaming support.

**CrewAI** — role-based, fastest prototyping. As of March 2026, CrewAI sits at 45,900+ GitHub stars and version 1.10.1, with native support for MCP (Model Context Protocol) and A2A (Agent-to-Agent) communication. It powers over 12 million daily agent executions in production. Teams that start with CrewAI for prototyping often migrate to LangGraph when they need production-grade state management and conditional routing.

**OpenAI Agents SDK** — imperative handoffs, smallest mental footprint, first-party tracing. The fastest path from zero to a working production agent if you're aligned with OpenAI models.

**Microsoft Agent Framework 1.0** (April 3, 2026) — unified Semantic Kernel + AutoGen, .NET + Python, native MCP and A2A.

**Dapr Agents** — different philosophy. While LangGraph and CrewAI focus on "how to make agents smarter," Dapr Agents focuses on "how to keep agents alive." A 2026 survey of MCP production environments found 52% of 2,181 endpoints were dead after deployment. That number is why Dapr Agents exists. Reliability-first, Kubernetes-native.

---

## The discipline patterns emerging

Across every credible source, the same patterns surface:

**1. Hierarchical orchestration wins for complex workflows.** Hierarchical orchestration (a supervisor delegating to specialized sub-agents) is the most common production pattern because you can trace decisions back through the chain. Single agents for simple tasks. Hierarchy for complex. Avoid flat multi-agent chaos.

**2. Memory is the substrate, not a feature.** Memory isn't a feature you add later. It's the substrate that makes everything else work. Every compounding error and context bleeding failure traces back to missing the right information at the right moment.

**3. Specification-driven development.** Vague or underspecified inputs often lead to inconsistent or unpredictable results. "If you don't fully describe what the intent is, you will have random results." Teams refusing PRs in favor of GitHub Issue-based workflows that feed structured specs into the agent.

**4. MCP is the standard tool protocol.** Every framework now supports it. It's becoming the USB-C of agent tool integration — one standard, any tool.

**5. Production failures trace to context, not models.** The underlying models got good enough to reason through complex problems, but reasoning without the right context is just expensive hallucination.

**6. Observability is non-negotiable.** Trace every decision. Audit every action. Reproduce every failure. Reasoning traces, auditable logs, and human-in-the-loop checkpoints are required for trust and compliance.

---

## What this means for OSA

You're not behind. You're on the right architecture and roughly on schedule with where the frontier is converging. A few specific takeaways:

**1. Your data platform direction is validated.** Active metadata, provenance fields, event log spine, knowledge graph relationships — that's exactly what Genie Code, Snowflake Cortex Code, and Qlik are now selling to enterprises. You're building it natively for OSA's vertical instead of retrofitting onto a sprawling enterprise estate. That's the right move.

**2. Don't adopt LangGraph/CrewAI yet.** Your Dumont architecture is already a hierarchical orchestrator (PIC pattern with capabilities). Adding LangGraph or CrewAI now would be solving a problem you don't have, and locking you into a framework whose abstractions might not fit your domain. Stay framework-light until you feel real pain. When you do adopt one, LangGraph is the bet for your reliability profile (regulated, high-stakes calls, audit trail required).

**3. MCP is your interop bet.** Already on it. The Dumont Intelligence MCP server you're moving to osa-data-platform is exactly the right move. Every framework supports MCP now, which means your tool surface stays portable across whatever agent host comes next.

**4. The metadata investment is the moat.** Aviation has nobody doing what Genie Code does for general data. The combination of (FAA registry + ADS-B activity + operator certificates + your own deal history + active metadata about how all of it relates) is what no horizontal tool can replicate. Lean into this.

**5. Observability is your next harness gap.** Generic observability is fine for Dumont. The data-specific signals — schema drift, validation pass/fail rates, charter index error per route, retrieval recall on labeled evals — those need to be visible. Dashboards over code is the right priority.

**6. Watch agent-driven database branching.** When you need staging environments, the Lakebase pattern (branch a production DB for agent experiments, merge or discard) is the modern way. You don't need it now. File the pattern for when scale forces you to think about it.

The frontier is moving fast, but most of the noise is enterprises catching up to what indie builders are already doing. You're in the second camp. Keep building.

---

## Phelipe

Yeah. So I'm trying to understand here the same way, uh, how people are using agents, like, how they are actually building the agents to develop data platforms or to do data modeling and data architecture, uh, with AI.

---

## Claude

Good — this is the layer below frameworks. Let me pull the actual patterns of *how* teams are structuring agents to do data work, not just "what framework do they pick."
[Used tool: web_search]
Agentic AI for Data Architecture: Patterns and Real Implementation | 2026: How teams are using agents to design schemas, model data relationships, and evolve data platforms autonomously.
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

Perfect. Now I have the real patterns. Let me synthesize this for you.

---

## How teams are actually building agents to design data platforms

There are three distinct architectural patterns emerging. Most people conflate them. Let me separate them:

### Pattern 1: The Role-Based Agent Swarm (Meta's Tribal Knowledge Model)

This is the most concrete example. Meta needed to document 4,100+ data pipeline files with tribal knowledge. They built **a swarm of 50+ specialized AI agents**, each with a narrow role:

**The agent roles:**
- **Explorers** — scan the codebase, identify file relationships, map dependencies
- **Analysts** — answer specific questions: "What does this module do?", "What are its failure modes?", "What patterns does it use?"
- **Writers** — synthesize the analysis into concise, legible documentation
- **Critics** — validate the output, check for contradictions, flag hallucinations
- **Fixers** — correct errors and auto-fix stale references

**The process:**
1. Each agent operates independently on a subset of files
2. Their outputs feed into a central knowledge aggregation layer
3. The system produces 59 concise context files encoding domain knowledge
4. This context becomes the navigation guide for future agents

**The result:** Structured context files for 100% of code modules (up from 5%), 40% fewer agent tool calls per task, documented 50+ non-obvious patterns.

**Key insight:** The swarm doesn't all run at once. They run in orchestrated phases. Explorers first, then analysts in parallel, then writers aggregate, then critics validate, then fixers clean up. Sequential phases, parallel execution within each phase.

This is how you'd build your data platform with agents. Not one agent designing the whole schema. A swarm of agents, each with a specific job.

---

### Pattern 2: The Semantic Ontology Layer (Google, Microsoft, IBM)

This is the **architectural layer that allows agents to reason about data, not just move it.**

The structure:
```
Application Layer (agents making decisions)
        ↓
Semantic/Ontology Layer (what things mean, how they relate)
        ↓
Data Platform Layer (the actual data)
```

The semantic layer codifies:
- **What entities exist** — Aircraft, Operators, Routes, Trips, Signals
- **What properties characterize them** — aircraft.n_number, operator.argus_rating, trip.origin_icao
- **What relationships connect them** — aircraft has an operator, operator flew a trip on a route
- **What rules govern them** — an aircraft can't be in two places at once, operator certificates expire

Two types of ontologies:

**Descriptive ontology** — defines business meaning ("what is a 'charter trip'?")
**Structural ontology** — binds that meaning to actual data ("charter trips are stored in this table with these columns")

For OSA, your data platform building would look like:

1. **Descriptive layer** (you're doing this now):
   - CLAUDE.md (how Dumont should think about aviation)
   - writing-guide.md (what good content looks like)
   - aircraft-scoring.md (what makes an aircraft relevant)

2. **Structural layer** (this is the gap):
   - An ontology file that says: "Aircraft entity has n_number, icao_hex, aircraft_class; Aircraft relates to Operator via 'operated_by'; Operator has argus_rating, base_airport"
   - The relationship schemas: which joins are meaningful, which produce nonsense
   - The constraint rules: what makes a valid aircraft record, what makes a valid operator

3. **Operational layer** (agents read both):
   - Agents reference both layers when making decisions
   - When an agent needs to understand "what's a charter-capable aircraft", it reads descriptive + looks up the structural mapping
   - When an agent needs to find related data, it follows the relationships defined in the ontology

---

### Pattern 3: The Multi-Agent Orchestration for Data Pipeline Work

This is how teams like Databricks, Snowflake, Qlik structure agents to **autonomously design and improve data pipelines.**

The agents by function:

**1. Ingestion Agent**
- Discovers data sources
- Maps schemas
- Handles schema drift
- Implements retry logic
- Writes ingestion specifications

**2. Quality Agent**
- Validates incoming data
- Detects anomalies
- Flags bad records to quarantine table
- Suggests quality improvements

**3. Transformation Agent**
- Generates SQL models
- Optimizes query performance
- Manages dependencies
- Tests transformations

**4. Governance Agent**
- Enforces access control
- Maintains lineage
- Ensures compliance
- Audits every change

**5. Orchestration Agent (supervisor)**
- Coordinates the above
- Resolves conflicts (quality agent says "stop", but transformation agent is mid-run)
- Decides: pause, reroute, or continue
- Manages scheduling and dependencies

**How they coordinate:**

They don't all talk to each other directly. They communicate through:
- **Shared event log** — every agent writes events when it does something
- **Shared config/state** — a central specification that all agents read and can propose changes to
- **Governance policies** — rules that prevent agents from taking risky actions
- **Human checkpoints** — for high-stakes decisions, agents pause and wait for approval

**Example flow:**

```
Ingestion Agent: "New column detected in source API"
  → writes event: "schema_drift_detected"
  → updates shared schema spec
  → Governance Agent reads event
  → checks policy: "column from new source, access restricted"
  → flags for human review
  → Transformation Agent waits (supervisor holds it)
  → Human approves
  → Transformation Agent resumes with updated schema
```

---

## How this maps to OSA's data platform work

If you were to build your data platform using agentic patterns, the architecture would be:

**Phase 1: Build the Ontology (you start here)**

Create a structured ontology file (YAML or JSON) that defines:

```
entities:
  aircraft:
    properties: [n_number, icao_hex, serial, manufacturer, model, aircraft_class, ...]
    owner_entity: true
  operator:
    properties: [canonical_id, legal_name, faa_cert, argus_rating, ...]
    relationships: [operates_aircraft, based_at_airport, ...]
  route:
    properties: [origin_icao, destination_icao, distance_nm, ...]
    derivable: true  # not ingested, computed from legs
  leg:
    properties: [icao_hex, origin_icao, destination_icao, departure_time, ...]
    immutable: true  # events never change

relationships:
  aircraft_to_operator:
    type: many_to_one
    temporal: true  # ownership changes over time
    resolution: operator_confidence
  operator_to_aircraft:
    type: one_to_many
    derive_from: aircraft_to_operator
  leg_to_aircraft:
    type: many_to_one
    requires: aircraft_class
    
constraints:
  aircraft:
    - n_number must be unique
    - n_number format: /^N[0-9]{1,5}[A-Z]{0,2}$/
    - aircraft_class must map to icao_type_code
  operator:
    - canonical_id must be globally unique
    - argus_rating is optional but when present in [gold, gold_plus, platinum]
  leg:
    - departure_time < arrival_time
    - flight_time_min > 0
```

**Phase 2: Specialized Agent Roles**

- **Aircraft Resolver Agent** — resolves tail numbers to canonical aircraft entities, owns the aircraft table
- **Operator Resolver Agent** — resolves operator names to canonical operator entities, owns the operators table
- **Route Intelligence Agent** — computes derived route statistics from completed legs
- **Validation Agent** — checks incoming data against the ontology constraints
- **Quality Agent** — detects anomalies, quarantines bad records
- **Lineage Agent** — tracks provenance, maintains event log
- **Governance Agent** — enforces access control, audit gates

**Phase 3: Orchestration Rules**

Define in code how agents coordinate:

```
when aircraft_resolver finishes:
  if confidence > 0.9:
    auto-update canonical_aircraft
  if confidence between 0.5-0.9:
    queue for operator_resolver to cross-check
  if confidence < 0.5:
    move to quarantine for human review

when operator_resolver finishes:
  if any aircraft_resolver conflicts exist:
    broadcast event to operator_resolver for re-evaluation

when validation_agent flags a record:
  if rule_type == "hard_constraint":
    quality_agent moves to quarantine
  if rule_type == "soft_constraint":
    flag for human review, log anomaly

when lineage_agent receives events:
  append to event_log
  trigger route_intelligence_agent recalibration if needed
```

**Phase 4: Self-Improving Loop**

The agents learn from mistakes:

```
weekly_evaluation:
  - run evals on resolver accuracy
  - compare aircraft_resolver v(n) vs v(n-1)
  - measure operator_resolver false positive rate
  - if accuracy dropping > 5%, trigger alert
  
monthly_calibration:
  - operator_resolver proposes threshold adjustments
  - aircraft_resolver proposes new matching rules
  - validation_agent proposes new constraint rules
  - all changes versioned, can be rolled back
```

---

## The key insight for OSA

The pattern that wins at scale is **role-based agent swarms with shared ontology, coordinated through events, mediated by a governance layer.**

Not: "build one mega-agent that designs your whole data platform"  
Yes: "build specialized agents for each entity (aircraft, operator, route), let them run in parallel, have them communicate through events, version the ontology they all read"

Meta's 50-agent swarm producing 59 context files is the same shape as:
- Aircraft resolver + operator resolver + route agent + 3 others
- Each one narrow, parallel, producing context the others consume
- A shared knowledge layer (the ontology) that evolves as agents improve

You already have the skeleton:
- Dumont is the supervisor agent (PIC pattern)
- Your data platform tables are the shared state
- Your skills (CLAUDE.md, writing-guide.md, aircraft-scoring.md) are proto-ontology
- Your event log is the coordination mechanism

The work is formalizing the ontology, breaking the data platform work into agent-shaped roles, and building the orchestration rules so they can improve autonomously.

Want to drill into any specific piece of this?

---

## Phelipe

Hey. Back.

---

## Claude

Hey. Good to have you back. Where were we headed with this? I was deep in the actual patterns of how teams are building agents to design data platforms — the swarm approach Meta used, the semantic layer architecture, the agent roles.

Want me to pick up there, or were you thinking about something else for OSA?

---

## Phelipe

No. Yeah. I was just thinking about how, uh, we can start this. Like, I don't wanna get very complex. Uh, I just wanna understand that what kind of agents they're fielding and, uh, how could we build something for us and, uh, what would be the capabilities of it. And then, uh, what would be the objective of building a data agent.

---

## Claude

Perfect. Let me give you the clean, simple version — what agents to actually build for your data platform, what they do, and why it matters for OSA.

## The three agents you actually need (not 50)

Start with these three. They're enough to handle your data platform at the scale you're at (and beyond):

**1. The Resolver Agent**
**What it does:** Takes messy, overlapping data from multiple sources and figures out what's the same thing.

**Example:** You ingest FAA registry, ADS-B data, and operator websites. All three mention "Priester Aviation." The resolver agent figures out they're the same canonical entity, merges them, and updates your operators table.

**Capabilities:**
- Fuzzy string matching (is "Priester Aviation LLC" the same as "Priester Aviation"?)
- Rule-based matching (tail number N123AB always maps to one operator)
- Confidence scoring (am I 99% sure or 60% sure this is a merge?)
- Conflict detection (two sources claim different info about the same operator)

**Why it matters:** Without this, your data stays fragmented. With it, every new ingestion automatically gets cleaner.

---

**2. The Validator Agent**
**What it does:** Catches bad data before it lands in production. Acts as a gatekeeper.

**Example:** An ingestion job produces a charter price estimate of $500/hour for a heavy jet (absurdly low). The validator flags it, sends it to quarantine, and logs why.

**Capabilities:**
- Schema validation (does this data match the shape we expect?)
- Business rule checks (charter prices can't be negative, can't be 10x the Charter Index estimate)
- Anomaly detection (is this value 3 standard deviations from normal?)
- Provenance checking (where did this come from, do we trust this source?)

**Why it matters:** One bad data point can corrupt your Charter Index calibration for months. This agent prevents that.

---

**3. The Orchestrator Agent**
**What it does:** Decides what should run, when, in what order, and what to do if things break.

**Example:** New ADS-B data arrives. The orchestrator triggers: ingest → leg detection → resolver → validator → route intelligence recalculation. If the validator quarantines bad data, the orchestrator pauses route recalculation until a human approves.

**Capabilities:**
- Scheduling (run the FAA registry refresh monthly, ADS-B ingestion daily, resolver nightly)
- Dependency management (don't calculate routes until legs are ingested and validated)
- Error handling (if resolver fails, quarantine the data and alert; don't proceed to validator)
- State tracking (which data has been processed, what's pending, what failed and why)

**Why it matters:** Without this, you're manually triggering jobs and deciding what to do when something breaks. With it, the system runs itself.

---

## What each agent actually looks like (the minimal version)

**Resolver Agent:**
```
Input: Operator name variants, operator metadata
Output: Canonical operator ID, confidence score, decision trace
Tools it uses:
  - fuzzy_string_match(string1, string2) → similarity score
  - lookup_by_faa_cert(cert_number) → canonical ID
  - search_operator_database(name) → existing matches
  - merge_operator_records(from_id, to_id) → executes merge + logs event
```

**Validator Agent:**
```
Input: Data row (could be an aircraft, operator, leg, etc.)
Output: PASS / QUARANTINE + reason
Tools it uses:
  - validate_against_schema(data, schema) → type errors
  - check_business_rules(data, rules) → "price > 0", "charter_class in [light, midsize, ...]"
  - detect_anomalies(value, historical_distribution) → z-score
  - log_to_quarantine(data, reason) → writes to quarantine table
```

**Orchestrator Agent:**
```
Input: Schedule trigger (daily, nightly, on-demand), pipeline definition
Output: Execution plan, status updates, error handling decisions
Tools it uses:
  - trigger_agent(agent_name, inputs) → runs resolver, validator, etc.
  - check_dependencies(job_name) → are prerequisites complete?
  - log_to_event_log(event_type, entity_id, payload) → audit trail
  - send_alert(severity, message) → notify humans on failure
```

---

## The objective: Why build these agents at all

**Short answer:** Your data platform becomes self-maintaining instead of you maintaining it manually.

**Longer answer:**

**Without agents:**
- You ingest FAA data → manually check for duplicates
- You get ADS-B data → manually run the leg detector, fix failures
- You detect bad data → manually write SQL to quarantine it
- Something breaks at 2 AM → you get paged

**With these three agents:**
- Ingestion happens → resolver automatically deduplicates → validator catches garbage → orchestrator logs everything
- Your data stays clean, consistent, and auditable
- You spend time on *strategy* (Charter Index methodology, new data sources) instead of *plumbing* (fixing broken queries)

**For OSA specifically:**
1. **You're solo right now.** These agents do the work a team would do.
2. **You're building a public benchmark (Charter Index).** Bad data breaks it. Validators prevent that.
3. **You'll eventually hire.** The CTO inherits a self-maintaining data platform instead of a mess.

---

## How to build them (the realistic sequence)

**Week 1: Build the Validator Agent**
This is the easiest and most valuable. It's just Zod schemas + business rules + a quarantine table.

```typescript
// validator-agent.ts
async function validateCharteredLeg(leg: any) {
  // Schema check
  const schema = z.object({
    origin_icao: z.string().length(4),
    destination_icao: z.string().length(4),
    aircraft_class: z.enum(['light', 'midsize', 'super_mid', 'heavy']),
    flight_time_min: z.number().positive(),
    departure_time: z.string().datetime(),
  });

  try {
    schema.parse(leg);
  } catch (error) {
    return quarantine(leg, `Schema validation failed: ${error.message}`);
  }

  // Business rule checks
  if (leg.flight_time_min > 14 * 60) {
    return quarantine(leg, 'Flight time exceeds 14 hours (likely data error)');
  }

  // Anomaly check
  const historicalMean = await getHistoricalFlightTime(leg.origin_icao, leg.destination_icao);
  const zscore = Math.abs((leg.flight_time_min - historicalMean) / historicalStdDev);
  if (zscore > 3) {
    return quarantine(leg, `Flight time is ${zscore.toFixed(1)} std devs from mean (anomaly)`);
  }

  return { status: 'PASS', confidence: 0.95 };
}
```

**Week 2: Build the Orchestrator Agent**
Wire up the scheduling and dependency logic.

```typescript
// orchestrator-agent.ts
async function dailyPipeline() {
  const orchestrationLog = [];

  // Step 1: Ingest ADS-B
  orchestrationLog.push(await runIngestion('adsb-lol', 'daily'));

  // Step 2: Run Resolver (depends on ingestion completing)
  orchestrationLog.push(await runResolver({
    sourceTable: 'adsb_completed_legs',
    targetTable: 'legs_resolved',
  }));

  // Step 3: Run Validator (depends on resolver)
  orchestrationLog.push(await runValidator({
    sourceTable: 'legs_resolved',
    validateAgainst: 'chartered_leg_schema',
  }));

  // Step 4: Update route intelligence (depends on validator)
  const validationStatus = orchestrationLog[2];
  if (validationStatus.pass_rate > 0.95) {
    orchestrationLog.push(await recalculateRouteIntelligence());
  } else {
    orchestrationLog.push({
      status: 'SKIPPED',
      reason: `Low validation pass rate: ${validationStatus.pass_rate}`,
    });
  }

  // Log the entire run
  await logPipelineRun('daily-pipeline', orchestrationLog);
}

// Triggered by cron or Temporal
schedule('0 2 * * *', dailyPipeline); // 2 AM every day
```

**Week 3: Build the Resolver Agent**
The trickiest, but now you have the other two working.

```typescript
// resolver-agent.ts
async function resolveOperators() {
  const unresolved = await db.query(`
    SELECT * FROM operators WHERE canonical_id IS NULL
  `);

  for (const operator of unresolved) {
    // Try deterministic match first
    const match = await fuzzyMatchOperator(operator.name, operator.faa_cert);
    
    if (match.confidence > 0.95) {
      await mergeOperators(operator.id, match.canonical_id);
      logEvent('operator_resolved', {
        from_id: operator.id,
        to_id: match.canonical_id,
        method: 'fuzzy_match',
        confidence: match.confidence,
      });
    } else if (match.confidence > 0.7) {
      // Medium confidence: flag for human review
      await quarantine(operator, `Possible merge with ${match.name} (confidence: ${match.confidence})`);
    } else {
      // No match: create new canonical ID
      const newCanonicalId = `op_${slugify(operator.name)}`;
      await updateOperator(operator.id, { canonical_id: newCanonicalId });
      logEvent('operator_created', { canonical_id: newCanonicalId });
    }
  }
}
```

---

## The honest truth about these agents

**They're not magic.** They're:
- Deterministic validators (run the same way every time)
- Orchestrators with decision logic (if A passes, run B; if A fails, pause)
- Resolvers with confidence scoring (make the best guess, log it, let humans override)

**They're not autonomous in the sci-fi sense.** They follow rules you define. When they can't decide (resolver confidence is 0.7), they escalate to humans.

**They're valuable because they:**
1. Run 24/7 without you
2. Leave an audit trail of every decision
3. Scale to handle 10x more data without 10x more work

---

## What would you build first for OSA?

My recommendation: **Start with the Validator Agent.**

Why? Because:
1. It's the smallest to build (pure schema + rules, no fuzzy matching)
2. It prevents the most damage (one bad Charter Index data point breaks the product)
3. It teaches you the pattern before you build the other two
4. You can deploy it this week and run it against your current data

Then the Orchestrator (scheduling + dependency logic), then the Resolver (the complex one).

Does that frame make sense? Or do you want to dig into a specific agent first?

---

## Phelipe

No. Before we keep going.

---

## Claude

Good call. Let me find the actual practitioners doing this at the frontier.
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

Perfect. Now I have the frontier picture. Let me show you what's actually happening.

---

## The frontier of agentic AI for data modeling — what's actually being built

Three distinct approaches are converging. Here's what the builders are doing:

### 1. **The DeepLearning.AI Pattern: Multi-Agent Knowledge Graph Construction**

The most structured approach. Deployed by teams building knowledge graphs autonomously. The architecture:

**Three specialized agents collaborate:**
- **Intent Agent** — talks to the user, clarifies what the knowledge graph should model, saves the goal to shared state
- **File Suggestion Agent** — identifies relevant data files based on the goal
- **Schema Agent** — examines the files, infers the entity types, relationships, properties needed

**The workflow:**
```
User intent (conversational)
    ↓
Shared State (the goal, saved formally)
    ↓
Parallel agents read the goal
    ↓
File suggestions + schema inference
    ↓
Knowledge graph structure emerges
    ↓
Validation + human review
```

**What matters:** The shared state is the contract. Each agent reads from it, works on its piece, writes back. No hallucination about what the other agents are doing because the goal is explicit.

---

### 2. **The Senzing Approach: Real-Time Autonomous Entity Resolution**

This is the most battle-tested pattern for your specific problem — matching entities across noisy, overlapping data sources.

**What they've locked:**
- **Real-time entity resolution** — not batch. When a record arrives, resolve it immediately to the canonical entity or create a new one
- **Relationship awareness** — entities don't exist in isolation. "Operator X manages Aircraft Y which operates from Airport Z" — the relationships matter as much as the entities
- **Autonomous learning** — the resolver gets better as it sees more data. Patterns get learned, confidence improves
- **On-prem execution** — no data leaves your infrastructure

**Senzing's specific innovation:** They've productized the pattern so agents can call it as a tool. An agent seeing "Priester Aviation LLC" and "Priester Aviation" no longer has to decide if they're the same operator — it calls the resolver, gets back a confidence-scored answer, and decides what to do based on that confidence.

For OSA specifically: this is how you'd handle the operator entity problem. The resolver becomes a tool Dumont calls.

---

### 3. **The Graphiti Approach: Temporal Context Graphs for Agent Memory**

Cutting-edge but conceptually simple. Built by Zep for production agent systems.

**The problem they solve:** LLM agents forget everything after a conversation ends. Context graphs give them persistent memory.

**How it works:**
- **Raw episodes** (the ground truth) — actual interactions, transactions, events
- **Extracted facts** — "Operator X responded to RFQ in 2.3 hours" (extracted from the episode)
- **Temporal validity windows** — facts have a "became true at" and "became false at" timestamp
- **Entity evolution** — operators evolve. Their status changes. Fleet changes. The graph tracks all of it with full history.

**Why it matters for OSA:** Dumont needs to remember: "We quoted operator X a month ago and they took 2 weeks to respond." That fact should persist across conversations, get richer as more data arrives, and inform future decisions about that operator.

---

### 4. **The dbt + Semantic Layer + Agent Skills Pattern**

The most pragmatic for analytics-heavy data work.

**The stack:**
- **dbt models** — your canonical transformations, version controlled
- **dbt Semantic Layer** — metrics and dimensions defined once, reused everywhere
- **Agent skills** — `.claude/skills/` files that teach agents how to use the semantic layer
- **MCP tools** — dbt Semantic Layer exposed as MCP tools so agents query it natively

**What the blog posts are saying:**
- Pre-compute as much as possible in the semantic layer (every metric you define eliminates a dozen agent queries)
- Document business context obsessively (agents use descriptions to pick the right metrics)
- Add agent rules (how to filter dates, handle nulls, disambiguate)

**The key finding from dbt blog 2026:** Agents querying a **modeled semantic layer** are 3-5x more accurate than agents querying raw tables. The semantic layer is the context engineering win.

---

### 5. **The GitHub Copilot Agentic Workflows Pattern: Spec-First Data Modeling**

The newest approach. GitHub just launched Agentic Workflows in technical preview.

**The philosophy:** Don't prompt agents to "build a semantic model." Give them:
- A specification file (`.semantic-model-implementation-guidance.md`)
- Business context (what questions do we want to answer?)
- Technical constraints (naming conventions, surrogate key handling, etc.)
- An example (what does a correct output look like?)

**The agent then:**
1. Reads the spec
2. Analyzes the raw data
3. Generates a semantic model conforming to the spec
4. Validates it against the constraints
5. Writes it back

**What's novel:** The spec is the context, not the prompt. Agent behavior becomes deterministic because you're encoding intent structurally, not prompting for it conversationally.

---

## The common thread across all five approaches

Every frontier team is doing the same thing in different domains:

1. **Explicit shared state** — agents don't hallucinate contracts; goals/specs/state are written down
2. **Entity-centric thinking** — data is modeled as entities + relationships, not tables + columns
3. **Temporal awareness** — facts have timestamps; systems remember when things changed
4. **Real-time autonomy** — no batch-at-midnight; decisions happen as data arrives
5. **Human-in-the-loop checkpoints** — agents propose; humans validate before commitment
6. **Semantic richness** — meaning (ontology) is as important as structure (schema)

---

## What this means for building agents to design OSA's data platform

You're not 50-agent swarm territory (yet). You're three to five agent territory. Here's what I'd recommend researching:

1. **Read the DeepLearning.AI agentic knowledge graph course** — their pattern of shared state + specialized agents is exactly what you need for designing your aircraft/operator/route schema

2. **Look at Senzing's agentic entity resolution pattern** — specifically how they've productized the "resolve this entity with confidence scoring" operation as a callable tool

3. **Study the dbt semantic layer + agent skills approach** — your route pages, your Charter Index, your Dumont reasoning all benefit from pre-computed metrics and semantic definitions

4. **Try the GitHub spec-driven pattern** — instead of "Claude, build my data schema," write `.data-platform-implementation-guidance.md` with exact specs, let the agent follow them deterministically

5. **Understand Graphiti's temporal context graphs** — for Dumont's memory across calls, for tracking how operator scores and aircraft status evolve

Do you want me to go deep on how to structure the first agent for your data platform, or are you still in the research phase?

---

## Phelipe

Hello. Can I have an American script, light blue, please?

---

## Claude

I'm not sure what you mean by "American script, light blue" — are you asking me to:

1. Write something in a particular style or format?
2. Help with a script for a project?
3. Something else entirely?

Or did you mean to send this message to someone else? Happy to help if you clarify what you're looking

---

## Phelipe

Give me one sec.

---

## Claude

No problem. Take your

---

## Phelipe

You have a lighter? Yes.

---

## Claude

I think you might be talking to someone else or there's been a mix-up — I'm Claude, an AI assistant. I don't have a lighter or physical objects.

Were you meaning to send a message to someone else, or did you want to get back to the data platform conversation we were

---

## Phelipe

Alright. Your total is twenty one twenty.

---

## Claude

Haha, I think you've got me confused with a barista or cashier! I'm Claude, an AI — no coffee shop here.

But hey, we were in the middle of something pretty interesting. We were talking about how teams are actually building agentic AI systems for data modeling and data platforms. I'd just pulled research on:

1. **DeepLearning.AI's multi-agent knowledge graph construction** — intent agent, file suggestion agent, schema agent collaborating
2. **Senzing's real-time autonomous entity resolution** — the pattern for matching operators/aircraft across noisy data
3. **Graphiti's temporal context graphs** — persistent memory for agents

Want to jump back in? Or did you want to step away and come back to this

---

## Phelipe

So -- Right. -- I'm gonna sit down. Alright. Have a good day. Thank you.

---

## Phelipe

Let me see. Like, can you do a research, Githubs, blogs, newsletter? Try to find the people they are doing the most advanced and sophisticated ways of building agentic AI for data modeling.

---

## Claude

You too! Have a great day. Thanks for the chat.

---

## Phelipe

Sorry let's evaluate again the best agents for data modeling

---

## Claude

No worries. Let me cut through the noise and give you the actual best patterns for **data modeling specifically** — not general data platform work, just the modeling layer.

## What "data modeling" actually means

Before picking agents, let me make sure we're aligned. Data modeling has three distinct sub-problems:

1. **Schema design** — what tables/entities exist, what columns, what types, what relationships
2. **Entity resolution** — when two records refer to the same real-world thing, merge them
3. **Semantic modeling** — what these entities *mean* in business terms (a "trip" vs a "leg" vs a "deal")

Different agents solve different problems. Mixing them is a common mistake.

---

## The four agents worth your attention

### 1. **Schema Design Agent** (the architect)

**Job:** Look at raw data + business intent, propose the canonical schema.

**Best implementation pattern:** DeepLearning.AI's three-agent workflow
- Intent agent (clarifies the goal)
- File/source agent (identifies relevant data)
- Schema agent (proposes structure)

**For OSA:** This is what designs your `aircraft`, `operators`, `routes`, `legs` tables. Reads FAA registry samples, ADS-B samples, your business needs, and proposes the entity model.

**Key capability:** Must read raw data samples, not just descriptions. Agents that design schemas from documentation alone consistently produce wrong models. Show them 100 actual rows.

---

### 2. **Entity Resolution Agent** (the matcher)

**Job:** Decide when "Priester Aviation LLC" and "Priester Aviation" are the same operator.

**Best implementation pattern:** Senzing's agentic entity resolution
- Real-time, not batch
- Confidence-scored decisions
- Relationship-aware (if two operators share aircraft, they're more likely the same)
- Productized as a callable tool

**For OSA:** This is the highest-leverage agent for your specific data problem. Aviation has deeply messy entity overlap (legal entity vs DBA vs trust vs management company).

**Key capability:** Must return confidence scores, not binary yes/no. Auto-merge above 0.95, queue for human review at 0.7-0.95, create new canonical entity below 0.7.

---

### 3. **Semantic Modeling Agent** (the meaning-keeper)

**Job:** Define what business concepts mean in terms of data. "What is a charter trip?" → "A leg from a charter-class aircraft (light/midsize/super_mid/heavy) operated under Part 135 with a non-empty origin and destination, where flight_time > 30 min."

**Best implementation pattern:** dbt Semantic Layer + agent skills
- Metrics and dimensions defined once in YAML
- Agents query the semantic layer, not raw tables
- 3-5x accuracy improvement over text-to-SQL on raw schemas

**For OSA:** This is what Dumont actually queries when answering "how many charter flights ran KTEB→KMIA last quarter." The agent doesn't write SQL against `legs`; it asks the semantic layer for the `charter_flights` metric filtered by route.

**Key capability:** Must be human-readable. Engineers, the agent, and eventually a CTO all read the same YAML.

---

### 4. **Schema Evolution Agent** (the watchdog)

**Job:** Watch the warehouse, detect drift, propose updates to the canonical model.

**Best implementation pattern:** Aboyalejandro's agentic-data-modeling on GitHub (Claude Code skills + OpenMetadata + PostgreSQL MCP)
- Three skills: impact analysis, mart audit, glossary management
- Detects when source schemas change
- Traces lineage to identify what breaks downstream
- Proposes fixes

**For OSA:** When FAA changes the registry format or adsb.lol changes their API, this agent catches it before it silently corrupts your data. Critical for your ingestion discipline.

**Key capability:** Lineage awareness. Must know that a column rename in `aircraft_raw` breaks `route_intelligence_calculation` downstream.

---

## Which one to build first for OSA

**Honest answer: Entity Resolution Agent.**

Why:
1. **It's your hardest data problem.** Operators have messy overlapping representations across FAA, ADS-B, websites, your own deal history. Aircraft trust ownership obscures real operators. Without resolution, your data is 30% duplicated.

2. **It's a proven pattern.** Senzing has productized this. You don't need to invent the architecture — you implement a known one.

3. **It compounds value.** Every other agent (semantic modeling, route intelligence, Dumont's outbound research) gets dramatically better when entities are clean.

4. **It's incrementally deployable.** Start with operators only. Validate. Add aircraft. Add routes. Each addition is contained.

The schema design agent is sexier. The semantic modeling agent feels more strategic. But the entity resolution agent is what actually unlocks the rest.

---

## What it would look like for OSA

```
Operator Resolution Agent
├── Inputs:
│   ├── New operator records from FAA, ADS-B, websites, deals
│   └── Existing canonical operators table
├── Tools:
│   ├── fuzzy_match_name(name1, name2) → similarity 0-1
│   ├── lookup_faa_cert(cert_number) → canonical_id or null
│   ├── check_shared_aircraft(op1, op2) → list of shared tails
│   ├── check_shared_address(op1, op2) → bool
│   └── propose_merge(from_id, to_id, confidence, reasons) → human queue or auto
├── Decision logic:
│   ├── If FAA cert match → confidence 1.0, auto-merge
│   ├── If name fuzzy + shared aircraft + shared address → confidence > 0.95, auto-merge
│   ├── If name fuzzy + one signal → confidence 0.7-0.9, human review
│   └── Else → new canonical entity, low confidence flagged
├── Outputs:
│   ├── Merged canonical operators table
│   ├── Event log of every decision (provenance)
│   └── Human review queue for ambiguous cases
└── Self-improvement:
    ├── Weekly eval: % of human-reviewed cases that resolved as agent predicted
    └── Monthly: tune confidence thresholds based on eval outcomes
```

---

## The honest sequencing

1. **Build Operator Resolution Agent first** (1-2 weeks)
2. **Add Aircraft Resolution Agent** (similar pattern, simpler — tail numbers are unique) (1 week)
3. **Add Schema Evolution Agent** (lighter weight, watches for drift) (3-5 days)
4. **Add Semantic Modeling Agent later** (after you have clean entities to model on top of)

Don't start with semantic modeling. Don't start with schema design. Start with the dirty work of entity resolution. That's where your data actually breaks.

Want me to detail the actual implementation plan for the operator resolver? Or compare specific tools like Senzing vs build-from-scratch?

---

## Phelipe

So look at our past chats. Especially the one from where we talk about building data platform architecture. Where we worked on or data platform yesterday. We're talking about getting closer to 97% on our operator entity resolution. And then, building or aircraft data resolution, How can we implement agents that could make this autonomous? Like, I'm thinking also, like, can we create an agent that is almost like a auto researcher on our datasets to organize or entity resolutions. For the operator side. That we started with the op spec. And for the aircraft side as well to track who is the ownership and then start making a fleet utilization or even a tail number utilization and start getting indicators on where to act We'll start getting data on what is their aircraft most used, most flown, stuff like that.

---

## Claude

Let me pull what was actually built so I can give you a grounded answer, not hypothetical.
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

Now I have enough grounding. Let me give you the actual answer based on what's already built and what makes sense to add.

---

## What you actually have right now

You're not starting from zero on this. Pulling from yesterday's session and the AERP work:

- Three-layer ER architecture running (matcher + LLM + validator)
- 73,088 ADS-B-tracked aircraft, 314,809 in registry, 4,968 charter-class identified
- Hidden-mode eval at 100%, citation validator working
- Firecrawl pulling operator websites, catching upstream bugs autonomously
- Two-Source Rule formalized as code-enforced constraint
- AERP v1 spec drafted (operator ER + aircraft ER + ADS-B linking as one living graph)
- Realistic ceiling locked: 97% operator ER, 95% aircraft ER

The architecture is sound. The question now isn't "should we build agents" — it's **"which autonomous agents extend what we have, and what do they do?"**

---

## The autonomous research agent you described

You called it: **"an auto researcher on our datasets to organize entity resolutions."** That's the right instinct. Here's what it actually is.

### Agent 1: The Operator Researcher

**Job:** For every operator in the queue (new, updated, low-confidence, or stale), autonomously gather + cross-reference + propose canonical state.

**Architecture:**
```
Trigger:
  - New operator detected in FAA OPSS daily diff
  - Existing operator with confidence < 0.85
  - Existing operator not re-corroborated in 90+ days
  - Manual flag from human reviewer

Workflow:
  1. PULL canonical state (what we currently believe)
  2. PULL all source records (FAA cert, ARGUS, Wyvern, website, news)
  3. SCAN for change signals (cert update, address change, fleet change)
  4. RESEARCH gaps — call Firecrawl on website, call Perplexity for news, 
     call Sayari/OpenCorporates for corporate structure
  5. PROPOSE update with full evidence chain + confidence + Two-Source verdict
  6. ROUTE: auto-merge if ≥0.95, human queue if 0.7–0.95, reject if <0.7
  7. LOG decision to er_decisions with prompt version + sources + reasoning

Output:
  - Updated canonical operator record (or pending_claim if single-source)
  - Daily brief: "5 new operators, 2 cert changes, 1 acquisition rumor needs review"
```

**Capability set:**
- FAA OPSS / Aircraft Registry / Airmen lookups (deterministic)
- ARGUS / Wyvern / IS-BAO membership checks (deterministic)
- Firecrawl on operator website + about page + fleet page
- Perplexity for trade press / news / acquisition rumors
- Sayari / OpenCorporates for corporate structure resolution
- LLM reasoning layer to synthesize + apply Two-Source Rule
- ER-Evaluation library to score every decision

**This is what you already have, formalized as an autonomous loop.**

---

### Agent 2: The Aircraft Researcher

**Job:** For every tail in the queue, resolve current ownership, current operator, current status, and feed utilization back into the graph.

This is the new one. Pulls from yesterday's work but adds the temporal ownership and utilization layer you just described.

**Architecture:**
```
Trigger:
  - New tail detected in FAA registry diff
  - FAA registry shows ownership change for existing tail
  - ADS-B detects tail going silent for 30+ days
  - ADS-B detects tail reappearing under new operating pattern
  - Existing tail with ownership confidence < 0.85

Workflow:
  1. PULL canonical state for tail
  2. PULL FAA registry record (registered owner, address, type cert)
  3. CROSS-REFERENCE Mode-S hex code + serial number (defeats N-number reuse)
  4. CHECK trust registrations (Bank of Utah, Wells Fargo Trustee patterns)
  5. CHECK shared aircraft signal — does this tail share base airport, 
     pilot patterns, or maintenance facility with a known operator's fleet?
  6. PULL ADS-B utilization (last 30/90/365 days legs, hours flown, 
     home base inferred, route patterns)
  7. INFER operating relationship via:
       - FAA Part 135 cert listing (deterministic, highest confidence)
       - Aircraft management contract from website (high confidence)
       - Behavioral match (fleet patterns) (medium confidence)
       - Pilot-to-operator linkage via Airmen DB (supporting evidence)
  8. PROPOSE canonical update with operator-of-record + confidence
  9. WRITE event to aircraft_operator_history (temporal record, never overwrite)
  10. LOG decision with full provenance

Output:
  - Updated canonical aircraft record
  - Temporal aircraft_operator_history event
  - Utilization snapshot (legs, hours, home base, route mix)
  - Status inference (active / idle / maintenance / repositioned / sold)
```

**The unique unlock:** *temporal* ownership. Most ER systems overwrite "current owner." Yours appends to history. Six months from now, you can answer: "Who operated N143QS in March 2026 vs September 2026?" That's data nobody else has.

---

### Agent 3: The Fleet Intelligence Agent

**Job:** Aggregate aircraft-level utilization into operator-level fleet intelligence. This is where your "indicators on where to act" lives.

```
Inputs: 
  - All aircraft records with operator-of-record assignments
  - All ADS-B legs from last 30/90/365 days
  - Operator certificate status (active, suspended, surrendered)

Computations (per operator):
  - Fleet size: total tails currently operated
  - Active fleet: tails with ADS-B activity in last 30 days
  - Dormant fleet: tails silent for 30+ days
  - Utilization: hours/month per tail, fleet average, distribution
  - Most-flown tails (busy aircraft = working operators)
  - Least-flown tails (idle aircraft = potential ghost positions or maintenance)
  - Route concentration: % of legs in operator's top 5 routes
  - Geographic spread: number of unique airports served in last 90 days
  - Class mix: light/midsize/super-mid/heavy distribution
  - Trend signals: utilization trend (growing, stable, declining)
  - Anomalies: sudden fleet additions or losses, big route shifts

Operator-level outputs:
  - operator_health_score (composite of utilization, certificate status, 
    fleet stability, ADS-B presence)
  - fleet_utilization_rate (industry-relative)
  - growth_signal (fleet growing, shrinking, churning)
  - distress_signal (utilization dropping, tails going silent, 
    cert at risk)
  - opportunity_signal (active fleet, available capacity, geographic match)

Tail-level outputs:
  - utilization_index (this tail vs class average)
  - status_inference (active, idle, maintenance, sold, repositioned)
  - ghost_probability (idle at airport away from home base)
  - last_seen / last_route / last_operator
```

**This is the intelligence layer Dumont uses.** When you're brokering a deal:
- "Find me an active super-mid in the Northeast" → Fleet Intelligence Agent returns ranked list with utilization, geographic match, operator health
- "Is N143QS available next week?" → status_inference + utilization pattern + recent route patterns
- "Which operators are growing?" → growth_signal sorted, with evidence chain

You're not querying a static database. You're querying a living model of fleet activity.

---

### Agent 4: The Drift Detector

**Job:** Watch the canonical graph itself for problems. The watchdog.

```
Continuous checks:
  - Two-Source Rule violations (any pending_claim older than 30 days)
  - Canonical confidence decay (record not re-corroborated in 90+ days)
  - Source disagreement (FAA says X, ARGUS says Y, both fresh)
  - Schema drift in upstream sources (FAA OPSS field changes, 
    ARGUS API changes)
  - ER decisions per prompt version (if v3 prompt resolves more 
    cases than v2 but with lower precision on validation set, alert)
  - Graph anomalies (operator with 0 tails, tail with 0 history, 
    aircraft with two simultaneous operators)
  - Stale ground truth (operator hasn't been re-checked in 90 days 
    + has signals of change)

Outputs:
  - Daily drift report
  - Items added to research queue for Agents 1-3
  - Alerts on validation set degradation
  - Source health monitoring
```

This agent is what makes the system *self-healing*. Without it, your 97% accuracy degrades to 90% over a year as the world changes. With it, you maintain steady-state freshness.

---

## How they coordinate (the orchestration layer)

The four agents don't all run at once. They run in a defined cadence:

```
Daily (2 AM):
  - Drift Detector scans canonical graph, populates research queue
  - Operator Researcher works the queue (priority: new + flagged)
  - Aircraft Researcher works the queue (priority: ownership changes)

Weekly:
  - Fleet Intelligence Agent recomputes operator health scores
  - Fleet Intelligence Agent recomputes utilization indices

Event-triggered:
  - FAA registry diff → Aircraft Researcher
  - FAA OPSS diff → Operator Researcher
  - ADS-B silence > 30 days → Aircraft Researcher (status check)
  - News alert (Perplexity webhook on key operators) → Operator Researcher

Monthly (1st of month):
  - Spot-check audit: 10 random canonicals, human review, log findings
  - Validation set re-run with current prompt versions
```

---

## What "autonomous" actually means here

Let me be precise, because "autonomous" is overused.

**The agents are autonomous in:**
- Deciding which records to research (drift signals + queue priority)
- Choosing which sources to query (based on entity type + gap)
- Synthesizing evidence into a confidence-scored proposal
- Auto-committing high-confidence updates (≥0.95)
- Writing temporal history without overwriting

**The agents are NOT autonomous in:**
- Committing low-confidence updates (those queue for human review)
- Resolving Two-Source Rule violations (single-source claims sit pending)
- Modifying the canonical schema (schema changes require explicit migration)
- Changing prompt versions or thresholds (those require validation re-run)

**This is the right level of autonomy for now.** As your validation set grows and you trust the system more, you can raise the auto-commit threshold (0.95 → 0.92 → 0.90). But you do that based on measured precision, not feeling.

---

## What this unlocks for OSA

Once these four agents are running:

**For Dumont:**
- Real-time operator health scores when matching trips
- Real-time aircraft availability inference
- Confidence-scored quotes with evidence chains
- "Why this operator" explanations grounded in data

**For OSA Connect (the brokerage):**
- Ranked operator lists by route, class, utilization, health
- Ghost positioning live signals
- Fleet utilization benchmarks for pricing leverage
- Operator distress signals (capacity available cheaper than market)

**For OSA Aircraft (transactions):**
- Ownership history per tail (years of provenance)
- Fleet movement intelligence (which operators are buying/selling)
- Aircraft utilization as proxy for valuation health

**For Loud Hawk:**
- Quarterly fleet utilization reports (data nobody else publishes)
- Operator growth/decline rankings (auto-generated)
- Route demand curves with full transparency

**For external positioning:**
- Provenance + temporal history makes your data *defensible*
- Competitors can't replicate without 4 years of ADS-B + the entity graph
- Methodology publishable → "OSA is the reference implementation for commercial aviation ER"

---

## The honest sequencing

Given Phase 7 + AERP v1 work in flight:

**Now:** Phase 7 finishes. AERP v1 spec gets locked. `osa-data-platform` repo carved out. (You're already doing this.)

**Next 2 weekends:** Operator Researcher Agent + Drift Detector. These reuse the three-layer architecture you've already built — just wrap it in the autonomous loop with queue + cadence.

**Following 2 weekends:** Aircraft Researcher Agent. New work, but follows the same pattern as Operator Researcher with aircraft-specific source priorities.

**Following 1 weekend:** Fleet Intelligence Agent. Pure SQL + scheduled aggregation jobs. Easiest of the four.

**Continuous:** Monthly spot-check, weekly fleet recompute, daily research queue.

By the time you close charter deal #20, this is running without your daily attention. By deal #50, the fleet intelligence is generating Loud Hawk content automatically. By deal #100, you've published your methodology and the data product becomes the moat.

---

## The one thing I'd add

You mentioned "indicators on where to act." Build a fifth output explicitly: **the daily action brief.**

```
Every morning, the Fleet Intelligence Agent produces:
- Top 10 ghost positions (idle aircraft at off-home airports)
- Top 5 operator distress signals (utilization dropping, capacity available)
- Top 5 operator growth signals (fleet expansion, new routes)
- Top 5 ownership changes detected last 24 hours
- Top 5 tails needing follow-up (low confidence, stale data)

Delivered as: email or Telegram via ph-agent
Format: 3-screen mobile read, action items, click-through to detail
```

This is the layer that makes the data platform *operational* instead of academic. Without it, you have a beautiful graph nobody acts on. With it, you have a daily decision queue that compounds value with every deal.

Want me to draft the spec for the Operator Researcher Agent first, or the Fleet Intelligence Agent? Those are the two highest-leverage next builds, and they're independent enough you can sequence them however you want.

---

## Phelipe

So now that you see the whole picture of what we're building, can you try to find in different niches or the people, researchers in data, that are implementing agentic AI or framework that could help us on this.

---

## Claude

Good question. Let me search systematically for who's actually doing this — across niches, not just aviation. The patterns transfer even when the domain doesn't.
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

I have enough now. Let me synthesize this into the actual answer — who's doing this work in different niches and what you can steal from each.

---

## The map of who's doing this — and what to steal

Let me organize this by niche, because the patterns are domain-specific even when the techniques transfer. I'm only including the ones that map directly to what you're building.

### 1. Sanctions / Trade Compliance — Sayari (the closest analog to OSA)

**What they are:** A 1.5B-entity knowledge graph across 250+ jurisdictions, built from public records. They resolve corporate ownership across shell companies, sanctions exposure, beneficial ownership chains. The world's most comprehensive open-source-derived corporate intelligence platform.

**What they built (the architecture):**
- **Commercial World Model** — 1.5B+ entities, 10.6B+ records, 250+ jurisdictions, 4-hour update lag from sanctions changes
- **Ontology** — encodes investigative tradecraft into the schema itself
- **Superconductor** — orchestration layer that scores every output against tradecraft standards before delivery
- **Graph AI** — autonomous fleet of agents handling entity resolution, relationship mapping, ownership traversal
- **MCP server** — standards-based data access for the entire knowledge graph

**Why this matters for OSA:** Sayari is what OSA's data platform looks like at scale, applied to sanctions instead of charter. Same architectural pattern: entity resolution + temporal history + provenance + agent orchestration on top. Their "Commercial World Model" is your "Aviation Operating Graph" with different entities.

**What to steal:**
- **The Superconductor pattern** — every agent output gets evaluated against tradecraft standards before reaching users. For OSA, your version would evaluate every ER decision against your Two-Source Rule and confidence thresholds before it lands in the canonical graph.
- **The "show your work" UX** — every assertion shows: confidence level, source documents, reasoning chain, what's missing. They don't say "Meridian Trading is clean" — they say "Likely exposure: Roughly Even Chance to Likely. Tier-1 suppliers clean. One Tier-2 supplier shares three officers with a sanctioned entity. Confidence limited by incomplete filing data. Recommend manual review of Austrian registries."
- **The infrastructure choice** — Memgraph (in-memory graph) over Neo4j for real-time analytical queries. They process 40M new entities + 50M new connections monthly. That's a benchmark for what your aviation graph needs to handle.

---

### 2. Identity Resolution — Senzing / Jeff Jonas (your foundation already)

You already locked this. Jeff Jonas is the godfather of entity resolution. Forty years of work from casino fraud (SRD/NORA in the 1980s) to IBM's G2 to Senzing today. Six principles you've already integrated: Full Attribution, Sequence Neutrality, Self-correction, Data Tethering, Field Hashing, Real-time processing.

**What's new since you locked this:** Senzing launched **Agentic Entity Resolution for Apache Spark** (March 30, 2026). The pattern: AI agents autonomously prepare data, load and resolve entities in real time, then conversationally explore results — without requiring experts to configure rules. Free tier covers up to 100K records.

**What to steal:**
- **The MCP server** — Senzing exposes ER as MCP tools. Wrap your ER engine the same way so Dumont and any future agent can call `resolve_entity` as a tool.
- **The Apache Spark integration** — when your data volume crosses 1M records (probably year 2-3), Spark + Senzing is the proven scaling pattern.

---

### 3. Pharma R&D — Deep Intelligent Pharma + Genentech gRED

**What they're doing:** Multi-agent systems for clinical trial automation, drug discovery, regulatory submission. Deep Intelligent Pharma uses autonomous multi-agent platforms with self-learning capabilities, claiming up to 1000% efficiency gains with 99% accuracy. Genentech built the gRED Research Agent to automate manual literature searches and accelerate drug discovery pipelines.

**Why this matters for OSA:** Pharma's regulatory compliance burden is *higher* than aviation's. They've solved problems you'll eventually face — auditable agent decisions, reproducibility, validated workflows. Pharma agents must produce zero-revision regulatory approvals. That's the bar.

**What to steal:**
- **"Digital Rehearsals"** — using synthetic data to validate the entire data-to-report pipeline before committing real records. For OSA: run your Operator Researcher Agent against a synthetic stress-test dataset before each prompt version change.
- **"Autonomy isn't binary"** — the pharma frame: autonomy lives on a spectrum, and in regulated domains, the design choice is always autonomy *with accountability*. "Autonomy without accountability is chaos. Accountability without autonomy is paralysis." That's the exact frame for your auto-merge thresholds.
- **The five-question framework** Meta uses for their swarm — every analyst extracts the same five answers per file. Translate to OSA: every Operator Researcher run answers the same five questions about the operator. Standardization makes the output composable.

---

### 4. Customer Experience — Minerva CQ

**What they built:** Real-time AI co-pilot for voice-based customer support. Integrates real-time transcription, intent and sentiment detection, entity recognition, contextual retrieval, dynamic customer profiling, and partial conversational summaries — enabling proactive workflows and continuous context-building.

**Why this matters for OSA:** This is Dumont's voice-call sibling. Same problem class: real-time entity recognition during a live conversation, retrieving context dynamically, building profiles over time. The architecture maps directly.

**What to steal:**
- **Continuous context-building during conversation** — every Dumont call should update the canonical operator graph in real time, not after batch processing. Customer says "we just changed insurance to Travelers" → graph updates → next call benefits.
- **Dynamic customer profiling** — over time, each operator/client gets a richer profile from accumulated interactions. Patterns you observe become structured fields.

---

### 5. Knowledge Graph Construction — Graphiti / Zep

**Who they are:** Open-source temporal context graph engine specifically built for AI agents. Backed by Zep, which is becoming the standard memory layer for production agent systems.

**What's novel:** A context graph is a temporal graph of entities, relationships, and facts — like "Kendra loves Adidas shoes (as of March 2026)." Unlike traditional knowledge graphs, each fact has a validity window: when it became true, and when (if ever) it was superseded. Entities evolve over time. Everything traces back to episodes — the raw data that produced it.

**Why this matters for OSA:** Your AERP needs exactly this. "Operator X was on Part 135 cert Y as of June 2024. As of February 2026, they're on cert Z." Aircraft change operators. Operators change addresses. Without temporal validity windows, you get stale data.

**What to steal:**
- **The temporal validity model** — every fact in your graph carries `valid_from` and `valid_to` (or `null` for current). Never overwrite. Append.
- **The episode → fact → entity chain** — Graphiti's data model where every derived fact traces back to the raw episode (ingestion event) that produced it. That's what makes your "show your work" capability functional.
- **The open-source codebase** — Graphiti is Apache-licensed. You can read the implementation. github.com/getzep/graphiti.

---

### 6. Data Engineering — Altimate AI + agentic-data-modeling repos

**What they are:** Two GitHub patterns directly relevant to building autonomous data agents.

**Altimate AI:** Open-source agentic data engineering harness for dbt, SQL, cloud warehouses. Fork of OpenCode. 100+ tools, 10 warehouses. Their innovation: **3-mode agents (builder/analyst/plan) with SQL write access control**.

**aboyalejandro/agentic-data-modeling:** Three Claude Code skills for autonomous data modeling:
1. Impact analysis before schema changes (traces lineage through dbt models)
2. Mart audit + enrichment for AI consumption
3. Glossary management derived from dbt models

**Why this matters for OSA:** These are the agent harnesses you adapt for AERP. Don't build orchestration from scratch — fork these patterns.

**What to steal:**
- **The 3-mode pattern** (builder/analyst/plan) — separates "make changes" from "understand state" from "design future." Your Operator Researcher Agent should operate in those three modes too. Plan mode proposes changes without executing. Analyst mode investigates without modifying. Builder mode commits with full audit trail.
- **The skill structure** — three discrete skills, each invoked as a slash command. Perfect for `osa-data-platform`: `/operator-research`, `/aircraft-research`, `/fleet-intelligence`, `/drift-detect`.

---

### 7. Vertical AI Founders — the playbook from Bessemer + Madrona

This isn't a niche; it's the meta-pattern. Vertical AI agent companies are reaching 80% of traditional SaaS contract values while growing 400% year-over-year. Bessemer projects vertical AI market capitalization could grow 10x larger than legacy SaaS.

The closest playbooks to OSA:

- **Abridge** (healthcare) — founder Shivdev Rao started as a cardiologist. Captures clinical conversations, structures them, feeds them to EHRs. Domain expert + AI-native build = moat.
- **Fieldguide** (audit) — founder Jin Chang was an auditor. AI agents handling audit workflows. Same pattern: insider domain knowledge + AI-native architecture.
- **EvenUp** (legal) — generates demand letters for personal injury cases.
- **Hebbia + Sixfold + Hyperexponential** (financial services) — diligence automation, insurance pricing, financial workflows.
- **Avitor.ai** — vertical AI for charter aviation, but built around chatbot/quoting workflow, not data infrastructure. They're a competitor to Dumont's intake layer, not your data platform.

**The Bessemer thesis on what makes vertical AI defensible:**
1. **Strong contextual data** — proprietary or hard-to-replicate domain data
2. **Domain expertise** at the founder level (your ATP + CFI/CFII + reserve flying)
3. **Workflow integration depth** — not just generating insights, but executing actions
4. **Embedded compliance** — for OSA, this is FAA/DOT/Two-Source Rule baked into agent behavior

**What to steal:** the framing. You're not "building a data platform." You're building a **vertical AI agent company for charter aviation**, with the data platform as the moat underneath. That's how Sayari is positioned. That's how Abridge is positioned. The data is the substrate; the agents are the product.

---

## The four researchers / practitioners worth following

Beyond the companies, the people whose work directly extends what you're building:

1. **Jeff Jonas (Senzing)** — already in your stack mentally. His blog and Senzing's documentation are the principle layer.

2. **Athulya Anil (Agentic GraphRAG)** — building multi-agent systems that automatically infer schemas, construct knowledge graphs, route queries between vector search and graph traversal based on query structure and risk signals. This is the architecture for your fifth agent (the Drift Detector).

3. **Daniel Chalef / Zep team (Graphiti)** — temporal context graph for AI agents. The actual code you'd fork.

4. **Yi Zhou (Agentic Engineering Body of Practices)** — distilled 2,000+ pages of field notes across 600+ real-world deployments spanning six industries. The first large-scale systematic study of AI agents in production, surveying 306 practitioners across 26 domains. AEBOP is the practitioner reference for production agents. Worth reading even just to validate your architecture against patterns that have shipped.

---

## What this synthesis tells me about OSA's position

Pulling all of it together:

**You're not behind.** The companies actually doing this at scale (Sayari, Senzing, Graphiti, Genentech, Minerva CQ) are using the same patterns you're already implementing — entity resolution + provenance + temporal history + agent orchestration + ontology. None of them have done it for aviation.

**Your moat shape is right.** Sayari's "Commercial World Model" applied to corporate intelligence is your "Aviation Operating Graph" applied to charter. They've validated the architecture's commercial viability at $1B+ valuation scale.

**Your tooling decisions are aligned with the frontier.**
- MCP server for the data platform → matches Sayari's MCP product
- Two-Source Rule + provenance → matches their "show your work" architecture
- Temporal entity history → matches Graphiti's validity window model
- Multi-agent orchestration with role-based agents → matches Meta's swarm pattern, Sayari's Superconductor, pharma's multi-agent systems

**The gap to close isn't architectural — it's execution discipline.** You need the equivalent of:
- Sayari's Superconductor (your eval gate that scores every ER decision before it lands)
- Graphiti's temporal model (formalized in your aerp-v1.md spec)
- Meta's five-question framework (standardized output schema for every researcher agent)
- Pharma's "Digital Rehearsals" (synthetic stress-test datasets for prompt version changes)

**The single highest-leverage move right now:** read the Sayari blog systematically, particularly their "Graph AI" product pages. They've publicly described an architecture that maps near-perfectly to what you're building, with the differences being domain (corporate vs aviation) and scale (1.5B entities vs ~50K). You're solving a smaller version of an already-validated $1B+ problem class.

Want me to drill into any of these — the Sayari architecture in detail, the Graphiti temporal model implementation, or the Bessemer vertical AI playbook applied to OSA's positioning?

---

## Phelipe

Yeah. What you just told me it does make sense. I just don't see, like, the only way we can build an agent is for an analytics. Right? I don't see anything, like, once the data like, platform is built, probably just the agent for ingest the legs every day from ADS below. And then processing, making to the medallion, But once the data platform is built, the operator entity resolution, the aircraft entity resolution, The only thing is just keeping up to date. So the agent needs to be built after that just to keep the data platform up to date. Right?

---

## Claude

You're mostly right but missing two important things. Let me push back precisely.

## What you've got correct

Once the data platform is built, the steady-state work is:
- Daily ADS-B ingestion → leg processing → medallion materialization
- Periodic ER refresh as new sources arrive or existing entities change
- Analytics on top

That's true. And you're right that you don't need a sprawling agent army for steady-state. **Most of the daily work is deterministic ETL, not agentic reasoning.**

The agent for "keep the data platform up to date" is real, and it's roughly what we mapped: Drift Detector + scheduled Researchers running on triggers. That part of your thinking is correct.

## What you're missing

**Two things.**

### 1. The data platform is never "built." It's continuously researched.

You're framing this as: build → maintain. But aviation entity reality changes constantly:

- An operator gets acquired. New parent. New cert. Old cert surrendered. 30 aircraft transfer. Fleet stays mostly the same but legal structure flips overnight.
- A trust restructures. Bank of Utah Trustee transfers 12 tails to a new LLC. FAA registry reflects it the next day. Operator-of-record needs re-resolution for all 12.
- An operator suspends ops. Cert remains technically active for 90 days. Aircraft go silent on ADS-B. Are they out of business? In maintenance? Repositioning? Something else?
- A new sub-operator emerges. Forms LLC in March. Gets cert in June. Buys fleet from a closing operator in August. Their entire history needs to be traced backward from the moment they appear.
- ARGUS upgrades or downgrades a rating. That's a meaningful change in operator quality scoring. Needs to flow through.

**The "research" never stops.** Not because the platform is broken, but because the world it models is moving. The Operator Researcher Agent is a steady-state agent, not a one-time build agent.

This is the same reason Sayari runs continuously, not as a one-time build. Their commercial world model updates within 4 hours of every sanctions list change because *the world changes*. They have agents that are always researching, always re-resolving, always re-corroborating. That work doesn't end.

So the right framing isn't:
- Phase 1: Build platform
- Phase 2: Build maintenance agents

It's:
- Phase 1: Build platform + research agents *together* (because you can't get to ER accuracy without iterative research)
- Phase 2: The research agents become the platform's heartbeat

The research agents *are* how the platform stays valuable. Without them, your 97% accuracy degrades to 90% within a year as operators rebrand, certs change, fleets move.

### 2. There are agents that aren't analytics and aren't maintenance — they're operational

This is the bigger miss. You're thinking about agents as either "build the data" or "report on the data." There's a third category that matters more for OSA's business: **agents that act on the data in real time during operations.**

Three concrete examples that aren't maintenance and aren't analytics:

**A. The Quoting Agent (Dumont's brain in operations)**

When a client requests a charter, this agent:
- Reads the trip parameters
- Queries the Fleet Intelligence Agent for active aircraft matching the route + class + date
- Filters by operator health score (drops distressed operators automatically)
- Cross-references ADS-B to confirm aircraft is actually available (not airborne, not in maintenance)
- Computes Charter Index estimate for the route + class
- Pulls operator-specific pricing patterns from prior quotes
- Generates ranked operator list with confidence scores and reasoning chain
- Drafts the RFQ for human review

This isn't maintenance. This isn't analytics. This is the data platform *being used in real-time decisions*. Without this agent, your data platform is a museum.

**B. The Outbound Research Agent (when you eventually do outbound)**

When you decide to reach out to a post-raise founder:
- Pulls funding event from Crunchbase
- Resolves founder identity (name → company → role → location)
- Checks ADS-B for any flights they've booked recently (commercial route patterns visible via LinkedIn check-ins, Twitter posts)
- Cross-references with your existing operator coverage in their geography
- Drafts personalized outreach grounded in their actual travel patterns
- Suggests timing (post-raise, pre-board-meeting, etc.)

This is the vertical AI SDR pattern from a few sessions ago, but built on top of your data platform.

**C. The Compliance / Risk Agent**

Before you finalize a deal:
- Verifies operator's Part 135 cert is currently active (not just last-known-good)
- Checks for recent NTSB incidents involving the tail
- Confirms insurance is current
- Validates the aircraft type cert matches the trip requirements
- Surfaces any anomalies (operator just had a check ride failure, aircraft just had an unusual maintenance event)

Again — not maintenance, not analytics. Real-time decision support.

## The full agent taxonomy for OSA

Here's the honest map:

**Tier 1: Ingestion / ETL (mostly deterministic, some agent)**
- ADS-B daily ingest
- FAA registry diff detector
- FAA OPSS scraper (when restored)
- News / press release watchers via Firecrawl
- This is 80% scripts, 20% agents (mainly for handling source changes)

**Tier 2: Research / Resolution (continuous, agentic)**
- Operator Researcher
- Aircraft Researcher
- Drift Detector
- Fleet Intelligence
- These run forever. They never "finish."

**Tier 3: Operational / Decision-support (real-time, agentic)**
- Quoting Agent
- Compliance / Risk Agent
- Outbound Research Agent (later)
- Dumont as the orchestrator that calls all of them

**Tier 4: Analytics / Reporting (periodic, mostly deterministic with some agent)**
- Daily action brief
- Weekly fleet utilization reports
- Quarterly Loud Hawk content
- Charter Index recalibration jobs

You're right that Tier 4 is mostly analytics. You're right that Tier 1 is mostly ETL. You're right that once Tier 2 is built, it shifts to maintenance mode.

**But Tier 3 is where the actual product lives.** That's the layer that turns the data platform into OSA the business. Without Tier 3, you have a beautiful aviation database that doesn't make money.

## The reframe

Instead of "data platform → then build agents to maintain it," the right mental model is:

**The data platform exists to power operational agents. The research agents keep the platform fresh. The analytics agents broadcast what the platform knows. All of it serves the operational layer.**

When Dumont quotes a trip, the entire stack lights up:
- Tier 2 ensures operator data is fresh
- Tier 1 ensures ADS-B activity is current
- Tier 3 (Quoting Agent) makes the decision
- Tier 4 logs the decision for future learning

This is why Sayari's stack works. They have:
- Continuous research agents keeping the world model fresh
- Operational agents (Graph AI) that analysts use in real-time investigations
- Reporting agents producing due diligence packages

You're building the same shape. Don't sell yourself short on what the agents do.

## So your question's real answer

**Yes, post-build the data platform shifts to maintenance.** True.
**No, that's not the only kind of agent that matters.** The maintenance agents are the smallest, least visible layer. The operational agents (Tier 3) are where OSA's product lives, and they don't exist yet — Dumont in its current form is intake-only.

The build sequence I'd recommend, in light of this:

1. Finish Phase 7 + AERP v1 spec (in flight)
2. Build Tier 2 research agents (Operator Researcher first) — these compound platform value continuously
3. Build the *first* Tier 3 operational agent: the Quoting Agent that uses the platform to make a real recommendation when Dumont takes an inbound call
4. Iterate on that loop — every real quote teaches the platform what queries actually matter, which sharpens Tier 2 priorities
5. Tier 4 analytics emerge naturally from the operational data Tier 3 generates

The Quoting Agent is the highest-leverage thing to build *after* AERP v1, because it's the bridge between "having data" and "using data to close charter deals." That's what turns this from infrastructure into a business.

Does that reframe land?

---

## Phelipe

No. What I'm trying, it's like Dumont is gonna be as operational for the charter brokerage. What I'm thinking is more for the data. Think like ASA as the intelligence layer. Where we can not only see the operators like who flies the most, who is fractional, like, so we can have, like, a market analysis on operators. And then, like, with the weeks spots, the strong spots, who is winning who is losing, who might even be on the verge of breaking because they're not doing business. And we can see on their flight And then on the aircraft market, we can see what are the hot airplanes they're being transaction. We don't need to know the price but we can know a little bit what is hot. And then after on top, we can implement the price. So if, like, some third party or scraping marketplaces, and even, like, to go outreach. Like, when we scrape an out marketplace, and then we see that that's like a owner just trying to sell their aircraft, and it's been there for a while. We can try to help them or something like that.

---

## Claude

Now I get it. You're not talking about Dumont at all. You're talking about a separate intelligence product. Let me reflect this back precisely so we're aligned, then map the agents.

## What you're actually describing

**OSA Intelligence** — a market intelligence layer for charter aviation. Not the brokerage product. Not the data platform substrate. The thing that *reads* the platform and produces insight.

Three distinct intelligence surfaces:

**1. Operator Market Intelligence**
- Who flies the most (fleet activity rankings)
- Who is fractional vs charter vs management vs Part 91 corporate
- Who is growing (fleet expansion, route additions, utilization climbing)
- Who is shrinking (utilization dropping, tails going silent, routes contracting)
- Who is at risk (distressed signals — fleet idle, certificate concerns, hiring freezes detectable in patterns)
- Who is gaining market share on specific routes
- Who is losing it

**2. Aircraft Market Intelligence**
- Which aircraft types are most actively transacting (ownership changes from FAA diff)
- Which tails are "hot" — registrations bouncing, multiple owners in short windows
- Which aircraft are sitting idle (potential distress sales)
- Geographic concentration of transactions
- Class-level transaction velocity
- No prices needed in v1 — just *transaction signal*

**3. Marketplace Outreach Intelligence**
- Scrape Controller, AvBuyer, Trade-A-Plane, JetBrokers
- Detect listings that have been sitting (price drops, days on market increasing)
- Cross-reference with FAA registry to identify the actual owner behind the listing
- Identify owners who might benefit from OSA's help
- Surface outreach opportunities

This is the **Bloomberg Terminal of Charter Aviation** thesis applied to a free / freemium intelligence product. Not Dumont. Not OSA Connect. A new product surface entirely.

Let me map the agents that build this.

---

## The agent stack for OSA Intelligence

This is a different shape than what I described before because the *output* is different. Dumont's agents make operational decisions in real time. Intelligence agents produce continuously updated market views.

### Agent 1: The Operator Market Analyst

**Job:** Continuously rank, score, and characterize every Part 135 operator on a battery of market metrics.

**Inputs:**
- Operator canonical graph (from your data platform)
- ADS-B activity (last 7/30/90/365 days)
- FAA OPSS cert status
- ARGUS / Wyvern / IS-BAO ratings
- Public news / acquisition signals
- Hiring data (LinkedIn pilot postings)

**Computations per operator, weekly:**
- **Activity rank** — flights/month, hours/month, growth vs prior period
- **Fleet utilization index** — how hard the fleet is being flown vs class average
- **Geographic footprint** — unique airports served, route diversity
- **Class composition** — fleet mix and changes over time
- **Operator type classification** — fractional / managed / pure charter / corporate flight dept / hybrid (this is computed, not declared)
- **Growth trajectory** — fleet trend, utilization trend, route trend (all 6-month rolling)
- **Distress signal score** — composite of utilization decline, tails going silent, route abandonment, hiring freezes
- **Health composite** — overall operator scorecard

**Output:**
- Ranked operator tables (top 100 by activity, by growth, by distress)
- Operator profiles updated weekly
- Trend lines per operator
- Daily anomaly alerts (operator goes silent, fleet drops 20%+ in week, etc.)

This is your "Crunchbase for charter operators" data layer. Nobody has it because nobody has the entity-resolved fleet + ADS-B continuous tracking.

---

### Agent 2: The Operator Type Classifier

**Job:** Determine what kind of operator each entity actually is, behaviorally.

This is harder than it sounds. The FAA cert tells you "Part 135." It doesn't tell you fractional vs managed vs charter. The behavior tells you that.

**Behavioral signatures:**

- **Fractional**: 50+ tails, high utilization across all aircraft, owner-flight patterns (multiple short same-day repositioning), branded ICAO callsigns (EJA, NJE, FLG)
- **Managed (large)**: 20+ tails, varied utilization (some heavy, some light), aircraft owned by trusts not the operator, fleet additions/subtractions tracking individual aircraft owner changes
- **Pure charter (mid)**: 5-20 tails, high utilization on revenue routes, fleet stable, base airport concentration
- **Pure charter (small)**: 1-4 tails, regional focus, mixed Part 91/135 use
- **Corporate flight dept (Part 91)**: 1-3 tails, low utilization (200-400 hours/year), based at one airport, predictable owner-related routes

**Classification confidence:** Some operators are clearly one type. Others are hybrid (Priester runs managed + charter + sales). The agent assigns probability vectors, not single labels.

**Why this matters:** The intelligence product is way more valuable if you can say "Among pure-charter operators in the Northeast with super-mid fleets, here are the top 10 by utilization growth" instead of just "Here are operators."

---

### Agent 3: The Aircraft Transaction Detector

**Job:** Detect ownership changes and characterize the aircraft transaction market.

**Inputs:**
- Daily FAA registry diff (you already have this)
- ADS-B going silent / reappearing under new patterns
- Listing scrapes (Controller, AvBuyer, Trade-A-Plane)
- UCC filings (loan amounts, when available)

**Detection:**
- New ownership recorded → flag as transaction
- Tail goes silent for 14+ days → potential transaction in progress
- Tail reappears with new operator pattern → transaction confirmed
- Previously-listed aircraft removed from listings + ownership change → sale closed
- Aircraft listing days-on-market increasing + price drops → distressed seller

**Outputs:**
- Daily transaction feed (what changed hands today)
- Transaction velocity by class (heavy jets transacting 2x normal rate this quarter)
- Transaction velocity by region
- "Hot tails" — aircraft with registrations changing multiple times in short windows (charter→private→fractional sequences are interesting)
- Distressed seller queue — for outreach prioritization

**No prices needed in v1.** Just the *signal* of what's transacting. Price comes later from triangulation.

---

### Agent 4: The Marketplace Scraper + Owner Resolver

**Job:** Continuously monitor aircraft listings and link each listing to a real beneficial owner.

**Sources:**
- Controller.com
- AvBuyer
- Trade-A-Plane
- JetBrokers
- Aircraftforsale (Globalair)
- Industry-specific brokers (Mente, JetCraft, Hagerty Jet Group)

**Per listing:**
- Tail number → FAA registry → registered owner
- Registered owner → state corp filings → beneficial owner
- Beneficial owner → SEC filings / news / LinkedIn → real person + role
- Cross-reference with operator graph (is this aircraft currently on a Part 135 cert?)
- Days on market tracking (when did it first appear, has price dropped, has description changed)

**Anomaly detection:**
- Aircraft listed but still flying actively (the owner is testing the market)
- Aircraft listed and grounded (the owner needs out)
- Aircraft listed with significant price drops (motivated seller)
- Aircraft listed multiple times via different brokers (frustrated, looking for new agent)

**Outputs:**
- Live marketplace inventory with beneficial owner attribution
- Distressed seller queue
- "Listings to watch" feed
- Owner outreach prioritization

This is the most outreach-relevant agent. When a tail has been on market 180 days with three price drops and the beneficial owner is identified, that's a phone call.

---

### Agent 5: The Market Movement Synthesizer

**Job:** Take outputs from Agents 1-4 and produce daily/weekly market intelligence narratives.

**Daily brief format:**
```
Top 5 operator anomalies (24h)
- [Operator X] activity dropped 40% week-over-week. Investigate.
- [Operator Y] added 3 tails this week. Growing.
- [Operator Z] cert status changed. Verify.

Top 5 aircraft transactions detected (24h)
- N12345 (Phenom 300, 2018) sold from [Operator A] to [Operator B]
- N67890 (Citation X) ownership change to trust, suggests private buyer
- ...

Top 5 marketplace movements
- 2010 Falcon 7X listed by [Owner], 90 days on market, just dropped $1.2M
- 2015 Phenom 300 by [Owner], second listing this year, motivated
- ...

Class-level market velocity
- Super-mid: +15% transactions vs trailing 90d
- Heavy: -5% transactions vs trailing 90d
- ...

Operator distress watchlist (5 operators worth monitoring)
```

**Weekly brief:** Deeper analysis, trend shifts, sector views.
**Monthly brief:** Loud Hawk-quality content. Publishable.

This is the agent that produces the "Crunchbase newsletter" of charter aviation. The product output. The thing your audience reads.

---

### Agent 6: The Outreach Opportunity Generator

**Job:** Convert intelligence signals into concrete outreach actions.

**Triggers:**
- Marketplace listing aged 120+ days with price drops → seller might want help
- Operator distress signals → potential acquihire / fleet acquisition opportunity
- Operator growth signals → potential operator-of-the-week feature, relationship build
- Aircraft transaction by founder/exec on your dream 500 list → relevant trigger event

**Per opportunity:**
- Why this person/operator/owner is worth reaching out to
- What's the specific signal (with evidence)
- What OSA can offer them (acquisition help, charter program, sales support, etc.)
- Drafted outreach grounded in the specific signal

**Output:** Ranked queue of outreach opportunities with full reasoning. Human approves and sends.

This is the bridge from intelligence to revenue. Without it, you have a great newsletter but no flywheel.

---

## How they connect

```
Data Platform (already being built)
   ↓
Agent 1: Operator Market Analyst ─────┐
Agent 2: Operator Type Classifier ────┼─→ Operator intelligence
Agent 3: Aircraft Transaction Detector┐
Agent 4: Marketplace Scraper + Owner Resolver ─→ Aircraft + listing intelligence
   ↓
Agent 5: Market Movement Synthesizer ──→ Daily/weekly/monthly briefs
   ↓
Agent 6: Outreach Opportunity Generator ──→ Action queue
   ↓
Human (you) → outreach → deals → flywheel
```

## What this is, strategically

This is **OSA Intelligence as a separate product surface from OSA Connect.** Three positioning options:

**Option A: Free public intelligence (Loud Hawk extension)**
- Daily newsletter "what moved in charter today"
- Public weekly leaderboards
- Drives audience, builds brand, generates inbound
- Monetization: brokerage, future SaaS

**Option B: Freemium SaaS**
- Free tier: weekly summary
- Paid tier: real-time alerts, custom watchlists, API access, full operator profiles
- Sold to: hedge funds (M&A signal), other brokers, operators (competitive intel), aircraft sales firms
- This is the JETNET-killer pattern at 1/10th the price

**Option C: Internal-only competitive advantage**
- OSA uses it for outreach, deal targeting, market awareness
- Doesn't sell, doesn't publish
- Pure private edge
- Fastest to build, slowest to monetize beyond brokerage

I'd argue **Option A as the public face, Option C as the internal layer**, with Option B as the year 2-3 SaaS expansion. The intelligence product is too valuable to give away entirely but too brand-defining to keep entirely private. Loud Hawk publishes the headlines; OSA Intelligence the SaaS sells the dashboards.

## Why this is more important than I gave it credit for

You're right that I underweighted this in my last response. The intelligence layer isn't a "nice to have" downstream of the data platform — **it's the actual product that emerges from the data platform**.

The three things make this powerful:

1. **It compounds.** Every day of ADS-B + FAA data makes operator and aircraft intelligence more accurate. JETNET has 38 years of head start on aircraft data; you have 4 years of ADS-B and a better architecture. With agents continuously enriching, you close the gap fast on the dimensions that matter (real-time activity, distress signals, behavioral classification).

2. **It's defensible.** Competitors can buy ADS-B feeds. They can't replicate your operator entity resolution + temporal history + behavioral classifier in less than 18 months. By the time they try, you've added another 18 months of historical depth.

3. **It generates leads automatically.** Agent 6 (Outreach Opportunity Generator) literally produces a queue of phone calls every day. Each one is grounded in a specific real signal. That's a flywheel competitors can't match because they don't have the underlying entity graph.

## The build sequence

Given you're solo and building the data platform in parallel:

**Phase 1 (now → AERP v1 done):** Don't build any of these agents yet. Phase 7 + AERP first.

**Phase 2 (AERP done):**
- Agent 3 (Aircraft Transaction Detector) — easiest, runs off FAA diff you already have
- Agent 1 (Operator Market Analyst) — second, runs off entity graph + ADS-B you have
- Both produce immediate intelligence value internally

**Phase 3:**
- Agent 5 (Market Movement Synthesizer) — turns Agents 1+3 outputs into Loud Hawk content
- This is when the public Loud Hawk intelligence layer goes live

**Phase 4:**
- Agent 4 (Marketplace Scraper + Owner Resolver)
- Agent 2 (Operator Type Classifier)
- These add depth and outreach surface

**Phase 5:**
- Agent 6 (Outreach Opportunity Generator)
- The flywheel layer

You don't need all six agents to start delivering value. Agents 1 + 3 + 5 alone produce a publishable daily intelligence product within a quarter of AERP completion.

Does this match what you were actually trying to build? If yes, I can go deep on Agent 1 or Agent 3 next — they're the foundation.

---

## Phelipe

Now on the aircraft brokerage, not charter brokerage. Aircraft brokerage. Like, there's any AI movement in there. There's anyone using AI or intelligence layer to do deals or to offer that to the seller or to the buyers. I mean, the a lot of, the brokers use JetNet, but there's anyone doing a full stack AI native aircraft brokerage.

---

## Claude

Good question. Let me actually research this rather than guess.
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

I have enough now. Let me give you the actual map of who's doing what in AI-native aircraft brokerage.

---

## The honest answer: nobody has done this fully. The field is wide open.

Let me walk you through who's claiming AI in aircraft brokerage, what they're actually doing, and where the real gap is.

## The current landscape — three categories

### Category 1: Traditional brokers using AI as a productivity tool

This is most of the industry. These are not AI-native businesses. They're traditional brokerages bolting AI onto existing workflows.

**Jetcraft (the most aggressive of the traditional players):**
- Built **JetGPT** — internal LLM hooked into their inventory and market data, used by their sales team
- Has a dedicated analytics team since 2018
- Publishes Market Forecast annually
- Built proprietary tools: Jetrange, Jetcraft App
- **What they're not doing:** No autonomous agents. No customer-facing AI brokerage. JetGPT is internal-only — it makes their human brokers faster, doesn't replace any part of the transaction.

**Duncan Aviation:** Has a proprietary "Duncan Aviation Knowledge-base (DAK)" with operational/ownership cost data. 70 years of transaction history, 3,750+ deals. Traditional advisory model with proprietary data, no agents.

**Guardian Jet:** Has "JetFinder" and "Guardian Estimate" — basic tools for searching aircraft and getting a valuation. Not agentic. More like a 1.5x improvement on Excel.

**Avjet, SOLJETS, Mente, JetCraft, Hagerty Jet Group:** Classic high-touch advisory brokerages. SOLJETS has SOLDATA (their data tool). The rest mostly rely on JETNET subscriptions. None are AI-native.

**The pattern across all of them:** AI is being used to make existing brokers more productive. None are reimagining the brokerage from the ground up.

---

### Category 2: AI-claiming companies doing partial AI work

**Aero Ventures (Sergey Petrossov's new platform):**

This is the closest thing to what you're asking about, and worth understanding deeply because Petrossov already built JetSmarter. He knows aviation. His new bet is AI-native ownership.

What they claim:
- AI agents pull real-time aircraft specifications, transaction data, market comps
- Generate instant fair market valuations
- Predictive modeling for ownership cost, depreciation, residual value
- Continuous market monitoring
- Capital-backed offers within 48 hours (institutional liquidity for sellers)
- Targets transactions above $10M
- Vetted buyers and sellers (curated marketplace)

What they're actually doing:
- **AI-powered valuation engine** — this part is real and probably useful
- **Market intelligence dashboard** — continuously updated comps and trends
- **Predictive ownership modeling** — depreciation curves, cost projections
- **Capital provision** — 48-hour offers backed by their own fund

What they're explicitly not doing:
- Replacing the broker. Petrossov says clearly: "AI accelerates the analytical foundation while advisors focus on high-value work — negotiation strategy, transaction structuring, relationship management."
- They position this as a Zillow-style "window shop and explore" entry point that funnels to human advisors.

**This matters for OSA:** Aero Ventures is the most direct competitor to what you'd build, but their thesis is "AI as the entry funnel, humans close." Yours could be different — AI agents that do more of the actual deal work, not just the analytics layer.

---

**Jet.AI (now part of flyExclusive):**
Acquired by flyExclusive in 2025. Their AI products were:
- **CharterGPT** — consumer charter booking app
- **Ava** — agentic booking AI
- **Jet.AI Operator platform** — B2B SaaS for Part 135 operators

They were charter-focused, not brokerage. Now folded into flyExclusive's vertically integrated charter business. No aircraft brokerage agent.

---

**AirSpace Auctions:**
Smaller player. Uses ChatGPT and Perplexity to analyze buyer behavior, draft listing copy, identify timing patterns. This is "broker uses AI tools daily" not "AI-native brokerage." Productivity layer, not transformation.

---

**PrivateJet.com (Wilbur):**
The most overhyped one. Built "Wilbur" — claims first AI broker in industry. What it actually does: chat-based quote estimation for charter (not brokerage), trained on millions of historical quotes. Hands off to humans for actual booking. They've added an aircraft sales marketplace recently (using Exclusive Jet Sales as launch customer), but the AI piece is charter-only.

---

### Category 3: Adjacent companies showing what's possible (worth studying)

**Sayari (corporate intelligence):** Already covered. Their architecture for entity-resolved transactions + ownership chains + temporal history is the closest analog to what aircraft brokerage intelligence should look like.

**EvenUp (legal — personal injury):** AI-generated demand letters. Single-purpose vertical agent that does real work, not just analysis. Worth studying because they took a high-touch advisory business (PI law) and inserted AI into the actual deal mechanics.

**Hebbia (financial diligence):** Used by large financial institutions for diligence on complex data rooms. Could be the model for aircraft transaction diligence — log analysis, AD compliance verification, maintenance pattern review.

**Hyperexponential (insurance pricing):** Vertical AI for insurance pricing models. Same shape: complex data → expert pricing decision. Aircraft valuation has the same structure.

---

## What's actually missing — the real gap

Here's the honest map of the aircraft brokerage workflow and where AI is / isn't:

| Workflow Step | Current State | AI-Native Opportunity |
|---|---|---|
| **Buyer/seller matching** | Manual, broker network, JETNET listings | ★★★★★ Massive gap — no one is doing AI-native matching |
| **Valuation** | Vref + broker experience + comps | ★★ Aero Ventures, Jetcraft starting to crack this |
| **Market intelligence** | JETNET subscription | ★★★ Jetcraft + Aero Ventures partial |
| **Off-market deal sourcing** | Broker relationships only | ★★★★★ Massive gap — this is the highest-leverage agent |
| **Listing creation** | Broker writes copy | ★ AirSpace using ChatGPT (productivity layer) |
| **Aircraft due diligence** | Manual logbook review by experts | ★★★★★ Massive gap — Hebbia-style diligence agent doesn't exist |
| **Transaction structuring** | Lawyer + broker | ★★★ Some legal AI applies here |
| **Pre-buy inspection coordination** | Broker manual | ★★★★★ Massive gap |
| **Closing/escrow** | Specialized firms (Insured Aircraft Title) | ★ Industry uses some software |
| **Post-sale ownership management** | Management companies | ★★ Aero Ventures's pitch |

**The gaps with five stars are the real opportunity.**

---

## The thesis I'd test for OSA Aircraft

Given your data platform's underlying entity resolution + ADS-B history + ownership tracking, the most defensible AI-native aircraft brokerage agents you could build:

### Agent 1: The Off-Market Sourcing Agent (highest leverage)

**The problem:** 60-70% of business jet transactions happen off-market. Brokers source deals through relationships. Nobody has cracked AI-native off-market sourcing.

**What yours would do:**
- Continuously monitor every charter-class tail in the registry
- Detect "soft" sale signals: utilization dropping for 6+ months, owner LLC dissolving, related entities filing UCCs, comparable aircraft in fleet being upgraded, owner's company going through M&A
- Cross-reference with corporate intelligence (SEC filings for newly liquid founders, recent fundraises)
- Identify owners likely to sell *before they list*
- Generate ranked outreach queue with full evidence chain

**Why this is unique:** Nobody has the entity-resolved, temporally tracked, ADS-B-enriched dataset to do this. JETNET sells the data; nobody runs agents on it for predictive seller identification.

**This alone is a $50M+ company if executed.**

---

### Agent 2: The Aircraft Diligence Agent

**The problem:** Pre-buy inspections take weeks. Logbook review takes days. AD compliance verification is manual. A buyer's broker spends 40-80 hours on diligence per deal.

**What yours would do:**
- Ingest logbooks (PDF, scanned, structured)
- Cross-reference with FAA AD database for compliance
- Compare maintenance history to fleet averages for that type
- Flag anomalies (unusually long downtime, frequent unscheduled maintenance, ownership chain red flags)
- Cross-reference NTSB for any incidents involving the tail
- Verify tail's identity matches serial number across all sources
- Generate diligence report with confidence scores and evidence chain

**Hebbia-shape applied to aircraft.**

---

### Agent 3: The Buyer Match Agent

**The problem:** Brokers spend hours qualifying buyers, understanding their mission profile, narrowing aircraft type, finding inventory. Most of this is pattern matching they could explain in 5 minutes.

**What yours would do:**
- Take buyer mission profile (typical routes, passenger count, range needs, budget)
- Match against aircraft type capabilities (from your aircraft entity graph)
- Filter by current market inventory (listings + predicted off-market candidates)
- Rank by fit, with explanation
- Surface "you should consider these alternatives" insights based on mission patterns

**The Avitor.ai of buy-side aircraft brokerage.**

---

### Agent 4: The Owner Engagement Agent

**The problem:** Aircraft brokers have hundreds of past clients and prospects. Maintaining relationships at scale is a CRM problem with too much context for traditional CRMs to handle.

**What yours would do:**
- Track every aircraft owner's situation continuously (utilization, ownership age, market conditions for their type)
- Generate timely outreach when their aircraft type's market is favorable
- Surface "your aircraft is now worth X, fleet utilization patterns suggest you might consider Y" insights
- Personalized at scale, grounded in your data platform

---

## The strategic answer to your question

**No, no one has built a full-stack AI-native aircraft brokerage.** Aero Ventures is the closest, but their thesis is "AI augments human advisors" — not "AI agents do most of the deal work."

**Why nobody has done it yet:**
1. The data layer is the prerequisite. JETNET sells access but doesn't let you run agents on it. Without entity-resolved aircraft + operator + ownership history, AI-native brokerage is impossible.
2. The aircraft brokerage industry has high switching costs (relationships) and low transaction volume (deals are huge but rare). Hard to build product-market fit fast.
3. Most AI builders don't understand aviation. Most aviation people don't understand AI.

**What OSA has that nobody else has:**
- Pilot credentials (you understand the product)
- Aircraft entity resolution being built
- Operator entity resolution being built
- ADS-B utilization continuously tracked
- Ownership history captured temporally
- The architectural discipline (Two-Source Rule, provenance, confidence scoring) to make this trustworthy

**This is a sleeping $1B opportunity.** Not because aircraft brokerage is undervalued — it's already a $20B+ industry. Because nobody has built the AI-native version, and the data prerequisites are exactly what you're building for charter.

The thesis crystal-clear:

**The data platform underneath OSA Connect (charter brokerage) is also the data platform underneath OSA Aircraft (aircraft brokerage). Same entities, same ADS-B, same ownership history. Different agents on top.**

You're not building two products. You're building one data platform with two product surfaces. Charter today (faster cash flow, higher transaction volume), aircraft tomorrow (massive deal sizes, longer cycles, but huge moat once you have the agents).

Aero Ventures is the warning shot — Petrossov is well-funded, knows aviation, building partial AI-native. He'll get there before you if you don't sequence right. But he's also not building the data substrate you have. He's licensing JETNET data and adding AI on top.

You have the better foundation.

Want to drill into any of the four agents I outlined, or talk strategy on whether OSA Aircraft becomes a real product line?

---

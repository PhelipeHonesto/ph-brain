---
title: Interesting GitHub repository discovery
created: 2026-03-15T15:02:45.468220Z
updated: 2026-03-15T15:06:49.723285Z
uuid: 690a1cf0-85bc-419e-b92a-834ec7b34a99
source: claude-conversation
type: source
message_count: 4
---

# Interesting GitHub repository discovery

## Phelipe

oh boy we found a good one ahha
https://github.com/garrytan/gstack

---

## Claude

Let me check out what this is!
```
This block is not supported on your current device yet.
```

Oh yeah, this is a great find. Garry Tan (YC's CEO) open-sourced his entire Claude Code workflow — 12.1k stars already.

The core idea is exactly what you've been building toward with OSA: instead of using one generic AI assistant, you create **specialized modes** that each think differently. His setup gives Claude Code eight "cognitive gears":

**The planning layer** — `/plan-ceo-review` forces the model into "founder brain" before any code gets written. Instead of taking a request literally, it asks what the 10-star version of the product actually is. Then `/plan-eng-review` locks in architecture, diagrams, edge cases, and test coverage.

**The execution layer** — `/review` acts as a paranoid staff engineer hunting for production bugs that pass CI. `/ship` handles the boring release hygiene (sync main, run tests, push, open PR). `/qa` reads your git diff and automatically tests the affected routes.

**The eyes** — `/browse` gives the agent a real Chromium browser so it can actually see the UI, click through flows, take screenshots, and verify things visually. `/setup-browser-cookies` imports your real browser sessions so it can test authenticated pages.

**The reflection layer** — `/retro` analyzes commit history and writes a candid weekly retrospective with per-contributor feedback.

The thing that probably resonates most with your setup: he's running **ten Claude Code sessions in parallel**, each in its own workspace with its own cognitive mode. One doing QA on staging, another reviewing a PR, a third implementing a feature.

This maps directly to the pattern you've already discovered — splitting context across dedicated Claude Projects (Growth Marketing HQ, Loud Hawk, OSA Connect) rather than cramming everything into one. Garry's just doing it at the code level with slash commands instead of Projects.

A few things worth stealing for OSA's Claude Code workspace: the idea of explicit "skill files" (markdown prompts that define each mode's persona and methodology), and the concept of a review/ship pipeline where each stage has its own rigor level. Your lh-news-pill skill with the signal/visual/relevance scoring gate is already doing something similar — you've got the instinct, this just validates the pattern at scale.

---

## Phelipe

can you find others open-sourced his entire Claude Code workflow. 
the best one they is going viral, mainstream, or that you say like omg this is a must have

---

## Claude

Let me dig into this — there's been an explosion of these lately.
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

Phelipe, this is a goldmine. Here's the landscape — I'll rank these by "holy shit you need to know about this" factor:

---

**#1 — Boris Cherny's Workflow (the creator of Claude Code himself)**

This is the one that broke the internet. VentureBeat called it "a viral manifesto on the future of software development." His setup is deceptively simple: he runs 5 Claudes in parallel in his terminal, numbered tabs 1-5, plus 5-10 more on claude.ai/code in his browser. The key insight: his team shares a single CLAUDE.md checked into git, and every time Claude does something wrong, they add it as a rule — so the system compounds and gets smarter over time. He uses Opus exclusively because "since you have to steer it less, it is almost always faster than using a smaller model in the end." There's no repo to clone — it's a philosophy. Someone packaged his thread into a CLAUDE.md you can drop into any project.

**#2 — Ralph Wiggum (official Anthropic plugin, went mega-viral)**

This one is genuinely wild. It's an official Claude Code plugin that turns a single prompt into a persistent autonomous loop — Claude works for hours without human intervention. The mechanism: a Stop hook intercepts Claude's exit attempts, re-feeds the original prompt, and Claude continues — each iteration sees the modified files and git history from previous runs. Geoffrey Huntley, who invented the technique, used it to clone an Atlassian product. He says it costs about $10/hour of compute. YC hackathon teams shipped 6+ repos overnight for $297 in API costs. Boris Cherny himself uses it. Install: `/plugin install ralph-wiggum@claude-plugins-official`

**#3 — Garry Tan's gstack (the one you found)**

12.1k stars. You already know this one — eight cognitive gears, ten parallel sessions. The "founder mode vs eng mode vs ship mode" framework is the cleanest expression of the multi-brain pattern.

**#4 — Antigravity Awesome Skills (22k+ stars, the mega-library)**

A community-maintained library of 1,234+ agent skills compatible with Claude Code, Cursor, Gemini CLI, and 7 other tools. It ships curated "bundles" by role — Web Wizard, Security Engineer, etc. Install with one command: `npx antigravity-awesome-skills --claude`. This is the ecosystem play — not one person's workflow, but the collective best practices of thousands of developers.

**#5 — alirezarezvani/claude-skills (180+ skills, 4.4k stars)**

This one goes beyond coding into marketing, product, compliance, and C-level advisory. It includes pre-configured **personas** — a startup CTO, a growth marketer, a solo founder — each with curated skill loadouts and distinct communication styles. Their solo founder timeline maps out: Week 1-2 build with startup-cto + architect skills, Week 3-4 prepare with growth-marketer + copywriting + SEO, Week 5-6 ship with email-sequence + analytics. That's basically your OSA trajectory in skill form.

**#6 — OneRedOak/claude-code-workflows (Patrick Ellis, AI-native startup)**

Automated code review, design review, and security review systems — all as Claude Code workflows with YouTube tutorials. The design review uses Playwright browser automation to visually inspect UI changes. Very practical, very production-oriented.

---

**The meta-pattern across all of these:** Everyone who's shipping serious work with Claude Code has converged on the same architecture — specialized modes/personas, a compounding instruction file (CLAUDE.md or SKILL.md), and parallel sessions. You're already running this pattern across your Claude Projects. The gap is that these developers are doing it in Claude Code with version-controlled instructions that get smarter over time, while your setup lives in Project Knowledge docs that don't compound the same way.

The alirezarezvani skills repo with the growth-marketer and solo-founder personas feels like the most directly actionable one for OSA right now. And Ralph Wiggum is the "omg" one — imagine pointing it at a batch of Loud Hawk newsletter drafts or Instagram posts and letting it iterate autonomously until quality gates pass.

---

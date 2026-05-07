---
title: Anthropic recent updates and news
created: 2026-04-29T00:29:42.135291Z
updated: 2026-04-29T00:30:48.675506Z
uuid: e1bd4230-73ba-4dad-b12e-60921cdea0db
source: claude-conversation
type: source
message_count: 6
---

# Anthropic recent updates and news

*Summary: **Conversation Overview**

The person asked Claude to provide recent Anthropic news from the past day or two. Claude used web search to retrieve current information and initially provided a broad overview covering topics including Anthropic's Sydney office expansion, a major Alphabet investment, congressional cybersecurity briefings, AWS infrastructure deepening, and a brief service outage. The person indicated they wanted consumer-focused updates specifically, prompting Claude to filter and re-present only the consumer-relevant items: the service outage and the Claude Cowork availability in Amazon Bedrock.

The person then asked a single-word follow-up — "Blender?" — signaling interest in a specific topic. Claude ran another web search and delivered detailed information about Anthropic's April 28 launch of creative tool integrations, including connectors for Blender, Adobe, Ableton, Autodesk, Affinity, Resolume, SketchUp, and Splice. Claude explained the Blender MCP connector specifically, covering its capabilities for scene analysis, Python script generation, and custom tooling within Blender's interface, as well as Anthropic joining the Blender Development Fund as a Corporate Patron. Claude also offered a strategic framing of the announcement.

The person communicates concisely and expects Claude to interpret minimal prompts in context. They prefer consumer-facing news over enterprise or investment news, and respond to single-word cues to redirect or drill into specific topics.*

## Phelipe

Talk to me about all the updates of antropic today or yesterday

---

## Claude

```
This block is not supported on your current device yet.
```

Here's what's been happening with Anthropic in the last 24-48 hours:

**Sydney office + APAC expansion (Apr 27)**
Anthropic named Theo Hourmouzis as General Manager of Australia & New Zealand and officially opened its Sydney office.

**$40B Alphabet investment**
Bloomberg reported Google parent Alphabet is making a major new investment — up to $40 billion total, starting with $10 billion at a $350 billion valuation, with subsequent tranches tied to milestones. Alphabet will also dedicate 5 gigawatts of computing capacity to Anthropic. Anthropic's annualized revenue has gone from $1B at end of 2024 → $9B at end of 2025 → $30B as of early April 2026, and an IPO is reportedly being eyed for later this year.

**Congressional cyber briefings (today)**
Anthropic and OpenAI briefed House Homeland Security Committee staff in two separate classified sessions on their new cyber-capable AI models. Anthropic has held off on a public release of its Mythos Preview model due to its ability to quickly find and exploit critical security flaws, while working with federal agencies on access.

**AWS deepening (Apr 27)**
Anthropic is now training its most advanced foundation models on AWS Trainium and Graviton, co-engineering at the silicon level with Annapurna Labs. Claude Cowork also went live in Amazon Bedrock — relevant for you since Cowork is the desktop file/task automation tool.

**Outage today (Apr 28)**
Claude saw a Downdetector spike to ~3,000 reports in an hour before Anthropic pushed a fix and reports dropped under 300. Short-lived.

**Election safeguards update (Apr 24)** — separate post on the news page worth flagging if you want me to pull it.

Want me to dig into any one of these? The Alphabet deal and the Mythos cyber posture are the two with real downstream implications.

---

## Phelipe

That was something for consumers

---

## Claude

Filtering for the consumer-facing stuff from the last day or two:

**Claude outage today (Apr 28)** — Claude went down with ~3,000 Downdetector reports in an hour. Anthropic pushed a fix and reports dropped under 300. Already resolved.

**Claude Cowork now in Amazon Bedrock (Apr 27)** — Cowork is now deployable inside Amazon Bedrock environments, letting teams keep data in AWS while using Claude for team workflows. More prosumer/enterprise than pure consumer, but relevant if you're already on AWS.

That's honestly it for consumer-side news in the 24–48 hour window. The bigger consumer-relevant stuff dropped a few days earlier — Claude Design (the new Anthropic Labs tool for prototypes, slides, one-pagers) and the Claude Code quality fixes both landed around Apr 20–22 with Opus 4.7.

Want me to pull the Claude Design details or check if anything specifically rolled out to claude.ai today that I might have missed?

---

## Phelipe

Blender?

---

## Claude

```
This block is not supported on your current device yet.
```

Got it — yes, this dropped today. Here's the consumer-relevant version:

**Claude for Creative Work (Apr 28)** — Anthropic launched a coalition release with Blender, Autodesk, Adobe, Ableton, and Splice: a set of connectors letting Claude work alongside the software creative pros already use.

The nine connectors: Ableton, Adobe (50+ Creative Cloud tools including Photoshop, Premiere, Express), Affinity by Canva, Autodesk Fusion, Blender, Resolume Arena/Wire, SketchUp, Splice. All new connectors are available immediately across all Claude plans.

**On the Blender piece specifically:**

The Blender developers built an MCP connector now officially available for Claude. 3D artists can use it to analyze and debug entire Blender scenes, or build custom scripts to batch-apply changes to objects. Using Blender's Python API, the connector lets Claude add new tools directly to Blender's interface.

Practical example: a 3D artist could request a procedural wood texture with specific characteristics, and Claude would generate the corresponding Python script for Blender to run — lowering the barrier for artists who lack coding expertise but want to automate complex modeling or animation tasks.

Anthropic also joined the Blender Development Fund as a Corporate Patron, with funding dedicated to Blender core development including the Python API that makes integrations like this possible. Because the connector is built on MCP, it's accessible to other LLMs too — a reflection of Blender's commitment to open source and interoperability.

The strategic read: Anthropic is embedding Claude into existing creative tools rather than building standalone apps, positioning itself as a counterpart to Adobe's Firefly with an open-ended API strategy that could outmaneuver vertically integrated competitors.

Want me to dig into any specific connector?

---

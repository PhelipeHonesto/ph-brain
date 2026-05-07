---
title: Claude-mem plugin and database indexing
created: 2026-04-18T04:19:34.712898Z
updated: 2026-04-18T04:20:09.843019Z
uuid: fc91020e-95b6-42fb-a5fd-3a74b5056b20
source: claude-conversation
type: source
message_count: 2
---

# Claude-mem plugin and database indexing

*Summary: **Conversation Overview**

The person shared two topics with a brief, informal prompt ("Let me knwo abot this") and Claude responded with detailed breakdowns of both. The first topic was claude-mem, a Claude Code plugin hosted at the GitHub repo thedotmack/claude-mem. Claude explained how it works — using five lifecycle hooks, a background worker on port 37777, SQLite storage at `~/.claude-mem/`, and Chroma vector DB to capture and compress tool-use observations across sessions — and provided the install command. Claude connected this tool to the person's apparent existing context: they work heavily in Claude Code, have experienced cross-session continuity pain, and maintain something called an OSA-Brain vault as a manually curated knowledge system. Key projects referenced include Dumont, HAWK, and osa-route-v3. Claude advised piloting claude-mem on the Dumont repo first rather than rolling it out broadly, noting the plugin's fast iteration pace, past noise issues with semantic injection, and the persistent worker requirement.

The second topic was PageIndex versus traditional RAG retrieval, prompted by an Instagram post. Claude explained the core distinction — traditional RAG uses flat vector similarity search over document chunks, while PageIndex builds a hierarchical table-of-contents tree that an LLM navigates structurally — and assessed the framing of the original post as partially oversimplified engagement content while acknowledging the underlying insight as legitimate for structured long-form documents. Claude explicitly connected the relevance to the person's own work: they use pgvector on osa-route-v3 for aircraft registry data, charter quotes, and ADS-B records, which are short flat records where traditional vector search is appropriate. PageIndex would be more relevant for deeply structured documents like FAA FAR/AIM or NTSB reports. Claude used web search and web fetch tools during the session to verify details about the claude-mem repository.*

## Phelipe

Let me knwo abot this

---

## Claude

Two separate things here, so let me hit both.

**1. claude-mem (the GitHub repo)**

It's a Claude Code plugin that auto-captures everything Claude does in your coding sessions, compresses it with the Claude agent SDK, and injects relevant context back into future sessions. Basically persistent memory across Claude Code sessions so you don't lose context between runs.

61.6k stars / 5.1k forks is legit traction — this is a real tool people use. Worth a look given you live in Claude Code and have hit context/continuity pain before (the OSA-Brain vault is partly you solving this problem manually). Let me pull the actual repo to see how it works.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Okay, now I have the actual picture. Here's the real breakdown:

**How it works:** 5 lifecycle hooks (SessionStart → UserPromptSubmit → PostToolUse → Summary → SessionEnd) run a background worker on port 37777. It captures every tool use, compresses it with the Claude Agent SDK into "observations" (tagged as decisions, bugfixes, features, discoveries), stores them in SQLite at `~/.claude-mem/`, and injects relevant context into future sessions via MCP tools.

**Install:** `/plugin marketplace add thedotmack/claude-mem && /plugin install claude-mem` inside Claude Code.

**Honest assessment for you:** This solves a real pain you're definitely hitting — losing Dumont/HAWK/OSA-route-v3 context between Claude Code sessions. But there's meaningful overlap with your OSA-Brain vault, and claude-mem is opinionated (SQLite + Chroma vector DB + a local web viewer). A few things worth knowing before you install:

- It's moving fast (they're on v12.x with recent breaking changes)
- The semantic injection on every prompt was noisy enough they made it opt-in by default
- It runs a persistent worker service you'll need to keep alive
- Your OSA-Brain vault is curated and portable; this is automatic and tool-specific

If you try it, I'd run it on one project first (probably the Dumont repo, since that's where cross-session context hurts most) rather than wiring it into everything at once.

**2. PageIndex vs Traditional RAG (the Instagram post)**

This is a real concept, not just a hot take. The claim — RAG fails because it searches instead of navigating — is the core pitch behind PageIndex, a retrieval approach from Vectify AI. Traditional RAG chunks documents, embeds the chunks, and does similarity search. PageIndex builds a tree-structured table of contents from the document and has the LLM navigate the tree like a human would flip through a book — root node, pick the relevant branch, descend until you find the section.

The argument is that similarity search returns *semantically similar* chunks, not necessarily *correct* ones, and breaks on long documents where the right answer requires understanding document structure (legal, financial, research papers). Tree navigation preserves hierarchy.

**Honest assessment:** The framing "RAG doesn't fail because of embeddings" is oversimplified engagement-bait — RAG has lots of failure modes, and embedding quality is definitely one of them. But the underlying insight is legitimate: for structured long-form documents, reasoning over a hierarchy often beats flat vector search. It's not a RAG killer, it's a different tool for a different document shape. For your use case — aircraft registry data, charter quotes, ADS-B records — traditional vector search (what you're already doing with pgvector on osa-route-v3) is actually the right call because those are short, flat records, not nested documents. PageIndex would matter more if you were doing retrieval over, say, the full FAA FAR/AIM or long NTSB reports.

Want me to dig deeper into either one?

---

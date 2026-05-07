---
title: Evaluating Zach's OSA architecture post
created: 2026-04-23T23:05:22.202791Z
updated: 2026-04-23T23:08:02.629681Z
uuid: c8ac426c-2e54-4d86-975d-2bcc1abb0d09
source: claude-conversation
type: source
message_count: 4
---

# Evaluating Zach's OSA architecture post

## Phelipe

What we tell about this?

---

## Claude

Zach's post is directionally right but shallow, and the framing is the kind of thing that sounds smart on LinkedIn but would actively mislead you if you took it as architectural guidance for OSA.

Here's my honest read:

**What he gets right:**
- The structured-to-unstructured continuum is a useful mental model
- Complex types (STRUCT, ARRAY<STRUCT>) matter for modeling real-world entities
- Graph modeling is genuinely powerful for relationship-heavy domains

**Where it falls apart:**

The "AI is just patterns in data" framing is a data engineer's cope. It's technically true in the same way "humans are just neurons firing" is true — accurate and useless. It lets DEs feel superior without engaging with what actually makes modern AI systems work: the emergent behavior, tool use, reasoning traces, context engineering. You're living this — Dumont isn't "patterns in data," it's an orchestrator invoking typed actions against an ontology.

The Neo4j + GraphRAG recommendation is the tell. GraphRAG is trendy but it's a retrieval technique, not an architecture. For most production systems, it's overkill and operationally expensive. You already made the better call: Postgres + pgvector + tsvector hybrid search, with a relational ontology underneath. That's closer to what Palantir actually does than anything Zach is describing.

The post conflates three different problems — (1) ingesting unstructured docs, (2) modeling entities, (3) making retrieval work for LLMs — and hand-waves all three with "add more struct types and maybe a graph DB."

**What's missing entirely:**
- Entity resolution (the actual hard problem — which you're building)
- Temporal provenance (every claim needs a source and a timestamp)
- The distinction between operational ontology and analytical schema
- Context engineering as the real discipline

**The OSA-relevant takeaway:** your instinct to build ER as the foundation, with five typed entities and temporal links, is the correct version of what Zach is gesturing at. He's describing the symptom (data is messy). You're solving the disease (entities don't resolve cleanly across sources).

Don't engage with it publicly. It's a newsletter funnel post.

---

## Phelipe

So we are actually doing this unstructered data to structure

---

## Claude

Yes — and you're doing the serious version of it, not the LinkedIn version.

Let me map what you're actually doing against his framing, because it'll clarify where you are and where the real work is:

**Your unstructured → structured pipeline (already running):**

- **Claude exports → ph-brain**: raw conversation JSON → markdown → Voyage embeddings + tsvector hybrid search in Supabase. That's transcript-level unstructured data getting structured into a searchable knowledge layer.
- **FAA registry + Part 135 list → ER pipeline**: semi-structured government data → resolved entities (operators, aircraft, FBOs, airports, people) with temporal provenance. This is the hard one.
- **ADS-B tarballs → flight events**: raw position data → H3-indexed route segments → operator/tail attribution.

**Where Zach's framing actively misleads:**

He treats "unstructured" as a document-format problem (PDFs vs transcripts). The real problem in aviation data isn't format — it's that the *same entity* shows up differently across sources:

- "NetJets Aviation, Inc." in FAA registry
- "NETJETS" in ARGUS
- "Netjets" in a podcast transcript
- N612QS registered to an LLC trustee that points to NetJets operationally

No amount of STRUCT/ARRAY<STRUCT> modeling solves that. That's ER, and it's the actual moat.

**The continuum he's missing:**

His version: `rows → JSON → PDFs → transcripts`

The OSA version: `raw source → parsed records → resolved entities → temporal links → operational ontology → agent-invokable actions`

Each step is a different discipline. Zach is describing step 1→2. You're building 2→6.

**What you're actually doing that's novel:**

1. **ER as infrastructure, not a feature.** Senzing-style principle-based resolution, not ML-based similarity matching. This is what Jonas figured out 20 years ago and most people still get wrong.

2. **Temporal provenance on every link.** Operator-operates-aircraft is time-bounded. Aircraft-based-at-FBO changes. Your link entities carry `valid_from` / `valid_to`. This is invisible in his post and it's where analytical truth lives.

3. **The ontology is the product surface.** Dumont doesn't query tables — it invokes typed actions on resolved entities. That's the Palantir pattern. Zach is still in the "query your lakehouse" world.

4. **Unstructured content feeds the ontology, doesn't replace it.** Loud Hawk articles, podcast transcripts, NTSB reports all get parsed into claims that attach to existing entities with source attribution. The graph doesn't expand from the unstructured data — it gets enriched by it.

**The honest assessment of where you are:**

You're past the conceptual stage Zach is describing. Your architectural decisions (TEXT + CHECK over ENUM, ARGUS as dedup survivor, Dagster for orchestration starting Stage 3, FBOs as first-class entities) are the kind of decisions you only make after you've actually tried to build this and felt the pain.

The risk isn't that you're doing it wrong. The risk is scope — ER across 415K global tails and 25–40K US records is a real engineering project, and the temptation will be to expand the ontology before the first five entity types are rock-solid.

**What I'd watch for:**

Don't let "we should add X entity type" creep in before operators, aircraft, FBOs, airports, and people are fully resolved with clean temporal links. Every new entity type multiplies the ER complexity. The discipline is saying no to the sixth entity until the first five are boring.

---

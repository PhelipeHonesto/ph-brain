---
title: Workflow patterns in AI agents
created: 2026-04-03T14:58:34.292725Z
updated: 2026-04-03T15:04:07.790988Z
uuid: 5668fc82-e6a3-4247-8e8d-3f603a93dec8
source: claude-conversation
type: source
message_count: 6
---

# Workflow patterns in AI agents

*Summary: **Conversation Overview**

The person asked two foundational questions about AI agent workflows and who teaches the subject best, then narrowed focus to ask who could be most helpful for a specific project called the "Dumont agent." Claude explained key workflow patterns (sequential/pipeline, parallel/fan-out, router/conditional, orchestrator-worker, and human-in-the-loop) and drew a distinction between deterministic workflows and agentic workflows, noting that production systems typically blend both approaches.

When asked about top educators in the space, Claude identified Andrew Ng and DeepLearning.AI, Harrison Chase and LangGraph, Anthropic's agent pattern documentation, Sam Witteveen, Matt Berman, and Dave Shapiro as leading resources, with Andrew Ng recommended for conceptual grounding and LangGraph for implementation patterns relevant to a five-agent pipeline architecture.

For the Dumont agent question, Claude searched prior conversation context and retrieved that Dumont is OSA's client-facing charter brokerage conversational agent featuring confidence-based escalation (HIGH confidence triggers auto-send, LOW confidence triggers a hold for human approval), whisper mode, takeover capability, and Mission Control integration for visibility and learning from edits. Claude ranked Harrison Chase and LangGraph as the top resource because Dumont's architecture maps directly to LangGraph's state machine model, particularly its human-in-the-loop primitives like "interrupt before" and "interrupt after" patterns. Anthropic's agent pattern documentation was ranked second given Dumont is built on Claude and the confidence escalation model aligns with Anthropic's workflow-to-autonomous-agent spectrum. Andrew Ng was noted as foundational but less tactically relevant for Dumont's current implementation challenges.*

## Phelipe

What is workflow in agents and ai?

---

## Claude

The user is asking a general knowledge question about workflows in agents and AI. This doesn't require web search - it's a conceptual/technical topic I can answer well from my training knowledge. Given Phelipe's background building OSA's agent architecture, I can make this practical and relevant.A **workflow** in the context of AI agents is the structured sequence of steps an agent (or group of agents) follows to complete a task — essentially the "flight plan" for how work moves from input to output.

There are a few key patterns:

**Sequential / Pipeline** — Each step feeds into the next in a fixed order. This is what you're building with OSA Connect: Intake → Sourcing → Quote → Scenario → Guardian. The output of one agent becomes the input of the next.

**Parallel / Fan-out** — Multiple agents work simultaneously on different sub-tasks, then results are merged. Example: sourcing availability from three operators at once.

**Router / Conditional** — A decision node inspects the input and routes it to different paths. Think of it like an FMS routing decision — if the request is a one-way under $50K, take path A; if it's a multi-leg international trip, take path B.

**Orchestrator-Worker** — A central "conductor" agent breaks down a complex task, delegates sub-tasks to specialized workers, then synthesizes results. Your Mission Control dashboard is essentially the human-facing view of this pattern.

**Human-in-the-Loop** — The workflow pauses at defined checkpoints for human review before proceeding. In your architecture, this is where *you* as the broker confirm or override before a quote goes to the client.

The big distinction in practice is **agentic workflows** (where the AI decides which tools to call and in what order at runtime) versus **deterministic workflows** (where the sequence is hardcoded and the AI just executes each step). Most production systems — including what you're building — are a hybrid: deterministic pipeline structure with agentic decision-making *within* each node.

The reason workflows matter so much is reliability. A single monolithic prompt trying to do everything is fragile. Breaking it into discrete, testable steps — each with clear inputs, outputs, and guardrails — is what makes the difference between a demo and something you'd trust with real money moving through it.

---

## Phelipe

Who teachs this the best?

---

## Claude

The user is asking who teaches AI agents and workflows the best. Let me think about the prominent educators/creators in this space.Here are the go-to names, depending on how you learn best:

**Andrew Ng** — His DeepLearning.AI courses are the gold standard. He has a specific "AI Agentic Workflows" series that breaks down the design patterns (reflection, tool use, planning, multi-agent). Free on YouTube, deeper content on Coursera.

**Harrison Chase** — CEO of LangChain/LangGraph. His talks and tutorials are very hands-on and practical for building agent pipelines. LangGraph specifically is built around the workflow patterns (nodes, edges, conditional routing) that map closely to what you're doing with OSA Connect.

**Anthropic's own cookbook** — The agent patterns documentation from Anthropic is one of the clearest technical breakdowns out there. It distinguishes workflows (predetermined paths) from agents (model-driven decisions), which is a useful mental model.

**Sam Witteveen** — YouTube channel that's very builder-focused. Walks through multi-agent architectures step by step with real code.

**Matt Berman** — Good for staying current on the latest agent frameworks and tools. More breadth than depth, but useful for knowing what's out there.

**Dave Shapiro** — Deeper philosophical and architectural thinking about autonomous agents, memory systems, and cognitive architectures. Closer to the SAFLA-style thinking you've explored.

If I had to pick one starting point for where you are right now — building a real production pipeline, not just learning theory — I'd say **Andrew Ng's agentic design patterns talks** for the conceptual framework, then **LangGraph's docs** for the implementation patterns. Ng gives you the "why," LangGraph gives you the "how" in a way that maps directly to your five-agent pipeline.

---

## Phelipe

Who can dd the most for our dumont agent?

---

## Claude

The user is asking "Who can do the most for our dumont agent?" - I need to figure out what "dumont" refers to. This isn't something I've seen in the memory context. Let me search past conversations to see if there's a "dumont" agent or project referenced.I don't have context on a "dumont agent" — that's not something I'm seeing in our past conversations. Let me check if we've discussed it before.
```
This block is not supported on your current device yet.
```

Now I have context. Dumont is OSA's AI agent — the client-facing charter brokerage agent. It's a single agent (not the five-agent pipeline) that handles client intake, qualification, engagement, and deal flow through a chat interface, with confidence-based escalation to Phelipe.

The question is "Who can do the most for our Dumont agent?" — meaning which of the people/resources I mentioned in my previous message about AI agent workflow teachers would be most helpful for building Dumont.

Let me think about this given what Dumont is:
- A client-facing conversational agent
- With confidence-based auto-send/hold escalation


- Operating in charter aviation with deep domain specificity
- Connected to Mission Control for visibility and learning from Phelipe's corrections over time
- Driving the full funnel from qualification through engagement to close

So I'm really looking for whoever has the strongest track record building production conversational systems that blend domain expertise with human feedback loops and know when to hand off to a human.Got it — Dumont, your client-facing charter brokerage agent with the confidence escalation model and Mission Control integration.

Given what Dumont actually is — a domain-expert conversational agent with human-in-the-loop, confidence-based autonomy, and learning from your edits — here's my ranking:

**Harrison Chase / LangGraph — #1 pick.** Dumont's architecture (confidence routing, human intercept, whisper mode, graduated autonomy) maps almost perfectly to LangGraph's state machine model. Nodes for qualification, sourcing, engagement. Conditional edges for confidence thresholds. Human-in-the-loop as a first-class primitive, not a bolted-on feature. His tutorials on "interrupt before" and "interrupt after" patterns are basically your 10-second delay and approval hold.

**Anthropic's agent patterns docs — #2.** Dumont is the textbook case of their "workflow with agentic nodes" pattern. The confidence escalation model (HIGH → auto-send, LOW → hold for approval) is exactly the spectrum they describe between deterministic workflows and fully autonomous agents. Plus, if you're building on Claude, their tool-use and structured output patterns are directly applicable to Dumont's intent classification and natural language parsing.

**Andrew Ng — foundational but less tactical.** Great for understanding *why* Dumont's architecture works (reflection, planning, tool use patterns), but less useful for the specific implementation challenges you'll hit — like managing conversation state across the confidence tiers or learning from your edit distance.

For where Dumont is right now, I'd spend time in **LangGraph's human-in-the-loop tutorials** first. That's the closest thing to a blueprint for the confidence escalation + whisper + takeover model you've already designed.

---

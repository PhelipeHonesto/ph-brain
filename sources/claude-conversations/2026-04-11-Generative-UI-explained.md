---
title: Generative UI explained
created: 2026-04-11T10:32:50.736257Z
updated: 2026-04-11T11:46:15.222226Z
uuid: c5bc9780-27a6-4db1-9dea-9be1b7631187
source: claude-conversation
type: source
message_count: 22
---

# Generative UI explained

## Phelipe

what is generative UI

---

## Claude

Brief answer.Generative UI is a pattern where an LLM dynamically produces user interface components — not just text — as part of its response. Instead of returning plain text that a frontend then renders in a chat bubble, the model outputs structured data (or actual code) that gets rendered as rich, interactive UI elements inline.

A few key ideas:

**How it works:** The model decides, based on context, to return a specific UI component (a chart, a form, a map, a card, a table) rather than describing it in words. The frontend has a registry of components and renders whatever the model specifies.

**Why it matters:** It closes the gap between "the AI knows the answer" and "the user can act on it." Instead of saying "here are 3 flights," it renders a sortable flight comparison card with booking buttons.

**Common implementations:** Vercel's AI SDK popularized this with React Server Components streamed from the model. The model calls a tool like `show_flight_results`, and the framework renders the corresponding React component. What you're seeing in this very conversation — weather widgets, maps, recipes, charts — is essentially generative UI.

**Distinction from chat + markdown:** Traditional chatbots return markdown that gets styled. Generative UI means the model is selecting and parameterizing real interactive components, not just formatting text.

It's becoming a core pattern for AI-native products because it lets the interface adapt to the task rather than forcing every answer through the same text box.

---

## Phelipe

how hard is to implement?

---

## Claude

Brief answer about implementation difficulty.It depends on how far you take it, but the core pattern isn't that hard — it's mostly a mapping problem.

**Simple version (a weekend):** Define a set of components (card, table, chart, etc.), have the model call tools that map to those components, render based on the tool name and parameters. This is basically what Vercel's AI SDK does. If you're already using function calling, you're 80% there — you just render a component instead of displaying the JSON.

**The hard parts:**

- **Streaming.** You want the UI to appear progressively, not flash in after the full response. Streaming structured tool call arguments while rendering partial components is fiddly.

- **State management.** Once the user interacts with a generated component (filters a table, clicks a button), you need to decide: does that trigger a new LLM call? Update local state? Both? This is where complexity explodes.

- **Component design.** The model needs to be able to parameterize your components reliably. If your component has 20 props with complex validation, the model will get it wrong. Simpler components with forgiving schemas work best.

- **Fallbacks.** The model will sometimes produce malformed output. You need graceful degradation — show the raw data or a text summary instead of crashing.

**Stack-wise**, the most common approach right now is React + Vercel AI SDK + tool calling, but you can do it with any framework. The pattern is framework-agnostic: model emits structured output → frontend maps it to a component → render.

If you're building something like this for OSA Connect, the Dumont agent already uses tool calling — so you'd essentially be adding a frontend rendering layer that maps agent actions to branded UI components instead of raw text responses. The architecture fits naturally.

---

## Phelipe

who is winning on this ?

---

## Claude

The user is asking who's winning in the generative UI space.
```
This block is not supported on your current device yet.
```

Clear picture.The space is consolidating fast. Here's the landscape:

**Google** is making the biggest push. They just shipped "dynamic view" in the Gemini app and generative UI in AI Mode in Google Search, where the model designs and codes a fully customized interactive response for each prompt. They also created **A2UI**, a declarative JSON spec that's framework- and platform-agnostic — works across React, Flutter, SwiftUI, Angular.

**CopilotKit** (open source) is winning the developer tooling layer. For most React projects, the recommendation is to start with CopilotKit or assistant-ui. They've built the **AG-UI protocol** (agent ↔ frontend communication) and have integrations with Google's A2UI, MCP Apps, and AWS AgentCore. They're the connective tissue right now.

**Vercel** pioneered the pattern with their AI SDK + React Server Components approach — still widely used but less talked about as the protocol layer matures beyond just "stream tool calls to React."

**assistant-ui** (YC W25) is the most popular open-source UI library for AI chat with 50k+ monthly downloads.

**Emerging standards:** Three protocols are converging — AG-UI for the runtime layer, A2UI/Open-JSON-UI for declarative specs, and MCP Apps for open-ended UI surfaces. The fact that Google, Oracle, AWS, and CopilotKit are all aligning around these suggests we're past the "competing standards" phase.

**Bottom line:** Google owns the research and the biggest consumer deployment. CopilotKit owns the open-source developer experience. Everyone else is adopting the protocols those two are setting. If you're building on this for Dumont's client-facing layer, CopilotKit + AG-UI is probably the most natural fit given you're already in TypeScript/React territory.

---

## Phelipe

who is doing it right

---

## Claude

The user wants to know who's executing generative UI well in practice.Honestly? Almost nobody yet. The tooling is ahead of the implementations.

**Claude.ai itself** is probably the best live example right now. What you're seeing in this conversation — maps, weather widgets, recipes, charts, sports scores — is exactly the pattern done well. The model picks the right component based on context, the UI renders inline, and it feels natural rather than forced. Anthropic doesn't call it "generative UI" but that's what it is.

**Google Gemini** just shipped dynamic view but early reports suggest it over-generates — it builds a whole interactive webpage when you just wanted a paragraph. The tech is impressive, the judgment of *when* to use it is still off.

**ChatGPT** has Canvas and some inline rendering but it still feels like "chat with occasional widgets bolted on" rather than a unified experience. The components don't feel native to the conversation flow.

**Perplexity** does a subtle version well — the answer cards, source panels, and follow-up suggestions are essentially generative UI, just not marketed that way. They nail the "minimum viable richness" principle.

**What "doing it right" actually means:**

The mistake most people make is treating generative UI as "make everything interactive." The real skill is restraint — knowing when a paragraph is better than a widget. The best implementations are the ones where you don't notice it's happening. You asked about weather, you got weather. You didn't get a loading spinner, a modal, and a "would you like to see this as a chart?" confirmation dialog.

For OSA Connect, this is actually a strategic advantage. Your quote delivery doesn't need to be a chat message — it should be a branded, interactive quote card with a validity countdown, aircraft details, route map, and a "confirm hold" button. That's generative UI applied to a real workflow, not a demo. Most startups in this space are building demos. You'd be building a deal engine that happens to use the pattern.

---

## Phelipe

I am not understanding yet. Is that personalization?

---

## Claude

He's asking if generative UI is the same as personalization. Let me clarify the distinction simply.No, they're different things that people confuse because they can overlap.

**Personalization** = showing different *content* to different people. "Welcome back Phelipe, here are flights you might like based on your history." The UI is the same template, the data changes.

**Generative UI** = showing different *interfaces* based on the task. The model decides the user needs a map right now, not a list. Or a comparison table instead of paragraphs. The structure itself changes, not just what fills it.

Think of it this way:

A traditional app has 50 pre-built screens. Personalization picks which screen to show you and what data to fill in. Generative UI means there are no pre-built screens — the AI assembles the right interface on the fly from components.

**A concrete example for OSA:**

Personalization: "Here's your quote, Phelipe, and since you usually fly out of Chicago, we pre-filled MDW."

Generative UI: Client A asks for a simple one-way — Dumont returns a clean single quote card. Client B asks for a complex multi-leg with flexible dates — Dumont returns a scenario comparison table with three routing options, cost breakdowns, and a map showing positioning legs. Same system, different interface, because the *task* was different.

The AI isn't just choosing what data to show — it's choosing *what kind of UI* to show it in.

Does that click?

---

## Phelipe

The problem is hallucinations

---

## Claude

He's pointing out the core problem with generative UI - if the LLM generates the UI, it can hallucinate components, pass wrong props, generate broken layouts, etc.Yeah, that's the real blocker. And it's why the "fully generated" approach (model writes raw HTML/React on the fly) is mostly a demo trick, not production-ready.

The solution everyone's converging on is **constrained generation** — the model doesn't *create* UI, it *selects* from a fixed catalog of components and fills in parameters. It's basically tool calling.

The model can't hallucinate a component that doesn't exist. It can only say "show quote_card with these fields." If the fields are wrong, you validate the schema and fall back gracefully. Same pattern you're already building with Dumont's tool calls.

**Where hallucination still bites:**

- Wrong component for the context (shows a map when it should show a table)
- Bad parameter values (wrong aircraft type, wrong price in the wrong field)
- Missing required fields

But those are the *exact same risks* you already manage in any LLM tool-calling pipeline. Guardian already validates mission parameters — it would validate UI parameters the same way.

**The insight:** Generative UI isn't really a new hallucination problem. It's the same hallucination problem you already have with agent actions, just applied to the presentation layer. If you trust Dumont to call an operator with the right parameters, you can trust it to render a quote card with those same parameters.

The trick is never letting the model freestyle. Catalog of components, strict schemas, validation layer. Boring answer, but that's what works.

---

## Phelipe

Can this be done at route pages?

---

## Claude

Phelipe is asking about using generative UI on OSA's route pages - the programmatic SEO pages for charter routes.Yes, and this is actually where it gets interesting for you.

Right now your route pages are static programmatic SEO pages — same template, different route data. That's the Paramount Business Jets playbook. But once someone *lands* on that page, the experience is identical whether they're a first-time browser or a repeat client ready to book.

**What generative UI on route pages looks like:**

Anonymous visitor lands on Chicago → Teterboro: they see the standard SEO content, Cost Anatomy breakdown, Charter Index estimate, and a simple "Get a Quote" CTA. That's the static version — good for Google, good for first impressions.

But the moment they interact — type a date, ask a question, click "get a quote" — Dumont takes over and the page *transforms*. The quote form becomes an intake conversation. The Cost Anatomy updates with real numbers. Available aircraft options render as cards. A map shows positioning legs. The page goes from content to transaction without a redirect.

**Why this is a moat:**

Every competitor's route page is a dead end — read some content, fill out a form, wait for a callback. Your route page becomes the *deal engine itself*. The SEO page is the top of funnel, and generative UI is what converts it without friction.

**The hallucination concern is minimal here** because the static SEO content is pre-built, and the dynamic layer is just Dumont doing what it already does — intake, quote, scenario — rendered as components instead of chat messages.

The hard part isn't the tech. It's making sure Google still sees a crawlable static page while users get the dynamic experience. But that's a solved problem — server-side render the static content, hydrate the interactive layer client-side.

This is basically your "route page is the product" thesis taken to its logical end.

---

## Phelipe

Any website is doing that?

---

## Claude

The user is asking if any website is currently implementing generative UI on their pages (not just chat interfaces).
```
This block is not supported on your current device yet.
```

The search results are mostly about AI landing page generators, not about websites that use generative UI on their actual pages (where the page transforms based on user interaction). Let me give a direct answer.Not really. Not the way I described it for your route pages.

What exists today is mostly two separate worlds:

**AI-generated landing pages** — tools like Figma Make, Unbounce, Sitekick that use AI to *build* the page. But once it's built, it's static. The AI is in the design process, not in the live user experience.

**Chat widgets embedded on pages** — Intercom, Drift, etc. slap a chatbot in the corner of a normal page. But the page itself doesn't change. The chat and the page are two disconnected experiences.

Some companies are generating dynamic landing pages that change tone and imagery based on who clicks the link, and edge computing now enables personalization decisions before the page even loads — but that's still just personalization (different content, same UI structure).

**Nobody is doing what I described** — a static SEO page that morphs into a transactional interface when the user engages, with an AI agent assembling the UI components in real time based on the complexity of the request.

That's the gap. And honestly, it's a gap because most companies either sell content pages OR sell agent experiences. Almost nobody is thinking about the page *as* the agent interface.

For OSA, this means you'd be genuinely first. Your route page starts as Paramount Business Jets (SEO content), and transforms into something nobody else has — the deal engine embedded in the page itself. That's not a feature, that's a category-defining UX pattern.

The closest comp might be how Zillow pages work — you browse listings (content), then the page seamlessly transitions into scheduling, mortgage calculators, and agent contact. But even Zillow doesn't have an AI assembling the interface dynamically. You'd be Zillow meets generative UI.

---

## Phelipe

What is design engineering?

---

## Claude

Simple knowledge question.Design engineering is a role that sits at the intersection of design and frontend development — someone who can both *design* an interface and *build* it in production code. Not a designer who hands off to engineers, not an engineer who implements someone else's mockups. One person, end to end.

The role got popularized by Vercel (Rauno Freiberg), Linear, and Stripe — companies known for obsessively polished UI. The idea is that the best interfaces come from people who think in both design and code simultaneously, because the handoff between designer and developer is where quality degrades.

**What they actually do:**

- Build interactive prototypes that *are* the production code
- Own micro-interactions, animations, transitions — the details that make UI feel alive
- Make design decisions in the browser, not in Figma
- Bridge the gap between "this looks right" and "this feels right"

**Why it matters now:** With AI generating more and more boilerplate UI, the differentiator is craft — the feel, the polish, the moments of delight. Design engineers are the people who create that. AI can generate a functional form; a design engineer makes it feel like the product *cares*.

For context on why you might be hearing about it — it's becoming the most sought-after profile at early-stage startups because one design engineer replaces a designer + frontend dev, ships faster, and produces higher quality output. Exactly the kind of hire that fits a four-person pre-seed team.

---

## Phelipe

This people are good?

---

## Claude

The user is showing a list of design engineers. Let me give a quick take.Yeah, this is basically the all-star list. A few standouts:

**Rauno Freiberg** — design engineer at Vercel, arguably the person who made the role mainstream. His personal site is a masterclass in craft and interaction design.

**Paco Coursey** — also Vercel. Built the dark mode toggle that every developer copied. Obsessive attention to detail.

**Dan Hollick** — known for incredible educational threads on color, typography, and animation. Makes complex design concepts accessible.

**SJ Zhang** — does beautiful generative/creative coding work.

**Liam Matteson** — strong interactive/3D work.

**Robert Pavlinić** — polished product UI work.

**Thariq Shihipar** — was at Stripe, known for data visualization and interactive explanations.

This looks like it's from the Design Engineer Club resource page. It's a legit curated list — these are the people whose portfolios you'd study to understand what "craft" means in frontend.

The reason this list matters for you: when you eventually hire a CTO or frontend person, you want someone who at least *appreciates* this level of polish, even if they're not at this level. The OSA Connect client experience — the quote cards, the route pages, the Cost Anatomy breakdowns — that's where design engineering separates you from every broker running a WordPress site with a contact form.

Worth bookmarking a few of their portfolios as design references for the OSA brand.

---

## Phelipe

Can we build our website from their style with claude code?

---

## Claude

He's asking if Claude Code can build an OSA website inspired by these design engineers' styles.Yes, absolutely. Claude Code is how you're already building Dumont, so the toolchain fits.

But let me be direct about what's realistic:

**What Claude Code can do well:**
- Build a clean, polished Next.js/React site with smooth animations (Framer Motion), good typography, and responsive layouts
- Implement specific interaction patterns you reference from these portfolios ("make the quote card animate like Rauno's site")
- Ship fast — you could have a production-quality marketing site in a few focused sessions

**What it won't do:**
- Originate the *taste*. These design engineers spend years developing an eye. Claude Code executes, it doesn't have design intuition. You need to be the creative director — pointing at specific references, saying "this feel, not that feel"

**The practical approach:**

1. Pick 3-4 portfolio sites from that list as references
2. Screenshot the specific elements you like — transitions, typography, spacing, hover states
3. Feed those to Claude Code with your brand system (OSA Orange, Near Black, Cream)
4. Build component by component, not page by page

The sites from that list that would translate best to OSA's brand positioning (premium, transparent, confident) are probably Rauno's minimalism, Paco's attention to micro-interactions, and Stripe's layout philosophy.

The real question is timing. You're 10 days from OSA Connect launch. Is the current site good enough to launch with, and this becomes a post-launch polish sprint? Or is the website blocking conversion right now?

---

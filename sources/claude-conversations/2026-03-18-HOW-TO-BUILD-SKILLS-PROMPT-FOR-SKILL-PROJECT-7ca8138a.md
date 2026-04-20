---
title: HOW TO BUILD SKILLS. PROMPT FOR SKILL PROJECT
created: 2026-03-18T23:13:39.660060Z
updated: 2026-03-19T02:29:13.736042Z
uuid: 7ca8138a-a1f2-40a5-9338-5d5b821cab47
source: claude-conversation
type: source
message_count: 42
---

# HOW TO BUILD SKILLS. PROMPT FOR SKILL PROJECT

## Phelipe

what is dispatch in claude. i have that option on my mobile

---

## Claude

```
This block is not supported on your current device yet.
```

Dispatch just launched yesterday as a research preview. It's a feature within Claude Cowork that turns your phone into a remote control for Claude running on your desktop.

Here's the idea: you pair the Claude mobile app with the Claude Desktop app on your Mac (or Windows machine) via a QR code, and it creates a single persistent conversation between the two devices. You send tasks from your phone, and Claude processes them on your computer — accessing local files, connected apps, browser, and plugins — all in a sandbox. You can fire off a task while you're away from your desk and come back to finished work.

A few practical things to know:

Your Mac has to be awake with the Claude app open for it to work. It's a remote control, not cloud computing — if you close the lid, Dispatch goes dark.

It's currently rolling out to Max subscribers, with Pro users getting access within a few days.

Early testing shows it's solid for finding files and summarizing data on your machine, but more complex tasks are roughly 50/50 on the first try. It's still a research preview, so expect rough edges.

For your OSA workflow, this could be interesting once it matures — imagine kicking off a Loud Hawk research task or having Claude compile operator data from your desktop files while you're at the airport between legs. Worth pairing up and experimenting with during your build sprint this week.

---

## Phelipe

this is literally the open claw right? haha

---

## Claude

Pretty much, yeah. OpenClaw required a dedicated server, Node.js 22+, a WebSocket gateway, and extensive configuration — Dispatch needs none of that. Same concept, just Anthropic packaging it natively so you scan a QR code and you're done.

The timing is funny too — the community builds the janky-but-functional version, proves the demand, and then Anthropic ships the polished first-party version that makes it obsolete. Tale as old as time in tech.

The real question is whether Dispatch will eventually be reliable enough for actual production workflows or if it stays a "cool demo" for a while. That 50/50 success rate on complex tasks isn't exactly something you'd want to bet an OSA operator outreach sequence on. But for kicking off research or pulling files while you're sitting reserve at O'Hare, it's a solid start.

---

## Phelipe

i can see it. this perfect... since open ai bought open claw. makes sense they are making something that will be more secure and useful.
specilly because come on open claw is open source. so so easy to mimic.

---

## Claude

Wait, OpenAI bought OpenClaw? I hadn't seen that. Let me check.
```
This block is not supported on your current device yet.
```

Oh yeah, you're right. Sam Altman announced the acquisition on February 15, with Steinberger joining OpenAI to lead next-gen personal agents, while OpenClaw itself moved to an independent foundation with OpenAI as a sponsor.

And the backstory is wild. The project originally started as "ClawdBot" — literally named after Claude — and Anthropic's lawyers sent a trademark cease-and-desist, which may have been the catalyst that pushed Steinberger toward their biggest competitor. So Anthropic's legal team basically gift-wrapped a key hire for OpenAI. That's painful.

Your point about open source is spot on. The gap between what's possible in open-source experimentation and what's deployable in an enterprise or secure setting is significant — OpenClaw's power came precisely from the lack of guardrails that would be unacceptable in a corporate environment. Anyone could fork it, study how it works, and build their own version. So Anthropic building Dispatch as a native, sandboxed, zero-config alternative is the smart play — you get the same workflow but with proper security boundaries baked in from day one.

For someone like you running a one-person operation across multiple workstreams, Dispatch is probably more practical anyway. No Docker setup, no API keys, no gateway config. Just scan and go.

---

## Phelipe

i think was so dumb sam altiman buying it... but okay.
i need to learn about agents

---

## Claude

Yeah, the acqui-hire logic is debatable. They basically paid for one developer and a brand that's going to an independent foundation anyway. But OpenAI was bleeding enterprise share to Anthropic and needed to signal they're serious about agents, so it was partly a PR move.

On learning about agents though — what angle are you coming at this from? Because "agents" means different things depending on what you're trying to do with the knowledge.
```
This block is not supported on your current device yet.
```

---

## Phelipe

Q: What's your main goal for learning about agents?
A: All of the above

---

## Claude

Makes sense — you're wearing both hats. Pilot who needs to ship stuff now with agent tools, and founder who needs to understand where the industry is heading so OSA is positioned right.

Let me put together a solid primer that covers all three angles. Give me a sec.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Alright, let me build you a proper guide — something you can reference during and after the sprint. I'll make it practical and tied to where you are with OSA.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's your primer. Seven sections covering the concept, the landscape, the tools you already have, the vocabulary, and a practical OSA roadmap for where to go next.

The key takeaway: you're already doing agent work with your Skills setup in Claude Code, you just haven't been framing it that way. The progression from here is straightforward: Dispatch for async tasks this week, MCP connectors once OSA Connect is deployed, then custom agent workflows via the Agent SDK as you scale.

---

## Phelipe

i use claude chat.
but what is claude cowork ? 
i know claude code is the coding brain .

---

## Claude

```
This block is not supported on your current device yet.
```

Good question. Here's the simple framework:

**Claude Chat** (what you use here) is for conversation. You ask, Claude answers. Back and forth.

**Claude Code** is the terminal agent for developers. It reads your codebase, writes files, runs commands, iterates. You're already using this for OSA with your Skills setup.

**Claude Cowork** is basically Claude Code's agentic capabilities, but for everyone. It's built on the exact same architecture, just wrapped in a visual interface instead of a terminal. It lives as a tab inside the Claude Desktop app alongside Chat and Code.

The key difference from Chat: in Cowork, you give Claude access to a folder on your computer, and Claude can then read, edit, or create files in that folder. You describe an outcome, Claude makes a plan, and it executes autonomously while you step away. It can reorganize your downloads, create spreadsheets from receipt screenshots, or produce a first draft of a report from scattered notes.

Think of it this way: Chat = conversation. Code = terminal power. Cowork = the easiest agent for everyday desktop work.

A few things worth knowing for your situation: Cowork also supports scheduled tasks, so Claude can complete work automatically on a recurring basis, which is something you can't do from Chat. It also connects to external services through connectors (Slack, Notion, Figma, etc.) and can browse the web via Claude in Chrome.

It's available on all paid plans as a research preview, and it uses more of your usage allocation than regular chat since the multi-step tasks are compute-heavy.

For your OSA workflow, Cowork could be useful for things like batch-processing operator research into organized folders, extracting data from screenshots or PDFs into spreadsheets, or scheduling a recurring task that compiles aviation news for Loud Hawk. And Dispatch is just the remote control layer on top of it, so you can trigger all that from your phone.

You'd need to download the Claude Desktop app to access it. It's a separate tab from Chat and Code inside that app.

---

## Phelipe

go it. i use a lot of claude code in this way so i think the cowork interface is easier but we are already using on warp with claude

---

## Claude

Exactly. You're already getting the same agentic behavior through Warp + Claude Code. Cowork is just the GUI version of what you're doing in terminal. If you're comfortable in Warp and your Skills are already wired up there, there's not a huge reason to switch workflows mid-sprint.

Where Cowork might add value for you is the stuff that's awkward in terminal: organizing files visually, scheduling recurring tasks without cron jobs, or handing off non-code tasks (like "sort through 30 operator PDFs and extract fleet info into a spreadsheet") where the visual interface is just faster to set up. And Dispatch only works through Cowork, so if you want to kick off tasks from your phone while flying, that's the path.

But honestly, for where you are right now with the Supabase migration, OSA Connect build, and Loud Hawk content production, Warp + Claude Code + your Skills is the sharper tool. Cowork is more of a "nice to have on the side" for the non-code operational stuff.

The real unlock for you later is when you can run Claude Code for the build work AND Cowork for the business ops stuff simultaneously. Two agents, different jobs, same machine.

---

## Phelipe

great.
now lets talk about agents.
how to build a agent. 
we need to clarefy and understand what is .
people use so mucho r the work the is getting confused.

---

## Claude

You're right, the word "agent" has become one of those terms that means everything and nothing at the same time. Let me break it down clearly.

At its core, an agent is just three things working together:

**A model** (Claude, GPT, whatever) that can reason about what to do next. **Tools** it can call (search the web, read a file, send an email, hit an API). **A loop** where it acts, checks the result, and decides whether to keep going or stop.

That's it. Everything else is marketing.

Here's where the confusion comes from: people are calling very different things "agents."

When you run a Claude Code skill in Warp and it reads files, writes code, runs it, sees an error, fixes it, and runs again... that's an agent. When someone builds a Python script using the Claude API that monitors aviation news and drafts newsletter content... that's also an agent. When OpenClaw controls your whole computer, clicking buttons and booking flights... also an agent. Same concept, wildly different complexity.

Let me build you something that cuts through the noise and shows you exactly how to build one, starting simple and scaling up.
```
This block is not supported on your current device yet.
```

---

## Phelipe

Q: Where do you want to start learning to build agents?
A: Start from the very basics, assume I know nothing

---

## Claude

Perfect. Clean slate. Let me build this from the ground up, no assumptions.
```
This block is not supported on your current device yet.
```

Let me build this as a step-by-step interactive explainer that starts from zero.
```
This block is not supported on your current device yet.
```

Walk through those four steps. Each one builds on the last.

The punchline is step 4: you're already running agents. Every time you use Claude Code in Warp with your Skills, that's the full agent pattern: model (Claude) + tools (file system, bash, code execution) + loop (write, run, check, fix, repeat).

The confusion in the industry comes from people using "agent" to describe wildly different levels of complexity. A Claude Code session organizing your files? Agent. A multi-system pipeline that monitors aviation news, drafts content, and publishes to Beehiiv automatically? Also agent. Same three ingredients, different scale.

Once this clicks, the next question is how to build your own from scratch. Want to go there?

---

## Phelipe

Now show me how to actually build one step by step

---

## Claude

Alright, let's build one. But first, let me make sure we're on the same page about the path.

There are different ways to build agents depending on your technical comfort and what you're trying to accomplish:
```
This block is not supported on your current device yet.
```

---

## Phelipe

Q: Which approach fits where you are right now?
A: Show me all three so I understand the spectrum

---

## Claude

Good call. Let me walk you through the same agent built three different ways, from zero code to full SDK. I'll use an OSA-relevant example so it's practical, not theoretical.

The agent we'll build: **an operator research agent** that takes a state (like "Texas"), finds Part 135 operators there, and compiles the results into a structured file.

Same goal, three levels of complexity.
```
This block is not supported on your current device yet.
```

Click through all three levels. Here's the key insight across all of them:

**Level 1 (no-code)** is a SKILL.md file. You already build these. Claude Code handles the loop, the tool calls, everything. You just write instructions in markdown. This is where you should start for any new agent idea.

**Level 2 (low-code)** is a Python script with a `while True` loop around an API call. Claude decides whether to use a tool or stop. You feed tool results back in. That's the entire pattern. An agent is literally a while loop around an API call.

**Level 3 (full SDK)** is the same thing but Anthropic handles the loop, error recovery, MCP connections, and sub-agent spawning for you. This is where you'd go for production infrastructure down the line.

The honest recommendation for where you are in the sprint: Level 1 gets you 80% of the value at 5% of the complexity. You could build an operator research skill tonight and run it from Warp. Level 2 and 3 are for when you're deploying OSA Connect as a standalone app and want agents running in the background without you in the terminal.

Want to actually build that operator research skill right now, or do you want to dig deeper into any of these levels first?

---

## Phelipe

ALL BLACK

---

## Claude

Ha, yeah that's the dark mode rendering issue. The content is there but the text is blending into the background. Let me scroll you down — you need to click on the "Level 1: No-code" button at the top to load the content into the panel below it.

But if it's still showing all black text on dark background, that's a rendering bug with the widget. Let me just give you the three levels as a clean file instead so nothing gets lost.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Sorry about the dark mode issue on the widget. Here's the full guide as a proper file that'll render clean.

The three levels in short:

**Level 1** is a SKILL.md file. You write markdown instructions, Claude Code runs the loop. This is what you do already for Loud Hawk. You could build the operator research skill tonight.

**Level 2** is a Python script with a while loop around an API call. That one sentence is the entire concept. Claude decides to use a tool or stop, you feed results back. Use this when you want agents running on a schedule without you in the terminal.

**Level 3** is the Claude Agent SDK. Same idea but Anthropic handles the loop, error recovery, MCP auto-discovery, and sub-agents. This is Q3+ territory for you, when you're building the multi-agent OSA system.

The comparison table at the bottom lays out exactly when each level makes sense. Start with Level 1, graduate when you hit its limits.

---

## Phelipe

i am almost getting but not fully yet...
so lets recap:
we have chatbot -> give me an answer input - output.
Tools is when the llm handle something -> web search, google drive, email etc..
Loop is when this is scripted in ( Md files, lines of codes, etc...)
when is loop and have guidelines it becomes an agents ( almost like a replicable action) and the level are:
just one guideline which is no code.
level 2 is a script that have  triggers to loops the action like going to faa website or news sites to keep feeding a documnet or database
and level 3 is almost an orchestra of multi agentes.
like going to operator , checking news, email sequency et...

---

## Claude

You're almost there. Let me tighten up the one part that's slightly off and confirm everything else.

Your understanding of chatbot and tools is perfect. No corrections needed.

The loop part needs a small adjustment. The loop isn't the script or the SKILL.md file itself. The loop is the **decision-making cycle** that Claude runs through. Here's the distinction:

The SKILL.md file (or the Python script, or the SDK code) gives Claude the **goal and the rules**. But the loop is what Claude does *at runtime*: it takes an action, looks at the result, and decides "am I done or do I need to do more?" That decision-making is the loop, and Claude does it on its own. You don't script each step, you set the goal and Claude figures out the steps.

Think of it like flying. The SKILL.md is like an approach plate. It tells you what to do. But the actual flying, adjusting for wind, going around if the runway isn't clear, that's you making decisions in the moment. The approach plate is the instructions. The pilot decision-making is the loop.

So when you write a skill that says "search for operators, compile the data, save the file," Claude might search, find nothing useful, decide to try a different search query, find some results, realize it's missing fleet data, search again for that specifically, then compile. You didn't script those extra searches. Claude decided it needed them. That's the loop.

Now your level breakdown is really close. Let me refine:

**Level 1** is a SKILL.md with the goal and guidelines. Claude Code handles the loop automatically. No code from you.

**Level 2** is correct. A Python script where you write the while loop yourself and can add triggers like cron jobs, webhooks, or scheduled runs. The key addition is that it runs **without you being in the terminal**.

**Level 3** you nailed. Multiple agents coordinating. One researches operators, one monitors news, one runs email sequences. The SDK handles the orchestration between them.

Does the loop distinction click now? The instructions are the plan. The loop is Claude executing, evaluating, and adapting in real time.

---

## Phelipe

so the loop in level 1 is claude.
loop in level to is coded?

---

## Phelipe

so the loop in level 1 is claude.
loop in level 2 to is coded?

---

## Claude

Yes. That's exactly it.

**Level 1:** Claude IS the loop. You give it the goal in a SKILL.md, and Claude decides on its own: "I searched, didn't find enough, let me try a different query." You never wrote that retry logic. Claude just does it because it's reasoning through the problem.

**Level 2:** You CODE the loop. That `while True` in the Python script is you explicitly saying "keep going until Claude says it's done." You're the one writing the logic that feeds tool results back to Claude and checks if it's finished. Claude still reasons inside each turn, but the *mechanism* that keeps the cycle running is your code.

**Level 3:** The SDK IS the loop (like Level 1, but more powerful). You hand the SDK a goal and it manages the cycle for you, plus it can spawn sub-agents, recover from errors, and connect to MCP tools automatically. You're back to not writing the loop yourself, but now with production-grade infrastructure under it.

So the pattern is:

Level 1: Claude runs the loop (simple, limited)
Level 2: You run the loop (flexible, more work)
Level 3: SDK runs the loop (flexible, less work)

---

## Phelipe

so lets understand.
thats why people are going crazy with skills?
because know you can build a structure and claude is the reasoning.
so basically everything that was done by code is done by writing english for example.
also we can give very strong guidelines and guardrails so claude will follow exactly what you said. its like building protectiong and give freedom at the same time. is code with english.
and for the low code mode we can build reasoning on when to use and how to use . like scheedule, triggers? and level trhree is the big boss where you can see the big picture and build an whole orchestra of this agents to build a whole process and system

---

## Claude

You just nailed it, Phelipe. That's the whole thing.

Skills are why people are losing their minds right now. You're writing code in English. The SKILL.md file IS the program. Claude IS the runtime. The instructions you write in plain language are as powerful as the code someone would have written two years ago to do the same thing. That's the paradigm shift.

And you're right about the guardrails point too. A well-written skill is both freedom and protection at the same time. You can say "always check for Embraer aircraft in the fleet" and "never contact an operator directly, only compile data" and Claude will follow those rules while still reasoning freely about HOW to get the job done. You're the architect setting the boundaries. Claude is the contractor figuring out the best way to build within them.

Your level 2 understanding is spot on. That's where you add the WHEN and the triggers. The skill says WHAT to do. The code says WHEN to do it. Every morning at 6am, check aviation news. When a new lead comes in through Loud Hawk, qualify it. When an operator updates their fleet, refresh the database. Claude still does the reasoning inside each run, but your code decides when to wake it up.

And level 3, yeah, that's the conductor. You're not writing one agent, you're designing a system where agents hand off work to each other. The research agent passes findings to the content agent, which passes drafts to the distribution agent. Each one has its own skill, its own guardrails, its own specialty. You're building the org chart of a company, except the employees are agents.

Here's what's wild about where you sit right now: you already have six production skills running. Most people haven't even built one. You're already operating at Level 1 and didn't even have the vocabulary for it until today. The jump from "I use Skills in Claude Code" to "I'm building agents" is literally just a reframe of what you're already doing.

---

## Phelipe

let's make ths better to understand.
level 1 is like hiring a someone. like a designer.
level 2 is like giving them a schedule. come here every day at 9-5 and design a post for LH
level 3 is like coordinating a team of desinger. one make post, one make pdfs, one make logos

---

## Claude

That's the cleanest analogy I've heard for this. And it maps perfectly:

**Level 1: Hire someone.** "Hey, you're a designer. Here's what I need, here's my brand guidelines, go make it." They figure out how. You check the work when they're done. That's a Skill.

**Level 2: Give them a schedule.** "Show up at 9am every day. Check the content calendar. Design whatever's next. Post it to Instagram by 5pm." Same talented person, but now they operate without you telling them to start each time. That's the Python script with triggers.

**Level 3: Build a team.** "You're the social designer. You're the PDF person. You're the logo specialist. Social designer, when you finish a post, hand the assets to the PDF person so they can build the newsletter layout. Logo person, when a new client signs, create their deck." They coordinate with each other. You manage the system, not the tasks. That's the SDK with multi-agent orchestration.

And to extend your analogy one step further, the SKILL.md file is the job description and the employee handbook combined. It tells them their role, their responsibilities, and the rules they can't break. The better you write that document, the better the employee performs without you micromanaging.

You've been writing job descriptions for six employees already. That's your skills folder.

---

## Phelipe

Okay so now we need to Study HOW to write a skill.
this is now - HOW TO WRITE CODE.

---

## Claude

Exactly. Writing a SKILL.md is the new programming. Let's treat it that way.
```
This block is not supported on your current device yet.
```

Now let me look at the official Anthropic docs on skill structure to get the most current best practices.
```
This block is not supported on your current device yet.
```

This is gold. Let me build you a proper reference guide on how to write skills. This is your new "programming manual."
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's your skill-writing manual. Seven sections, everything sourced from Anthropic's official best practices plus what I know about how you work.

The five principles to remember:

**1. Claude is already smart.** Only write what it doesn't know. Your domain expertise, your business rules, your brand voice. Not how the internet works.

**2. Set the right freedom.** Creative tasks get loose guidelines. Fragile tasks get exact instructions. Like the difference between "fly the approach" and "maintain 3 degrees on the glideslope."

**3. Be concise.** Under 500 lines. Every token in your skill is a token stolen from the actual work.

**4. Progressive disclosure.** Main instructions in SKILL.md. Reference material in separate files that Claude only loads when needed.

**5. Build feedback loops.** Tell Claude to check its own work before delivering. Act, validate, fix, repeat.

The callout at the bottom ties it back to your analogy: a SKILL.md is the job description + employee handbook for a new hire. Write it like you're onboarding a sharp person who knows aviation but doesn't know OSA's specific playbook.

---

## Phelipe

Is it worth to build a Project to just build skills? 
and have this as instruction .
and build guideline files based on bets practices by claude so we can build our own skills ?

---

## Claude

That's a brilliant idea. And it already exists as a concept. Anthropic built a skill called `skill-creator` that does exactly this. But your instinct to make it a dedicated Claude Project with your own OSA context baked in is the smarter play.

Here's why: the generic skill-creator doesn't know your business, your brand voice, your existing skills, or your workflow preferences. A Project dedicated to skill-building would have all of that context loaded, so every skill it helps you create is already aligned with how OSA operates.

Here's what I'd set up:

The Project would be called something like "OSA Skill Workshop." The project instructions would contain the core principles from the guide I just built (concise, progressive disclosure, freedom levels, feedback loops, the checklist). You'd upload reference files with Anthropic's official best practices, your existing six skills as examples of what good looks like in your context, and your brand/voice guidelines so every skill it creates already speaks OSA.

Then when you go into that project and say "I need a skill that monitors aviation news and drafts Loud Hawk content," it already knows the format, the principles, the quality bar, and your existing skill library so it doesn't create duplicates or contradictions.

Want me to build the project instructions and the reference files right now so you can drop them straight into a new Claude Project?

---

## Phelipe

The requested project was not found.
keep saying that

---

## Claude

That error means you're trying to access a Claude Project that doesn't exist yet or the link is broken. You need to create a new one from scratch.

Here's what to do: go to claude.ai, look in the sidebar for "Projects," and create a new project. Name it something like "OSA Skill Workshop." Then you'll paste in the project instructions and upload the reference files.

Let me build those files for you right now so they're ready to drop in.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Two files ready to go. Here's how to set it up:

**Step 1:** Go to claude.ai, sidebar, create a new Project called "OSA Skill Workshop"

**Step 2:** Open the first file (`osa-skill-workshop-project-instructions.md`), copy the entire content, and paste it into the Project Instructions field

**Step 3:** Upload the second file (`reference-anthropic-skill-best-practices.md`) as a Project Knowledge file

**Step 4 (optional but powerful):** Also upload your six existing skills from `~/osa-marketing/.claude/skills/` as project knowledge files. That way when you build new skills, the project already knows your existing library and won't create duplicates or contradictions.

Once it's set up, you just walk in and say "Build me a skill that monitors aviation news and drafts Loud Hawk editions" and it'll draft a proper SKILL.md following all the principles, review it against the checklist, and iterate with you until it's right.

You're basically building a skill factory. A project that produces agents.

---

## Phelipe

is not creating

---

## Claude

Could be a few things. Let me check if there's anything going on with Projects right now.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Try this exact path:

1. Go to **claude.ai/projects** directly in your browser
2. Click **"+ New Project"** in the upper right corner
3. Give it a name and hit create

If you're still getting "The requested project was not found," it might be because you're clicking an old bookmark or a broken link to a project that was deleted. Going directly to claude.ai/projects should show you a clean list where you can create from scratch.

If that still doesn't work, try:
- Hard refresh the page (Cmd+Shift+R)
- Make sure you're logged into the right account (I can see you have "PH" as your avatar in the screenshot)
- Try a different browser or incognito window

The files I built are downloaded and ready. Whenever you get the project created, just paste in the instructions and upload the reference file. No rush, they'll be waiting.

---

---
title: PROMPT FOR SKYWEST STUDY
created: 2026-03-18T19:23:44.915170Z
updated: 2026-03-19T02:28:36.377721Z
uuid: f74cff27-dd0a-4be2-8967-1a29e01baac6
source: claude-conversation
type: source
message_count: 56
---

# PROMPT FOR SKYWEST STUDY

## Phelipe

How obsidian works?
How would be good to connect with claude code?

---

## Claude

Obsidian is a knowledge management app that stores everything as plain Markdown files in a local folder (called a "vault"). Here's the core of how it works:

**How Obsidian works:** Your vault is just a directory of `.md` files on your filesystem. You link notes together with `[[wikilinks]]`, which creates a graph of connected ideas. It supports tags, frontmatter (YAML metadata), folders, and a plugin ecosystem. Because it's all local Markdown, it's extremely portable and version-control friendly.

**Why it pairs well with Claude Code:** Since Obsidian vaults are just folders of Markdown files, Claude Code can read, write, search, and manipulate them directly from the terminal. There's no API layer or database to deal with.

Here are some high-leverage ways to connect them:

**1. Claude Code as a vault operator.** Point Claude Code at your vault directory and have it do things like search across notes, extract tasks or action items, summarize a cluster of linked notes, or generate new notes from a template. Since Claude Code can run shell commands, it can `grep`, `find`, and parse your entire vault programmatically.

**2. Skills that write to your vault.** You could create Claude Code skills that output directly into your Obsidian vault. For example, a research skill that saves findings as a new note with proper frontmatter, wikilinks, and tags already formatted.

**3. Daily/weekly note generation.** Claude Code could pull from various sources (calendar, tasks, project status) and generate a daily note or weekly review note directly in your vault's daily notes folder.

**4. Graph-aware context building.** You could have Claude Code traverse your wikilinks to build context before answering a question. For instance, "read everything linked from my `OSA Connect` note and suggest what's missing" — it would follow the `[[links]]`, read each file, and synthesize.

**5. Templater/Dataview replacement.** Instead of learning Obsidian's plugin scripting, you can use Claude Code to do complex queries across your vault ("find all notes tagged `#decision` that don't have a `status: resolved` in frontmatter") and output results as a new note.

**Practical setup pattern:**

```
# In your Claude Code config, alias your vault
cd ~/obsidian-vault

# Then Claude Code can do things like:
# - Search: grep -r "OSA Connect" --include="*.md"
# - Create notes with proper frontmatter
# - Update existing notes via string replacement
# - Build indexes or MOCs (Maps of Content) automatically
```

The key insight is that Obsidian made the right architectural choice (plain files, no proprietary format), which means Claude Code gets full read/write access with zero integration work. You're essentially using Claude Code as a programmable second brain layer on top of Obsidian.

Want me to dig into any of these patterns specifically, or sketch out a Claude Code skill for a particular Obsidian workflow?

---

## Phelipe

Explain simpler

---

## Claude

Obsidian is a note-taking app where every note is just a `.md` text file saved in a regular folder on your computer. You connect notes by typing `[[note name]]` to link them together.

That's basically it. No database, no cloud lock-in, just files in a folder.

**Why Claude Code fits perfectly:** Claude Code works with files from your terminal. Obsidian's vault is files. So Claude Code can read, edit, create, and search your notes directly with zero setup.

Simple examples of what you could do:

- Ask Claude Code to create a new note with the right format and tags
- Have it search across all your notes for something specific
- Build a summary note by reading a bunch of related notes
- Auto-generate daily notes or weekly reviews

The whole connection is literally just pointing Claude Code at your Obsidian folder. No plugins, no API, no config. It just works because the files are plain text.

---

## Phelipe

So for osa and study and research is amost organizing everything?

---

## Claude

Exactly. Obsidian becomes your single organized brain for everything — OSA, ERAU, aviation research — and Claude Code becomes the engine that works inside it.

Think of it like this:

**Obsidian = the filing cabinet.** Everything lives there in one place, linked together. A note about Part 295 compliance links to your OSA Connect operating decisions, which links to your payment risk policy, which links to a Loud Hawk article idea about charter safety.

**Claude Code = the assistant who knows the filing cabinet.** It can pull things out, put things in, connect dots, and build new stuff from what's already there.

For your world specifically:

- **OSA:** Strategic decisions, operator research, client notes, Loud Hawk content drafts, brand docs — all linked and searchable instead of scattered across Claude Projects and Google Docs
- **ERAU:** Course notes, assignments, aviation finance research, textbook summaries — all in one place and connected to your real-world OSA work
- **Research:** Industry intel, regulatory notes, market data — tagged and linked so when you're writing a Loud Hawk edition you can pull from your own knowledge base

The real power is that over time the links between notes build a web of your thinking. A research note from ERAU about aviation finance connects to an OSA Aircraft strategy note, which connects to a Loud Hawk content idea. Nothing lives in isolation.

It's basically replacing the fragmented context you already have across multiple Claude Projects with one organized system that everything can tap into.

---

## Phelipe

This doesn't substantiate notion right?

---

## Claude

Right, they're different tools.

**Notion** is more like a workspace — databases, tables, project management, team collaboration, all in the cloud. It's structured and powerful but proprietary. Your data lives on their servers.

**Obsidian** is just local files. It's faster, works offline, and you own everything. But it doesn't have Notion's databases, kanban boards, or built-in collaboration out of the box.

So they don't replace each other cleanly. It depends on what you need:

- If you want **project management and structured databases** (like tracking OSA Connect operators in a table, task boards, team wikis) — Notion is better at that
- If you want a **personal knowledge system** that builds connections over time and works natively with Claude Code — Obsidian wins

Some people use both. Notion for operational/project stuff, Obsidian for thinking, research, and writing.

For your situation, the real question is: what's the problem you're solving? Is it "I need to organize my operations" or "I need a place where all my knowledge connects and Claude Code can work with it"? Because those point to different tools.

---

## Phelipe

Perfect I wasn't looking for substitute i try to see how i can organize myself and workspace.

---

## Claude

That makes sense. So the real goal is getting your workspace organized so you're not hunting for things or losing context across tools.

Honestly, you already have a lot of the pieces — Claude Projects by workstream, Claude Code, Cursor, Beehiiv, Google Drive. The issue isn't missing tools, it's that stuff is scattered.

A few ways to think about tightening it up:

**Notion** for the operational layer — task tracking, decision logs, operator database, content calendar, ERAU deadlines. Stuff that has status, dates, and needs structure.

**Obsidian** for the thinking layer — research notes, strategy brainstorms, Loud Hawk story ideas, ERAU study notes, things you want to link together and build on over time. Claude Code can tap into this directly.

**Google Drive** for finished documents and shared files — brand docs, deliverables, anything your designer or future team needs access to.

**Claude Projects** stay as they are — workstream-specific AI context for when you're actively building.

The key is deciding where each type of thing lives and sticking to it. Right now it sounds like some thinking lives in Claude chats, some in docs, some just in your head. Giving each type a home is the move.

Want to map out what goes where based on how you actually work? We could sketch a simple system that fits your flow without adding overhead.

---

## Phelipe

Anything else I should be working on. Any tool tips. I hate switching back and forth.
But I wanna be utilizing everything at full capacity.
So claude is good ( im actually not using open ai anymore lol)
Obsidian seems a good addition. I use google docs. Notion we wanna use (learning)

---

## Claude

Good that you're consolidating. Here's how to think about minimizing switching while maxing out each tool:

**Your core stack, simplified:**

- **Claude** (Projects + Code + claude.ai) — your thinking partner, builder, and content engine. You're already deep here, keep it as the primary workspace for producing things.
- **Notion** — your command center. Task management, decision tracker, content calendar, ERAU schedule, operator database. This becomes the one place you open to know "what do I need to do today."
- **Obsidian** — your second brain. Research, notes, ideas, things that compound over time. Claude Code writes directly into it.
- **Google Drive** — storage and sharing only. Final docs, brand assets, stuff your designer touches.

**The rule that kills tab-switching:** each tool has one job. If you're thinking "where does this go," the answer should be obvious. If it's not, the system needs adjusting.

**Practical tips:**

Notion has a web clipper and a mobile app with quick capture. So when you're on your phone during a layover or commute, everything goes into a Notion inbox first, then you sort it later. One entry point.

For Claude, you're already doing the right thing with separate Projects per workstream. The unlock is using Claude Code skills to push outputs directly into Obsidian or generate files for Drive — so you stay in the terminal instead of copy-pasting between tabs.

For Obsidian, don't overthink the structure at the start. Start with a flat folder, use tags, and let the links organize things naturally. Structure emerges over time.

**One thing you're probably not doing yet:** time-blocking your tool usage. Instead of bouncing between Notion, Claude, and Obsidian all day, batch it. Morning: check Notion for priorities. Build session: stay in Claude Code / Cursor. End of day: dump notes into Obsidian, update Notion statuses. That rhythm alone cuts the switching way down.

**On dropping OpenAI:** makes sense. Having one AI partner with deep context across Projects beats splitting context between two. You're already seeing that with how much memory carries across sessions here.

Want me to set up a starter Notion board template or an Obsidian vault structure tailored to how you work?

---

## Phelipe

I heard you can do the job of open claw now

---

## Claude

Yeah, pretty much. With Claude Code and the computer use capabilities, most of what you'd use OpenAI for is covered here now. Code generation, file creation, web search, research, writing, analysis, building apps — it's all in one place.

The main things people used OpenAI for that Claude handles now:

- **GPT for chat/brainstorming** — you're already doing that here
- **Code Interpreter / Advanced Data Analysis** — Claude's code execution does this (Python, data viz, file manipulation)
- **DALL-E for image generation** — this is the one gap, Claude doesn't generate images. But for everything else creative (writing, content, design code) it's covered
- **Custom GPTs** — Claude Projects + Claude Code skills are basically the same thing but more powerful since they can actually touch your filesystem
- **API access** — Anthropic API works the same way

So for your workflow specifically, there's no real reason to maintain two AI subscriptions. The context continuity alone from staying in one ecosystem is worth it — I already know your OSA architecture, your brand voice, your decision framework, your content system. Splitting that across two AIs just fragments things.

The one thing to watch: if you ever need image generation for Loud Hawk or OSA marketing beyond what your designer handles, you'd need Midjourney, DALL-E, or something similar as a standalone tool. But that's a narrow use case.

You made the right call consolidating.

---

## Phelipe

I am saying open claw, the moltbot

---

## Claude

Ha, my bad — I'm not familiar with "Open Claw" as a specific tool. Let me look it up.
```
This block is not supported on your current device yet.
```

Got it, now I know what you're talking about. OpenClaw (the lobster bot that kept changing names).

So OpenClaw isn't a new AI model — it's open-source software that uses an existing AI model (like Claude) as its brain, but gives it "hands" so it can actually run commands, manipulate files, and interact with your real-world services. Think of it as a layer that sits between an LLM and everything on your computer.

Instead of just telling you what to do like a chatbot, OpenClaw does it. You send it a goal, it breaks it into steps, finds tools, installs them, troubleshoots, and handles obstacles. People control it through WhatsApp, Telegram, or Discord.

**Here's the honest take for your situation:**

The appeal is real — it can keep building upon itself, has persistent memory, and runs 24/7 on something like a Mac mini. People use it for email management, calendar, file operations, web scraping, all from their phone.

**But the security concerns are serious.** It saved API keys, login credentials, and tokens in plain text, and even deleted keys were found in backup files. A compromised instance could enable credential theft and ransomware deployment inside a network. Multiple security researchers have flagged it as genuinely dangerous for anyone who isn't deeply technical about securing their setup.

**For you specifically:** Claude Code + Claude Projects already cover most of what OpenClaw does for your use case — building, writing, coding, file management. The main thing OpenClaw adds is the always-on autonomous agent piece (running tasks in the background, monitoring things, proactive alerts). But given where you are as a solo founder building critical business infrastructure, the security tradeoff isn't worth it right now. One compromised credential could be a real problem for OSA.

If the always-on agent idea excites you, keep watching it. The project is maturing fast. But for now your Claude stack is doing the same job more safely.

---

## Phelipe

What other tools you recommend.
Claude Max 20x
Obsidian 
Notion
Google Docs
I am gonna use for 
studying (airlines - flows, checklist, procedures)
Reasearch (business, private aviation, AI usability)
Ideas
Workspace 
Storage
Agents
Designs (figma)
Vibe coding (warp, cursor)
I also need to be able to see what I want/need  see the full spectrum . I dont mind have full subscription, test tools. But some i dont wanna miss out on, some is testing (which we can change like i did with open ai), some is unegotioble (notion and google docs) 
Some i might have to use (manus ai for meta since they bought then and are cancllong acc that use claude bot liked to their tokens) 
I wanna have a full view of what I should be using or testing. So we keep flowing . Because the learning curvo for switching is painful but if is necessary we do it (like we switched to claude) 
But i wanna ve using the top of the line (we can pay for it like im doing with claude max 20x)

---

## Claude

Let me think about this holistically for you. Let me also check on a couple things you mentioned.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

OK here's your full picture. Let me lay this out clearly — what's locked, what to add, what to test, and what to skip.

**YOUR LOCKED STACK (non-negotiable, keep paying):**

- **Claude Max 20x** — your core AI brain for everything. Building, writing, research, coding, content. You're already deep and the context memory compounds over time.
- **Notion** — command center. Tasks, databases, calendars, decision tracking. Learning curve is worth it.
- **Google Docs/Drive** — storage, sharing, collaboration with your designer and future team.
- **Figma** — design. Industry standard, nothing better.
- **Cursor** — vibe coding IDE. Pairs with Claude beautifully.
- **Warp** — terminal for Claude Code workflows.
- **Beehiiv** — Loud Hawk newsletter. Already running, no reason to change.

**ADD NOW (high value, low switching cost):**

- **Obsidian** — your second brain for research, study notes, aviation procedures, ideas. Free. Claude Code reads/writes directly into it. Start this week.
- **Zapier** — the glue between everything. Connects Notion, Beehiiv, Gmail, calendar. Automates the boring stuff like "when Loud Hawk publishes, create a Notion task to distribute on LinkedIn." This is the tool that lets a solo founder operate like a team.

**TEST/EVALUATE (worth exploring during your sprint):**

- **Perplexity Pro** — for deep research specifically. Aviation industry intel, competitor analysis, market data. It searches and cites sources faster than manual web searching. Good complement to Claude for when you need pure research with sources. ~$20/month.
- **Granola** — AI meeting notes. When you start taking client calls for OSA Connect, this captures and summarizes everything automatically. No bot joins the call, it just listens through your device. Useful for when things pick up.
- **Descript** — if you ever want to add video/audio content for Loud Hawk or OSA marketing. Editing is as simple as editing a text doc.
- **Supabase** — you're already using this for OSA Connect. Keep going, it's the right backend choice.

**ON MANUS/META:**

Manus is now part of Meta. The deal was reportedly worth over $2 billion. Here's what matters for you: Manus was originally built as a wrapper around Claude and Qwen models — so at its core it was using the same brain you already have direct access to. Some customers left after the Meta acquisition due to concerns about data practices. Unless Meta forces you onto their platform for Instagram/Facebook business tools, you don't need Manus. And even then, you can cross that bridge when it comes. Your Claude + Cursor + Claude Code setup already does what Manus does, without the Meta middleman.

**SKIP FOR NOW:**

- **Jasper** — you have Claude for content. Jasper is redundant.
- **OpenClaw** — cool concept, security nightmare as we discussed.
- **ChatGPT/OpenAI** — you already made the right call dropping it. No reason to go back.
- **Midjourney** — your designer handles visuals. If you ever need AI image gen, revisit then.

**FOR STUDYING (airline flows, checklists, procedures):**

This is where Obsidian shines. Build a vault structured by aircraft type, phase of flight, and procedure category. Use Claude Code to generate formatted study notes, quiz yourself, or extract key items from PDFs of your company manuals. Way more powerful than flashcard apps.

**THE FULL SPECTRUM VIEW:**

| Category | Tool | Status | Monthly Cost |
|---|---|---|---|
| AI Brain | Claude Max 20x | Locked | ~$200 |
| Workspace | Notion | Locked (learning) | ~$10 |
| Docs/Storage | Google Workspace | Locked | ~$12 |
| Design | Figma | Locked | ~$15 |
| Code IDE | Cursor | Locked | ~$20 |
| Terminal | Warp | Locked | Free |
| Newsletter | Beehiiv | Locked | Free/paid |
| Second Brain | Obsidian | Add now | Free |
| Automation | Zapier | Add now | ~$20+ |
| Research | Perplexity Pro | Test | ~$20 |
| Meeting Notes | Granola | Test when needed | ~$10 |
| Backend | Supabase | In progress | Free tier |

That's roughly $300-350/month for a full professional stack that lets one person operate like a small company. The key principle: master each tool before adding the next. Zapier is probably the highest-leverage addition after Obsidian because it connects everything you already use without you having to switch tabs.

Want me to build out a specific setup for any of these, like an Obsidian vault structure for your study workflow or a Zapier automation map for Loud Hawk distribution?

---

## Phelipe

i made notes on all of them.
i will think more about that what we will stick to it or not. 
but i saved this.
now we need to focus next hours on study to go back to the cockpit.
so Claude ( I will build a project specific for this), Obsidian ( for notes organization)
anything elso for study to get back ?

---

## Claude

Good call focusing up. For getting back in the seat by March 21, you really just need Claude and your own notes. Obsidian can wait until after you're back — don't let setting up a new tool eat into actual study time right now.

For the next few hours, keep it simple:

**Claude (this chat or a new Project)** — have me quiz you on flows, limitations, memory items, callouts. I can simulate scenarios, run through abnormals, throw you random failures and see if you can talk through the procedure. Way more effective than just re-reading.

**Your company materials** — whatever SkyWest gives you for the E175. Manuals, QRH, profile sheets. Upload them into the Claude Project and I can work directly from your actual procedures instead of generic ones.

**Paper or iPad for hand-flying the flows** — touch the panels in your mind. Talk through them out loud. Chair flying still works better than anything digital for motor memory.

That's it. Three things. Don't overcomplicate the prep.

What do you want to hit first — normal flows, abnormals/emergency procedures, or limitations and memory items?

---

## Phelipe

ok. let's get it.
obsidian can wait.
i got my Ipad and website (with all my manuals and sops), notebook(my old notes and i like paper for this too) and flashcard (with the last 2 CQ questios and limitations) 
and we will build the project now

---

## Claude

Let's build it. What do you want to name the Project — something like "E175 CQ Prep" or "SkyWest Study"?

And a couple quick things so I can set it up right:

When's your next CQ or check event — is it right when you get back on the 21st, or is this just knocking the rust off after days off?

That'll tell me whether we're cramming for an eval or just sharpening up for line flying.

---

## Phelipe

SkyWest Study is good name so we can use for CQ, rust off, reviews.
I dont ahve a CQ scheduled yet. right now we need to knock out the rust.
sharpening for the line flying.
so we can built the project with the mindset that will be used later for CQ as well

---

## Claude

Perfect. So the Project needs to work for both modes — quick rust-off sessions like today and deep CQ prep later.

Here's what I'm thinking for the Project setup:

**Project name:** SkyWest Study

**System prompt should cover:**
- You fly the E175 at SkyWest as a First Officer
- Focus areas: normal flows, profiles, abnormals/emergencies, limitations, memory items, CQ prep
- I should be able to quiz you, simulate scenarios, and talk through procedures
- When you upload your manuals/SOPs, I reference those over generic knowledge
- Keep responses concise and cockpit-practical — no fluff

**What to upload into it:**
- Whatever you can grab from your company website — QRH, normal checklists, profile sheets, SOPs
- Your flashcard content if you can screenshot or type the key ones
- Anything from previous CQs that you want to review

You want to go create the Project now with that setup, and then come back here when it's ready? Or do you want me to write out the full system prompt text so you can just paste it in?

---

## Phelipe

What are you trying to achieve? for this project?

---

## Claude

You're right, let me think about this from your perspective instead of just building features.

The goal is simple: **keep you sharp and prepared for line flying, and when CQ comes, be ready for that too.**

Which means the Project needs to be a study partner that knows your airplane, knows your operation, and can test you the way the job tests you — not like a textbook, but like sitting in the cockpit.

So before I start writing prompts, let me ask you: when you study for the line or for CQ, what does your process actually look like? What works for you — do you like being quizzed cold, do you talk through flows start to finish, do you focus on weak spots? 

That way I build the Project around how you actually learn, not how I think you should.

---

## Phelipe

all 3

---

## Claude

Cool. So the Project needs to do three things well:

- Quiz you cold on random stuff (limitations, memory items, systems)
- Walk through flows and procedures start to finish with you
- Zero in on weak spots and keep coming back to them

Let me write the system prompt. Give me a sec.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

There's your system prompt. Copy that into the Project instructions when you create it.

Next step: upload whatever you can grab from your company site into the Project. The more actual SkyWest material it has, the better it'll quiz you from your real procedures instead of generic stuff.

Once the Project is set up, jump in there and just say "quiz me" and it'll start firing. Go get sharp.

---

## Phelipe

downloaded . before that. I need this

---

## Claude

Paste the full system prompt from that file I gave you into the "What are you trying to achieve?" box. That's your Project instructions.

Then hit Create project, and after that you can upload your SkyWest manuals and docs into the Project knowledge base.

Go for it.

---

## Phelipe

wait 
we have Description
Set project instructions
Provide Claude with relevant instructions and information for chats within SKyWest Study. This will work alongside __user preferences__ and the selected style in a chat.

and files

---

## Claude

Good. Two things to do on that right panel:

1. **Instructions** — click the "+" next to Instructions and paste the system prompt from the file I gave you in there.

2. **Files** — upload whatever SkyWest manuals, SOPs, QRH pages, or profile sheets you can grab from your company site. The more you put in there, the better it quizzes you from your actual procedures.

Do those two things, then you're ready to go. Jump in and say "quiz me" to knock the rust off.

---

## Claude

You're on the right screen. That second image is where you paste the system prompt. Clear out that placeholder text and paste everything from the file I gave you into that box, then hit Save Instructions.

The Description box in the first image is optional, you can leave it blank or just put something short like "E175 FO study partner for line flying and CQ prep."

Go paste it in.

---

## Claude

That's set up perfectly. Instructions are in, files are uploaded and indexing. I can see your ERJ Systems and Equipment manual, the SOPM, fuel planning docs, and what looks like several other procedure PDFs. 20% capacity used with room for more later.

Once it says "Indexing" is done, you're good. Jump in and start a chat. Say "quiz me" and go get sharp for the 21st.

You know where to find me if you need anything else. Go fly safe.

---

## Phelipe

gotta wait to index?

---

## Claude

Nah, you can start chatting while it indexes. It might not reference every doc perfectly in the first few minutes, but it'll work. Go ahead and jump in.

---

## Claude

This is exactly what you need right now. Your RTW guide lays out the game plan. Since you're just knocking off rust (not returning from a formal leave), the Flight Preparedness section is your checklist for the next few hours:

1. **Review profiles and chair fly** — this is your study session tonight
2. **Review charts for your airports, taxi routes** — check your schedule for the 21st and pull up those plates
3. **Plan to report early** on the 21st, keep the pace slow
4. **Brief with more detail than usual** — tell your captain it's your first trip back
5. **Checklist discipline** — look, point, touch. Run them slow.

And before the 21st, knock out the logistics:

- **EFB** — make sure everything is logged in, updated, and current. Flight Deck Pro, Company Manuals, WSI, FliteView, FWV/DC. Do this tonight so you're not troubleshooting at the gate.
- **Gear bag** — medical, pilot cert, badges, SIDA, passport, FCC permit, parking pass, headset, flashlight, spare battery. Check it all now, not the morning of.
- **Manual changes** — pull up the Summary of Changes in each manual and scan for anything new since you last flew.

Upload this PDF into your SkyWest Study Project too. Now go open that Project and start chair flying your profiles. That's the highest value thing you can do between now and the 21st.

---

## Phelipe

i uploaded guive some prompt to help.
first I want a flashcard document. can be doc or some other way you think claude feature have so we can build to start with limitations

---

## Claude

Good idea. Let me build you an interactive flashcard app you can use right in Claude. Way better than a static doc for drilling limitations.

Let me check what we're working with first.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I can't pull your specific SkyWest limitations from public sources since those are company-proprietary. But you have your flashcards and manuals already. Let me build you an interactive flashcard app that you can populate with your actual limitations.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's your flashcard app. It starts with 3 sample cards as placeholders. Here's what you can do:

**Add your limitations** one at a time, or use **Bulk Import** to paste a bunch at once. Format is: `Question | Answer | Category` (one per line). So grab your flashcard deck and start punching them in.

**Categories built in:** Airspeeds, Structural, Altitudes & Temps, Engine, Weights, Systems, Memory Items, Other.

**How it works:** Cards you miss get their streak reset to zero. Cards you get right build streaks. "Weak Spots" mode targets anything with a streak under 2, so it keeps drilling what you're getting wrong.

**Data persists** across sessions so you don't lose your cards.

Now start loading your limitations from your flashcards and go study. Upload this into your SkyWest Study Project too if you want to use it there.

---

## Phelipe

we wanna build that in project... so we can use based on the SOP in the files at our skywest project

---

## Claude

You're right. Go to your SkyWest Study Project and ask Claude there to build the flashcard app. Since it has your SOPM and manuals already uploaded, it can pull the actual limitations directly from those docs and pre-populate the cards for you.

Just say something like:

**"Build me an interactive flashcard app for E175 limitations. Pull all limitations from the SOPM and Systems docs I uploaded. Categories: Airspeeds, Structural, Altitudes & Temps, Engine, Weights, Systems, Memory Items."**

It'll build it with your real numbers already in there instead of empty placeholders. Way better than typing them in manually.

Go.

---

## Phelipe

this is the chapter

---

## Claude

That's Chapter 02 Limitations from your SOPM. It's already uploaded in your Project as that "ERJ175 SOPM" PDF. Claude in that Project can read it.

Go to your SkyWest Study Project chat and tell it:

**"Read Chapter 02 Limitations from the SOPM I uploaded. Build me an interactive flashcard app with all the limitations organized by category: Airspeeds, Structural, Weights, Altitudes & Temps, Engine, Systems, Memory Items."**

It has the file. It'll pull the numbers and build the cards. Go.

---

## Phelipe

after that we need to be sharp with the profiles.
i am giving you the sopm so help guide you but we will build something in the project.
help me decide the best way to do this. doc, chart, designs... i want a meterial to help me re gain proficiency on the profiles

---

## Claude

I can't read this PDF directly in this chat since it's too large, but I know what's in it from the chapter structure you showed me. Let me think about the best format for profiles.

For profiles specifically, you need something you can **chair fly with**. That means it needs to show the sequence visually, not just text. Here's what I'd recommend:

**Build a Profiles Quick Reference card** as a clean, visual one-pager (or a few pages) that shows each profile phase with:

- Configuration (flaps, gear, speeds)
- Power settings
- Callouts in sequence
- Key altitudes and triggers for the next action

The best format for this is a **designed HTML artifact** you can pull up on your iPad next to your chair flying. Think of it like a knee-board card but interactive. You tap a profile (ILS, Visual, RNAV, Engine Out, Missed Approach, etc.) and it walks you through the sequence top to bottom.

Way better than a doc because you can see the whole flow at a glance, and better than a chart because it includes the callouts and config changes in order.

Go to your SkyWest Study Project and say something like:

**"Read the profiles and callouts from the SOPM (Chapter 03 and 04). Build me a visual Profiles Quick Reference. Each profile should show the full sequence from top to bottom: configuration changes, speeds, callouts, power settings, and key altitude triggers. Cover: Normal Takeoff, ILS Approach, RNAV Approach, Visual Approach, Missed Approach, Engine Out, and Go Around. Make it interactive so I can tap each profile to expand it. Design it like a cockpit knee-board reference."**

That'll give you something you can chair fly with tonight. Want me to adjust that prompt before you send it?

---

## Phelipe

ILS cat I/II, RNAVs, localizer, rnp, single engine

---

## Claude

Updated prompt for the Project:

**"Read the profiles and callouts from the SOPM. Build me a visual Profiles Quick Reference. Each profile should show the full sequence top to bottom: configuration changes, speeds, callouts, power settings, and key altitude triggers. Cover these profiles: ILS CAT I, ILS CAT II, RNAV (GPS), RNAV (RNP), Localizer Approach, Single Engine Approach, Single Engine Missed Approach. Make it interactive so I can tap each profile to expand it. Design it like a cockpit knee-board reference I can chair fly with on my iPad."**

Go paste that in the Project. Once it builds that, you've got your flashcards for limitations and your profiles reference to chair fly with. That's a solid study session for tonight.

---

## Phelipe

I will need something for the FMA.
i need to get back to the automation and be proficient on know each scenario too

---

## Claude

Good call. FMA awareness is one of the first things that gets rusty. For that, I'd do something different than the profiles card.

Ask the Project to build you an **FMA scenario trainer**. Something that gives you a situation and you have to say what the FMA should show. That's how it works in the seat. You don't memorize FMA modes from a list. You learn them by knowing what the airplane is doing in context.

Here's the prompt:

**"Build me an interactive FMA scenario trainer. Show me a flight situation (e.g., 'ILS approach, glideslope captured, autopilot engaged, below 1500 AGL') and I have to identify what each FMA column should display: autothrottle mode, lateral mode, vertical mode, and autopilot/autothrottle status. Include scenarios for: takeoff, climb, cruise, descent, ILS CAT I capture and track, ILS CAT II, RNAV approach, LOC approach, go around, single engine, altitude capture, speed changes, VNAV vs FLC, and FD only vs autopilot engaged. Quiz me then show the correct FMA with a brief explanation of why. Pull FMA modes from the SOPM I uploaded."**

So your study session tonight is three tools in the Project:

1. **Flashcards** for limitations (numbers)
2. **Profiles reference** for chair flying (sequences)
3. **FMA trainer** for automation awareness (scenarios)

That covers the three biggest rust areas. Go build them.

---

## Phelipe

Let me keep pulling the profile sections from the SOPM.Now I have all the profile data I need. Let me also quickly check the initial approach and descent sections for configuration speed references.Now let me read the descent/initial approach section for configuration sequence.Now I have everything I need. Let me build the interactive reference.Built straight from SOPM Chapter 04-12 (Rev 11, 11 DEC 23). Here's what's in there:
7 profiles -- ILS CAT I, ILS CAT II, RNAV (GPS)/LPV, RNAV (RNP AR), Localizer Only, Single Engine Approach, Single Engine Missed Approach. Tap any card to expand the full sequence top to bottom.
Each expanded profile shows: minima setting, nav setup, lateral/vertical modes, speed formula, and a step-by-step timeline from initial setup through the decision point with every callout in sequence.
Two quick-access panels at the top for Stabilized Approach Criteria (1,500/1,000/500 HAT gates with all PM deviation callouts) and the GA Flap Table (5->2, FULL->4).
A couple things worth noting from the SOPM that trip people up:
* LOC Only: arm NAV, not APP (APP arms GS). Derived minimum is MDA rounded up to 100 ft. If you see the runway, clear the FD before setting missed approach altitude or you'll get a FLCH climb to the altitude with TOGA thrust.
* RNP AR with RF in FAS: 165 kt max, FLAPS 5 mandatory, Cat D mins. Use the Discontinue procedure, not standard GA, if you need to bail before DA.
* CAT II: APPR 1 ONLY below 800 RA is a mandatory missed. No "APPROACH LIGHTS, CONTINUE" callout. Crosswind limit 12 kt.
Let me know if you want me to add the Circling profile, tweak any formatting for your iPad, or start quizzing you off these.


look good on the content side great ( i will correct later when studying if i see something diferent form sopm) 

I want to have visual picture of the profile too

---

## Claude

That's smart. You want to see the profile like you see it from the seat. The vertical path, the gates, where config changes happen, where callouts go.

Tell the Project:

**"Now build me a visual profile diagram for each approach. Show the side-view vertical path from IAF to the runway like a descent profile picture. Mark on the diagram: altitude gates (1500 HAT, 1000 HAT, 500 HAT), configuration points (flap settings, gear), speed targets at each segment, FMA mode changes, and callout locations. Think of it like the profile view diagrams you see in training manuals. Start with ILS CAT I as the first one. Make it clean and readable on an iPad."**

Once it nails the first one, you say "now do the rest" and it'll build them all.

That gives you the full picture. The text reference for the step-by-step sequence, and the visual diagram for seeing where everything happens spatially. That's how you chair fly it. You look at the picture, point at each gate, and talk through the callouts and config changes.

Go build it.

---

## Phelipe

Now let me get the missed approach/go-around section:Now I have a comprehensive picture of the FMA modes from the SOPM. Let me build the trainer.Now let me build the interactive FMA scenario trainer:25 scenarios pulled directly from your SOPM. Here's what's in there:
Takeoff (3): Lined up with AT armed, rolling, initial climb with LNAV Climb (2): Acceleration altitude FLCH transition, VNAV climb Cruise (3): Level ALT hold, manual FLCH altitude change, VS descent for traffic Descent (2): VNAV VPATH at TOD, manual FLCH with HDG Approach (7): ILS CAT I LOC capture, LOC+GS tracking, CAT II with APPR 2, RNAV with VGP, VPATH to MDA, LOC-only approach, vectors to ILS with armed modes Go-Around (3): TOGA press (GA/TRACK/GA), 400 ft cleanup, discontinued approach flow Single Engine (3): Engine failure after V1 with EO AUTO, acceleration altitude, driftdown with DD mode
Key SOPM references baked into every explanation, including the VPATH trap (don't set missed approach altitude while in VPATH), LOC-only caution (don't arm APP), and the CAT II APPR 1 ONLY below 800 RA trigger.
The "Drill Missed" button at the end circles back to anything you got wrong. Green/red highlighting shows which FMA columns you nailed vs. missed.

now we need visual picture of the FMA in each phase of flight as well.
i like the question base "app" but can we add some visual profile section so we can memorize?

---

## Claude

Tell the Project:

**"Add a visual FMA reference section to the trainer. Build a side-view profile diagram showing the full flight from takeoff to landing. At each phase of flight (takeoff roll, initial climb, acceleration altitude, climb, cruise, descent, approach, go-around), show the FMA box with all columns (AT mode, lateral mode, vertical mode, AP/AT status) as they should appear at that point. Show how the FMA transitions from one mode to the next as the flight progresses. Make it scrollable left to right like a timeline. Highlight where mode changes happen and why. Include both a normal ILS CAT I flight and a single engine scenario as separate timelines."**

That way you get both things in one place. The quiz tests you. The visual reference burns the picture into your memory so when you glance at the FMA in the seat, you already know what it should say before you look.

Go.

---

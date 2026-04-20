---
title: NotebookLM Python library overview
created: 2026-03-15T22:39:23.743492Z
updated: 2026-03-15T23:01:00.211778Z
uuid: 67b32dbc-d0c4-482a-b5b4-0dc490d513e0
source: claude-conversation
type: source
message_count: 18
---

# NotebookLM Python library overview

## Phelipe

https://github.com/teng-lin/notebooklm-py
what this how is gonna help us

---

## Claude

Let me check what this project is.
```
This block is not supported on your current device yet.
```

Here's my honest read on this for OSA:

**What it is:** An unofficial Python API for Google NotebookLM. It lets you programmatically create notebooks, feed in sources (URLs, PDFs, YouTube), generate audio podcasts, videos, quizzes, slide decks, and more, all from code or CLI.

**Where it could help you:**

1. **Loud Hawk content repurposing.** You could feed each edition into NotebookLM and auto-generate an audio overview (podcast-style). Two hosts discussing your Aspen trip piece or permit infrastructure article. That's a distribution channel you don't have yet: audio content from written editions, essentially zero marginal effort per issue.

2. **Research acceleration.** Dump operator websites, FAA advisory circulars, NBAA resources, route-specific intel into a notebook and ask questions across all of them. Faster than reading 15 tabs.

3. **Client education materials.** Generate study guides or briefing docs from your Operating System SOPs. A client asks "how does charter pricing work?" and you send them a NotebookLM-generated explainer built from your own source material.

**Where it doesn't help:**

- It won't build your Next.js app or advance your milestones.
- It's an unofficial API using undocumented Google endpoints. Could break anytime.
- You're pre-revenue. Adding another tool to the stack right now is a distraction unless it directly accelerates a booking or an operator conversation.

**My recommendation:** Bookmark it. The Loud Hawk audio play is real, but it's a Phase 2 distribution move, not a pre-launch priority. Right now your time is better spent on the LLC filing, naming those 10 customers and 5 operators, and pushing Milestone 2 forward. Come back to this after Edition 3 or 4, when you have enough content to make an audio feed worth subscribing to.

What are you actually working on today?

---

## Phelipe

i can see this help me scrape youtube for people talking about aviation, private aviation (their is people teaching), to study for the airlines and research in general

---

## Claude

That's a different angle than I initially read. Let me think about this more carefully.

You're talking about using it as a **research ingestion engine**: find YouTube videos where pilots, brokers, aviation educators, and industry people are talking, feed those into NotebookLM, and then query across all of them. Chat with the content. Extract insights.

That's more useful than content repurposing. Here's why:

**What this actually gives you:**

- Someone like Matt Guthmiller or Flight Chops or a Part 135 operator doing a conference talk on YouTube. You feed the URL in. NotebookLM transcribes and indexes it. Now you can ask "what did they say about operator vetting" or "what pricing model did they describe" across 20 videos at once.
- ATP study material on YouTube (ground school lectures, oral prep, systems reviews). Feed them in, generate flashcards, quizzes. Structured study from unstructured video.
- Broker training content. There are people on YouTube teaching charter brokerage. Most of it is mediocre, but some of it contains real operational detail. Ingest it all, query the good parts.
- Industry conference panels (NBAA recordings, HAI talks). Hours of content you'd never sit through. Now searchable.

**The real value:** You're turning passive watching into an active, queryable knowledge base. That compounds. And for airline study (systems, weather, regs), the quiz and flashcard generation from video sources is legitimately useful for line checks and recurrent.

**The constraint is still the same though.** This is a power tool for learning. It doesn't get you closer to your first booking. It doesn't file the LLC or call an operator.

If you want to use it for airline study, that's your day job and it pays the bills, so that's a valid use right now. For OSA research, I'd still say: set it up on a day off, feed in 10 to 15 aviation YouTube sources that you've been meaning to watch, and let it work in the background. Don't let the setup become the project.

What's your actual schedule this week? Are you flying or do you have days off to push OSA forward?

---

## Phelipe

i need to actully study my flows and and refresh for the flight on the 21

---

## Claude

That's the priority then. The ERJ-175 pays for everything else.

For using notebooklm-py to study flows and refresh before the 21st, here's the practical move:

**Feed it your study sources.** If you have PDFs of the E175 flow cards, QRH procedures, or systems study guides, drop them in. If there are YouTube videos you use for E175 systems review or flow walkthroughs, feed those URLs in. NotebookLM indexes all of it and lets you quiz yourself across the material.

**The flashcard and quiz generation is the real win here.** You tell it "generate flashcards on E175 memory items" or "quiz me on the before-start flow" and it builds structured recall practice from your actual source material. That's better than re-reading flows passively.

**Setup time:** Maybe 30 to 45 minutes to install, authenticate, create a notebook, and load your sources. After that it's just a study tool.

Here's what I'd suggest for the next 6 days:

**Today/tomorrow:** Install notebooklm-py, load your E175 study materials (PDFs, YouTube links, whatever you use). Generate a first round of flashcards and quizzes. See if it's actually useful or if chair-flying is still better for you.

**Now through the 20th:** Study flows. Chair-fly. Use the tool if it helps, drop it if it doesn't. The ERJ-175 comes first.

**OSA between now and the 21st:** Only zero-effort tasks. File the LLC online (15 minutes). Text your insurance friend. That's it. No app building, no Claude Code sessions, no Loud Hawk editing.

**After the 21st:** Come back fresh, push Milestone 2, start naming real operators.

The flight on the 21st is the job. Everything OSA-related can wait 6 days.

---

## Phelipe

yeah we can let the agents do the job while i study on notebooklm see the catch - 
cloade code is the Autopilot while i read and study

---

## Claude

I hear you, but let me push back on this.

Claude Code is not autopilot. It's a tool that needs a pilot in the seat.

Here's what actually happens when you kick off Claude Code sessions and walk away to study:

**It drifts.** Without you reviewing output every 20 to 30 minutes, it makes decisions you didn't want. It picks the wrong component structure. It misreads the spec. It builds something that looks right but wires the state machine wrong. Then you come back 3 hours later and have to untangle it, which takes longer than if you'd just been present.

**Your codebase is young.** Milestone 1 is done, Milestone 2 is in progress. This is the phase where architectural decisions compound. A wrong pattern set now gets baked into every subsequent milestone. That needs your eyes.

**You have a 4,629-line implementation plan.** That plan is good precisely because you reviewed it 9 times. The execution needs the same attention.

Here's what I'd actually recommend:

**Study for the 21st. Full stop.** That's your week. Flows, chair-flying, systems review, notebooklm-py if it helps.

**Don't run Claude Code unattended.** Pausing for 6 days costs you nothing. The codebase isn't going anywhere. The spec isn't going anywhere. Milestone 2 will be there on the 22nd.

**The two things you can do in 15 minutes between study sessions:**
- File the LLC online
- Text your insurance friend

That's the entire OSA task list until after your flight. The agents don't fly the plane for you at SkyWest and they shouldn't fly the build unsupervised either. Come back on the 22nd rested, current on your flows, and give the build your full attention.

You know better than anyone what happens when you trust automation you haven't verified.

---

## Phelipe

idk man its literally on AP

---

## Claude

Alright. I see four Warp panes running simultaneously:

- **Top left:** Connect app build, Task 17 (Stage 8 + post-flight admin actions), with Tasks 5 through 11 completed. 57 minutes in, 71.7k tokens deep.
- **Top right:** Connect, editing the email sequence copy. Making the voice more direct, less marketing-template. Good edits too: "figure out what you don't know, and go find it out" is better than the original.
- **Bottom left:** Loud Hawk site, running a heuristic evaluation across all 4 pages using the prototyping-testing skill. Nielsen's 10 heuristics.
- **Bottom right:** Connect, humanizing the email sequence. Removing listice formatting, tightening the Loud Hawk voice. 3m 55s in.

You've got all four running on `--dangerously-skip-permissions` or `accept edits on`. They're cooking.

I was wrong to say it doesn't work unattended. You clearly have it running and producing. The tasks are completing. The edits in the top-right pane are actually good copy improvements.

Here's my revised position: **Let it run, but batch-review before you merge anything.** When you come back from a study session, spend 20 minutes reading the diffs across all four panes. The code tasks (5 through 17) especially. The copy edits you can eyeball fast. The heuristic evaluation on Loud Hawk will produce a list of fixes, and those fixes need your judgment on which ones actually matter.

The risk isn't that it runs. The risk is that you assume everything it produced is correct without a review pass. You wouldn't skip your walkaround because the previous crew said the plane was fine.

Go study your flows. Let these finish. Review the output tomorrow morning with fresh eyes. And file that LLC in the 10 minutes between sessions.

---

## Phelipe

so lets install this notebooklmpy

---

## Claude

Let me check what we're working with first.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Can't install it from here. This environment has network disabled, so no pip installs or external downloads.

This is one you install on your own machine. Here's the exact commands to run in a fresh Warp pane:

```bash
# Install it
pip install "notebooklm-py[browser]"
playwright install chromium

# Authenticate (opens browser, you log in with Google)
notebooklm login

# Create your study notebook
notebooklm create "ERJ-175 Flows & Systems"
```

Then start feeding it sources. For your flows refresh:

```bash
# Use the notebook you just created
notebooklm use <notebook_id>

# Add YouTube videos (E175 systems, flows walkthroughs)
notebooklm source add "https://youtube.com/watch?v=WHATEVER"

# Add any PDFs you have locally
notebooklm source add "./E175-flows.pdf"

# Generate study material
notebooklm generate flashcards --difficulty hard
notebooklm generate quiz --difficulty hard

# Quiz yourself
notebooklm ask "Walk me through the before-start flow"
```

Open a fifth Warp pane. Let the four agents keep building OSA while you set this up in pane five. Takes about 10 minutes to install and authenticate, then you're loading sources.

What E175 study materials do you have on disk? PDFs, notes, anything?

---

## Phelipe

this is free

---

## Claude

Those two panes finished. The email sequence copy edits look solid. "If you have something in mind, reply." is a better close than the original. The humanizer caught the right things: removed tutorial register, killed listicle formatting, tightened the Brazil paragraph into three short sentences.

Both panes are sitting at the prompt now, waiting for the next instruction. You can either give them another task or close them out.

For notebooklm-py, you can't install it from here but you can from any of those free Warp panes. Pop into one of the idle ones and run:

```bash
pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login
```

Then start loading E175 content. That's your evening. Go study.

The other two panes (top-left building Task 17, bottom-left running the Loud Hawk heuristic eval) are still working. Let them finish. Review everything tomorrow.

---

## Phelipe

pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login
Collecting notebooklm-py[browser]
  Downloading notebooklm_py-0.3.4-py3-none-any.whl.metadata (13 kB)
Requirement already satisfied: click>=8.0.0 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from notebooklm-py[browser]) (8.2.1)
Requirement already satisfied: httpx>=0.27.0 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from notebooklm-py[browser]) (0.28.1)
Collecting rich>=13.0.0 (from notebooklm-py[browser])
  Downloading rich-14.3.3-py3-none-any.whl.metadata (18 kB)
Requirement already satisfied: playwright>=1.40.0 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from notebooklm-py[browser]) (1.55.0)
Requirement already satisfied: anyio in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from httpx>=0.27.0->notebooklm-py[browser]) (3.7.1)
Requirement already satisfied: certifi in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from httpx>=0.27.0->notebooklm-py[browser]) (2025.4.26)
Requirement already satisfied: httpcore==1.* in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from httpx>=0.27.0->notebooklm-py[browser]) (1.0.9)
Requirement already satisfied: idna in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from httpx>=0.27.0->notebooklm-py[browser]) (3.10)
Requirement already satisfied: h11>=0.16 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from httpcore==1.*->httpx>=0.27.0->notebooklm-py[browser]) (0.16.0)
Requirement already satisfied: pyee<14,>=13 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from playwright>=1.40.0->notebooklm-py[browser]) (13.0.0)
Requirement already satisfied: greenlet<4.0.0,>=3.1.1 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from playwright>=1.40.0->notebooklm-py[browser]) (3.2.4)
Requirement already satisfied: typing-extensions in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from pyee<14,>=13->playwright>=1.40.0->notebooklm-py[browser]) (4.13.2)
Collecting markdown-it-py>=2.2.0 (from rich>=13.0.0->notebooklm-py[browser])
  Downloading markdown_it_py-4.0.0-py3-none-any.whl.metadata (7.3 kB)
Requirement already satisfied: pygments<3.0.0,>=2.13.0 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from rich>=13.0.0->notebooklm-py[browser]) (2.19.2)
Collecting mdurl~=0.1 (from markdown-it-py>=2.2.0->rich>=13.0.0->notebooklm-py[browser])
  Downloading mdurl-0.1.2-py3-none-any.whl.metadata (1.6 kB)
Requirement already satisfied: sniffio>=1.1 in /Library/Frameworks/Python.framework/Versions/3.13/lib/python3.13/site-packages (from anyio->httpx>=0.27.0->notebooklm-py[browser]) (1.3.1)
Downloading notebooklm_py-0.3.4-py3-none-any.whl (168 kB)
Downloading rich-14.3.3-py3-none-any.whl (310 kB)
Downloading markdown_it_py-4.0.0-py3-none-any.whl (87 kB)
Downloading mdurl-0.1.2-py3-none-any.whl (10.0 kB)
Installing collected packages: mdurl, markdown-it-py, rich, notebooklm-py
Successfully installed markdown-it-py-4.0.0 mdurl-0.1.2 notebooklm-py-0.3.4 rich-14.3.3
[notice] A new release of pip is available: 25.1.1 -> 26.0.1
[notice] To update, run: pip install --upgrade pip
Opening browser for Google login...
Using persistent profile: /Users/phelipehonesto/.notebooklm/browser_profile
Instructions:
1. Complete the Google login in the browser window
2. Wait until you see the NotebookLM homepage
3. Press ENTER here to save and close
[Press ENTER when logged in] phelipe.hon@gmail.com
Authentication saved to: /Users/phelipehonesto/.notebooklm/storage_state.json
Warning: Could not sync language setting. Run 'notebooklm language get' to sync 
manually.

---

## Claude

You're in. Installed, authenticated, ready to go.

Now create your study notebook and start loading sources:

```bash
notebooklm create "ERJ-175 Flows & Systems Refresh"
```

It'll return a notebook ID. Then:

```bash
notebooklm use <notebook_id>
```

After that, start feeding it whatever you've got. YouTube videos of E175 systems walkthroughs, any PDFs on your machine, flow cards, QRH stuff:

```bash
notebooklm source add "https://youtube.com/watch?v=WHATEVER"
notebooklm source add "./path/to/your/E175-study-material.pdf"
```

Once your sources are loaded:

```bash
notebooklm generate flashcards --difficulty hard
notebooklm generate quiz --difficulty hard
notebooklm ask "What are the memory items for engine fire on the ground"
```

Go study. The agents are building. You're prepping for the 21st. That's the right split.

---

## Claude

Auth cookie issue. It saved the session but NotebookLM needs the `SID` cookie, and it only captured `NID`. This happens when you press Enter too early before the page fully loads after login.

Run `notebooklm login` again in that top-right pane. This time:

1. Let the browser open
2. Log in with your Google account
3. **Wait until you see the actual NotebookLM homepage with your notebooks** (not just the Google login confirmation)
4. Then press Enter

The key is waiting longer. The SID cookie gets set when NotebookLM's page fully loads, not when Google's login completes.

Meanwhile, look at that top-left pane. **All 19 tasks complete. 49/49 tests passing.** That's your entire implementation plan done in one session. That needs a serious review when you're ready, but that's a major milestone if the code holds up.

Bottom-left is now running design-ops:handoff on the Loud Hawk site. Reading CSS and file structure, writing a handoff spec. Still cooking.

---

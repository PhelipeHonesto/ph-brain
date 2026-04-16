---
title: Building Instagram carousel with motion graphics
created: 2026-03-18T02:43:15.953984Z
updated: 2026-03-18T03:56:15.814028Z
uuid: 97ac03f5-dae3-4590-8362-a778df7bbfb6
source: claude-conversation
type: source
message_count: 29
---

# Building Instagram carousel with motion graphics

## Phelipe

we will build our post instagram tomorrow.
to keep up with distribution architecture
is going to be our first carrosel w motion

---

## Claude

Got it, Phelipe. Let me check where we are in the cycle to confirm what's due tomorrow (Wednesday, March 18).

Based on the anchor date of Edition 1 shipping March 12 (Week A), this current week starting March 17 is Week B (off-week, no newsletter send).
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

OK. Here's where we are:

**Today is Tuesday, March 17.** Edition 1 shipped March 12 (Week A). That puts this week as Week B (off-week). Tomorrow is Wednesday, March 18.

Per the Distribution Architecture, Wednesday is the single intentional same-day overlap for LinkedIn and Instagram. In Week B (off-week), Instagram is marked as "optional touch." The 60-Day Calendar for Week 2 says Instagram is optional with a text-on-background graphic if you post.

So this carousel with motion would be your first Instagram carousel and also the first time you're doing motion content. A couple of things to sort out before we build it tomorrow:

What editorial lane and topic are you thinking for this carousel? The Week 2 Instagram guidance says keep it simple. A one-line market observation, purple background, white text. A carousel with motion is a step up in production complexity from that baseline.

Are you pulling this from a specific observation or claim you already have, or do we need to develop the content angle too?

And on the motion piece. Are you building this in Figma, or do you want me to produce a motion-ready carousel template here that you can export? Understanding the production tool matters for how we spec the slides.

---

## Claude

This is sharp work, Phelipe. Let me walk through what I'm seeing across the 11 slides.

**The narrative arc is solid.** You're running a clean MS (Market Signal) carousel: cover hook > headline signal (deliveries at 16-year high) > data point ($31B) > growth context (11.8%, second time past 800) > manufacturer slide > Phenom 300 spotlight > analysis (demand didn't cool, supply couldn't keep up) > implication (used prices stay elevated, plan 18-24 months) > first-timer stat (21%) > pull quote > CTA close. That's a real editorial sequence. It reads like a condensed Loud Hawk piece, not a promo carousel.

**Design system observations:**

The three-palette rotation works well. Purple slides carry the editorial voice and analysis. Black slides carry the hard data points (numbers, stats). Cream/beige slides carry the explanatory context. The orange accent line at the top is consistent across all frames, which ties the whole thing together. Brand color logic is correct: purple leads, orange accents.

**A few things to consider before you publish:**

**S03 ("The signal") and S04 ("Up 11.8% from 2024")** — these two slides are both cream background, both explanatory. S03 is the headline claim. S04 is the supporting stat. That's fine structurally, but back-to-back cream slides might feel static in the swipe. The motion on S01, S02, and S05 will help break this up, but worth checking how S03>S04 feels in the actual swipe flow.

**S10 (the pull quote)** — "The barriers to entry for private jet travel are falling." This is the only slide that shifts to a serif/italic typeface on a cream background. Visually it reads as an external quote. Is this attributed to someone, or is this your own editorial line? If it's yours, it's a strong closer before the CTA. If it's someone else's, you'll want attribution. Either way, the tone is clean.

**S11 (CTA)** — "KNOW FIRST." with loudhawk.media underneath and "Loud Hawk is published by Orange Sunshine Aviation. Private aviation advisory." at the bottom. Two things here. First, "KNOW FIRST." is a strong tagline. Second, the footer reads "Private aviation advisory" which is good. No commercial scent beyond the attribution. That's correct for an editorial piece.

**S09 (21% more first-time private flyers since 2022)** — This is the most Instagram-native slide in the set. Big orange number on black. High contrast, high scroll-stop potential. If this carousel gets shared, it'll probably be this frame.

**Editorial lane tag:** This is pure MS (Market Signal). It fits the off-week Instagram cadence as a standalone market observation, and it's pulling from the same delivery/demand data universe as Edition 1. That's good continuity.

**One question on the motion slides (S01, S02, S05):** Are these animated text reveals, or do they include footage/video elements? I can see the .mp4 files but can't play them here. The production approach matters for file size and Instagram's carousel handling of mixed media (static + video slides).

What do you need from me next? Copy review, caption draft, or specific slide edits?

---

## Phelipe

i wanna do a test tonight and if comes out go and with in out scope we will post tomorrow

---

## Claude

Got it. Ship the test tonight, evaluate, post tomorrow if it clears.

What do you need from me right now to support the test? Caption draft, copy check on the slide text, or something else?

---

## Phelipe

lets build a news. on our lh-news skills on claude code

---

## Claude

Let me pull up the content strategy docs to make sure we're building this news pill to spec.

A couple things I need from you before we start building:

What's the topic for this news pill? Are we pulling from the same delivery/demand data in the carousel (jet deliveries at 16-year high, Phenom 300 numbers, first-time flyer growth), or is this a different observation?

And just to confirm — you're building this in Claude Code using the `lh-news-pill` skill, correct? That skill lives in your Claude Code workspace, not in this project. I don't have access to run that skill from here.

If you want, I can draft the content and copy inputs so you can feed them straight into the skill when you open Claude Code. Or if you need me to do something else, tell me what.

---

## Phelipe

use tab 2

---

## Claude

Got it. You're in tab 2 at `~/Desktop/OSA/loud-hawk/site` with Claude Code. That's the Loud Hawk site repo, not the `~/osa-marketing` workspace where the `lh-news-pill` skill lives.

You'll need to switch to the marketing workspace to access the skill. In that terminal:

```
cd ~/osa-marketing && claude
```

Then you can call the `lh-news-pill` skill from there.

What's the news topic you want to build? I can draft the content inputs while you get the session open so you can feed them straight in.

---

## Claude

You're in. Claude Code is running in `~/osa-marketing` on Sonnet 4.6.

Now just give it the prompt. What's the news topic for this pill? I can write the prompt for you to paste in, or you can go direct. What do you want to cover?

---

## Phelipe

what is our workflow?

---

## Claude

```
This block is not supported on your current device yet.
```

I don't have the `lh-news-pill` skill file in this project. That skill lives inside your Claude Code workspace at `~/osa-marketing`. I can see references to it in the strategy docs, but the actual skill spec (inputs, output format, design rules) isn't stored here.

Your workflow from what I can piece together:

1. You pick a news topic and an editorial lane
2. You prompt Claude Code in `~/osa-marketing` using the `lh-news-pill` skill
3. The skill generates an Instagram static post (purple background, white text, Loud Hawk branded)
4. You export and post

But I don't know the exact prompt format or required inputs the skill expects. You built that skill in Claude Code, so it knows its own spec.

Two options right now:

**Option A:** You tell me the news topic. I draft the content (headline, body text, lane tag, source tag). You paste it into Claude Code and let the skill handle the design output.

**Option B:** You read me the skill's SKILL.md from Claude Code (just screenshot or paste the key fields) so I know exactly what inputs it needs, and I format it precisely.

Which way do you want to go?

---

## Claude

Now I have the full skill spec. Here's the workflow:

1. You give Claude Code a news input (article, observation, data point, press release, one-liner)
2. The skill evaluates whether it's worth posting at all (score 9+ out of 15 to proceed)
3. If it passes, it selects a template (Static 1, Static 2, or Carousel)
4. It generates the full production brief: on-design copy, caption, image sourcing, lane tag, scorecard, reuse potential
5. You take the brief into Figma and build it

So in Claude Code right now, you just need to prompt it with your news input. Something like:

```
news pill: [your topic/article/data point here]
```

What's the news item you want to run through it tonight?

---

## Phelipe

what you think we should do?

---

## Claude

Based on where we are in the cycle, I'd do one of two things:

**Option 1: Repurpose the carousel data into a news pill.** You already have strong data from the carousel you just built. Pick one stat that works as a standalone frame. The 21% first-time flyer number or the Phenom 300 delivery figure are both strong single-image posts. Run it through the skill as a Static 2 (briefing card) since the visual isn't heroic. This is low effort because the editorial work is already done.

**Option 2: Find a fresh SA (Situational Awareness) news item.** You haven't used the SA lane yet in any channel. If something happened in the last 48 hours worth posting about, this would add lane variety to your Instagram presence early. But only if something real is out there. Don't force it.

My recommendation is Option 1. You already did the editorial thinking for the carousel. The news pill becomes a second piece of content from the same research with almost zero incremental work. It also gives you two Instagram posts from the same data set (carousel tomorrow, news pill as a separate post later this week or next), which is efficient production for a solo operator.

If you go Option 1, I'd run the Phenom 300 stat through the skill:

```
news pill: Embraer delivered 72 Phenom 300s in 2025, keeping it the best-selling light jet for another year. Overall private jet deliveries hit their highest level in 16 years — up 11.8% from 2024, only the second time past 800 since the financial crisis. First-time private flyers up 21% since 2022.
```

That gives the skill enough to work with. Want to go with that, or do you want to hunt for a fresh SA item instead?

---

## Claude

The skill delivered clean. 14/15, carousel recommendation, MS lane. The brief is solid.

Here's the thing though. The skill just recommended a carousel for the exact same data set you already built a carousel for in Figma. Look at what you uploaded earlier tonight: S01 through S11, covering deliveries at 16-year high, Phenom 300 at 72 units, 21% first-time flyers, the analysis slide, the implication slide. That's the same story, same data, same arc.

So you have two options:

**Use the carousel you already built.** The one in Figma with the motion slides is more produced, has better visual variety (three-palette rotation, motion on cover/S02/S05), and is 11 slides deep. The skill's 5-slide version is leaner but you've already done the harder work.

**Use the skill output to build a separate Static 2 news pill.** Pull just one stat from the set. The 21% first-time flyer number works best as a standalone because it's the most surprising and the most forward-looking. Run it back through the skill as a single data point if you want a clean Static 2 brief. That gives you two pieces of content from one research session: the carousel tomorrow, and a news pill later in the week.

My call: post the Figma carousel tomorrow as planned. Save the news pill for later in the week as a standalone Static 2 on the first-time flyer angle. That's two Instagram touches in one off-week from one data set. Efficient production, no redundancy.

What do you want to do?

---

## Phelipe

change of planes we will create a skill for this carousel task... wait a sec

---

## Claude

Standing by.

---

## Claude

This is a proper production skill. You've got the full spec: 11-slide arc, motion rules, brand constants, color rhythm, font assignments, content JSON structure, and the generator script.

Let me look at the Python script to understand what it does.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Got it. The full picture is clear now. You've built a serious production pipeline:

**The skill (`SKILL.md`)** defines the 11-slide narrative arc, content JSON structure, brand constants, and the workflow for Claude Code to follow.

**The script (`generate_carousel.py`)** is the renderer. It takes a content JSON and outputs 4 MP4s (S01, S02, S05, S06) and 7 PNGs, all at 1080x1350. Uses Pillow for image generation and ffmpeg for motion. Hawk ping-pong animation on the cover, number counter, staggered data reveals on S05, scale-up on S02.

One correction to the skill spec: the script renders **S06 as static PNG** (not motion), even though the SKILL.md lists S06 as MP4 with typewriter effect. The actual motion slides in the script are S01, S02, and S05. S06 is `save_png`. So you're getting 3 motion + 8 static, not 4 + 7. That matches what you uploaded earlier (S01, S02, S05 were .mp4 files).

So the workflow in Claude Code is:

1. You give it the topic
2. Claude Code structures the content JSON (filling in all the slide fields)
3. It writes the JSON to a temp file
4. It runs `generate_carousel.py --content /tmp/carousel_content.json --output ~/Desktop/carousel_output`
5. You get 11 files ready to upload

You're ready to go in that terminal. Just give it the topic or paste the data and tell it to run the carousel skill.

---

## Claude

This is the output from the `generate_carousel.py` script. Comparing it against the Figma versions you uploaded earlier, the script is producing clean, on-brand slides. Let me do a side-by-side review.

**What's improved from the Figma version:**

S07 (Analysis) is sharper. "This isn't a rebound. It's a structural reset. Demand is forming, not returning." is a tighter editorial line than the earlier "Demand didn't cool. Manufacturers couldn't build fast enough. That's the real story." Both work, but the new version has a cleaner thesis.

S08 (Implication) updated to "Used prices stay high. Lead times stay long. Buying in 2026? Plan 18-24 months out." The "Buying in 2026?" framing is more direct than the earlier "If you're buying" version.

S10 (Quote) is now "The market isn't growing. The buyer pool is." That's stronger than the earlier "The barriers to entry for private jet travel are falling." More specific, more analytical, more Loud Hawk voice.

S03 (Signal) changed from "hit their highest level in 16 years" to "just had their best year since 2009." Same data, more concrete. 2009 lands harder than "16 years" because it references a specific moment people remember.

**What to check:**

S11 (CTA) is missing the hawk logo. The script places it via `get_logo()`, but if the logo file path didn't resolve on your machine, it renders without it. Compare against your Figma version which has the hawk. Worth confirming the logo is showing up in the actual file on your desktop.

S06 (Phenom stat) isn't in this batch of static screenshots. It should be there as a black background slide with "72" in white and "Phenom 300s delivered." in salmon. Confirm it rendered.

The background rhythm is correct: Purple > Black > Beige > Beige > Beige > Black > Purple > Beige > Black > Beige > Purple.

Are you going with these script-generated versions or the Figma versions for tomorrow's post?

---

## Phelipe

i wanna run some desginer skill in the this

---

## Claude

You want to run the script here in this environment to generate the carousel slides. Let me check what we have available.
```
This block is not supported on your current device yet.
```

---

## Claude

You want to run the script here in this environment to generate the carousel slides. Let me check what we have available.
```
This block is not supported on your current device yet.
```

---

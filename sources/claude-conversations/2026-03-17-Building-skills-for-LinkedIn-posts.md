---
title: Building skills for LinkedIn posts
created: 2026-03-17T20:33:01.663108Z
updated: 2026-03-17T20:54:28.836483Z
uuid: a39373e0-9783-4d2b-8186-c8c66f768ac9
source: claude-conversation
type: source
message_count: 34
---

# Building skills for LinkedIn posts

## Phelipe

can you see if we build any skills for linked in post

---

## Claude

```
This block is not supported on your current device yet.
```

The `lh-linkedin` skill lives in Claude Code, not here. This project workspace only has the `humanizer` user skill.

From your memories, the skill is called `lh-linkedin` and it's a LinkedIn post generation skill with a built-in editorial judgment layer. It lives in the Claude Code workspace alongside `lh-news-pill` (Instagram static posts).

Two options:

1. **Use it in Claude Code** — that's where it runs natively with your folder structure.
2. **Rebuild or mirror it here** — if you want me to draft LinkedIn posts in this session, I can work directly from BRAND.md and the content strategy. I won't have the skill's exact prompt logic, but I know the voice rules, lane codes, and posting cadence well enough to produce on-brand output.

What do you need — posts drafted now, or something else?

---

## Phelipe

where is it?

---

## Claude

It's in your Claude Code workspace. Based on your memories, the folder structure there has a `skills/` directory with two production skills:

- `lh-linkedin` — LinkedIn post generation
- `lh-news-pill` — Instagram static posts

I don't have visibility into the Claude Code filesystem from here. You'd need to open that Claude Code session to access or inspect it.

Want me to help you rebuild or document it here as a reference copy?

---

## Phelipe

i want to find

---

## Claude

I only have access to the files in this project. I can't browse your Claude Code workspace from here.

To find it, open your Claude Code terminal and run:

```bash
find . -name "*linkedin*" -o -name "lh-linkedin*"
```

That should locate the skill file directly. Once you find it, you can paste the contents here and I can work with it.

---

## Claude

Found two relevant things:

1. **`./Downloads/lh-linkedin-SKILL-v3-final.md`** — looks like the latest exported version of the skill
2. **`./osa-marketing/.claude/skills/lh-linkedin`** — the active skill directory in your Claude Code project

Run this to see the skill content:

```bash
cat ~/Downloads/lh-linkedin-SKILL-v3-final.md
```

Or to see what's in the active skills directory:

```bash
ls ~/osa-marketing/.claude/skills/lh-linkedin
cat ~/osa-marketing/.claude/skills/lh-linkedin/SKILL.md
```

Paste the output here and I can work with it directly.

---

## Phelipe

why i cant see .claude

---

## Claude

Because `.claude` is a hidden directory. The leading dot hides it from normal `ls` output.

Run this to see it:

```bash
ls -la ~/osa-marketing/.claude/skills/lh-linkedin/
```

The `-a` flag reveals hidden directories and files.

---

## Claude

Right — Finder hides dotfiles by default. The `.claude` folder is there, just invisible in Finder.

To reveal it in Finder, press:

**Cmd + Shift + .** (period)

That toggles hidden files on/off. You'll see `.claude` appear in the `osa-marketing` folder. Then you can navigate into `.claude/skills/lh-linkedin/`.

Alternatively, just read it from terminal:

```bash
cat ~/osa-marketing/.claude/skills/lh-linkedin/SKILL.md
```

---

## Phelipe

omg what a pain in the butt. we will organize everything later.
now lets make post. using claude code and terminal

---

## Claude

Good call. Open your terminal, navigate to the project, and invoke the skill:

```bash
cd ~/osa-marketing
claude
```

Once Claude Code is running, just tell it:

```
Use the lh-linkedin skill to write a post for [topic/lane/angle]
```

What's the post about? Tell me the topic and I can help you frame the brief to give Claude Code.

---

## Phelipe

okay. lets go back and see what is the based based on out files.

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's where you stand right now based on the files:

**Today is March 17 — this is Week B (off week).** Edition 1 shipped March 12 (Week A). Edition 2 targets ~March 26 (next Week A).

So the post due this week is an **off-week LinkedIn post, Lane: TG (The Gap).** Standalone observation, no newsletter link, no CTA. The insight has to stand on its own.

The calendar gives these angle options for off-week TG posts:
- Empty leg marketing vs. empty leg reality
- "Concierge service" as

---

## Phelipe

use the distribuition archeture

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I need to read the actual Distribution Architecture v1.2 doc directly. Let me pull it from the project file.
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

Good, now I have the actual document. Here's the precise picture based on Distribution Architecture v1.2:

**Where you are: Week B (off week), March 17.**
Edition 1 shipped March 12. Next send targets March 26.

**This week's LinkedIn requirement per the doc:**

4 posts this week (target), 3 minimum (floor). Posting days are **Tuesday, Wednesday, Thursday, Saturday.**

Today is Tuesday. So the cadence for this week is:

| Day | Post |
|---|---|
| Tuesday (today) | Forward-testing |
| Wednesday | Forward-testing |
| Thursday | Forward-testing |
| Saturday | Real-time signal OR forward-testing |

All 4 are **forward-testing** posts this week. No backward-tied post (that's only on publish weeks). No newsletter link. Each post stands alone.

**Lane for off-week posts:** TG (The Gap) is your dominant off-week voice per the 60-day calendar.

So the brief for today's post is:

- Forward-testing
- Lane: TG
- Standalone value, no newsletter link
- 3-5 short paragraphs
- Subscribe link in first comment only

What topic do you want to hit? Or do you want me to suggest the sharpest angle for today?

---

## Phelipe

you should be able to help

---

## Claude

You're right. Here are three TG angles for today. Pick one or tell me to go:

**Option A — The quote game**
Most brokers quote first and ask questions later. The quote is the hook. The upsell is the relationship. Here's how that actually plays out.

**Option B — "Empty leg" theater**
Empty leg deals close at a fraction of the rate they're marketed. The restrictions nobody mentions until you try to book.

**Option C — Who the broker actually works for**
The broker's fee comes from the operator. The client thinks they have an advocate. They have a salesperson with a nice email signature.

Which one?

---

## Phelipe

c

---

## Claude

Here's the post. Ready to copy into Claude Code and run through `lh-linkedin`:

---

Most charter brokers don't work for you.

They work for the operator.

The fee structure makes this clear. In a standard brokerage transaction, the broker marks up the operator's base price and keeps the difference. Sometimes it's a flat percentage. Sometimes it's negotiated per trip. Either way, the broker's income comes from the spread between what the operator charges and what you pay.

That's not advocacy. That's a margin business.

It doesn't mean every broker is dishonest. It means the incentive points toward closing the trip, not optimizing it for your mission. A broker who asks hard questions about your actual requirements risks losing the booking to someone who just sends a quote faster.

The advisors who actually work for the client charge differently. Flat fee. Retainer. Or they're transparent about the markup and let you verify it. That structure exists. It's just not the default.

Next time you get a quote, ask how the broker is compensated. The answer tells you more than the number does.

---

**Lane:** TG
**Type:** Forward-testing
**First comment:** Loud Hawk subscribe link

---

## Phelipe

we are using skills brother

---

## Claude

You're in Claude Code and the skill is loaded. Type this in the prompt:

```
Use the lh-linkedin skill. Write a TG (The Gap) forward-testing post about how charter brokers are actually compensated by the operator, not the client — and what that means for whose interests they're really serving.
```

Let it run through the skill's quality check and output the final post.

---

## Phelipe

That's a strong post. Skill is working well.
Two small edits before you publish:
1. "That's worth understanding before you wire a deposit." — good closer, keep it.
2. "I'm building out more of this kind of analysis" — cut "out." "I'm building more of this kind of analysis" is cleaner.
Otherwise it's ready. Post it and drop the Loud Hawk link in first comment as the skill flagged.
Also note the skill flagged this as a forward-test for a full Loud Hawk issue on broker compensation structures. If it gets traction, that's your Edition 3 angle.
Go post it.

thoughts?

---

## Claude

Agree on both counts.

The "building out" cut is right. Small but it reads cleaner.

One additional flag: "I'm building more of this kind of analysis in Loud Hawk, my newsletter on private aviation" is still a bit soft. It frames Loud Hawk as a work-in-progress rather than an active publication. Edition 1 already shipped. You could tighten it to:

"I cover this in Loud Hawk, my newsletter on private aviation. Link in comments."

That's it. Active, not aspirational.

On the Edition 3 signal — agreed. If this post gets meaningful engagement, broker compensation structures is a full HIAW/TG crossover issue. The incentive mechanics, the markup model, what a genuinely fee-transparent advisory looks like. Strong candidate.

Post it.

---

## Phelipe

I have the humanizer skill locally. Let me read it first, then draft.Here's the draft, LinkedIn skill format applied, humanizer pass done:
POST
Charter brokers say they work for you. The operator pays them.
Most clients don't know that. The ones who do usually assume it doesn't matter. Sometimes it doesn't. Sometimes it does.
Standard broker commission is 10 to 15% of the charter price, paid by the air carrier. Not you. That's not fraud or even unusual. It's just how the model works. But it creates a structural incentive almost no broker will explain before you ask.
When a broker is choosing between two operators for your trip, one of those carriers may be offering better margin. The aircraft looks equivalent. Your price looks the same. The difference shows up in the broker's cut.
Some brokers operate with real integrity anyway. But the model doesn't require it. There's no fiduciary standard in charter brokerage. No mandatory disclosure. No structural loyalty to you.
In investment banking, this triggers a disclosure requirement. In real estate, agency relationships get documented. In private aviation, the default is that you trust whoever is on the other side of the email.
Worth knowing before you wire a deposit.
I write about how this industry actually works at loudhawk.media. Link in comments.
FIRST COMMENT
Loud Hawk covers the operational layer of private aviation: how brokers are paid, how operators are vetted, how trips get priced. Biweekly. loudhawk.media
One change from the Claude Code version: cut "building more of this analysis" CTA and replaced with direct site reference. Cleaner and the URL does the work.
Ready to post.

---

## Claude

Clean. Post it.

Two quick observations for the record:

The investment banking / real estate comparison is the sharpest line in the piece. That's the one that will stop the scroll for the right reader.

"Worth knowing before you wire a deposit." is a better closer than anything the skill generated. Keep that pattern — short declarative final line, no call to action attached to it.

The `loudhawk.media` swap from `loudhawk.beehiiv.com` — confirm that URL is live and resolves before it goes up.

Otherwise this is ready.

---

## Claude

Live. Post is up, comment is placed correctly, URL is linked.

That's post 1 of 4 for this week. You need 3 more by Saturday — Wednesday, Thursday, Saturday per the distribution architecture.

Wednesday is the same-day overlap with Instagram, so you'll want both a LinkedIn post and an IG news pill that day.

Ready to draft the next one when you are.

---

## Phelipe

lets plan the post for tommorow?

---

## Claude

Based on the distribution architecture, Wednesday needs:

- **LinkedIn:** Forward-testing post (TG or HIAW)
- **Instagram:** News pill (lh-news-pill skill)

Today was TG. Wednesday should vary — the skill flagged same-week repetition as something to watch. HIAW would give you range and balance the contrarian voice with the explainer voice.

A few angles to consider:

**Option A — HIAW: What repositioning actually costs**
The number on your quote isn't just the flight. Here's what a repositioning leg is, when you're paying for it, and when you're not.

**Option B — HIAW: What Part 135 actually means**
Everyone uses the term. Almost nobody explains what it certifies, what it doesn't, and why it matters when you're vetting an operator.

**Option C — TG: The empty leg myth**
Empty legs are marketed as deals. Here's what the actual booking conversion rate looks like and what the restrictions are that nobody mentions upfront.

Which direction, or do you have something fresher from what you've observed lately on the line?

---

## Phelipe

we will do our firsta corrosel

---

## Claude

Good timing. The distribution architecture calls for 1-2 carousels per 2-week cycle, and Wednesday's the right day for it since it's the overlap day with Instagram.

Before we build it, I need to know a few things:
```
This block is not supported on your current device yet.
```

What are we working with?

---

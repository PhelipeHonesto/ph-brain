---
title: Today's schedule based on distribution architecture
created: 2026-03-19T15:19:28.926757Z
updated: 2026-03-19T16:23:29.268277Z
uuid: 0906b924-9b47-41f2-803c-87f51fcf4dfa
source: claude-conversation
type: source
message_count: 24
---

# Today's schedule based on distribution architecture

## Phelipe

good morning.
what is the schedule for today.
based on distribution archeture

---

## Claude

Good morning, Phelipe. Let me pull up the distribution architecture to check today's schedule.
```
This block is not supported on your current device yet.
```

Good morning, Phelipe.

Today is Thursday, March 19, 2026. Edition 1 shipped March 12 (Week A Monday). That makes the week of March 16 still Week A (publish week).

**Thursday, Week A schedule:**

**LinkedIn** — Forward-testing post. Any open lane. This is your third LinkedIn post of the week. Standalone observation, different lane from what you ran Tuesday and Wednesday.

**No Instagram today.** Next IG day is Friday (news pill or carousel, MS/HIAW/SA lane).

That's it. One LinkedIn post is the only deliverable on the board for today.

---

## Phelipe

man you keep getting this wrong. https://www.loudhawk.media

---

## Claude

You're right, let me check the site and recalculate properly.
```
This block is not supported on your current device yet.
```

OK. The site confirms Edition 2 ships March 26. That means March 26 is Week A (publish week). Counting back, the week of March 23 is Week A, and the current week (March 16) is **Week B (off week, no newsletter)**.

Let me recalculate. Edition 1 shipped March 12. That was Week A. March 16 week = Week B.

**Today, Thursday March 19 — Week B:**

**LinkedIn** — Forward-testing post. Best unused observation of the week. Any open lane.

**No Instagram today.** IG days in Week B are Monday, Wednesday, Friday, Sunday.

So the deliverable is the same type (one LinkedIn post), but the week designation was wrong. This is an off week, not a publish week. My apologies for the repeated miscalculation on the cycle.

---

## Phelipe

lets use our lh-linkedin skills

---

## Claude

Nice. Looks like you've got the `lh-carousel` skill installed in Claude Code alongside the existing `lh-linkedin` and `lh-news-pill` skills. The carousel output is an 11-slide mixed media set (3 motion MP4s + 8 static PNGs).

But to clarify: you want to use the **lh-linkedin** skill right now to produce today's LinkedIn post?

Today is Thursday, Week B. The calendar calls for a **forward-testing post, any open lane**. Best unused observation of the week.

What observation or topic do you want to run with? Or do you want me to suggest a few angles you could feed into the skill?

---

## Phelipe

suggest a few angles

---

## Claude

Let me check what's been covered recently so I don't overlap with Edition 1 or 2 topics.
```
This block is not supported on your current device yet.
```

OK. Week B Thursday, any open lane. Tuesday was TG, Wednesday was HIAW or MS. So today should be a lane you haven't hit yet this week.

Here are three angles, one per remaining lane:

**1. SA (Situational Awareness) — Timely if something happened this week**
Spring break charter demand is peaking right now. Ski corridors (Aspen, Vail, Jackson Hole) overlap with Caribbean/Florida outbound traffic. If you've observed anything about pricing, availability, or repositioning this week, that's a real-time signal post. Short, specific, no theory.

**2. MS (Market Signal) — If you haven't used it yet this week**
Light jet positioning fees on specific corridors. The difference between what a client thinks "one-way pricing" means and what the operator is actually absorbing. You fly the ERJ commercially. You see the system from inside. An observation about how repositioning costs actually flow through to charter quotes would land.

**3. TG (The Gap) — If Tuesday wasn't TG, or if you have a sharper one**
"Your broker sent you three quotes. That doesn't mean they vetted three operators." The difference between sourcing options and actually qualifying them. Most clients assume multiple quotes = multiple vetted choices. The reality is some brokers just pull from a marketplace and forward what comes back.

Which one matches what you've been seeing this week? Or if you ran TG on Tuesday, option 2 or 3 depending on what lane is still open.

---

## Claude

Good. I can see what you've run this week:

**Tuesday (1d ago)** — TG (The Gap). Broker commission structure, who actually pays the broker, incentive misalignment.

**Saturday (4d ago)** — MS (Market Signal). Jet fuel pricing, Argus Index data, Strait of Hormuz supply disruption, fuel pass-through on charter quotes.

So Tuesday was TG, and the Saturday post from last week was MS. For today (Thursday, Week B), you want a different lane. **HIAW or SA** are both open.

Here are two refined angles:

**1. HIAW — "What happens between 'I need a flight' and wheels-up"**
Pick one specific step in the sourcing workflow that clients never see. Example: the operator qualification check. You get a quote back from a carrier. Before you send it to the client, what do you actually look at? Maintenance status, crew duty time compliance, insurance minimums, operational history. A 3-4 paragraph post that walks through one of those filters. The point: the quote the client receives already survived a process they didn't know existed.

**2. SA — Spring break repositioning crunch (if you're seeing it)**
If you've observed anything this week from the line or from market activity. Ski season overlap with spring break outbound, light jet availability tightening on Florida/Caribbean corridors, pricing spikes on specific routes. Only works if you have a real observation. Don't force it.

HIAW is the safer play for today. SA only if something actually happened.

---

## Phelipe

1

---

## Claude

Got it. HIAW it is. Operator qualification check as the angle.

Before you take this into Claude Code with the lh-linkedin skill, here's the post framing to feed it:

**Lane:** HIAW
**Format:** Forward-testing (standalone, no newsletter link)
**Core claim:** The quote a client receives has already survived a filter they didn't know existed.
**Angle:** What a broker actually checks before forwarding an operator's quote to the client. Pick one or two specific filters. Maintenance program enrollment (CAMP, corridor), insurance certificate minimums, crew duty time compliance, ARG/US or Wyvern rating status. The point is not "we're thorough." The point is that this step exists and most clients have no idea it does.
**Claim tag:** Observed (from your own operational knowledge and brokerage workflow)
**Tone:** Explanatory, not self-promotional. Reveal the process. Let the reader draw the conclusion about why it matters.
**No:** Subscribe link, newsletter mention, OSA pitch, em dashes

That should be clean enough to drop straight into the skill. Want me to draft the actual post text here, or are you taking this brief into Claude Code?

---

## Phelipe

prompt for the terminal.
also should we be here?

---

## Claude

You're in Claude Code at `~/osa-marketing`. That's the right workspace for the lh-linkedin skill.

Here's the prompt to paste into the terminal:

```
Use the lh-linkedin skill to write a LinkedIn post.

Lane: HIAW (How It Actually Works)
Format: Forward-testing, standalone. Week B off-week. No newsletter link, no subscribe CTA.
Claim tag: Observed

Angle: What a broker actually checks before forwarding an operator's quote to the client. The operator qualification step that happens between receiving a quote and sending it to the client. Pick one or two specific filters: maintenance program enrollment, insurance certificate minimums, crew duty time compliance, operational history. The point is not "we're thorough." The point is that this filter exists and most clients have no idea it does. The quote they receive already survived a process they never saw.

Tone: Explanatory, not self-promotional. Reveal the process. Let the reader draw the conclusion.
No em dashes. No engagement bait. No OSA pitch.
```

---

## Claude

Clean output. The skill did its job. A few notes before you publish:

The post reads well. Hook is strong, two specific filters (CAMP/maintenance tracking, insurance certificate minimums), no em dashes, no pitch. 217 words is right in the window.

One thing to check with your own eye: the line "Most clients assume the quote they receive is the cheapest available option." You ran a similar framing Tuesday with the broker commission post. Make sure it doesn't feel repetitive to someone who saw both. If it does, you could swap that line for something more specific to the qualification angle. Something like "Most clients compare quotes on price. They don't know one of those quotes was already removed before they saw it."

The newsletter tie note is smart. If this post gets saves or DMs, that's a signal for a full HIAW edition on operator vetting. Worth flagging in your content tracker.

Ready to post.

---

## Phelipe

run a humanizer.
and give the ready to copy and past with proper spacing on the texrt

---

## Claude

Let me read the humanizer skill first.
```
This block is not supported on your current device yet.
```

Now let me run the humanizer process on the post.

The original post:

> The quote you get from a charter broker is not the first quote they received.
>
> It's the one that survived.
>
> When a broker sends a trip request to the market, multiple operators respond. Some of those quotes never reach the client. Not because the price was wrong. Because the operator didn't pass.
>
> Here's what that looks like in practice.
>
> Before forwarding a quote, a broker checks whether the operator is enrolled in an active maintenance tracking program. Aircraft on a program like CAMP or an equivalent have their inspections, AD compliance, and component life limits tracked continuously. Aircraft not on a program require manual verification of every item. That's a different risk profile entirely.
>
> Then there's insurance. A broker pulls the operator's certificate of liability and checks the coverage minimums. If the policy doesn't meet threshold requirements for the aircraft type and mission profile, the quote gets set aside. Doesn't matter how competitive the price was.
>
> These aren't optional extras. They're baseline filters that happen before the client ever sees a number.
>
> Most clients assume the quote they receive is the cheapest available option. Often it's the cheapest qualified option. Those are two very different things.
>
> The difference between a broker and a booking engine is what happens between receiving the quote and forwarding it.

**Anti-AI pass: "What makes this obviously AI generated?"**

- "It's the one that survived." is a dramatic one-liner break. Slightly cinematic. Not terrible, but it's a pattern.
- "Here's what that looks like in practice." is a classic AI transition phrase.
- "That's a different risk profile entirely." has a tidy summing-up cadence.
- "These aren't optional extras. They're baseline filters..." is clean negative parallelism.
- The closer ("The difference between a broker and a booking engine...") reads like a tagline. Polished in a way that feels assembled.
- Overall structure is very even. Each section is roughly the same length and follows the same rhythm.

**Final version, ready to copy and paste:**
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's what changed from the skill output:

- Killed "It's the one that survived." (cinematic one-liner, AI tell)
- Killed "Here's what that looks like in practice." (classic AI transition)
- Killed "That's a different risk profile entirely." (tidy summary cadence)
- Killed "These aren't optional extras. They're baseline filters..." (negative parallelism)
- Rewrote the closer. Instead of a tagline, it ends with a concrete statement that lands without trying to sound clever
- Shifted one paragraph to second person ("You pull the operator's certificate...") to break the rhythm and add operational texture
- Added two specific failure examples (liability coverage short, no AD compliance records) to make it feel observed rather than assembled
- Varied paragraph length so the structure isn't so even

209 words. Ready to post. One note: the two specific failure examples I added are illustrative. Make sure they match scenarios you've actually seen or would credibly see. Swap the details if needed.

---

## Phelipe

` But it's the reason the booking confirmation is worth anything.`
this is a little akward

---

## Claude

You're right. How about:

"None of this shows up on the booking confirmation. But it's the work behind it."

Short, clean, no forced cleverness. Want me to update the file?

---

## Phelipe

yes

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Updated. Ready to post.

---

## Phelipe

posted

---

## Claude

Good. That's Thursday done.

Next content day is **Friday, March 20**. Instagram. The calendar calls for a **market observation** (text-heavy visual), TG or MS lane. That's an lh-news-pill or a standalone visual in Figma.

Let me know when you're ready to work on that, or if you've got other things to hit today.

---

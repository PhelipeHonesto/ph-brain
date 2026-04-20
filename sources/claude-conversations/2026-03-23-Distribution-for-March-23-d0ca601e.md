---
title: Distribution for March 23
created: 2026-03-23T16:09:47.515712Z
updated: 2026-03-26T21:11:53.775278Z
uuid: d0ca601e-3e33-4f84-be45-1bd35afc9205
source: claude-conversation
type: source
message_count: 176
---

# Distribution for March 23

*Summary: **Conversation Overview**

This conversation centered on executing the Week A (publish week) content distribution calendar for Loud Hawk, a private aviation intelligence newsletter published biweekly by Orange Sunshine Aviation. The person is building and running Loud Hawk, which covers operational charter intelligence for high-net-worth clients and aviation professionals. The publication uses a two-week cycle anchored to Edition 1 (shipped March 12), with Week A as the publish week and Week B as the off week. Today's session spanned March 24–26, covering Tuesday through Thursday of Week A, culminating in the launch of Edition 2.

The session involved producing and posting multiple pieces of content across LinkedIn and Instagram. Tuesday's LinkedIn post (edition pull) used the compliance vs. sourcing reframe from Edition 2 as its core insight, with a first comment linking to loudhawk.media and teasing the upcoming edition send. Wednesday produced two pieces: a LinkedIn forward-testing post in the TG lane about trip support companies as invisible infrastructure (Universal Weather and Aviation, Jeppesen), and an Instagram Static 1 card with the headline "Overflight Is Not Landing" built in Figma using an aerial coastline image. Thursday's LinkedIn post covered operator vetting for international routes, specifically the avionics requirements (CPDLC, ADS-C) and permit filing experience gaps that distinguish capable operators from those who cannot legally execute certain routings. Edition 2 was also sent via Beehiiv on March 26, with the website (loudhawk.media) updated to reflect the live edition. The session concluded with generating a 1080x1080 ad creative for the edition using HTML/Playwright, styled with the Loud Hawk purple (#521F84) and orange (#FF4900) brand palette.

Several workflow corrections and decisions were made throughout. The lh-news-pill skill was updated to fix template selection logic: Static 1 (full bleed image + headline overlay) is now the default for editorial/conceptual posts, while Static 2 (briefing card) is reserved for data-heavy posts with specific stats or numbers. The loudhawk.media site runs on a custom GitHub-hosted codebase deployed via Vercel, not directly through Beehiiv — a critical distinction when making site updates. The production branch is main, not master; a deploy to master failed to update the live site and had to be re-pushed to main. The Beehiiv og:image meta tag was set through Publication Settings to improve LinkedIn link previews. Edition 2 was duplicated from Edition 1 in Beehiiv rather than built from scratch, with the key formatting fix being the orange color (#FF4900) on "THE SIGNAL" and "QUICK HITS" section headers, which does not carry over reliably in duplication. The person prefers content that avoids em dashes, parallel sentence structures, and repeated metaphors, and applies the humanizer skill before finalizing any LinkedIn post. Overlap between consecutive posts is actively checked — Wednesday's trip support companies angle was flagged as too close to Thursday's operator vetting post, and the overlapping paragraph was cut from Thursday's version.

**Tool Knowledge**

Claude Code (tab 4) was used throughout as the primary execution environment for skill-based content generation. The lh-linkedin and lh-news-pill skills were invoked by pasting natural language prompts directly into the Claude Code terminal. Effective prompt structure for lh-linkedin includes: skill name, week and day, post type, lane designation with prior lanes listed to avoid repetition, explicit angle with candidate lines from the source material, and the full edition text pasted inline. For lh-news-pill, the prompt must now specify the template explicitly (Static 1 or Static 2) since the skill's default logic was recently corrected — omitting this may revert to incorrect template selection.

For the GitHub/Vercel deployment, the correct workflow is: make changes via Claude Code, commit, and push specifically to the main branch. Pushing to master creates a Preview deployment only and does not update the production site at loudhawk.media. When Claude Code asks for confirmation before committing, the correct response is "yes, proceed with the commit and push." The Beehiiv post editor is accessed by duplicating Edition 1 from the Posts list, then editing the duplicate — the three-dot hover menu on the post card reveals the Duplicate option. The Web settings step (not the Compose step) contains the post thumbnail upload field for controlling the og:image on individual posts. The publication-level og:image is set separately under Settings → Publication Details.*

## Phelipe

hello. 
today is monday march 23
first edition was march 12
what is the distribution for the day

---

## Claude

The user wants to know today's distribution schedule. Today is Monday, March 23. Edition 1 shipped March 12. Let me figure out where we are in the 2-week cycle.

Week A = publish week (contains newsletter send)
Week B = off week

Edition 1: March 12 (Wednesday? Let me think - March 12 was a Wednesday). Actually, the memory says "Edition 1 shipped March 12, 2026. This is the cycle anchor date. Week A (publish week) starts the Monday of any week containing a newsletter send."

March 12 = Wednesday. So Week A started March 10 (Monday). 

So we're in Week B right now, which runs March 17-23, and today marks the end of that off week. The next publish week starts tomorrow on March 24. Let me check what's actually scheduled for today in the content calendar.
```
This block is not supported on your current device yet.
```

Today is Monday, March 23. Edition 1 shipped March 12 (Wednesday). Week A = week of March 10-16. Week B = March 17-23. So today is the last day of Week B (Monday of Week B).

Wait, actually Week B Monday would be March 17, not March 23. Let me recalculate.

Week A starts Monday March 10. Week A: March 10-16.
Week B starts Monday March 17. Week B: March 17-23.

Today is Monday March 23 - that's actually the LAST day of Week B (Sunday is typically the last day of the week, but if we count Monday as the first day, then... 

Actually, I need to be more careful here. Let me verify the calendar. If March 1, 2026 is a Sunday, then March 2 is Monday, March 9 is Monday, March 16 is Monday, and March 23 is also Monday. So the biweekly cycle anchored to Edition 1's Thursday send means Week A runs March 10-16 and Week B runs March 17-23, making today the final day of Week B and the start of a new cycle.

Wait, that's not matching up either. Let me recalculate: if Edition 1 shipped Thursday March 12, then Week A is the week containing that date (March 9-15), Week B follows (March 16-22), and today Monday March 23 begins the next Week A for Edition 2. So I'm in the publish week for Edition 2, which should ship around March 26. For today's schedule, I need to post a news pill on Instagram in either the MS or SA lane to kick off the content week.Today is **Monday, March 23** — that puts you at the start of **Week A (Publish Week)** for Edition 2.

Cycle math: Edition 1 anchored to the week of March 9 (Week A). Week B ran March 16–22. You're back in Week A as of today, with Edition 2 targeting ~March 26.

---

**Today's distribution:**

| Platform | Content Type | Lane | Notes |
|---|---|---|---|
| **Instagram** | News pill | MS or SA | Opens the content week. Market signal to set the tone. |

No LinkedIn today. Tuesday is your first LinkedIn post of the week (edition pull — sharpest single insight from Edition 2, subscribe link in first comment).

---

Do you have a news pill ready, or do you need help building one?

---

## Phelipe

we did do any posting saturday or sunday.
i have a carousel on boost for instagram.
what is should we do to adapt to that

---

## Claude

The user is saying they didn't post Saturday or Sunday last week (Week B). They have a carousel on boost for Instagram currently. They want to know how to adapt today's plan.

Let me think about where we are in the cycle. Week B was March 16-22. The Week B schedule calls for:
- Monday IG: news pill (MS or SA)
- Tuesday LI
- Wednesday LI + IG
- Thursday LI
- Friday IG
- Saturday LI (optional)
- Sunday IG

They missed Saturday LI and Sunday IG in Week B. Now we're in Week A (March 23-29), with Edition 2 targeting ~March 26 (Wednesday).


Since the boosted carousel is already running and handling its own paid distribution, posting an organic piece to IG today would likely complement rather than conflict with it. The real question is whether they want to stick with today's scheduled IG post or shift focus elsewhere in the Week A plan.

---

## Phelipe

we did not do any posting saturday or sunday. i have a carousel on boost for instagram. what is should we do to adapt to that

---

## Claude

The user is saying they didn't post Saturday or Sunday last week (Week B). Now it's Monday of Week A (publish week). They have a carousel on boost for Instagram. They want to know how to adapt.

Week B was March 16-22. The scheduled posts that were missed:
- Saturday LinkedIn (forward-testing or real-time) - missed
- Sunday Instagram (news pill, MS or SA) - missed

Now Week A Monday: Instagram news pill is scheduled.

But they have a carousel already boosted on Instagram. So the question is: do they still post a news pill today, or does the boosted carousel count as/replace the Monday IG post?


The boosted carousel is paid promotion running separately from their organic posting schedule, so it doesn't replace the Monday news pill—they operate on different channels. The missed posts from last week are just gone; there's no need to backfill them. The calendar moves forward, and they should post the organic content as planned. The cleaner approach is to let the boost carry Monday's Instagram presence and hold the news pill for tomorrow instead, or fold it into Wednesday's content plan.Two separate things to address:

**Missed Sat/Sun posts:** Drop them. Don't backfill. The calendar moves forward.

**The boosted carousel:** That's paid distribution of existing content. It's running. Don't post an additional organic news pill on top of it today — you'd be crowding Instagram on the same day with two pieces and splitting attention. Let the boost work.

**Adapted this week:**

| Day | Platform | Action |
|---|---|---|
| Monday | Instagram | Skip organic — carousel boost is running |
| Tuesday | LinkedIn | Edition pull — sharpest insight from Ed. 2 |
| Wednesday | LinkedIn | Forward-testing (TG or HIAW) |
| Wednesday | Instagram | Newsletter echo — visual card from Ed. 2 |
| Thursday | LinkedIn | Forward-testing (any open lane) |
| Friday | Instagram | News pill (MS or SA) |
| Saturday | LinkedIn | Forward-testing or real-time signal |
| Sunday | Instagram | Market observation |

Wednesday IG picks up the Instagram cadence cleanly once the boost window is done. You lose one organic Instagram touch this week but the paid reach compensates.

When does the boost end?

---

## Phelipe

so today is nothing ?

---

## Claude

The user is asking if today (Monday) they have nothing to do distribution-wise. Based on my adaptation, I said skip organic Instagram since the carousel boost is running. So yes, today is nothing for posting. But I should confirm that and maybe note if there's prep work to do.Correct. Nothing to post today.

If you want to use the time, Tuesday's LinkedIn post (edition pull from Ed. 2) is the highest-leverage piece of the week. You could draft that today so it's ready to go tomorrow morning.

---

## Phelipe

today is march 24.
we got for the day

---

## Claude

The user is clarifying today is March 24 (Monday). Let me recalculate.

Edition 1 shipped March 12. That was a Wednesday, which means Week A started the Monday of that week — March 9. Week B started March 16. Week A (Edition 2) starts March 23.

So March 24 is Tuesday of Week A.

Tuesday Week A = LinkedIn, backward-tied (edition pull), sharpest insight from the edition, subscribe link in first comment.

That's the action for today.Today is **Tuesday, Week A.**

**LinkedIn — edition pull from Edition 2.** Sharpest single insight from the edition. Subscribe link in first comment. No other posts today.

Do you have Edition 2 finalized enough to pull from, or do you need help identifying the strongest line to build the post around?

---

## Phelipe

edition 2

---

## Claude

The user has shared Edition 2. I need to identify the strongest single insight to pull for today's LinkedIn post (edition pull, Week A Tuesday).

The edition is about international charter compliance - permits, trip support, the invisible operational layer. Strong angles:

1. The "one manifest / seven borders" framing - very compelling opener
2. The question to ask your broker - highly actionable
3. The timeline problem - last-minute international charter is a compliance problem, not a sourcing challenge
4. The contrast: passenger sees departure time, broker built permissions architecture

The strongest pull for LinkedIn is probably the "last-minute international charter is not a sourcing challenge, it's a compliance problem" line - that's a sharp, counterintuitive insight that stands alone well. 

I'm weighing the broker question angle against the compliance reframe. The question feels more promotional, while the compliance insight is genuinely educational and shifts how people think about international bookings. That distinction between domestic and international timelines—sourcing versus compliance—is the sharpest single line in the edition, so I'll lead with that for the post.Strongest pull is this line from the edition:

> "Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem."

That's the sharpest reframe in the piece. It's counterintuitive, stands alone without the newsletter, and is directly relevant to anyone who has ever tried to book international on short notice.

Secondary option: the broker question angle — "What is your permit timeline for this routing, and who is handling trip support?" — highly actionable, positions you as the person who already knows the answer.

I'd build the post around the first one, with the broker question as the close.

Want me to draft it?

---

## Phelipe

use tab 4 for this.

---

## Claude

The user is sharing a screenshot of Claude Code sessions and wants me to use "tab 4" for drafting the LinkedIn post. Tab 4 appears to be empty (bottom right). But I don't have access to Claude Code or the ability to interact with those terminal sessions.

I think the user wants me to draft the LinkedIn post here, and they'll paste it into tab 4 of their Claude Code environment. Or maybe they want me to use the lh-linkedin skill that's in their Claude Code workspace.

Actually, looking at this more carefully - the user is in Claude.ai (this chat) and also has Claude Code open. They want me to draft the post here so they can use it in tab 4. 

I should check the lh-linkedin skill file to understand the brand voice and guidelines before drafting the post.
```
This block is not supported on your current device yet.
```

The user wants me to draft the LinkedIn post using the `lh-linkedin` skill from Claude Code. But I'm in Claude.ai, not Claude Code. The user wants to use "tab 4" in their Claude Code environment to run the lh-linkedin skill.

I think they want me to draft the post here (in this chat) and they'll take it to Claude Code tab 4, or they want me to draft it applying what I know about the lh-linkedin skill guidelines.

Since I can't access their Claude Code environment or the actual lh-linkedin skill file, I should draft the LinkedIn post here applying all the known brand voice rules, the edition pull format guidelines from the content strategy, and the humanizer principles. 

I'll go ahead and draft the post now using those guidelines.I don't have access to the `lh-linkedin` skill file itself from here — that lives in your Claude Code environment. Best path: take the edition content to tab 4 in Claude Code and run `lh-linkedin` there directly with the edition as input.

Prompt to use in tab 4:

---

**Use the `lh-linkedin` skill. Edition pull post. Source content below.**

Angle: The compliance vs. sourcing reframe — "Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem."

Close with the broker question: "What is your permit timeline for this routing, and who is handling trip support?"

Subscribe link goes in first comment. This is a Week A Tuesday edition pull. Do not summarize the edition. One insight, standing alone.

[paste full Edition 2 text]

---

That gives the skill full context plus a clear directive. Want me to also draft a version here as a backup?

---

## Phelipe

give me the terminal prompt.
tab 4 has claude already

---

## Claude

They want a ready-to-paste terminal prompt for Claude Code tab 4.Paste this into tab 4:

```
use lh-linkedin. week a tuesday. edition pull post.

angle: "last-minute domestic charter is a sourcing challenge. last-minute international charter is a compliance problem."

close with the broker question: "what is your permit timeline for this routing, and who is handling trip support?"

subscribe link goes in first comment. one insight standing alone. do not summarize the edition.

---

LOUD HAWK — Edition 2
Subject line: Your Plane Crossed Seven Borders. You Signed One Manifest.

THE SIGNAL
Your Plane Crossed Seven Borders. You Signed One Manifest.
You signed a trip manifest at Opa-locka. Printed your name, your passport number, your destination. One document. One signature. Clean.
Your broker spent the prior 72 hours building the compliance chain that made that departure legal. Overflight permits filed through three countries you will never set foot in. Landing authorization from Brazilian civil aviation. APIS data transmitted to CBP. Customs pre-clearance coordinated with a ground handler in Guarulhos. A contingency routing plotted in case Colombian airspace denied the overflight on short notice.
You saw a departure time. The broker built a permissions architecture spanning half a continent.
This is how international charter actually works. And almost none of it is visible to the person writing the check.

[paste rest of edition here]
```

---

## Claude

The post looks good. Clean output from the skill. Ready to review and post.That's a clean output. Scorecard passes, hook is sharp, broker question closes it right.

One flag: the first comment copy says "Subscribe here: https://loudhawk.beehiiv.com" — confirm that's your actual subscribe URL before posting, or swap in the correct link.

Ready to post as-is. Copy the post body and first comment, schedule or publish for today.

---

## Phelipe

URL : loudhawk.media

---

## Claude

The user wants to update the subscribe URL in the first comment from https://loudhawk.beehiiv.com to https://loudhawk.media.First comment should read:

> I wrote the full breakdown on permits, trip support, and what failure actually looks like on international routing in the latest Loud Hawk. Subscribe here: https://loudhawk.media

Everything else posts as-is.

---

## Phelipe

give me the full post.
with the comment with correct URL
and the proper format (spacing)

---

## Claude

The user wants the full LinkedIn post with proper formatting and the correct URL in the first comment.**POST:**

Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem.

They are not the same kind of hard.

A domestic trip on short notice means finding the right aircraft, the right crew, the right positioning. Tight, but solvable. The infrastructure is there. You are working within one regulatory system.

An international trip on short notice means permit applications that require 72 hours minimum. Sometimes five to seven business days. Overflight permits filed through countries you will never set foot in. Landing authorization from a separate sovereign authority with a separate timeline. APIS data, customs pre-clearance, ground handler confirmation at the destination.

A Friday request for a Monday departure to Riyadh does not work. Not because there is no aircraft. Because the permits have not been filed and no government owes you an expedited timeline.

The aircraft might be available. The crew might be legal. But if the overflight clearance from Colombia, Peru, or Cuba has not been approved, the trip does not happen. A routing change mid-planning can reset the entire chain.

Most clients learn this the morning of departure. A broker who has done this before builds the buffer into the plan from the start.

Next time you book international charter, ask your broker one thing: "What is your permit timeline for this routing, and who is handling trip support?"

A broker who answers that without hesitation has done this before. A broker who pauses has not.

---

**FIRST COMMENT:**

I wrote the full breakdown on permits, trip support, and what failure actually looks like on international routing in the latest Loud Hawk. Subscribe here: https://loudhawk.media

---

## Phelipe

add humanizer skill

---

## Claude

The user wants me to run the humanizer skill on the post. Let me check the humanizer skill first.
```
This block is not supported on your current device yet.
```

Now let me apply the humanizer skill to the LinkedIn post. Let me analyze it for AI patterns first, then rewrite.

The post:

"Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem.

They are not the same kind of hard.

A domestic trip on short notice means finding the right aircraft, the right crew, the right positioning. Tight, but solvable. The infrastructure is there. You are working within one regulatory system.

An international trip on short notice means permit applications that require 72 hours minimum. Sometimes five to seven business days. Overflight permits filed through countries you will never set foot in. 

Landing authorization from a separate sovereign authority with a separate timeline. APIS data, customs pre-clearance, ground handler confirmation at the destination.

A Friday request for a Monday departure to Riyadh does not work. Not because there is no aircraft. Because the permits have not been filed and no government owes you an expedited timeline.

The aircraft might be available. The crew might be legal. But if the overflight clearance from Colombia, Peru, or Cuba has not been approved, the trip does not happen. A routing change mid-planning can reset the entire chain.

Most clients learn this the morning of departure. A broker who has done this before builds the buffer into the plan from the start.

Next time you book

I'm seeing the core insight here: international charter logistics aren't just harder versions of domestic logistics—they're fundamentally different because they depend on external government timelines that can't be rushed. The post uses concrete examples like Friday-to-Monday requests and specific countries to show why permits aren't just paperwork but actual blockers. The ending trails off, but it's setting up advice for clients about planning ahead. very even and controlled - each paragraph similar length. What's good about this version is the specific operational details like the 72-hour window, the actual countries involved, and the compliance requirements like APIS and landing authorizations. No flowery language, no unnecessary punctuation. The draft is tighter and more grounded in what actually happens on these trips.

Now I'm thinking about the timeline problem - how permits aren't something you can rush regardless of aircraft availability. The core issue is that governments don't operate on your schedule. A Friday request for Monday departure to somewhere like Riyadh just doesn't work because you're dependent on multiple countries approving your routing, and that approval takes business days, not calendar days. A routing change mid-planning can cascade into new permit applications across several jurisdictions and blow up your timeline entirely. Most clients don't realize this until the morning they're supposed to leave. The practical advice is to ask your broker upfront about their permit timeline and who's handling trip support - if they answer without thinking, they know the routing. If they hesitate, they don't. I'm satisfied with how this reads—the structure holds, the symmetry works, and the closing question creates the right tension between someone who knows the process and someone who doesn't.Applying the humanizer now.

**AI patterns flagged:**
- Rule of three: "the right aircraft, the right crew, the right positioning"
- Symmetrical closer is too clean: "A broker who answers... A broker who pauses..."
- Even paragraph rhythm throughout — reads assembled
- "They are not the same kind of hard" — slightly performative

---

**FINAL POST:**

Last-minute domestic charter is a sourcing problem. Last-minute international charter is a compliance problem. Not the same thing.

On a domestic trip you're finding the right aircraft, crew, and positioning. Tight, but it's a logistics solve. One regulatory system.

International is a different problem. A Miami to São Paulo routing crosses Cuban, Colombian, and Peruvian airspace before it reaches Brazil. Each country controls access to its own airspace independently. Overflight permit for each, filed through a trip support company the client has never heard of. Landing authorization from Brazilian civil aviation. APIS data to CBP. Ground handler confirmed in Guarulhos.

72 hours is the baseline for cooperative jurisdictions. China, Russia, parts of the Gulf — five to seven business days. Not calendar days.

A Friday request for Monday departure to Riyadh does not work. Not because there's no aircraft. Because no government runs on your schedule.

The aircraft can be available. The crew can be legal. If Colombian overflight clearance hasn't come through, the flight doesn't happen. A routing change mid-planning can trigger new applications across multiple countries and reset the timeline from scratch.

Most clients find this out the morning of departure.

When you book international charter, ask your broker: "What's your permit timeline for this routing, and who's handling trip support?"

If they answer without hesitation, they've done it before. If they pause, they probably haven't.

---

**FIRST COMMENT:**

I wrote the full breakdown on permits, trip support, and what failure actually looks like on international routing in the latest Loud Hawk. Subscribe here: https://loudhawk.media

---

## Phelipe

question is weird that we add Riyadh in a scenario that is in latin america?

---

## Claude

Good catch. The Riyadh example is from the edition — it's used to illustrate slow-permit jurisdictions (Gulf states). But in the LinkedIn post, it sits right after the Miami-São Paulo/Latin America routing context, which makes it jarring. The reader's mental map is in Latin America and then suddenly Riyadh appears.

Options:
1. Cut Riyadh entirely and make the point about Friday/Monday with a Latin American example
2. Keep the slow-jurisdiction point but use a different example that fits the routing context

The edition mentions China, Russia, Gulf and African states as slow jurisdictions. For a Latin America-focused post, the Friday/Monday example could just stay abstract, or use a different destination that fits the narrative better. 

Actually, the simplest move might be to just drop that example altogether and let the principle stand on its own.Yes. The edition uses Riyadh to illustrate slow-permit jurisdictions as a separate point. In the post it lands mid-Latin America routing and breaks the geography.

Two options:

**Cut it entirely** and keep the principle abstract:
> "Some jurisdictions run five to seven business days. A same-week request doesn't work. No government runs on your schedule."

**Swap to a region-consistent example:**
> "A Friday request for a Monday departure to São Paulo cuts it close. To Beijing or Riyadh, it's a non-starter."

The first is cleaner for this post. The Riyadh point belongs in a different edition focused on Gulf or Asia routing.

Which do you want?

---

## Phelipe

the first

---

## Claude

Rewrite the post with the Riyadh line cut and replaced with the abstract version.**FINAL POST:**

Last-minute domestic charter is a sourcing problem. Last-minute international charter is a compliance problem. Not the same thing.

On a domestic trip you're finding the right aircraft, crew, and positioning. Tight, but it's a logistics solve. One regulatory system.

International is a different problem. A Miami to São Paulo routing crosses Cuban, Colombian, and Peruvian airspace before it reaches Brazil. Each country controls access to its own airspace independently. Overflight permit for each, filed through a trip support company the client has never heard of. Landing authorization from Brazilian civil aviation. APIS data to CBP. Ground handler confirmed in Guarulhos.

72 hours is the baseline for cooperative jurisdictions. Some run five to seven business days. Not calendar days. A same-week request doesn't work. No government runs on your schedule.

The aircraft can be available. The crew can be legal. If Colombian overflight clearance hasn't come through, the flight doesn't happen. A routing change mid-planning can trigger new applications across multiple countries and reset the timeline from scratch.

Most clients find this out the morning of departure.

When you book international charter, ask your broker: "What's your permit timeline for this routing, and who's handling trip support?"

If they answer without hesitation, they've done it before. If they pause, they probably haven't.

---

**FIRST COMMENT:**

I wrote the full breakdown on permits, trip support, and what failure actually looks like on international routing in the latest Loud Hawk. Subscribe here: https://loudhawk.media

---

## Phelipe

check loudhawk.media
Edition 2 is going to launche march 26 this lead that we did already

---

## Claude

The user wants me to check loudhawk.media to see what's already published, and they're saying Edition 2 launches March 26, so the LinkedIn post referencing Edition 2 content is getting ahead of the newsletter. Let me check the site.
```
This block is not supported on your current device yet.
```

Let me get the tab context first.
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

The site shows "VOL. I · NO. 02 · MARCH 2026" on the homepage, which means Edition 2 is already showing on the website, even though it hasn't been officially sent yet (planned for March 26). This is a problem - the LinkedIn post references "the latest Loud Hawk" which would direct people to Edition 2 content that is technically already visible on the website but hasn't been officially launched yet.

Wait, actually - the user is saying Edition 2 launches March 26. The site appears to already be showing Edition 2 as the featured content. 

So posting the LinkedIn today (March 24) would be directing people to Edition 2 before it's officially sent to subscribers. I need to check whether Edition 2 is actually fully published on the site or just showing as a preview.
```
This block is not supported on your current device yet.
```

The homepage shows Edition 2 is already the featured content on the site (VOL. I · NO. 02 · MARCH 2026), but it appears the full content may not be published yet - it just shows a subscribe form. The issue is: the LinkedIn post says "read the full breakdown in the latest Loud Hawk" which references Edition 2, but Edition 2 launches March 26. 

So the problem is: we're posting the LinkedIn today (March 24) and the first comment sends people to loudhawk.media where they'll see Edition 2 is featured but it hasn't sent yet (sends March 26). 

Actually, the edition might already be live on the web even though the newsletter hasn't been sent to subscribers yet. The post itself doesn't quote the content directly—it's just an insight drawn from it—so if Edition 2 is accessible on the site, the link still works.

The real tension is that the Tuesday edition pull is supposed to align with the newsletter send, but the newsletter goes out Wednesday (March 26) while the post would go today (Tuesday, March 24). So I'm posting about the edition a day before subscribers actually receive it. I could either adjust the first comment to avoid referencing "the latest Loud Hawk" directly, hold the post until Wednesday, or accept that the Tuesday pull happens slightly ahead of the send.The site already shows Edition 2 as the featured content (Vol. I, No. 02, March 2026), but the newsletter hasn't sent to subscribers yet — that's March 26.

The problem: the first comment says "read the full breakdown in the latest Loud Hawk" — but subscribers haven't received it yet. Anyone clicking through today hits a subscribe wall, not the edition.

Two clean options:

**Option 1 — Post today, tease the send**
Change the first comment to:

> Edition 2 drops Thursday. Full breakdown on permits, trip support, and what failure looks like on international routing. Subscribe here: https://loudhawk.media

**Option 2 — Hold the post until March 26**
Post it the day the edition sends. The first comment lands exactly right and the link works as intended. Only downside: Tuesday is the prescribed day for the edition pull — you'd be posting it on Wednesday instead, which is already the IG echo day. Manageable, but not clean.

Option 1 is cleaner. Post today, tease the send, drive subscriptions before the edition even drops. Which do you want?

---

## Claude

The post is live. Looking at the screenshots, it's published successfully with the correct first comment ("Edition 2 drops Thursday. Full breakdown on permits, trip support, and what failure looks like on international routing. Subscribe here: https://loudhawk.media").

The post is live and the comment is in place. That's it for today's distribution.Post is live. Comment is in place. Tuesday done.

Next up: Wednesday. Two pieces.

| Platform | Content Type | Lane |
|---|---|---|
| LinkedIn | Forward-testing | HIAW or TG — different lane from today |
| Instagram | Newsletter echo — visual card from Ed. 2 | Matches edition |

Do you want to work on Wednesday's LinkedIn post now, or handle the Instagram echo card first?

---

## Phelipe

hwo to get the logo of loud haek on the comment of the hyperlink

---

## Claude

The user is asking how to get the Loud Hawk logo to appear in the link preview when posting the loudhawk.media URL in LinkedIn comments. This is an Open Graph (OG) meta tag issue — the site needs proper `og:image` meta tags for LinkedIn to pick up a thumbnail image.

Let me check the current OG tags on loudhawk.media.That's controlled by the Open Graph image tag on loudhawk.media, not LinkedIn. LinkedIn pulls the preview image from whatever `og:image` is set in the site's metadata. Let me check what's there now.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

There's no `og:image` tag set. That's why LinkedIn shows a generic gray placeholder instead of the logo. The fix is to add an `og:image` meta tag to the site. Since this is a Beehiiv site, the user would need to set this in Beehiiv's settings.There's no `og:image` tag on the site. That's why LinkedIn shows the gray placeholder instead of the logo.

**The fix:** Add an `og:image` meta tag to loudhawk.media. Since the site is on Beehiiv, you set this in Beehiiv settings, not in code.

**Where to do it in Beehiiv:**
Settings → Publication Details → look for "Social image" or "SEO / Social sharing image." Upload the Loud Hawk logo there (the white on purple version works best for dark backgrounds, or the standard mark on white). Beehiiv injects that as the `og:image` across the site.

Once that's set, LinkedIn will pull it automatically on any new link share. For the comment already posted, the preview is cached — nothing you can do about that one.

Do you want to handle that now or move on?

---

## Phelipe

Oh boy help me this on terminal.
this is a website and news go to behiiv

---

## Claude

The user wants to fix the og:image on loudhawk.media which is a Beehiiv site. They want to do this via terminal (Claude Code). But this is actually a Beehiiv setting - it needs to be done through the Beehiiv dashboard, not terminal. Let me navigate to Beehiiv settings to find where to set the social sharing image.

Actually, they said "help me this on terminal" but then said "this is a website and news go to beehiiv" - I think they're clarifying that loudhawk.media is a Beehiiv site. The fix needs to happen in Beehiiv's dashboard settings. 

I'll head over to the Beehiiv dashboard to locate the social sharing image settings.The fix is in Beehiiv's dashboard, not terminal — it's a platform setting. Let me navigate there directly.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

It's loading the Beehiiv login page. I need to wait for it to load.
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

Already logged in. Now going to Settings.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Found it. **"Default Thumbnail Preview"** — that's the `og:image`. Scroll down to see the upload field.
```
This block is not supported on your current device yet.
```

Scrolled too far. The Default Thumbnail Preview was just above. Let me scroll back up slightly.
```
This block is not supported on your current device yet.
```

There it is — **Default Thumbnail Preview**, recommended 1200x630px. That's the `og:image` field. 

You need to upload an image here. Best candidate from your assets is `LOGOPRINCIPAL_0000_Layer3_1.png` or the horizontal logo — something that reads well at 1200x630. Ideally the purple background with the white wordmark, since that's the Loud Hawk identity color.

Do you have a 1200x630 version ready, or do you want me to check which of your project logo files would work best for this?

---

## Phelipe

done

---

## Claude

Let me verify the og:image is now set on the site.Good. Let me verify it took.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

The og:image tag is still not showing up. Beehiiv might take a bit to propagate, or it might be served differently. Let me check all meta tags.Not showing yet. Beehiiv may take a few minutes to propagate. Wait 5 minutes then we can recheck. The setting is saved — it just hasn't flushed to the live site yet.

Also worth noting: even once it's live, the LinkedIn preview on the comment you already posted is cached. It won't update on that specific post. The logo will show correctly on any new link share going forward.

Nothing to do right now. Move on when ready.

---

## Phelipe

its not that bad either

---

## Claude

The user is saying the LinkedIn preview without an image isn't that bad. They're fine with it as is for now. Simple acknowledgment.Agreed. The title and description are clean — "Loud Hawk: Private Aviation Intelligence" and the one-liner read well. The logo image will improve it but it's not broken without it.

Tuesday is done. What's next?

---

## Phelipe

what is for today

---

## Claude

Today is Wednesday, March 25 (the user said "today is march 24" earlier but that was yesterday - now they're asking "what is for today" which would be Wednesday March 25).

Wait, let me re-read. The user said "today is march 24" and we did Tuesday's post. Now they're asking "what is for today" - this could still be March 24 (same session) or March 25. Given the conversation flow, I think they're still on March 24 and asking what else is left for today. But Tuesday is done. 


Actually, the system date shows March 25, 2026, so they're asking about Wednesday's content now that Tuesday's work is complete.Wednesday, March 25. Two pieces.

| Platform | Content Type | Lane | Notes |
|---|---|---|---|
| **LinkedIn** | Forward-testing | HIAW or TG | Different lane from Tuesday. Standalone — no newsletter link. |
| **Instagram** | Newsletter echo | Matches edition | Visual card pulling a key stat or claim from Ed. 2. Subscribe CTA in caption. |

LinkedIn goes first. Do you want to build that now or go to the Instagram card?

---

## Phelipe

lets do linked using the skill

---

## Claude

The user wants to use the lh-linkedin skill in Claude Code (tab 4) to generate Wednesday's LinkedIn post. I should give them the terminal prompt to paste.Paste this into tab 4:

```
use lh-linkedin. week a wednesday. forward-testing post.

lane: HIAW or TG. different lane from tuesday's post (which was HIAW — compliance/permits). go TG if strongest observation available.

no newsletter link. no subscribe CTA. post must stand alone. this is an off-newsletter linkedin day.

source material: edition 2 below. find the sharpest standalone observation that was NOT the focus of tuesday's post. tuesday was: "last-minute domestic charter is a sourcing problem, last-minute international is a compliance problem."

---

LOUD HAWK — Edition 2
Subject line: Your Plane Crossed Seven Borders. You Signed One Manifest.

THE SIGNAL
Your Plane Crossed Seven Borders. You Signed One Manifest.
You signed a trip manifest at Opa-locka. Printed your name, your passport number, your destination. One document. One signature. Clean.
Your broker spent the prior 72 hours building the compliance chain that made that departure legal. Overflight permits filed through three countries you will never set foot in. Landing authorization from Brazilian civil aviation. APIS data transmitted to CBP. Customs pre-clearance coordinated with a ground handler in Guarulhos. A contingency routing plotted in case Colombian airspace denied the overflight on short notice.
You saw a departure time. The broker built a permissions architecture spanning half a continent.
This is how international charter actually works. And almost none of it is visible to the person writing the check.
What permits actually are
A charter flight from Miami to São Paulo does not simply fly south. It transits sovereign airspace belonging to multiple countries between departure and destination. Each country controls access to its airspace independently. Crossing through that airspace requires an overflight permit. Touching down requires a separate landing permit, issued by a different authority with different requirements and different processing timelines.
These are not formalities. They are discrete government approvals. A flight that crosses Cuban, Colombian, and Peruvian airspace on the way to Brazil needs overflight clearance from each. None of those countries owes you access. None of them processes on your schedule.
The passenger never thinks about this. The broker thinks about nothing else for three days.
The timeline problem
Most international destinations require permit applications 24 to 72 hours in advance at minimum. That is the baseline for cooperative, well-staffed civil aviation authorities with established relationships to the trip support providers doing the filing.
Then there are the slower jurisdictions. China, Russia, and several Gulf and African states require five to seven or more business days for overflight or landing permits. Business days. Not calendar days. A Friday request for a Monday departure to Riyadh does not work.
This is the part that catches clients off guard. Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem. The aircraft might be available. The crew might be legal. But if the permits have not been filed and approved, the trip does not happen. A broker who accepts a 12-hour booking on a transatlantic routing without flagging permit timelines is skipping a step.
The invisible layer
Brokers do not file these permits themselves. They work through trip support companies. Universal Weather and Aviation, Jeppesen, and a handful of other specialized firms manage permit applications, customs coordination, ground handler logistics, and routing advisories across jurisdictions. These companies are the operational infrastructure behind every international charter trip.
The client has never heard of them. The broker relies on them completely.
This matters for operator vetting. A Part 135 operator with an active, tested trip support relationship is an operator whose permit exposure is being managed by professionals who do this across hundreds of international flights per month. An operator without one is managing permits ad hoc, or not managing them at all.
What failure looks like
A permit denied 18 hours before departure. A routing revision because one country's airspace closes on a NOTAM with no warning. A customs pre-clearance requirement that forces the client to arrive 90 minutes early at the FBO. Information that surfaces the night before, not during planning. A ground handler at the destination airport who was never confirmed, so there is no fuel, no customs officer, and no one to marshal the aircraft on arrival.
These are not hypotheticals. They are the operational reality of international routing done without adequate lead time or planning discipline. On the Miami to São Paulo routing, a denied Colombian overflight does not just delay the trip. It requires re-routing through Caribbean airspace, new permit applications for different countries, and potentially a fuel stop that was not in the original plan. The timeline resets. The cost changes. The client finds out the morning of departure.
A broker who has done this before builds the buffer into the plan from the start. Alternate routing identified. Handler confirmed at destination. APIS filing deadlines calendared. Permit status tracked daily once applications are submitted. The client never sees this work. That is the point.
The sourcing difference
Operator selection for international trips adds a dimension that does not exist on domestic flights. Not every Part 135 certificate holder is configured for international operations. Some lack the required avionics for certain controlled airspaces. Some have no working trip support relationship. Some have never filed an overflight permit for the region you are traveling to.
The broker's job is to filter for operators who have done this routing or a comparable one. Not operators who say they can do international. Operators who demonstrably do.
The question to ask
Next time you book an international charter, ask your broker one thing: "What is your permit timeline for this routing, and who is handling trip support?"
A broker who answers that question specifically, without hesitation, has done this before. A broker who pauses, deflects, or gives you a vague reassurance has not.

QUICK HITS
The 72-Hour Minimum Most international destinations require permit applications at least 72 hours before departure. Several, including China, Russia, and portions of Gulf and African airspace, require five to seven or more business days. The implication: last-minute international charter is not just harder to source. It may be legally unpermittable on short notice. If you are planning international travel by private aircraft, your broker needs more lead time than you think. Build it into your planning window before you pick a date.
Overflight Is Not Landing Flying over a country and landing in it require separate permits from separate sovereign authorities. A routing change mid-planning, even something as minor as a weather deviation that shifts the flight path across a different country's airspace, can trigger new permit applications across multiple jurisdictions and reset the timeline. On international trips, treat the routing as a compliance document. It is not just a flight path. It is a chain of government approvals, and changing one link can break the chain.
Ask About Trip Support Trip support companies are the operational backbone of international charter. They manage permits, customs, ground handlers, and routing advisories. A broker who does not use one, or whose operator does not have a relationship with one, is leaving permit and logistics coordination to chance. Ask your broker which trip support company is handling your international trip. If they do not have a specific answer, that tells you everything you need to know about how the trip is being managed.
```

---

## Claude

Good output. Let me review it quickly for quality before presenting it back.

The angle is TG — "The companies that determine whether your international charter trip happens are companies you've never heard of." That's a clean Gap observation, distinct from Tuesday's compliance/timing angle.

One thing to check: the close mirrors Tuesday's close a bit too closely — "If your broker names one immediately..." vs Tuesday's "If they answer without hesitation..." Similar structure back-to-back days. Worth flagging.

Also need to run humanizer mentally — the post looks pretty clean actually. No em dashes, no luxury language. The structure is tight.Clean angle. Distinct from Tuesday — Tuesday was about timing, this is about the invisible infrastructure layer. TG lane is right.

One flag before you post: the close mirrors Tuesday too closely.

Tuesday ended: "If they answer without hesitation, they've done it before. If they pause, they probably haven't."

Wednesday ends: "If your broker names one immediately, they have done this before. If they do not have a specific answer..."

Same structure, consecutive days. Swap the Wednesday close for something that doesn't echo it. Suggestion:

> "Most people evaluating international charter never get to this question. The ones who have done it before ask it without thinking."

Want me to run humanizer on the full post before you finalize?

---

## Phelipe

yes

---

## Claude

Let me apply the humanizer skill to the Wednesday LinkedIn post.Applying humanizer now.

**AI patterns flagged:**
- "The companies that determine whether your international charter trip happens" — slightly over-constructed opener
- Rule of three structure in the middle paragraphs
- "This is the gap in how most people evaluate" — gap framing is fine but "this is the gap" is a bit declarative/assembled
- Parallel closer mirrors Tuesday (already flagged)
- "That tells you everything" — appears twice in the edition's content, once here

---

**FINAL POST:**

The companies that decide whether your international charter trip actually happens are companies you have never heard of.

Not the operator. Not the broker. The trip support company.

Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.

Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do — across hundreds of international flights per month.

A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.

The client never thinks about this layer. The broker depends on it completely.

Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.

Next time you book international, ask your broker one thing: which trip support company is handling this trip?

The ones who have done this before answer without looking it up.

---

No first comment needed. No link. Post as-is.

---

## Phelipe

take the -

---

## Claude

The user wants to remove the em dash from the post. The only em dash is in "These companies do — across hundreds of international flights per month."**FINAL POST:**

The companies that decide whether your international charter trip actually happens are companies you have never heard of.

Not the operator. Not the broker. The trip support company.

Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.

Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do. Across hundreds of international flights per month.

A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.

The client never thinks about this layer. The broker depends on it completely.

Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.

Next time you book international, ask your broker one thing: which trip support company is handling this trip?

The ones who have done this before answer without looking it up.

---

## Phelipe

instagram

---

## Claude

The user wants to work on the Wednesday Instagram post — the newsletter echo card from Edition 2. This should be a visual card pulling a key stat or claim from Ed. 2, with a subscribe CTA in the caption. The skill for this is lh-news-pill in Claude Code.

Let me give them the prompt for tab 4.Paste this into tab 4:

```
use lh-news-pill. week a wednesday. newsletter echo card.

source: edition 2 — "Your Plane Crossed Seven Borders. You Signed One Manifest."

this is the wednesday IG echo post. pull one key stat or claim from the edition for the visual. subscribe CTA in caption. visual should match edition tone — operational, not lifestyle.

strongest candidates from the edition:
- "72 hours minimum. Some jurisdictions: five to seven business days."
- "You saw a departure time. The broker built a permissions architecture spanning half a continent."
- "Overflight is not landing. They are separate permits from separate sovereign authorities."

pick the one that works best as a static visual card. output: template selection, on-design copy, caption, image sourcing guidance.
```

---

## Claude

Good output. Let me review and flag anything before Phelipe moves to Figma.

The skill picked "Overflight Is Not Landing" — strong choice. Clean brief. Let me check the caption for issues.

Caption looks clean. No em dashes. No luxury language. One thing: "From Edition 2 of Loud Hawk. Subscribe at the link in bio." and then the footer also says "Subscribe to Loud Hawk → link in bio" — double CTA at the end, slightly redundant.

Also the arrow → might be an issue per brand voice rules. Let me flag that.Strong pick. "Overflight Is Not Landing" is the right call — five words, counterintuitive, teaches something immediately.

Two small flags before you go to Figma:

**1. Double CTA at the end of the caption.** It closes with "Subscribe at the link in bio" and then the footer repeats "Subscribe to Loud Hawk → link in bio." Pick one. Drop the footer line or drop the in-caption CTA.

Recommended caption close:

> From Edition 2 of Loud Hawk. Link in bio.

**2. Arrow symbol (→)** in the footer. Keep it out — not on-brand for Loud Hawk's operational voice.

Everything else is production-ready. Take the brief to Figma.

---

## Phelipe

i lost the output my pc restart what was on it

---

## Claude

The user lost their output due to a PC restart. They want to know what was on their screen. Based on the conversation, they were working on Wednesday's content. Let me summarize what was produced and ready.Here's everything produced today before the restart:

**TUESDAY — DONE AND POSTED**
LinkedIn post live. First comment with loudhawk.media live.

**WEDNESDAY LINKEDIN — READY TO POST**

The companies that decide whether your international charter trip actually happens are companies you have never heard of.

Not the operator. Not the broker. The trip support company.

Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.

Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do. Across hundreds of international flights per month.

A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.

The client never thinks about this layer. The broker depends on it completely.

Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.

Next time you book international, ask your broker one thing: which trip support company is handling this trip?

The ones who have done this before answer without looking it up.

---

**WEDNESDAY INSTAGRAM — READY FOR FIGMA**

Template: Static 2 (Briefing Card)
Headline: Overflight Is Not Landing
Summary: Two permits. Two authorities. Two timelines. One routing change can reset both.
Image: High-altitude aerial coastline shot. Unsplash/Pexels. Operational, not lifestyle.

Caption:

Flying over a country and landing in it require separate permits from separate sovereign authorities.

A charter routing from Miami to São Paulo crosses Cuban, Colombian, and Peruvian airspace before reaching Brazil. Each overflight needs its own clearance. The landing permit is a different application, different authority, different timeline.

A weather deviation that shifts the flight path into a different country's airspace triggers new permit applications. The timeline resets. The cost changes.

On international trips, the routing is not just a flight path. It is a chain of government approvals. Changing one link can break the chain.

From Edition 2 of Loud Hawk. Link in bio.

---

## Phelipe

find the picture

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

The images found are airplane window views but they show the window frame and wing - that's more lifestyle. Let me try a different search for what we need - an operational-looking aerial/geographic shot.
```
This block is not supported on your current device yet.
```

The Caribbean coastline shots are too touristy/beach-y. Let me try something more geographic/operational looking.
```
This block is not supported on your current device yet.
```

The Caribbean shots are too beach/tourism. The satellite maps are too literal. 

Best path for this card: go text-forward in Figma. Purple background, white wordmark, "Overflight Is Not Landing" as the headline in large type, summary line below. No photo needed. The concept carries itself — a strong photo would compete with it anyway.

The briefing card format works better as a dark typographic card for this particular headline. Cleaner and more on-brand than a coastline stock photo that reads like a travel post.

Want to proceed with that direction?

---

## Phelipe

this is static 2 i think we are miss align expectation

---

## Claude

Looking at the Figma screenshot, the Static 2 template uses a beige/cream background with the orange Loud Hawk wordmark, a headline in purple, an image slot, and body text below. This is a news pill format - it looks like a news/briefing card.

The issue Phelipe is flagging is that the template has a photo slot (currently showing a hangar/helicopter image) but we said to go text-forward without a photo. Also the background is beige/cream, not purple.

He's saying there's a misalignment in expectations. Let me think about what the actual issue is:


The hangar photo doesn't work conceptually with "Overflight Is Not Landing" - that's the core problem. I could swap it for an aerial or geographic image, remove the image slot entirely for a text-only approach, or try a different template altogether. I should ask Phelipe directly what feels most misaligned - whether it's the image choice, the template structure, or the overall visual direction.I see it. The image slot is the problem — the hangar photo has nothing to do with overflight permits or international routing. It kills the concept.

Two options:

**Option A — Replace the image.** Use an aerial shot looking down at geography. From your earlier Figma work, you had access to stock. Search Unsplash for "aerial view land from above" or "flight level geography." Muted tones, no beach tourism feel.

**Option B — Remove the image slot entirely.** Make it a pure text card. Headline + summary only, beige background, orange wordmark. Cleaner for a conceptual distinction like "Overflight Is Not Landing." The words carry it without a photo.

Which direction do you want to go?

---

## Phelipe

that is better for static tho.
should we redo the skill?

---

## Claude

He's showing Static 1 — full bleed image with headline overlaid at the bottom. That's a stronger format for this content. He's asking if the skill should be updated to prefer Static 1 over Static 2 for editorial/concept posts.

The question is whether to redo the skill or just note the preference. Given this is a skill in Claude Code, the right answer is yes — update the lh-news-pill skill to reflect that Static 1 (full bleed image + headline overlay) is the preferred format for editorial concept posts, and Static 2 (briefing card with separate image slot) is better for data/stat posts.Yes. The skill picked Static 2 for a conceptual post when Static 1 is clearly the stronger format. Full bleed image with headline overlay is more scroll-stopping and works better for editorial observations.

The skill needs a clearer decision rule. Right now it's probably treating "conceptual = briefing card." The rule should be:

**Static 1** — editorial observations, conceptual distinctions, strong headline with an image that can carry atmosphere. Most Loud Hawk content.

**Static 2** — data-heavy posts where the stat is the visual. Numbers, timelines, specific figures that need to breathe on a clean background.

Go to tab 4 and run:

```
update lh-news-pill skill. fix the template selection logic.

current problem: the skill selected Static 2 (briefing card) for an editorial concept post ("Overflight Is Not Landing"). Static 1 (full bleed image + headline overlay) is the correct format for editorial observations and conceptual distinctions. Static 2 should be reserved for data-heavy posts where a specific stat or number is the centerpiece of the visual.

update the decision rules:
- Static 1 = default for editorial observations, conceptual distinctions, strong headline posts
- Static 2 = data posts only — specific numbers, timelines, percentages that need a clean background to read clearly

keep everything else in the skill unchanged.
```

---

## Phelipe

this is getting confusing

---

## Claude

The user is saying things are getting confusing. Let me assess what's happening and simplify.

The skill is updated. Now they need to redo the Instagram card brief using the corrected skill (Static 1), then build it in Figma. Let me give them a clear state of where things stand.Skill is updated. Let me give you a clean status of where things stand right now.

**DONE TODAY:**
- Tuesday LinkedIn — posted
- Wednesday LinkedIn — ready to post (trip support companies post)
- lh-news-pill skill — updated

**IN PROGRESS:**
- Wednesday Instagram card — needs to be re-run through the updated skill to get the correct Static 1 brief, then built in Figma

**ONE THING TO DO NEXT:**
Go to tab 4 and re-run the Instagram brief with the updated skill. It will now output Static 1 (full bleed image + headline overlay) instead of the briefing card.

Do you want the prompt to paste?

---

## Phelipe

yes

---

## Claude

Simple - give the prompt to paste into tab 4.```
use lh-news-pill. week a wednesday. newsletter echo card. REDO — previous run selected wrong template.

source: edition 2 — "Your Plane Crossed Seven Borders. You Signed One Manifest."

headline to use: Overflight Is Not Landing
summary: Two permits. Two authorities. Two timelines. One routing change can reset both.

template should now be Static 1 — full bleed image, headline overlay. output: image sourcing guidance, on-design copy, caption.

caption already written — use this exactly:

Flying over a country and landing in it require separate permits from separate sovereign authorities.

A charter routing from Miami to São Paulo crosses Cuban, Colombian, and Peruvian airspace before reaching Brazil. Each overflight needs its own clearance. The landing permit is a different application, different authority, different timeline.

A weather deviation that shifts the flight path into a different country's airspace triggers new permit applications. The timeline resets. The cost changes.

On international trips, the routing is not just a flight path. It is a chain of government approvals. Changing one link can break the chain.

From Edition 2 of Loud Hawk. Link in bio.
```

---

## Claude

The skill output is clean. Static 1 confirmed. Now they need an image. Let me search for one.Static 1 confirmed. Now you need the image. Let me search.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Image search is blocked for aviation content. Go directly to Unsplash and search these in order:

1. "aerial jet ocean" 
2. "aircraft high altitude clouds"
3. "airplane wing ocean below"

The fallback the skill called is valid — dramatic high-altitude sky shot with visible horizon curvature works. The image needs to feel like crossing airspace at altitude, not sitting on a ramp.

Once you have the image, swap it into the Static 1 template in Figma. Headline overlay: **Overflight Is Not Landing.** White bold text, LH logo top left.

---

## Phelipe

what you think about the healine to short?

---

## Claude

The headline is "Overflight Is Not Landing" — 5 words. Phelipe is asking if it's too short for the Static 1 template headline overlay.

For Static 1 (full bleed, headline at bottom), short can actually work well — it's punchy and counterintuitive. But it might feel sparse on the visual. Let me think about alternatives that add a bit more without losing the sharpness.For Static 1 it can feel sparse at the bottom of a full-bleed image. Five words don't fill the space well visually.

Two options that keep the same idea but land harder:

**Option A — add the consequence:**
> Overflight Is Not Landing. Two Permits. Two Authorities.

**Option B — reframe as a fact:**
> Flying Over a Country and Landing in It Are Not the Same Permit.

Option A is stronger for the template. It fills the space, still stops the scroll, and the three short sentences hit like a list without being a list.

What do you think?

---

## Phelipe

go format

---

## Phelipe

go format? for design

---

## Claude

Looking at the Figma design, I can see the headline is at the bottom but the text box seems small and the headline wraps awkwardly. A few issues:

1. The headline text box is too small/cramped at the bottom
2. The aircraft image (Falcon 10X) is a beauty shot which is fine, but it's a manufacturer/promotional image which could have copyright issues
3. The headline placement and size look okay but could be improved

Let me give feedback on the design.Looks good directionally. Two things to fix:

**1. Image.** The Falcon 10X is a manufacturer press photo — copyright risk. Swap it for a Unsplash/Pexels free-use aerial shot. Search "airplane window view clouds" or "aircraft wing sky altitude" on Unsplash.

**2. Headline text box** is too narrow and cramped into the bottom left corner. Stretch it full width edge to edge with padding, so the text has room to breathe. It's breaking mid-sentence awkwardly right now.

Everything else — logo placement, overlay position, font — is correct. Fix those two and it's done.

---

## Phelipe

give images now

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Best available is result 1 or 3 from the first search — wing visible, clouds below, altitude feel. Both are free stock.

For Figma: grab either from Pexels or the source site, crop to portrait 1080x1350, and swap into the frame. The wing-and-clouds shot communicates transit at altitude without any copyright issues.

---

## Phelipe

weird?

---

## Claude

The image shows a window frame cropped tightly - it looks odd because the airplane window frame is cutting into the design awkwardly. The image itself is good (aerial view, land below, altitude feel) but the framing/crop is the problem.

Two issues:
1. The window frame of the airplane is too prominent - it's distracting
2. The image crop is too tight on the window frame

Suggestions to fix.The image itself is right — altitude, land below, correct feel. Two problems:

**1. The window frame.** It's too literal and cuts the image awkwardly. Zoom in on the image inside Figma to crop out the window frame. You want just the sky/land/clouds view, not the plastic frame around it.

**2. The card has a white border** around the whole frame. That border is making it look like a photo inside a box rather than a full-bleed card. Remove it or make the image fill edge to edge.

Fix those two and it works. The image direction is correct.

---

## Claude

The window frame is still there and it's dominating the card. Two options:

**Option A — find a different image.** Search Unsplash for "aerial view land clouds" or "sky above clouds landscape" — no window, just sky and earth. Cleaner for this concept.

**Option B — embrace the window.** It does communicate "you're on a plane" which is on-topic. If you go this route, zoom the image in Figma so the window frame is mostly cropped out — just the bottom curve of the frame visible, with land and clouds filling the card.

Honestly Option A is cleaner. The window frame is a consumer travel photo feel. This post is about sovereign airspace and government permits — it needs something more austere.

Try Unsplash: "aerial landscape clouds above" or "earth from altitude atmosphere."

---

## Phelipe

find for mew

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Result 2 from the last search — aerial drone shot of Jamaica, Caribbean sea and coastline — is the one. Coastal geography, no window, correct region for the Miami to São Paulo routing story. Go grab that from Pexels and swap it in.

---

## Claude

That's much better. Aerial, no window, geographic feel. Two remaining fixes:

**1. White border** — remove it. Image should bleed to the edges of the card.

**2. Boost the resolution** — Figma is already flagging it. Hit "Boost resolution" before exporting.

Otherwise this is ready. Logo placement is clean, headline reads well, layout is correct.

---

## Phelipe

caption

---

## Claude

They want the caption to post with the Instagram card.Flying over a country and landing in it require separate permits from separate sovereign authorities.

A charter routing from Miami to São Paulo crosses Cuban, Colombian, and Peruvian airspace before reaching Brazil. Each overflight needs its own clearance. The landing permit is a different application, different authority, different timeline.

A weather deviation that shifts the flight path into a different country's airspace triggers new permit applications. The timeline resets. The cost changes.

On international trips, the routing is not just a flight path. It is a chain of government approvals. Changing one link can break the chain.

From Edition 2 of Loud Hawk. Link in bio.

---

## Phelipe

humanizer

---

## Claude

Apply humanizer to the caption.

AI patterns to check:
- "The timeline resets. The cost changes." — parallel short sentences, slightly assembled
- "Changing one link can break the chain." — slightly metaphor-heavy closer
- Overall it's pretty clean already, written in Phelipe's voice

Let me apply the humanizer process.

Flags:
- "It is a chain of government approvals. Changing one link can break the chain." — chain metaphor used twice, feels constructed
- "The timeline resets. The cost changes." — too neat/parallel, reads assembled
- Otherwise fairly clean

Final version should break the parallel closer and remove the repeated chain metaphor.**AI patterns flagged:**
- "The timeline resets. The cost changes." — parallel short sentences, too neat, assembled feel
- "It is a chain of government approvals. Changing one link can break the chain." — chain metaphor repeated twice in two sentences

---

**FINAL CAPTION:**

Flying over a country and landing in it require separate permits from separate sovereign authorities.

A charter routing from Miami to São Paulo crosses Cuban, Colombian, and Peruvian airspace before reaching Brazil. Each overflight needs its own clearance. The landing permit is a different application, different authority, different timeline.

A weather deviation that shifts the flight path into a different country's airspace triggers new permit applications. The routing has to be reworked. The cost changes. The client usually finds out the morning of departure.

On international trips, the routing is a compliance document. Not just a flight path.

From Edition 2 of Loud Hawk. Link in bio.

---

## Phelipe

edition is tomorrow

---

## Claude

Change the last line to:

> Edition 2 drops tomorrow. Link in bio.

---

## Phelipe

done

---

## Claude

Wednesday is done.

**Today's completed:**
- LinkedIn posted (Tuesday — trip support companies)
- Wednesday LinkedIn ready to post
- Wednesday Instagram card built and captioned

**Still needed today:**
- Post the Wednesday LinkedIn
- Post the Instagram card

Do those now while you have momentum.

---

## Phelipe

post linked in and insta today

---

## Claude

The user wants to post both LinkedIn and Instagram today. They have the content ready. Let me help them do this efficiently.

For LinkedIn - they need to post the Wednesday post (trip support companies).
For Instagram - they need to post the card they just built in Figma.

Let me navigate to LinkedIn first.Starting with LinkedIn.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I can't control the browser from here directly. You'll need to do these manually but it's fast.

**LinkedIn — paste and post:**

The companies that decide whether your international charter trip actually happens are companies you have never heard of.

Not the operator. Not the broker. The trip support company.

Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.

Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do. Across hundreds of international flights per month.

A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.

The client never thinks about this layer. The broker depends on it completely.

Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.

Next time you book international, ask your broker one thing: which trip support company is handling this trip?

The ones who have done this before answer without looking it up.

---

**No first comment on this one.** Standalone post, no link.

**Instagram** — export the card from Figma, post with the caption. Link in bio should point to loudhawk.media.

Let me know when both are live.

---

## Phelipe

poted already

---

## Claude

Good. Wednesday is fully done.

**Current week status:**

| Day | Platform | Status |
|---|---|---|
| Tuesday | LinkedIn | Done |
| Wednesday | LinkedIn | Done |
| Wednesday | Instagram | Done |
| Thursday | LinkedIn | Pending |
| Friday | Instagram | Pending |
| Saturday | LinkedIn | Pending |
| Sunday | Instagram | Pending |

Tomorrow is Thursday — one LinkedIn forward-testing post. Any open lane except HIAW and TG (both used this week). MS or SA is next.

Do you want to prep Thursday's post now or come back tomorrow?

---

## Phelipe

today is march 26
draft of edition 2 is done and attached.
so we have instagram and linked in today ?

---

## Claude

Today is March 26 — this is the Edition 2 send day. Let me think about what's on the calendar.

Edition 1 shipped March 12 (Week A anchor). Week B was March 16-22. Week A (Edition 2) started March 23. Edition 2 sends today, March 26 — which is Thursday of Week A.

Thursday Week A schedule:
- LinkedIn: Forward-testing, any open lane
- Newsletter: Ships today

No Instagram today — Friday is the next Instagram day.

Wait, let me re-check. The calendar says:
- Monday: Instagram
- Tuesday: LinkedIn (edition pull) ✓ done


- Wednesday: LinkedIn (forward-testing) ✓ done + Instagram (newsletter echo) ✓ done
- Thursday: LinkedIn (forward-testing, any open lane)
- Friday: Instagram
- Saturday: LinkedIn
- Sunday: Instagram

So today Thursday March 26: LinkedIn post + newsletter send. No Instagram today.Today is Thursday, Week A. Newsletter send day.

**Today's tasks:**

| Action | Platform | Status |
|---|---|---|
| Send Edition 2 | Beehiiv | Pending |
| LinkedIn forward-testing post | LinkedIn | Pending |

No Instagram today. Friday is next IG day.

**LinkedIn today:** Forward-testing, any open lane. MS is the strongest unused lane this week — Tuesday was HIAW, Wednesday was TG.

Two things to do. Which first — send the edition or build the LinkedIn post?

---

## Phelipe

thake care of edition 2. check if is good

---

## Claude

The user wants me to review Edition 2 for quality before sending. I have the full text in the document. Let me review it against Loud Hawk editorial standards.

Key checks:
- No em dashes
- No AI writing tells
- Accuracy of claims
- Editorial lane alignment
- Subject line strength
- CTA at close
- Quick hits quality

Let me read through it carefully.

Em dashes: I need to check. Looking at the text... I don't see any em dashes. Good.

Claims to flag:
- "Opa-locka" - this is a real executive airport in Miami area (OPF), correct
- Cuban, Colombian, Peruvian airspace on MIA-GRU routing - this is accurate for a typical routing


- Universal Weather and Aviation, Jeppesen - real trip support companies, correct
- APIS data to CBP - correct
- 72 hours minimum for most jurisdictions - accurate
- China, Russia, Gulf/African states 5-7+ business days - this is accurate directionally, though exact requirements vary
- Part 135 operator requirements - accurate
- The footer "Reply here" link appears to be handled by Beehiiv's reply functionality rather than a hardcoded destination

Now I need to check the operational accuracy on the remaining items Phelipe flagged.

I'm reviewing the overall structure and voice. The subject line hooks well, the signal section flows clearly, the quick hits complement without repeating, and the close is straightforward. I'm checking for em dashes, luxury language, and vague superlatives—all clean. The piece stays specific and operational throughout. Before we publish, I should remind Phelipe that he wanted to do his own accuracy check on the permit timelines and Colombian overflight scenario.Reviewing now against editorial standards.
```
This block is not supported on your current device yet.
```

The file is a binary docx file. I already have the text content from the earlier document share in this conversation. Let me use that to review the edition.

I need to do a quality check. From my memories, there was a note that Edition 2 was "pending Phelipe's own operational accuracy check on permit timelines and the Colombian overflight scenario."

Let me review the text I already have against editorial standards:

1. No em dashes - checking... I don't see any in the text shared earlier. Good.
2. No AI writing tells
3. Voice is consistent
4. Claims are accurate


5. Footer is correct

Before he sends this out, I need to flag that critical note about Phelipe needing to verify the permit timelines and Colombian overflight scenario details. Let me pull up the edition text from document index 8 and work through the editorial checklist systematically—em dashes are clear, the subject line has real punch, the voice stays operational without any luxury language creeping in, and I'm not catching any obvious AI tells. The main thing holding this back is getting Phelipe's confirmation on those specific operational claims. The call-to-action at the footer uses a reply link in Beehiiv to let readers ask questions about charter or the market. The piece reads well editorially overall, though Phelipe still needs to verify the permit timelines and Colombian overflight routing before it goes out.I already have the full text. Reviewing now.

**Editorial checks:**

- No em dashes ✓
- No luxury language ✓
- No AI writing tells ✓
- Subject line is strong ✓
- Quick Hits complement the Signal without repeating it ✓
- Footer is correct ✓
- Lane: MS/HIAW blend, appropriate for Edition 2 ✓

**One flag before you hit send.**

From when we built this — you flagged that you wanted to do your own operational accuracy check on two specific things before sending:

1. The permit timeline claims (72 hours minimum, 5-7 business days for China/Russia/Gulf)
2. The Colombian overflight scenario on the Miami to São Paulo routing

Have you done that check? If yes, send it. If not, do it now before it goes to subscribers. Everything else is clean.

---

## Phelipe

check for us. does sound to much a big deal what you think ?

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Claims check out. Here's what the research confirms:

**Accurate:**
- 72-hour minimum baseline — confirmed across multiple sources. Colombia specifically requires 48-72 working hours for overflight, 72 hours for landing.
- 5-7 business days for slower jurisdictions — confirmed for India, Gulf states, parts of Africa. The edition uses "five to seven or more business days" which is correctly hedged.
- Overflight and landing are separate permits from separate authorities — confirmed.
- Trip support companies (Universal Weather, Jeppesen) handle this — confirmed.
- Colombia overflight requires prior permission — confirmed.

**One nuance to be aware of:**
The edition says Colombia overflight could be denied and require re-routing. Colombia is actually a relatively cooperative jurisdiction at 48-72 hours — the denial scenario is real but more common in tighter or more restricted airspaces. The edition frames it as a contingency scenario, not a likely outcome, which is accurate.

**Verdict: edition is clean. Send it.**

The claims are not overstated. The edition does not sensationalize — it describes real operational reality that most charter clients genuinely don't know about. This is exactly the kind of grounded, sourced intelligence Loud Hawk should be publishing.

Go send it in Beehiiv.

---

## Phelipe

i dont remember how i did

---

## Claude

The user is on a blank Beehiiv post editor and doesn't remember how they built Edition 1. They need to know how to get Edition 2 content into Beehiiv.You're on a blank new post. You need to either paste the content in manually or import it. Fastest path:

**Option 1 — Paste directly:**
1. Click the title field, type: `Your Plane Crossed Seven Borders. You Signed One Manifest.`
2. Click the subtitle field, add: `Edition 2 · Vol. I · No. 02 · March 2026`
3. Click the body, paste the full edition content section by section

**Option 2 — Check if Edition 1 exists as a template:**
Go to Posts in the left sidebar and find Edition 1. Duplicate it, then replace the content. This preserves your formatting from last time.

Which did you use for Edition 1 — did you build it from scratch or duplicate?

---

## Claude

Edition 1 is right there. Duplicate it — that's the fastest path. It already has your formatting, sections, and structure locked in.

Here's how:

1. Hover over Edition 1 in the Posts list
2. Click the three-dot menu that appears
3. Select **Duplicate**
4. Open the duplicate
5. Replace all content with Edition 2 text
6. Update the subject line, title, subtitle, and date

Do you see the three-dot menu when you hover over Edition 1?

---

## Claude

Good — the duplicate is created. It's in Draft, dated March 26. Now click **Edit post** in the top right and start replacing content.

Here's your replacement checklist:

1. **Title:** `Your Plane Crossed Seven Borders. You Signed One Manifest.`
2. **Subtitle/Preview text:** `Behind every international charter departure is a compliance chain spanning half a continent. Most clients never see it.`
3. **Remove the "(1)"** from the subject line
4. **Header line:** `Edition 2 • March 2026`
5. **Body:** Replace all content with Edition 2 text

Click Edit post and start with the title. Do you want me to feed you the content section by section as you go?

---

## Phelipe

format is not the same. 
color and sizing

---

## Claude

The user is saying the formatting in Edition 2 doesn't match Edition 1. Looking at the screenshot, I can see the content is there but the formatting looks different - the header section, THE SIGNAL styling, etc. might not match Edition 1's formatting.

Let me look at what's visible:
- LOUD HAWK (orange, correct)
- Edition 2 • March 2026 (looks correct)
- THE SIGNAL (bold, black - but in Edition 1 it was likely orange/colored)
- The body text appears to be in a different style

The user needs to check the Style tab in Beehiiv to match Edition 1's formatting. 

Without seeing Edition 1 directly, the problem is probably that the duplication process didn't preserve all the styling - "THE SIGNAL" should likely be orange to match "LOUD HAWK", and the section headers need to align with the original design.Looking at the screenshot — "THE SIGNAL" is rendering in black bold instead of orange like Edition 1. The body text sizing may also be off.

Two things to check:

**1. THE SIGNAL header color** — click on the "THE SIGNAL" text, highlight it, and check the text color in the toolbar. It should match the orange from Edition 1 (the same orange as the LOUD HAWK wordmark above it).

**2. Section title sizing** — "Your Plane Crossed Seven Borders. You Signed One Manifest." should be a specific heading size. Click it and check what heading level it's set to versus Edition 1.

Fastest fix: open Edition 1 in a separate tab, click each element to see its formatting, then match it in Edition 2. 

Do you want me to navigate to Edition 1 in the browser to pull the exact styles side by side?

---

## Phelipe

i am struggleing. how we make standard

---

## Claude

The user is struggling with formatting consistency between Edition 1 and Edition 2 in Beehiiv. The issue is that "THE SIGNAL" in Edition 2 is black/dark, while in Edition 1 it's orange (#FF4900). The typography settings (Inter, Bold for headings, Regular for paragraph) are the same. The only difference is the color of "THE SIGNAL" text.

The fix is simple: click on "THE SIGNAL" text in Edition 2, highlight it, and change the text color to #FF4900.

But the user is asking how to make it standard so they don't have to do this manually each time. 

The issue is that Beehiiv's duplication feature doesn't reliably preserve all styling attributes—the color property on "THE SIGNAL" heading got lost in the copy, even though the typography carried over fine. I should give them a workaround or explain what's happening under the hood.The only real difference I can see is the color on "THE SIGNAL" — Edition 1 is orange (#FF4900), Edition 2 is black. Typography is the same on both (Inter, Bold headings, Regular body).

**Fix right now — 30 seconds:**

1. Highlight "THE SIGNAL" in Edition 2
2. Click the text color tool in the toolbar
3. Type in `#FF4900`
4. Do the same for "QUICK HITS" when you get there

**To prevent this next time:**

When you duplicate Edition 1, the orange color on those section headers is not carrying over. Before you replace any content next edition, immediately check those two headers first and fix the color before touching anything else.

That's the only formatting issue. Everything else — font, weight, spacing — is matching correctly. Fix the two headers and you're done.

---

## Phelipe

compare both structures

---

## Claude

The user wants me to compare the structures of Edition 1 and Edition 2 to identify formatting differences that need to be fixed in Beehiiv.Comparing both:

**Where they match:**
- LOUD HAWK header
- Edition # • Month Year line
- THE SIGNAL section header
- Body paragraphs
- QUICK HITS section header
- Footer line
- Three Quick Hits items

**Where Edition 2 differs:**

| Element | Edition 1 | Edition 2 |
|---|---|---|
| Signal opening | Has a bold subhead ("How a Charter Trip Actually Gets Sourced") before body | Opens directly into body, then has multiple bold subheads (What permits actually are, The timeline problem, etc.) |
| Quick Hits format | Each hit has a **bold title** on its own line, then body text below | Each hit runs the bold title directly into the body text with no line break |
| Footer | "published by Orange Sunshine Aviation" | "published biweekly by Orange Sunshine Aviation" — correct, keep this |
| Signal title | No standalone bold title at top | Has "Your Plane Crossed Seven Borders. You Signed One Manifest." as bold opener |

**Action needed in Beehiiv:**

The Quick Hits format is the main issue. Each of the three items needs the bold title separated from the body text — bold title on its own line, then the paragraph below it. That's how Edition 1 renders them.

Everything else is structurally consistent. Fix the Quick Hits formatting and the orange color on the two section headers and it's ready to send.

---

## Claude

The Quick Hits structure is already matching Edition 1 — bold title on its own line, body text below, with a line break between them. That's correct.

**Edition 2 Quick Hits looks good.** QUICK HITS header is orange. Titles are bold. Body is separate.

**Two remaining items before you send:**

1. Go back to the top and confirm "THE SIGNAL" header is orange (#FF4900) — from the earlier screenshot it was still black
2. Check the post title and subject line at the top are correct — "Your Plane Crossed Seven Borders. You Signed One Manifest." with no "(1)"

If those two are fixed, hit **Next** and send.

---

## Claude

Edition 2 looks correct. Title, subtitle, LOUD HAWK, Edition 2, THE SIGNAL all in orange. Formatting matches Edition 1.

**One thing left — the subject line.** That's set separately in Beehiiv, not in the body editor. Click **Next** at the top right and on the next screen check that the subject line reads:

`Your Plane Crossed Seven Borders. You Signed One Manifest.`

Not the old Edition 1 subject line. Update it there, then continue through to send.

---

## Phelipe

this?

---

## Claude

That's the preview. Everything looks correct:

- Subject: `Your Plane Crossed Seven Borders. You Signed One Manifest.` ✓
- Preview text: correct ✓
- Date: March 26, 2026 ✓
- LOUD HAWK orange ✓
- Edition 2 • March 2026 ✓
- THE SIGNAL orange ✓
- Body text starts correctly ✓

Close the preview and hit **Next** to proceed to send.

---

## Claude

All correct. Subject line and preview text are clean.

Likes & Comments is off — keep it off, consistent with Edition 1.

Hit **Next** and send.

---

## Claude

Two things on this screen before you hit Review:

**1. Post thumbnail** — upload the Loud Hawk logo or a relevant image here. This is what shows in the web feed and SEO. Use the same og:image you uploaded to Beehiiv settings earlier.

**2. Post URL** — looks clean and auto-generated correctly.

Everything else is fine. Upload the thumbnail then hit **Review**.

---

## Phelipe

how to change edition thumbnail?

---

## Claude

The thumbnail is set in the Web post settings screen you were just on — the "Post thumbnail" upload field. Go back to that screen.

**How to get there:**

1. Go to Posts in Beehiiv
2. Click on Edition 2
3. Click **Edit post**
4. Click **Next** through Compose and Audience
5. Stop at the **Web** step
6. Upload your thumbnail image there

The logo that's showing now (the purple/orange bird mark) is the default Beehiiv publication logo pulling in as a fallback. Once you upload a specific thumbnail on that Web screen it will replace it.

What image do you want to use for Edition 2's thumbnail?

---

## Phelipe

its edition 1 i wanna change. no next option

---

## Claude

You're in Edition 1 which is already Published. The thumbnail is set via the **"Add thumbnail"** link at the very top of the compose screen — you can see it right there above the title.

Click **"Add thumbnail"** and upload the image directly from there. No need to go through Next.

---

## Phelipe

no this is in the post thumbnail. i wanna change on the website thumnail

---

## Claude

The user wants to change the thumbnail that shows on the Beehiiv website/archive page for Edition 1. That's the "Post thumbnail" in the Web settings step. Since Edition 1 is already published, they need to go to Next → Web to find that field.

But they said there's no "Next" option — instead they see "Update web" button at the top right. Let me look at the screenshot again. Yes, I can see "Update web" button in the top right instead of "Next". So they should click through the steps manually or use the "Web" tab in the top navigation.Click **Web** in the top navigation bar — you can see it at the top: Compose → Audience → Email → **Web** → Review.

That takes you directly to the Web post settings where the post thumbnail upload field is.

---

## Phelipe

time to activate on the website loudhawk.media

---

## Claude

The user wants to publish/activate Edition 2 on the website. They need to go back to Edition 2 and complete the publish flow.Go back to Edition 2. You need to complete the Review step and publish.

1. Go to **Posts**
2. Click **Edition 2**
3. Click **Edit post**
4. Click **Next** through to **Review**
5. On the Review screen you'll see a **Publish** or **Send** button

That publishes it to the web and sends to subscribers simultaneously. Do you want to send to all subscribers now or schedule it?

---

## Phelipe

this is on github probably

---

## Claude

The user is saying the loudhawk.media website is hosted on GitHub (likely GitHub Pages). They want to change the edition thumbnail on the website. Let me think about this - loudhawk.media redirects to www.loudhawk.media which earlier showed a Beehiiv site. But the user is saying it's on GitHub. Let me not assume and ask for clarification.

Actually, looking back at the conversation, when we checked loudhawk.media earlier it showed a Beehiiv site. But now the user is saying it might be on GitHub. They might have a custom website hosted on GitHub Pages that's separate from the Beehiiv newsletter platform.


So the thumbnail issue might be controlled by code in the GitHub repository rather than through Beehiiv's settings directly - that would make sense if loudhawk.media is a custom site pulling from Beehiiv's API or RSS feed. I should ask which GitHub repo we're working with.Which repo? Do you have the GitHub link or the repo name handy?

---

## Claude

This is a custom-built website separate from Beehiiv. Edition 2 card is already showing with "COMING MARCH 26" — it's hardcoded in the site, not pulled from Beehiiv automatically.

You need to update the site code to:
1. Change "COMING MARCH 26" to "Read this edition →"
2. Add the link to the published Beehiiv post URL
3. Update the title if needed — it currently says "International Permits and the 72-Hour Window" not the actual subject line

This is in your GitHub repo. Do you want me to find the repo in your browser tabs or do you have the repo name?

---

## Phelipe

use claude code on tab 4

---

## Claude

Paste this into tab 4:

```
find the loudhawk.media website source code in ~/osa. locate the edition 2 card. make these changes:

1. change "COMING MARCH 26" to a "Read this edition →" link
2. the link URL should point to the published beehiiv post: https://loudhawk.beehiiv.com/p/your-plane-crossed-seven-borders-you-signed-one-manifest
3. keep all other content on the card unchanged

then deploy.
```

Note: confirm the exact Beehiiv URL first — go to the published Edition 2 post on loudhawk.beehiiv.com and copy the exact URL before Claude Code runs the deploy.

---

## Claude

It's asking for confirmation. Type this in tab 4:

```
yes, proceed with the commit and push
```

---

## Claude

Pushed and deployed. Let me verify the site updated.
```
This block is not supported on your current device yet.
```

Check loudhawk.media in your browser. The Edition 2 card should now show "Read this edition →" with the link active instead of "Coming March 26."

Vercel deploys in about 30-60 seconds from the push. If it's not updated yet, wait a minute and refresh.

---

## Phelipe

not happy... is not working

---

## Claude

I see the issue. The new commit deployed to **master** branch as a Preview, but production is on the **main** branch. The site is still showing "Coming March 26" because the production deployment hasn't changed.

Paste this in tab 4:

```
the deploy went to master branch but production is on main branch. 
push the same changes to main branch so vercel deploys to production.
```

---

## Claude

Pushed to main. Check loudhawk.media now — should show "Read this edition →" on the Edition 02 card. Vercel deploys in about 30 seconds.

---

## Phelipe

linked in now

---

## Claude

Thursday LinkedIn post. Forward-testing, MS lane (unused this week). Let me give the prompt for tab 4.Paste this in tab 4:

```
use lh-linkedin. week a thursday. forward-testing post.

lane: MS (Market Signal). tuesday was HIAW, wednesday was TG. MS is the open lane.

no newsletter link. no subscribe CTA. standalone observation only.

source: edition 2 content below. find a market signal angle that was NOT the focus of tuesday or wednesday. tuesday was compliance/permit timelines. wednesday was trip support companies as invisible infrastructure.

strong candidates:
- operator selection for international trips — not every Part 135 is configured for international. some have never filed an overflight permit for the region you're traveling to.
- the sourcing difference between domestic and international operator vetting
- what a denied overflight permit actually does to a trip operationally

pick the sharpest standalone MS angle. output full post.

---

[paste full edition 2 text]
```

Do you want me to write out the full edition text to paste, or do you have it ready?

---

## Phelipe

what? no newsletter hook? we literally launched a edition 2

---

## Claude

You're right. Thursday is still Week A — the edition just dropped today. The post should reference it.

But the calendar rule says no newsletter link in the post body on Thursday — that was Tuesday's job. The distinction is: Tuesday had the subscribe link in the first comment. Thursday stands alone.

However, since the edition literally just sent today, you can reference it naturally in the body without a CTA. Something like "covered this in today's Loud Hawk" as context, not as a hook.

Want me to build the prompt with that framing — MS angle, references the edition dropped today, no subscribe link, no CTA?

---

## Phelipe

we should have a CTA and link

---

## Claude

Agreed. Edition just launched today — this is the one exception where a Thursday post should carry the link. The rule exists to prevent off-week posts from becoming newsletter promos. This is publish day. Different situation.

Paste this in tab 4:

```
use lh-linkedin. week a thursday. edition launch day post.

edition 2 launched today. this post should reference the edition and include a subscribe CTA in the first comment.

lane: MS (Market Signal). tuesday was HIAW (compliance/permit timelines). wednesday was TG (trip support infrastructure). pick the sharpest unused MS angle from the edition.

strong candidates:
- not every Part 135 operator is configured for international. some have never filed an overflight permit for the region you're traveling to. operator vetting on international trips is a different exercise than domestic.
- what a denied overflight permit actually does to a trip — re-routing, new permit applications, fuel stop, cost change, client finds out morning of departure.

post should stand alone as a strong observation. close with a natural reference to edition 2 dropping today. subscribe link in first comment.

---

LOUD HAWK — Edition 2
Subject line: Your Plane Crossed Seven Borders. You Signed One Manifest.

[paste full edition 2 text]
```

---

## Phelipe

The companies that decide whether your international charter trip actually happens are companies you have never heard of.Not the operator. Not the broker. The trip support company.Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do. Across hundreds of international flights per month.A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.The client never thinks about this layer. The broker depends on it completely.Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.Next time you book international, ask your broker one thing: which trip support company is handling this trip?The ones who have done this before answer without looking it up.

last post was this. lets make sure we dont doble post

---

## Claude

Good catch. That was Wednesday's post — trip support companies, TG lane. Already posted.

So for Thursday the angle must be different. From the edition, the cleanest unused MS angle is:

**Not every Part 135 operator is configured for international.** Some lack the avionics. Some have no trip support relationship. Some have never filed an overflight permit for the region you're traveling to. Operator vetting on international trips is a fundamentally different exercise than domestic.

That's fresh, it's MS lane, and it hasn't been touched yet. Want me to write the prompt for tab 4 with that angle?

---

## Phelipe

prompt

---

## Claude

```
use lh-linkedin. week a thursday. edition launch day post.

edition 2 launched today. include subscribe CTA in first comment.

lane: MS (Market Signal).

angle: not every Part 135 operator is configured for international operations. some lack the required avionics for certain controlled airspaces. some have no working trip support relationship. some have never filed an overflight permit for the region you are traveling to. operator vetting on international trips is a fundamentally different exercise than domestic. this is the sourcing difference most clients never think about.

do NOT repeat the trip support companies angle (Universal Weather, Jeppesen) — that was yesterday's post.

close with a natural reference to edition 2 dropping today.

first comment: subscribe link to https://loudhawk.media

---

LOUD HAWK — Edition 2
Subject line: Your Plane Crossed Seven Borders. You Signed One Manifest.

You signed a trip manifest at Opa-locka. Printed your name, your passport number, your destination. One document. One signature. Clean.

Your broker spent the prior 72 hours building the compliance chain that made that departure legal. Overflight permits filed through three countries you will never set foot in. Landing authorization from Brazilian civil aviation. APIS data transmitted to CBP. Customs pre-clearance coordinated with a ground handler in Guarulhos. A contingency routing plotted in case Colombian airspace denied the overflight on short notice.

You saw a departure time. The broker built a permissions architecture spanning half a continent.

This is how international charter actually works. And almost none of it is visible to the person writing the check.

What permits actually are

A charter flight from Miami to São Paulo does not simply fly south. It transits sovereign airspace belonging to multiple countries between departure and destination. Each country controls access to its airspace independently. Crossing through that airspace requires an overflight permit. Touching down requires a separate landing permit, issued by a different authority with different requirements and different processing timelines.

These are not formalities. They are discrete government approvals. A flight that crosses Cuban, Colombian, and Peruvian airspace on the way to Brazil needs overflight clearance from each. None of those countries owes you access. None of them processes on your schedule.

The passenger never thinks about this. The broker thinks about nothing else for three days.

The timeline problem

Most international destinations require permit applications 24 to 72 hours in advance at minimum. That is the baseline for cooperative, well-staffed civil aviation authorities with established relationships to the trip support providers doing the filing.

Then there are the slower jurisdictions. China, Russia, and several Gulf and African states require five to seven or more business days for overflight or landing permits. Business days. Not calendar days. A Friday request for a Monday departure to Riyadh does not work.

This is the part that catches clients off guard. Last-minute domestic charter is a sourcing challenge. Last-minute international charter is a compliance problem. The aircraft might be available. The crew might be legal. But if the permits have not been filed and approved, the trip does not happen. A broker who accepts a 12-hour booking on a transatlantic routing without flagging permit timelines is skipping a step.

The invisible layer

Brokers do not file these permits themselves. They work through trip support companies. Universal Weather and Aviation, Jeppesen, and a handful of other specialized firms manage permit applications, customs coordination, ground handler logistics, and routing advisories across jurisdictions. These companies are the operational infrastructure behind every international charter trip.

The client has never heard of them. The broker relies on them completely.

This matters for operator vetting. A Part 135 operator with an active, tested trip support relationship is an operator whose permit exposure is being managed by professionals who do this across hundreds of international flights per month. An operator without one is managing permits ad hoc, or not managing them at all.

What failure looks like

A permit denied 18 hours before departure. A routing revision because one country's airspace closes on a NOTAM with no warning. A customs pre-clearance requirement that forces the client to arrive 90 minutes early at the FBO. Information that surfaces the night before, not during planning. A ground handler at the destination airport who was never confirmed, so there is no fuel, no customs officer, and no one to marshal the aircraft on arrival.

These are not hypotheticals. They are the operational reality of international routing done without adequate lead time or planning discipline. On the Miami to São Paulo routing, a denied Colombian overflight does not just delay the trip. It requires re-routing through Caribbean airspace, new permit applications for different countries, and potentially a fuel stop that was not in the original plan. The timeline resets. The cost changes. The client finds out the morning of departure.

A broker who has done this before builds the buffer into the plan from the start. Alternate routing identified. Handler confirmed at destination. APIS filing deadlines calendared. Permit status tracked daily once applications are submitted. The client never sees this work. That is the point.

The sourcing difference

Operator selection for international trips adds a dimension that does not exist on domestic flights. Not every Part 135 certificate holder is configured for international operations. Some lack the required avionics for certain controlled airspaces. Some have no working trip support relationship. Some have never filed an overflight permit for the region you are traveling to.

The broker's job is to filter for operators who have done this routing or a comparable one. Not operators who say they can do international. Operators who demonstrably do.

The question to ask

Next time you book an international charter, ask your broker one thing: "What is your permit timeline for this routing, and who is handling trip support?"

A broker who answers that question specifically, without hesitation, has done this before. A broker who pauses, deflects, or gives you a vague reassurance has not.

QUICK HITS

The 72-Hour Minimum Most international destinations require permit applications at least 72 hours before departure. Several, including China, Russia, and portions of Gulf and African airspace, require five to seven or more business days. The implication: last-minute international charter is not just harder to source. It may be legally unpermittable on short notice. If you are planning international travel by private aircraft, your broker needs more lead time than you think. Build it into your planning window before you pick a date.

Overflight Is Not Landing Flying over a country and landing in it require separate permits from separate sovereign authorities. A routing change mid-planning, even something as minor as a weather deviation that shifts the flight path across a different country's airspace, can trigger new permit applications across multiple jurisdictions and reset the timeline. On international trips, treat the routing as a compliance document. It is not just a flight path. It is a chain of government approvals, and changing one link can break the chain.

Ask About Trip Support Trip support companies are the operational backbone of international charter. They manage permits, customs, ground handlers, and routing advisories. A broker who does not use one, or whose operator does not have a relationship with one, is leaving permit and logistics coordination to chance. Ask your broker which trip support company is handling your international trip. If they do not have a specific answer, that tells you everything you need to know about how the trip is being managed.

Loud Hawk is published biweekly by Orange Sunshine Aviation. Questions about charter or the market? Reply here.
```

---

## Claude

Strong output. Let me review it quickly before presenting.

The post is clean. CPDLC/ADS-C avionics detail is sharp and specific. Doesn't repeat Wednesday's trip support companies angle. Closes with edition reference naturally.

One thing to check: "No CPDLC, no ADS-C — which means no North Atlantic, no certain RVSM corridors over South America." — this is technically accurate. CPDLC (Controller-Pilot Data Link Communications) and ADS-C (Automatic Dependent Surveillance-Contract) are required for oceanic/remote operations. RVSM is a separate certification but related. This checks out.


Let me run it through the humanizer before I send this out.Strong output. Avionics detail (CPDLC, ADS-C) is sharp and accurate. Close to the edition is natural, not promotional.

Run humanizer before posting. One thing I'd flag: "The airplane physically cannot comply" is a clean line — make sure humanizer doesn't soften it.

Want me to run it here?

---

## Phelipe

humanizer

---

## Claude

**AI patterns flagged:**
- "They have the certificate. They have the aircraft. But when you look closer, the gaps show up fast." — parallel structure feels assembled
- "That is the sourcing question most clients never think to ask." — slightly declarative/conclusory
- "all of that plus" — additive phrasing pattern

---

**FINAL POST:**

Not every Part 135 operator can actually fly international.

They have the certificate. They have the aircraft. But look closer and the gaps show up fast.

Some operators lack the avionics required for certain controlled airspaces. No CPDLC, no ADS-C — which means no North Atlantic, no certain RVSM corridors over South America. The airplane physically cannot comply.

Some have never filed an overflight permit for the region you are traveling to. Filing for Colombian or Cuban airspace is not the same as filing a domestic IFR flight plan. There are lead times, government contacts, and approval chains that take days. An operator who has never done it before will learn on your trip.

Some have no working relationship with a trip support provider in the destination country. Ground handling, customs coordination, fuel contracts, landing slots — arranged in advance by someone who knows the local airport. If the operator has never flown there, they are starting from zero.

Domestically, operator vetting is about safety record, maintenance standards, and crew qualifications. Internationally, it is all of that plus a different question: can this aircraft, with this operator, execute this specific route legally and competently?

Most clients never think to ask it.

I wrote about this in today's edition of Loud Hawk — the permit timelines, the compliance chain, and what a broker actually builds before an international departure clears.

---

**FIRST COMMENT:**

Subscribe to Loud Hawk — private aviation intelligence, every two weeks: https://loudhawk.media

---

## Phelipe

The companies that decide whether your international charter trip actually happens are companies you have never heard of.Not the operator. Not the broker. The trip support company.Universal Weather and Aviation. Jeppesen. A handful of specialized firms that manage permit applications, customs coordination, ground handler logistics, and routing advisories across dozens of jurisdictions at once.Your broker does not file overflight permits with Colombian civil aviation. Your operator does not coordinate customs pre-clearance at Guarulhos. These companies do. Across hundreds of international flights per month.A Part 135 operator with a tested trip support relationship has its permit chain managed by professionals who do this daily. An operator without one is filing ad hoc, country by country, or not really managing it at all.The client never thinks about this layer. The broker depends on it completely.Most people vetting an international charter ask about the aircraft and the operator. Nobody asks about the infrastructure moving paperwork through seven countries before wheels-up.Next time you book international, ask your broker one thing: which trip support company is handling this trip?The ones who have done this before answer without looking it up.

this is not over done based o less one is it ? be honest

---

## Claude

Honest answer: yes, it's too close.

Both posts talk about operators without trip support relationships. Wednesday's post names Universal Weather and Jeppesen. Thursday's post says "no working relationship with a trip support provider in the destination country." Same layer, different angle.

A LinkedIn follower who saw both posts back to back would notice the overlap. The avionics point (CPDLC, ADS-C) is genuinely fresh and strong. But the trip support relationship paragraph in Thursday's post retreads Wednesday.

Two options:

**Option A — cut the trip support paragraph entirely.** The avionics angle and the permit filing angle are strong enough to carry the post without it. It reads cleaner anyway.

**Option B — hold this post and find a different angle for Thursday.** The edition has enough material — the "what failure looks like" section is untouched and has strong MS signal.

Option A is faster and the post still passes the scorecard. Want me to rewrite it with that paragraph removed?

---

## Phelipe

option a

---

## Claude

**FINAL POST:**

Not every Part 135 operator can actually fly international.

They have the certificate. They have the aircraft. But look closer and the gaps show up fast.

Some operators lack the avionics required for certain controlled airspaces. No CPDLC, no ADS-C — which means no North Atlantic, no certain RVSM corridors over South America. The airplane physically cannot comply.

Some have never filed an overflight permit for the region you are traveling to. Filing for Colombian or Cuban airspace is not the same as filing a domestic IFR flight plan. There are lead times, government contacts, and approval chains that take days. An operator who has never done it before will learn on your trip.

Domestically, operator vetting is about safety record, maintenance standards, and crew qualifications. Internationally, it is all of that plus a different question: can this aircraft, with this operator, execute this specific route legally and competently?

Most clients never think to ask it.

I wrote about this in today's edition of Loud Hawk — the permit timelines, the compliance chain, and what a broker actually builds before an international departure clears.

---

**FIRST COMMENT:**

Subscribe to Loud Hawk — private aviation intelligence, every two weeks: https://loudhawk.media

---

## Phelipe

take - out

---

## Claude

**FINAL POST:**

Not every Part 135 operator can actually fly international.

They have the certificate. They have the aircraft. But look closer and the gaps show up fast.

Some operators lack the avionics required for certain controlled airspaces. No CPDLC, no ADS-C. Which means no North Atlantic, no certain RVSM corridors over South America. The airplane physically cannot comply.

Some have never filed an overflight permit for the region you are traveling to. Filing for Colombian or Cuban airspace is not the same as filing a domestic IFR flight plan. There are lead times, government contacts, and approval chains that take days. An operator who has never done it before will learn on your trip.

Domestically, operator vetting is about safety record, maintenance standards, and crew qualifications. Internationally, it is all of that plus a different question: can this aircraft, with this operator, execute this specific route legally and competently?

Most clients never think to ask it.

I wrote about this in today's edition of Loud Hawk — the permit timelines, the compliance chain, and what a broker actually builds before an international departure clears.

---

**FIRST COMMENT:**

Subscribe to Loud Hawk — private aviation intelligence, every two weeks: https://loudhawk.media

---

## Phelipe

cta talking about edition 2 cta

---

## Claude

**FIRST COMMENT:**

Edition 2 is out today. Full breakdown on international permits, operator vetting, and what a broker actually builds before wheels-up: https://loudhawk.media

---

## Phelipe

Smart making an ad ta links to the news?

---

## Claude

Yes. Strongest move right now is a LinkedIn Lead Gen ad or a simple Meta ad pointing directly to the subscribe page, running for the next 48-72 hours while the edition is fresh.

The hook writes itself from today's posts. Something like:

> "Not every Part 135 operator can fly international. Most clients never ask the right questions. Loud Hawk covers what brokers actually do before an international departure clears."

Target: business owners, executives, frequent flyers, aviation adjacent professionals.

Destination: loudhawk.media subscribe page.

Budget: even $20-30/day for 3 days gets meaningful impressions in a tight audience.

Two questions before building this out: do you want LinkedIn, Meta, or both? And is the Beehiiv subscribe page the landing destination or do you want a dedicated landing page?

---

## Phelipe

Something like this

---

## Claude

Exactly the right format. Dark background, bold headline, short descriptor, single CTA button. Clean and editorial. Works perfectly for Loud Hawk.

Direct adaptation:

**Background:** Purple (#521F84)
**Category label:** Private Aviation
**Headline:** Your Plane Crossed Seven Borders. You Signed One Manifest.
**Body:** The permit timeline that determines whether your international charter actually departs. What brokers build before wheels-up. Most clients never see it.
**Logo:** Loud Hawk wordmark (white, bottom right)
**CTA button:** Read Edition 2 (orange, #FF4900)
**Destination:** loudhawk.media

This runs on Instagram and Facebook. You already have the creative infrastructure in Figma. This is essentially a Static 1 card with a CTA button overlay.

Want me to build the full ad brief for the lh-news-pill skill, or take it straight to Meta Ads Manager?

---

## Phelipe

Should go to the beehiv page or website?

---

## Claude

Website — loudhawk.media.

Reasons: it's your owned property, it has the subscribe button, it shows both editions which builds credibility, and it doesn't send people into Beehiiv's interface which feels like a backend tool, not a publication.

Beehiiv is where they land after they subscribe. The website is the front door.

---

## Phelipe

Generate the ad image

---

## Claude

The user wants me to generate an ad image similar to the Forbes ad they showed - dark purple background, bold headline, Loud Hawk branding. I should use the computer/design tools. Let me check the skills first for any relevant design skills, then create the image.

Let me create this as an HTML file that renders the ad, then screenshot it. Or I can use the frontend-design skill to create a proper ad creative.

Actually, let me read the frontend-design skill first.
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

How does that look? The logo came out white on the purple background which is correct. If you want adjustments — headline size, layout, font weight, anything — let me know.

---

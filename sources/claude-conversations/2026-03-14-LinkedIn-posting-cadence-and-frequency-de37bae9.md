---
title: LinkedIn posting cadence and frequency
created: 2026-03-14T02:16:31.918141Z
updated: 2026-03-14T05:17:09.071799Z
uuid: de37bae9-cda5-48af-b82a-279d9f7c7f38
source: claude-conversation
type: source
message_count: 10
---

# LinkedIn posting cadence and frequency

## Phelipe

Do we have a defined posting cadence or content calendar for LinkedIn? How many posts per week did we agree on? Check any strategy docs, notes, or prior conversations in this project.

---

## Claude

Let me search the project knowledge for LinkedIn posting cadence and content calendar details.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's what the docs say:

There are actually **two slightly different numbers** across the strategy documents, but they reconcile once you look at the context.

**The Execution Memo (Phase 1 operating strategy)** sets the baseline at **3 LinkedIn posts per week**. That's the number stated for the Loud Hawk Phase 1 cadence alongside the biweekly newsletter. The Wednesday content block in the Phase 2 weekly rhythm also calls for drafting "2–3 LinkedIn posts for the week."

**The 60-Day Content Calendar** operationalizes it differently — it locks in **1 LinkedIn post per week** tied to the biweekly newsletter cycle: one post on publish weeks (pulling from the edition), one standalone post on off-weeks. That's 1 post/week, not 3.

**The Beehiiv Launch Playbook** splits the difference with its guardrail: "Don't post on LinkedIn more than 2–3x per week."

So the picture is: the Execution Memo set an aspirational cadence of 3/week, the Content Calendar scaled it back to a sustainable 1/week rhythm that a solo founder can actually maintain alongside everything else, and the Launch Playbook set 2–3/week as the ceiling.

**The practical answer:** the 60-Day Content Calendar is the most recent and most operationally specific document, so **1 post per week is the locked cadence** — alternating between edition-linked posts and standalone observations. If you have capacity and something worth saying, you can go up to 2–3, but the system doesn't require it. The Content Calendar's operating rhythm table is the one to follow.

---

## Phelipe

I need to revisit our content strategy and posting cadence. The context has changed since the original docs were written.
What's changed:
- We now have a production-ready Claude Code skill for LinkedIn posts (lh-linkedin) that generates editorial-quality posts in under 2 minutes
- We have the lh-news-pill skill for Instagram static posts with built-in template selection, image sourcing, and caption writing
- Both skills have editorial judgment layers (kill switch, hold logic, quality checks) so output quality doesn't degrade with volume
- The newsletter (biweekly on Beehiiv) is live — Edition 1 launched March 12, 2026
- LinkedIn first post got 136 impressions, Instagram has 28 posts and 51 followers
- Content distribution system is locked: newsletter is source content, LinkedIn is text-driven authority, Instagram is visual news
What I need:
1. Revisit the LinkedIn cadence — the old docs said 1/week (conservative) to 3/week (aspirational). With the skill handling production, what's the optimal growth cadence? Factor in LinkedIn algorithm behavior, audience fatigue, and editorial quality standards.
2. Revisit the Instagram cadence — we have static posts dialed in with the skill. What's the right frequency for IG news posts given Loud Hawk's niche (private aviation intelligence)?
3. How do LinkedIn and IG posting schedules coordinate with the biweekly newsletter cycle? Map out a repeatable 2-week content rhythm.
4. What's the right ratio of backward-tied content (pulling from newsletter) vs. forward-testing content (standalone observations that could become future newsletter topics) vs. real-time market signals?
Constraints:
- Solo founder also flying the ERJ-175 line and building OSA
- Quality > quantity — the skills protect quality but editorial selectivity still matters
- Loud Hawk's edge is being selective and sharp, not being everywhere all the time
- Instagram reels strategy is coming but not ready yet — don't factor that in
- Newsletter is biweekly, not weekly
Give me a revised content strategy with a specific 2-week posting calendar I can repeat. Be opinionated about what the right numbers are and why.

---

## Claude

Let me pull the editorial blueprint and any other relevant strategy context before I give you a revised framework.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now I have the full picture. Let me build this out.
```
This block is not supported on your current device yet.
```

I don't need the docx skill for this — I'll deliver this as a markdown strategy doc. Let me build it.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's the revised strategy. The short version of the key decisions:

**LinkedIn: 3x/week** (Tue/Thu/Sat). The old 1/week was a production constraint that no longer exists. Three gives you algorithmic momentum without audience fatigue. The content mix is roughly 1 backward-tied (edition pull), 1–2 forward-testing (standalone observations), and 0–1 real-time signals — shifting based on whether it's a publish or off week.

**Instagram: 4x/week** (Mon/Wed/Fri/Sun). Static news pills are the backbone. The `lh-news-pill` skill makes this sustainable. Interleaving with LinkedIn means you have a daily Loud Hawk touchpoint across platforms without doubling up on any single day.

**The ratio question:** Roughly 1/3 backward-tied to the newsletter, 1/2 forward-testing (standalone observations that may become future edition material), and the rest real-time when something actually happens. The forward-testing posts are the most important growth lever — they're what reaches people who've never heard of the newsletter.

**The one thing I'd flag:** the Saturday LinkedIn slot is the most expendable. If after a few cycles it consistently underperforms Tuesday and Thursday, drop to 2/week on LinkedIn rather than publishing filler. The kill switch matters more than the number.

---

## Claude

Let me ground the platform claims in current data before building this.
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

Good — I have strong current data. Now let me build the document.
```
This block is not supported on your current device yet.
```

This is a substantial governance document — I'll build it as a professional .docx file using docx-js. Let me create the script.
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

Here's the governing document. A few things worth flagging on the platform data that backs the decisions:

**LinkedIn at 4/week** is well-supported. LinkedIn's VP of Product Gyanda Sachdeva recommended 2–5 posts per week for optimal impact, noting that members posting twice weekly see up to 5x more profile views. Buffer's analysis of 2M+ posts found that moving from 1 post/week to 2–5 produces a significant jump in both per-post reach and engagement. Multiple 2026 sources converge on 3–5 as the range for founder-led B2B accounts, with a warning that posting more than once per day can reduce per-post reach significantly due to content cannibalization. Four posts with 24-hour buffers sits in the upper band without triggering self-competition.

**Instagram at 4/week** aligns with the data. Adam Mosseri has stated that posting more generally leads to faster follower growth because more content gets discovered and shared. Buffer's IG analysis of 2M+ posts found 3–5 posts per week to be the practical sweet spot where effort and returns balance.

**The carousel push is real.** Socialinsider's 2026 benchmarks show static images declining 17% YoY in engagement, while carousels are driving the most saves and views across all brand sizes, with engagement holding steady at ~0.55%. This is why the document positions carousel production as a strategic priority once the Figma workflow is operational.

The document supersedes the old cadence docs. One note: I updated LinkedIn from 3/week (from the earlier revision we did) to 4/week per your brief, with Saturday as the explicit experimental slot with a clear decision gate at 8 weeks.

---

## Phelipe

I need 6 edits to the Content Strategy & Distribution Architecture v1.0 doc. Apply all of them and produce an updated v1.1.
1. FIX THE MONDAY OVERLAP: The doc says the schedule creates daily touchpoints "without doubling up" but both LinkedIn and Instagram post on Monday. Either move one Monday post to another day, or change the language to: "This schedule creates daily cross-platform presence, with limited same-day overlap only where strategically useful."
2. SOFTEN PLATFORM CLAIMS: Any very specific algorithm claims (like exact percentage improvements, specific multipliers like "3-5x", or claims about reach penalties) should be softened to "benchmarks suggest," "practitioner analyses indicate," "current data points toward," or "reported by [source]." This is a governing doc, not a blog post. If you can't source it precisely, frame it as directional evidence.
3. TARGET CADENCE VS HARD CADENCE: Reframe the cadence section. LinkedIn should be "target cadence 4/week, publish floor 3/week if kill switch overrides." Instagram should be "target cadence 4/week, publish floor 3/week if pipeline quality slips." This aligns the cadence with the editorial judgment system.
4. ADD LANE GLOSSARY: Add a short glossary section (can be an appendix or inline) defining:
- TG = The Gap (industry marketing vs. operational reality)
- MS = Market Signal (pricing, demand, fleet trends, seasonal patterns)
- HIAW = How It Actually Works (mechanics, process, operational reality)
- SA = Situational Awareness (FAA action, incident, regulatory change, external events)
5. REMOVE FROZEN BENCHMARKS: Remove any specific current-state numbers like "136 impressions on post 1" or "51 followers" from the governance doc. These belong in a live KPI tracker, not doctrine. Keep the measurement framework and interpretation logic but remove the snapshot data.
6. NARROW SUPERSESSION SCOPE: Change the opening supersession language to: "Supersedes prior Loud Hawk and OSA content cadence guidance only. Broader OSA strategic and operating documents remain in force unless separately updated."
Produce the updated doc as v1.1. Keep all existing content that isn't affected by these edits. Format the same way as v1.0.

---

## Claude

```
This block is not supported on your current device yet.
```

I'll apply all 6 edits and rebuild the document. Let me work through the full script with the changes incorporated.
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

All 6 edits applied. Here's what changed:

**1. Monday overlap fixed.** LinkedIn posting days shifted to Tuesday/Wednesday/Thursday/Saturday. Instagram stays Monday/Wednesday/Friday/Sunday. Wednesday is now the single intentional overlap day — both platforms post but in different formats to different audiences. The language now reads "daily cross-platform presence, with limited same-day overlap only where strategically useful."

**2. Platform claims softened.** Replaced hard multipliers and exact penalty percentages with "practitioner analyses indicate," "benchmarks suggest," "current data points toward," and explicit source attribution (Socialinsider, Buffer, Sachdeva). The opening of the evidence base section now includes a disclaimer that platform algorithms change frequently and these are directional inputs.

**3. Target vs. hard cadence.** The cadence table now has separate "Target Cadence" and "Publish Floor" columns. LinkedIn is 4/week target, 3/week floor if the kill switch overrides. Instagram is 4/week target, 3/week floor if pipeline quality slips. Added a paragraph explaining the distinction and how it connects to the editorial judgment system.

**4. Lane glossary added.** Appendix A defines all four lane codes (TG, MS, HIAW, SA) with full definitions pulled from the Editorial Blueprint. The lane distribution table in Section 5 now cross-references the appendix.

**5. Frozen benchmarks removed.** Stripped "136 impressions on post 1," "51 followers," and all snapshot-specific numbers from the measurement section. Kept the interpretation framework ("look for steady week-over-week climb") and added a note that current-state metrics belong in a live KPI tracker, not doctrine.

**6. Supersession scope narrowed.** Title page and body now read: "Supersedes prior Loud Hawk and OSA content cadence guidance only. Broader OSA strategic and operating documents remain in force unless separately updated."

---

## Phelipe

4 final edits to produce v1.2. This is the lock version.
1. FIX PHASE 1 WORDING IN DECISION GATES: Remove the literal citation of the old Execution Memo Phase 1 rule about not extending to other platforms. Replace with: "In this updated content phase, do not expand beyond LinkedIn, Instagram, and the newsletter until the current system proves itself through at least 4 full cycles of consistent execution and measurable traction."
2. ADD EVIDENCE SOURCES APPENDIX: Add an Appendix B called "Evidence Sources" that lists the key external references behind the platform claims in the doc. Include:
- Buffer 2025-2026 analysis of 2M+ LinkedIn posts (posting frequency and reach)
- Buffer 2025-2026 analysis of 2M+ Instagram posts (posting frequency and growth)
- Socialinsider 2026 Instagram Organic Engagement Benchmarks (35M posts analyzed — carousel vs static vs reels performance)
- LinkedIn official marketing blog guidance on posting timing and content quality
- Instagram head Adam Mosseri's public recommendations on posting frequency
- beehiiv State of Newsletters 2026 (cadence and curation findings)
Format as a simple reference list, not full academic citations. This makes the doc auditable.
3. NARROW GOVERNANCE SCOPE: In the front matter where it says this governs "all Loud Hawk and OSA content operations," add a clarifying sentence: "This document primarily governs the Loud Hawk-led editorial and distribution system. OSA Connect and OSA Aircraft content operations are addressed here in terms of their brand roles within the ecosystem funnel. Standalone content operating manuals for those sub-brands may be developed separately as needed."
4. ADD CHANNEL HIERARCHY: Add a short section (can be right after the cadence section or as part of the Platform Context) with one clear statement:
"Channel hierarchy for this phase:
- LinkedIn = primary authority and professional discovery channel
- Instagram = visual reach, memory, and intelligence packaging channel
- Newsletter = depth, trust, and subscriber relationship channel
- Stories/DMs/Comments = daily lightweight distribution and relationship layer"
Produce as v1.2. Keep everything else from v1.1 intact.

---

## Claude

```
This block is not supported on your current device yet.
```

I'll rebuild the full script with the 4 edits applied precisely.
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

v1.2 is locked. Here's what changed from v1.1:

**1. Phase 1 wording fixed.** The "Do not add new platforms" constraint in Decision Gates no longer cites the Execution Memo Phase 1 rule verbatim. It now reads: "In this updated content phase, do not expand beyond LinkedIn, Instagram, and the newsletter until the current system proves itself through at least 4 full cycles of consistent execution and measurable traction." Stands on its own logic, not a dependency on an older doc's phrasing.

**2. Appendix B: Evidence Sources added.** Seven numbered entries covering Buffer (LinkedIn and Instagram analyses), Socialinsider 2026 benchmarks, LinkedIn official guidance via Sachdeva, Mosseri's public statements, beehiiv State of Newsletters 2026, and the practitioner analysis sources. Each entry identifies the source, approximate date, what it covers, and where relevant, the sample size. The practitioner sources are explicitly framed as directional signals, not peer-reviewed findings. The appendix opens with a note to re-verify before treating any specific claim as current.

**3. Governance scope narrowed.** The front matter now includes: "This document primarily governs the Loud Hawk-led editorial and distribution system. OSA Connect and OSA Aircraft content operations are addressed here in terms of their brand roles within the ecosystem funnel. Standalone content operating manuals for those sub-brands may be developed separately as needed."

**4. Channel hierarchy added.** New section right after the cadence table, before posting days. Four-tier hierarchy: LinkedIn (primary authority and professional discovery), Instagram (visual reach and intelligence packaging), Newsletter (depth, trust, subscriber relationship), Stories/DMs/Comments (daily lightweight distribution). Includes a practical note on how to prioritize when time is constrained in a given week.

---

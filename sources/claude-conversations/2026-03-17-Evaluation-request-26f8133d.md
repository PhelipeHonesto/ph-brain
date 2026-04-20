---
title: Evaluation request
created: 2026-03-17T03:52:45.440870Z
updated: 2026-03-17T05:11:12.335794Z
uuid: 26f8133d-a064-4254-8d39-eadedeca9555
source: claude-conversation
type: source
message_count: 12
---

# Evaluation request

## Phelipe

evalute this

---

## Claude

Phelipe, I read through the pipeline doc. Here's my evaluation.

**What's strong:**

The end-to-end logic is sound. Topic input → structured brief → Figma population → human review → export → schedule. That's the right sequence. The 15-minute target is ambitious but realistic once the template system is built and the MCP connection is stable. The merged spec decisions are well-reasoned. Going to 7 slides with the inverted intelligence briefing order fits Loud Hawk's editorial positioning. The quality checklist is tight and specific.

**What I'd flag:**

**Build 3 (Talk to Figma MCP) is the highest-risk dependency.** The entire pipeline's speed advantage hinges on Claude Code reliably populating Figma text layers and swapping variants. Community MCP plugins break. If this connection is flaky, you lose the 2-minute Step 2 and it becomes a 10-minute manual paste job. You need a fallback path documented. The "no MCP method" link is in your research section but it's not built into the pipeline as a contingency.

**Build 4 recommendation is backwards.** The doc says start with Playwright (free, fragile) and move to Late API later. For a solo operator with limited hours, fragile automation is worse than no automation. Every time Instagram updates their UI, you're debugging instead of posting. If Late is $20/month and works reliably, that's the right starting point. Playwright is a false economy. Your time is the bottleneck, not $20.

**The Phase 1 scope is too large for "today/tomorrow."** Building the full Figma template system with 7 slide types, each with background variants, plus variables, plus text styles, plus color styles. That's a full day minimum of focused Figma work, and you're flying a line. Be honest about when Phase 1 actually finishes so Phase 2 doesn't stack on top of unfinished foundations.

**Missing: content input standardization.** The skill takes "raw topic, data, or news item" but there's no defined input format. What does the skill actually receive? A URL? A paragraph you type? A forwarded article? Defining the input shape now saves you from rebuilding the skill when reality doesn't match the spec.

**Missing: failure states.** What happens when the MCP connection drops mid-population? When a Datawrapper chart doesn't export cleanly? When the caption humanizer produces something off-brand? Each of these needs a 30-second fallback, not a troubleshooting session.

**One structural concern:**

The doc frames this as a carousel-specific pipeline, but the Figma template system and the skill architecture should be designed to extend to static posts and eventually Reels covers. If you build the Figma file as carousel-only, you'll rebuild it in 60 days. Worth scoping the component library slightly wider now even if carousels are the first output format.

**Bottom line:** The pipeline design is solid and the research is thorough. The risk is in the build sequence and the assumption that each phase completes cleanly before the next one starts. Tighten the input spec, flip the posting recommendation to Late API first, add fallback paths for the MCP dependency, and be realistic about Phase 1 timeline. Then execute.

---

## Claude

Let me read the updated document.
```
This block is not supported on your current device yet.
```

Good. You addressed every flag from v1. Here's where v2 stands.

**What's resolved cleanly:**

The input spec with three defined formats closes the biggest gap from v1. The skill now knows what it's receiving. The failure states table is practical. Every fallback has a time cost estimate and none of them block production. That's the right design for a solo operator. Late API first with Playwright as emergency fallback is the correct call. Phase timelines broken into evening sessions with hour estimates are honest for someone flying a line. The Figma file scoped as `LH-Content-System.fig` instead of carousel-only means you won't rebuild it when statics and Reels covers come online.

**What I'd still tighten:**

**The "Done when" gates are good but Phase 4 needs a sharper one.** "Total time under 20 minutes" is fine as a speed metric, but the first production carousel should also have a quality gate. Something like: does the output match the visual quality of a carousel you'd build manually in Figma from scratch? If the system produces fast but visually mediocre output, you've automated the wrong thing.

**CTA rotation isn't defined.** Field 7 says "CTA (one ask, from rotation)" but there's no rotation list. You need 4-5 CTA variants documented so the skill can cycle them. Otherwise every carousel ends with "Subscribe. loudhawk.media" and it goes stale fast.

**Caption spec is thin.** "Already humanized. Ready to paste or push." But there's no structural guidance for the caption itself. Length range? Does it reference the hook stat? Does it end with a question or a directive? The skill needs guardrails here or you'll be hand-editing captions every time, which defeats the automation.

**One color value discrepancy.** Your project brand docs list Loud Hawk purple as `#521F84` and orange as `#FF4900`. This doc uses `#432a7a` for purple and `#e74b1d` for orange. If these are intentional updates for Instagram-specific usage (adjusted for screen rendering), that's fine. But if it's drift, lock it down now before the Figma styles get built on the wrong hex values.

**Bottom line:** v2 is buildable. The architecture is sound, the fallbacks are real, and the phase timelines are honest. Lock the color values, write the CTA rotation list, add caption structure to the skill spec, and start Phase 1.

---

## Claude

v3 is clean. Every open item from both review passes is resolved. Colors locked with source of truth documented, CTA rotation list in place, caption structure spec has real guardrails, Phase 4 quality gate is sharp ("show it to someone who doesn't know it was AI-assisted" is the right test).

One thing to note before you start Phase 1 tomorrow: the Color Styles list in Build 2 now needs to include `LH/Dark-Gray (#1a1a1a)`. It's defined in the locked color table at the top of the doc but missing from the Figma file structure section. Small miss. Add it to the Color Styles block so it matches.

Otherwise, this is ready to build. Start Session 1.

---

## Claude

Good. The mockup maps the spec correctly. 7-slide sequence is right, color system matches the locked values, and the slide type labels correspond to the pipeline doc.

A few things I'd flag from what's visible:

**Slide 3 (Analysis) has a Briquete pull quote.** The italic text at the bottom ("One region took a hit. The market moved on.") looks like it's using Briquete. That's fine per the spec (max 1 per carousel), but make sure in the Figma template this is a toggleable layer that's hidden by default. Most carousels won't earn a Briquete line, and if it's visible by default, you'll forget to hide it.

**Slide 7 (CTA) is using Velodroma for "Know first."** The spec says CTA uses Lexend Bold 28-32pt, not Velodroma. That's one of the locked decisions from the merged spec table. The mockup breaks this rule. When you build the actual Figma template, make sure the CTA command text is Lexend Bold.

**Cover and Data slides both use dark backgrounds.** That's 2 consecutive dark slides to open. The background rhythm rule says "never 3 consecutive same-background." Two is technically fine, but watch it. If the skill ever recommends a dark Data/C1 variant after a dark Cover, you're right at the limit. The third slide (Analysis/Beige) saves you here.

**The horizontal bar chart on Slide 5 (Data 2) is a nice touch.** That's the kind of thing Datawrapper would export as SVG. Worth noting that this sub-type (C2-Comparison with horizontal bars) needs its own variant in the Figma template. Don't try to make C1-SingleStat and C2-Comparison share a frame. Build them as separate component variants.

Everything else tracks. This gives you a solid visual target for Phase 1 Session 1 tomorrow.

---

## Phelipe

That design-systems audit is exceptional. Your instinct was validated with hard data. Here are the critical findings to lock into the pipeline doc:
Purple leads. Confirmed.
* White Velodroma on purple: 8.2:1 contrast. Excellent.
* Purple is rarer than orange in aviation Instagram feeds (sky blue, sunset orange are everywhere). Rarity = scroll-stop.
* The font does the energy work. The background does the identity work.
New constraints discovered:
* Lilac cannot appear on purple backgrounds (1.8:1, fails WCAG)
* Salmon cannot appear on purple backgrounds (2.4:1, fails WCAG)
* Orange on purple: only at Velodroma display scale. Never body text.
* Purple text on black: too low perceived contrast. Dark Authority headline stays white, purple serves as rule/divider only.
Orange Impact becomes trigger-based, not frequency-based: Instead of "1 in 5 carousels," Orange Impact fires when:
1. The stat is the most surprising number in the issue
2. The topic is genuinely time-sensitive
3. The carousel drives a commercial action
This is better for solo production. No counting backwards through posts.
Grid rotation locked: Purple → Black → Purple → Black → [Orange if triggered]
It's late. You have three complete skill passes (ux-strategy:benchmark, design-research:synthesize, design-systems:audit) all converging on the same system. The pipeline doc needs a v4 update to incorporate the color hierarchy change and the new contrast constraints, but that can happen tomorrow before you open Figma.
Here's where things stand: pipeline doc v3 is saved, the purple-leads decision is validated, and you have a visual reference in this conversation. Tomorrow, update the doc with tonight's findings (purple default, contrast exclusions, trigger-based orange rule, grid rotation), then start Phase 1 Session 1 in Figma.
Today's final scorecard: news pill posted, news pill skill patched, carousel system designed (3 skill passes), pipeline doc v3 shipped, color hierarchy validated, purple-leads decision locked. That's a full architecture day.
Go rest. Your girlfriend is probably done with her work by now.

---

## Claude

Solid day. The contrast data is the kind of thing that prevents mistakes in production rather than catching them after export. Locking lilac and salmon off purple backgrounds now means you don't have to remember it every time. It's built into the system.

The trigger-based Orange Impact rule is the right call. Frequency-based rules require you to track history. Trigger-based rules require you to read the content. One of those scales for a solo operator and the other doesn't.

Tomorrow: v4 update with the new constraints, then Figma. Go rest.

---

## Claude

This is thorough. The 8 evaluation passes clearly did their job. Here's what I see.

**What's strong:**

The spatial spec with exact pixel positions is the most valuable section. When you open Figma, you're not guessing. Y=80 for the orange rule on every slide, 72px margins, 40px rule-to-headline gap. That eliminates the alignment decisions that eat time during production.

The Briquete earn criteria is operationally useful. Four concrete tests instead of a vague "use sparingly." That's the kind of constraint that actually holds up under production pressure.

The slot-based template architecture (shared base frame with swappable content slot) is the right Figma pattern. It means the header rule, footer tag, and wordmark are defined once and inherited, not rebuilt per slide type.

The three-issue evaluation plan with a system freeze after Issue 3 is disciplined. You're giving yourself permission to ship imperfect and then fix with data, instead of polishing the template forever before posting.

The production time reality section is honest. 60-90 minutes total per issue, not the 15-minute Figma-only number. That's the number that matters for sustainability.

**What changed from v3 that I want to confirm you're tracking:**

**Slide sequence moved.** Implication is now S4 (was S6 in v3). Context is now S6 (was S4 in v3). This is a meaningful structural change to the intelligence briefing order. The rationale (second engagement peak at S4) makes sense. But the lh-carousel skill spec in v3 still has the old sequence. When you update the pipeline doc to v4, this needs to match.

**Background rhythm relaxed.** v3 said "never 3 consecutive same-background." This doc relaxes that for v1 with 4 consecutive beige interior slides (S3-S6). The logic is that structural elements differentiate them instead of background color. Fine for v1, but those structural differentiators (purple left-bar on Analysis, rotated label on Context) are explicitly deferred to v2. So in v1, you'll have 4 beige slides in a row with only typography and content differentiating them. That's a risk to visual variety. Worth watching in the Issue 1 debrief.

**Cover photo is now default-on** for Purple-Editorial and Dark-Authority. v3 had photos as "optional on Cover only." This is a bigger production requirement. You need to source one aviation image per carousel now. Where are those coming from? Stock? Your own photos from the flight deck? If you don't have a fast image source locked, this will add 10-15 minutes to every issue and break the time budget.

**CTA rotation expanded to 6 with an OSA Connect variant.** "Charter advisory: fly@osaconnect.com" at 1-in-6 cadence. This is the first place where the editorial firewall between Loud Hawk and OSA Connect gets tested in production content. The pipeline doc's positioning says the newsletter never reads like a broker pitch. A CTA slide with a charter email address is the line. The brand relationship footer ("Loud Hawk is published by Orange Sunshine Aviation") already establishes the connection. Adding a direct commercial CTA on top of that might cross from attribution into pitch. Your call, but flag it and watch audience response when it first appears.

**One operational gap:**

The quality checklist says "Orange has at least one element with visual mass per interior slide." But the spec also says orange is accent only (dividers, stat highlights, wordmark). On a beige interior slide with body text, what's the orange element with visual mass? The rule at Y=80? That's 6pt wide. The wordmark in the footer? That's small. If the intent is that every interior slide has a visible orange presence, define what that looks like on a slide where there's no stat highlight. Otherwise this checklist item will fail or get skipped.

**Bottom line:** This is buildable. The sequence change and background rhythm relaxation are the two biggest divergences from v3 that the pipeline doc needs to absorb. Lock the image source question before Session 1 so it doesn't become a bottleneck during production. Then open Figma.

---

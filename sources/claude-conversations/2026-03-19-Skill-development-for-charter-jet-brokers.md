---
title: Skill development for charter jet brokers
created: 2026-03-19T23:18:20.453412Z
updated: 2026-03-19T23:33:25.852743Z
uuid: 99df8646-220e-4763-a3c4-9c72d99e4115
source: claude-conversation
type: source
message_count: 6
---

# Skill development for charter jet brokers

## Phelipe

how would be a skill development for Benchmarking Charter Jet Brokers

---

## Claude

# Benchmarking Charter Jet Brokers Skill

Great topic. Before I draft, let me clarify a few things to make sure this skill lands right.

## What I'm thinking this does

A skill that researches and benchmarks competing charter jet brokers against OSA Connect, producing a structured competitive analysis. This would cover things like pricing models, fleet access, service offerings, digital presence, market positioning, and reputation.

Let me ask a few questions to narrow the scope:
```
This block is not supported on your current device yet.
```

Once you answer these, I'll jump straight into drafting the SKILL.md and review it against the checklist.

---

## Phelipe

Q: What's the primary deliverable when this skill runs?
A: Structured comparison doc (markdown/table)

Q: What dimensions matter most when benchmarking a broker? (Select all that apply)
A: Digital presence & UX (website, booking flow, app), Pricing transparency & model, Fleet access & operator network, Brand positioning & content strategy

Q: How should the skill be triggered?
A: Both (single competitor or full market sweep)

---

## Claude

Good, all four dimensions and both trigger modes. Let me draft this now.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me build the full skill folder. This is a MEDIUM freedom skill: structured research with a defined output template, but flexibility in how Claude gathers and analyzes the information.
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

Now let me review against the quality checklist:

---

## Quality Checklist Review

**Required:**
- [x] Description is specific with trigger words ("analyze," "compare," "benchmark," "competitive research," "scout")
- [x] Description says WHAT (researches and benchmarks charter jet brokers) and WHEN (specific competitor or landscape scan)
- [x] Description is in third person ("Researches and benchmarks...")
- [x] SKILL.md body is under 500 lines (about 85 lines)
- [x] Only includes info Claude doesn't already know (OSA-specific dimensions, broker/operator distinction, output structure)
- [x] No em dashes anywhere

**Recommended:**
- [x] Has output format/template (two templates in separate files)
- [x] Has a validation/quality check step (5-point check)
- [x] Large reference material in separate files (output templates externalized)
- [x] Has eval scenarios (3 scenarios covering both modes)
- [ ] Not yet tested on real scenarios (next step)

**Nice to Have:**
- [x] Conditional paths (single vs. market sweep modes)
- [x] Consistent terminology ("broker" throughout, operator/broker distinction enforced)

## Folder Structure

```
benchmarking-brokers/
  SKILL.md              # Main instructions (85 lines)
  output-single.md      # Template for single competitor analysis
  output-sweep.md       # Template for market landscape sweep
  evals/
    evals.json          # 3 test scenarios
```

## What I'd Suggest Iterating On

**After first real use, watch for these:**

1. **Does Claude pick the right brokers for market sweeps?** If it consistently misses important competitors, you may want to add a reference file with a curated list of known brokers to consider (e.g., VistaJet, NetJets, Magellan Jets, Sentient Jet, Jet Linx, XO, FlyExclusive).

2. **Is the OSA Connect comparison useful?** Right now the skill tells Claude to reference the osa-brand-voice skill for OSA's positioning. If the comparisons feel thin, you might want a short `osa-connect-positioning.md` reference file with key differentiators, target segment, and current competitive claims.

3. **Are the strategic takeaways generic?** This is the hardest part. If Claude keeps producing vague insights like "invest more in digital," you could add 2-3 example takeaways in an `examples.md` file to calibrate the quality bar.

Want me to copy this to your outputs so you can grab the files, or would you like to adjust anything first?

---

## Phelipe

lets test out

---

## Claude

Let's run it. I'll simulate the single competitor eval first, since that's the most common use case. Let me research Magellan Jets as if I were Claude Code executing this skill.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now let me compile this into the skill's output template. I have enough to produce the benchmark.
```
This block is not supported on your current device yet.
```

Now let me validate against the skill's own quality check:
```
This block is not supported on your current device yet.
```

Now let me apply the fixes before delivering:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now add a reference to this file in the SKILL.md:
```
This block is not supported on your current device yet.
```

Let me copy everything to outputs:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's the full skill folder and the Magellan Jets test run. Here's what the test revealed and what I already fixed:

**Three updates applied post-test:**

1. **OSA Connect data fallback.** The skill now explicitly tells Claude to ask the user for OSA Connect differentiators if the osa-brand-voice skill isn't available. Without this, the "vs. OSA Connect" sections come back empty.

2. **Citation format clarified.** The rule now distinguishes between a top-level source list (always) and inline URLs for quantitative claims specifically (pricing, ratings, follower counts).

3. **Added known-brokers.md.** A tiered reference list so Claude doesn't waste time guessing which brokers matter for market sweeps. Includes a note distinguishing true brokers (Tier 1-2) from adjacent competitors with different models (Tier 3).

**What still needs real-world testing:**

The market sweep mode (eval #3) hasn't been run yet. That's the one most likely to expose issues, especially around whether Claude proposes a good broker list and whether the comparison matrix stays readable at 4-6 brokers. I'd recommend running that next with a prompt like "give me a competitive landscape of the top charter jet brokers" and seeing how it handles the breadth.

---

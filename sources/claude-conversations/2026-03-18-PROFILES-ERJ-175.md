---
title: PROFILES ERJ-175
created: 2026-03-18T21:49:42.992344Z
updated: 2026-03-18T22:42:43.548701Z
uuid: b2f8ddcd-0671-4461-8ca9-ac6807ef6872
source: claude-conversation
type: source
message_count: 14
---

# PROFILES ERJ-175

## Phelipe

"Read the profiles and callouts from the SOPM. Build me a visual Profiles Quick Reference. Each profile should show the full sequence top to bottom: configuration changes, speeds, callouts, power settings, and key altitude triggers. Cover these profiles: ILS CAT I, ILS CAT II, RNAV (GPS), RNAV (RNP), Localizer Approach, Single Engine Approach, Single Engine Missed Approach. Make it interactive so I can tap each profile to expand it. Design it like a cockpit knee-board reference I can chair fly with on my iPad."

---

## Claude

Let me pull the profiles and callouts from your SOPM first.
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

Let me go directly to the SOPM PDF to find the profiles sections.
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

Now let me extract the actual profile content sections.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I wasn't able to fully extract all the text from the SOPM before the tool limit was reached. Here's what I **did** get from the approach chapter (04-12), and I can continue pulling the rest in a follow-up.

---

## Phelipe

Continue

---

## Claude

Let me keep pulling the profile sections from the SOPM.
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

Now I have all the profile data I need. Let me also quickly check the initial approach and descent sections for configuration speed references.
```
This block is not supported on your current device yet.
```

Now let me read the descent/initial approach section for configuration sequence.
```
This block is not supported on your current device yet.
```

Now I have everything I need. Let me build the interactive reference.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Built straight from SOPM Chapter 04-12 (Rev 11, 11 DEC 23). Here's what's in there:

**7 profiles** -- ILS CAT I, ILS CAT II, RNAV (GPS)/LPV, RNAV (RNP AR), Localizer Only, Single Engine Approach, Single Engine Missed Approach. Tap any card to expand the full sequence top to bottom.

Each expanded profile shows: minima setting, nav setup, lateral/vertical modes, speed formula, and a step-by-step timeline from initial setup through the decision point with every callout in sequence.

Two quick-access panels at the top for **Stabilized Approach Criteria** (1,500/1,000/500 HAT gates with all PM deviation callouts) and the **GA Flap Table** (5->2, FULL->4).

A couple things worth noting from the SOPM that trip people up:

- **LOC Only**: arm NAV, not APP (APP arms GS). Derived minimum is MDA rounded up to 100 ft. If you see the runway, clear the FD *before* setting missed approach altitude or you'll get a FLCH climb to the altitude with TOGA thrust.
- **RNP AR with RF in FAS**: 165 kt max, FLAPS 5 mandatory, Cat D mins. Use the Discontinue procedure, not standard GA, if you need to bail before DA.
- **CAT II**: APPR 1 ONLY below 800 RA is a mandatory missed. No "APPROACH LIGHTS, CONTINUE" callout. Crosswind limit 12 kt.

Let me know if you want me to add the Circling profile, tweak any formatting for your iPad, or start quizzing you off these.

---

## Phelipe

"Now build me a visual profile diagram for each approach. Show the side-view vertical path from IAF to the runway like a descent profile picture. Mark on the diagram: altitude gates (1500 HAT, 1000 HAT, 500 HAT), configuration points (flap settings, gear), speed targets at each segment, FMA mode changes, and callout locations. Think of it like the profile view diagrams you see in training manuals. Start with ILS CAT I as the first one. Make it clean and readable on an iPad."

---

## Claude

Let me load the visualizer design guidelines first.
```
This block is not supported on your current device yet.
```

That's a lot of guidance. For this profile diagram, I need a clean side-view descent path. Let me build this as an interactive HTML widget with inline SVG since it needs to show a detailed flight path with multiple annotation layers.
```
This block is not supported on your current device yet.
```

There's your ILS CAT I profile view. Reading left to right, top to bottom on the glideslope:

**What it shows at each point along the path:**
- FMA modes across the top (VNAV descent -> Arm APP before FAF -> LOC/GS captured)
- Configuration boxes below the path (gear/flaps 3 by 1,500 HAT, landing flaps by 1,000 HAT)
- Altitude gates on the right margin (1,500 / 1,000 / 500 / DA) with the gate requirements
- Callouts on the right side of the path at their trigger altitudes ("ONE THOUSAND, STABILIZED, CLEARED TO LAND" at 1,000, "APPROACHING MINIMUMS" at 80 above DA, "MINIMUMS" at DA)
- Speed reference box on the left (VAP formula, min VREF+5, max VREF+20)
- Stabilized criteria summary box at lower left
- The decision fork at DA: land (if visual) or missed approach (TOGA, GA flaps, positive rate, gear up)

Want me to do RNAV (GPS)/LPV next, or would you rather I adjust the layout on this one first? The LOC Only profile would be a good one to contrast since the FMA modes and the procedure at minimums are completely different (NAV not APP, wait for ALT active, clear FD before setting missed approach altitude).

---

## Phelipe

looks good. just make sure is not to crumbled the words so we can read clearly

---

## Claude

Good call. Let me space it out more, bigger text, fewer boxes competing for the same space. I'll keep all the same information but give everything more room to breathe.
```
This block is not supported on your current device yet.
```

Much more readable now. Everything has room to breathe: bigger text, wider boxes, more spacing between annotations so nothing is fighting for the same real estate.

Want me to build the next profile? I'd suggest RNAV (GPS)/LPV next since it's your most common non-precision with vertical guidance, then LOC Only since the FMA flow and the procedure at minimums are where people trip up the most.

---

## Phelipe

still crumble on some area can you see that. anyway we can have more room to breath so is smooth

---

## Claude

Yeah I see it. The problem is I'm trying to pack too much into one view and the boxes overlap. Let me take a completely different approach: wider canvas, fewer annotation boxes, and use clean horizontal bands instead of boxes competing for space. Every label gets its own clear lane.
```
This block is not supported on your current device yet.
```

Big difference. Here's what changed:

**Layout is now in horizontal lanes** instead of everything fighting for space around the glideslope. FMA modes across the top, the profile view in the middle, config boxes in their own row below the ground line, and callouts in a clean stack at the bottom. Nothing overlaps.

The canvas is wider (scrollable on iPad) so you can pan across the full approach from initial descent to the runway. Every label is 14-16px now, no tiny text anywhere.

Want me to keep this same lane layout for the remaining profiles? I can knock out RNAV (GPS)/LPV next.

---

## Phelipe

better but you can create a little more space. lets make very readable. is getting there.

---

## Claude

Let me push the spacing even further. More padding inside every box, more vertical gap between lanes, and bump the font sizes up one more notch.
```
This block is not supported on your current device yet.
```

That should be a lot cleaner. Everything has real padding now: bigger font sizes (16-18px for content, 17px for headers), wider boxes with more internal space, and each lane (FMA, profile view, config, callouts, stabilized criteria) has generous vertical separation so nothing crowds its neighbor.

The whole thing scrolls horizontally on iPad so you get the full approach path without squishing. Ready for RNAV (GPS)/LPV next?

---

## Phelipe

now do for all profiles and add to our profiles quick reference tool

---

## Claude

Let me build all the profile diagrams and integrate them into the expandable reference. I'll use the same spacious layout for each profile.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now I'll rebuild the entire file with profile diagrams integrated into each expandable card. This is a big file so I'll create it fresh.
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

All seven profiles now have diagrams built in. Here's what you get:

**Each profile card** expands to show the text reference (minima, nav setup, modes, speeds, step-by-step callouts, go-around) plus a **"Show Profile Diagram"** button that opens the full side-view descent profile with the spacious layout we dialed in.

**Profiles with diagrams:**

1. **ILS CAT I** -- VNAV -> Arm APP -> LOC/GS. Standard gates, standard callouts.
2. **ILS CAT II** -- Adds 800 RA and 500 RA mandatory missed triggers, APPR 2 requirement, no "APPROACH LIGHTS, CONTINUE" callout.
3. **RNAV (GPS) / LPV** -- LNAV/VGP path. APPR annunciator required 2 NM before FAF. DGRAD = discontinue.
4. **RNAV (RNP AR)** -- RF vs non-RF FAS split. 165 kt limit. Altimeter crosscheck at FAF. Maintain centerline even in VMC.
5. **Localizer Only** -- NAV not APP. VNAV PTH to derived min. The LOC procedure at minimums (clear FD before setting MA alt) is called out in both the diagram and the caution text.
6. **Single Engine Approach** -- FLAPS 5 mandatory, VREF FULL + 20, same callouts as AEO.
7. **Single Engine Missed Approach** -- Climb profile (reversed path), slow rotation, neutral aileron, GA RSV -> CONT thrust at VFS.

All diagrams scroll horizontally on iPad with the same spacious layout. Want me to quiz you off any of these?

---

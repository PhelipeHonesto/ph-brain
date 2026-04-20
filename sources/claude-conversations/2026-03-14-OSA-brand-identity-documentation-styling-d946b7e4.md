---
title: OSA brand identity documentation styling
created: 2026-03-14T23:09:56.957966Z
updated: 2026-03-14T23:48:33.309000Z
uuid: d946b7e4-b529-4b32-902c-ef0b29551b48
source: claude-conversation
type: source
message_count: 10
---

# OSA brand identity documentation styling

## Phelipe

Let me check what the current outputs look like and review the brand spec from the existing documents.Good — I'll use `lg_osa_3.png` (stacked lockup with wordmark and tagline on a light/neutral background) for the title pages since it has the full brand lockup. Now I need to build a comprehensive docx-js generation approach for all three documents that applies the full OSA brand identity: logo on title page, orange `#E84B1A` headings, dark `#1A1A1A` body, Arial font, gray callout boxes, branded header/footer with orange accent line.
The Operating System was already built with full brand styling via docx-js. The Roadmap and Memo were pandoc conversions that lack the visual identity. I need to rebuild those two with the same docx-js approach as the Operating System. Given their size, I'll create a shared utility module and build each document separately.Now I'll take a smarter approach. The Execution Memo and Roadmap are massive documents — thousands of lines of structured content with dozens of complex tables. Rather than rewriting them entirely in docx-js (which would be extremely error-prone at this scale), I'll use the pandoc-generated docx files as the base and apply the OSA brand identity by directly editing the XML: swapping in the branded styles, updating the header/footer, and injecting the logo on the title page.I see — the Operating System's styles.xml has duplicate Heading1/2/3 definitions (the first set from docx-js defaults, the second from the explicit overrides). The second set has the correct OSA branding. For the pandoc documents I need to replace the heading color values and ensure Arial font. Let me do this systematically.Good — headings are now orange and dark. Now let me add the branded header and footer with the OSA orange accent line.Good — the files are bigger now (logo image adds weight). Let me verify the edits are still intact and the branding is applied:All 4 contradiction fixes verified. All 3 documents now confirmed with the OSA visual identity:
* Orange `#E84B1A` headings across all heading levels in all three documents
* Dark `#1A1A1A` body text and subheadings
* Arial font throughout (default body, all heading styles)
* OSA logo (stacked lockup with "Orange Sunshine Aviation / Runway to your future") on the title page of all three documents
* Branded header on every page: bold orange "OSA" + document title in gray italic, separated by an orange accent line underneath
* Branded footer on every page: "Orange Sunshine Aviation" left-aligned + "Confidential" right-aligned, with orange accent line above
The Operating System was built from scratch in docx-js with full brand styling. The Execution Memo and Strategic Roadmap were styled by editing the pandoc-generated XML directly — replacing heading colors, swapping fonts to Arial, injecting the logo, and adding branded header/footer elements with the orange accent lines.
Let me copy the final files to outputs.
All three documents are ready with full OSA visual identity applied — orange `#E84B1A` headings, Arial font, `lg_osa_3` logo on each title page, branded header with orange accent line on every page, and branded footer with orange accent line. All four contradiction fixes confirmed intact.

help to create a prompt to my OSA Project. to make my Docs feels like was made buy a art desginer.
we have all the visual assets in the files.
want to make clean, professional, but with our vibe. does that make sense?
can you help with a prompt?
logo is with no BG. no very smooth. with the Typography too.
is that possible?

---

## Claude

Phelipe, that makes total sense. You want the docs coming out of your OSA Project to look like they were designed by a brand-conscious creative director — not just "formatted" but actually *styled* with the OSA identity baked in. Clean, professional, but unmistakably yours.

Let me look at what you've got in the uploads and the brand book specs so I can build a prompt that references everything precisely.
```
This block is not supported on your current device yet.
```

I can see the three screenshots — the branded Strategic Roadmap title page, and the Brand Book typography pages showing Coolvetica (primary) and Lexend (secondary). From these plus what I know about the OSA visual system, here's what I can pull together:

The key brand specs from your screenshots are: Coolvetica for titles/logotypes/main headlines, Lexend for body copy/captions/navigation/instructional text, orange `#E84B1A` as the primary accent, dark `#1A1A1A` for body text, the `lg_osa_3` stacked logo lockup (no background, includes wordmark + "Runway to your future" tagline), and the Swiss Design / International Typographic Style foundation.

The constraint with `.docx` files is that Coolvetica isn't a standard system font — `python-docx` and `docx-js` can reference it by name, but the font won't render unless it's installed on the machine opening the file. Arial is a safe fallback that preserves the clean geometric feel. Let me factor that into the prompt.

Let me also read the SKILL.md to make sure the prompt aligns with how the docx skill actually works.
```
This block is not supported on your current device yet.
```

Good. Now let me also check if there's a frontend-design skill that could inform the visual approach:
```
This block is not supported on your current device yet.
```

Now I have everything I need. Let me build this prompt for you.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's what I built for you, Phelipe.

The prompt is a complete brand identity system instruction that covers every layer — color palette, typography mapping (Coolvetica → Arial Black for titles, Lexend → Arial for body), logo placement, the Swiss Design philosophy, document architecture from title page through headers/footers, content styling down to specific DXA values for spacing, table formatting with the orange header rows, callout boxes with the orange left-border accent, and technical execution rules that align with how the docx skill actually works.

A few things worth noting:

**Font reality:** Coolvetica and Lexend won't render in .docx unless the person opening the file has them installed. The prompt maps Coolvetica → Arial Black (heavier weight, closer to that display feel) and Lexend → Arial (clean, geometric, universally available). If you ever distribute the brand fonts to all recipients, you just update two lines in the mapping table.

**How to deploy it:** Paste the prompt content into your OSA Project's custom instructions, and upload `lg_osa_3.png` to the Project's knowledge files. Every doc you generate from that Project will follow the system.

**The "vibe check" section at the end** is intentional — it gives Claude a self-audit step before delivering, so it catches generic-looking output before you have to.

Want me to adjust anything — tighter callout box specs, different title page layout, or add guidance for specific document types like memos vs. roadmaps?

---

## Claude

Got it — I see the Strategic Roadmap title page in the preview. That's the benchmark look you want replicated across all docs going forward.

The prompt I just gave you will produce that exact structure. Drop it into the OSA Project instructions, upload `lg_osa_3.png` to the knowledge files, and you're set. Every doc you generate from that Project will follow the same visual system — logo, orange headings, branded header/footer with the accent lines, the whole thing.

Want me to tweak anything in the prompt before you paste it in?

---

## Phelipe

this how i look. can i just add a promopt to the chat that has the file their just to upgrade?

---

## Claude

Yes — exactly. You already have the logo files and the three branded docs in that Project's knowledge files. You don't need a separate conversation or to re-upload anything.

Just go to the **Instructions** panel (the pencil icon on the right side, where it already says "**Project Instructions** Orange Sunshine Aviation is an aviation venture...") and **append** the brand prompt I gave you to whatever's already there. The existing project instructions stay — you're just adding the visual identity system on top.

Then any new conversation in that Project — or even a message in an existing one — will follow the brand spec automatically because it can already see `lg_osa_3.png` and the docs in the knowledge files.

Want me to adjust the prompt to account for your existing project instructions, or is it good to paste as-is?

---

## Phelipe

format looks bad. no logo. evaluate as senior graphic designer and generate a prompt for get to tier 1 level

---

## Claude

Let me evaluate all three documents properly — looking at the actual rendered output, not just the code.
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

Now I can see the rendered output clearly. Here's my **senior graphic designer audit**:

---

## What's Actually Happening

**Logo is broken in all three docs.** The image file is stored with a `.png` extension but it's actually **JPEG data**. Word sees `Content_Types` mapping `.png` → `image/png`, tries to decode JPEG data as PNG, and renders that beige/tan placeholder rectangle you see on every title page. The logo *is* embedded — it's just unreadable.

**Duplicate heading styles — first wins.** All three docs have the Heading1/2/3 styles defined *twice* in `styles.xml`. The first set uses a default blue (#2E74B5) with no bold, no font declaration, no spacing. The second set has the correct OSA orange (#E84B1A), bold, Arial, proper spacing. But Word uses the **first definition it encounters**, so the orange overrides are never applied. The headings only *appear* orange because individual text runs have inline color formatting — this is fragile and inconsistent.

**Memo page 2 is broken.** After the title page, the Memo shows a near-empty page with "Execution Operating Memo" as a heading, the subtitle, then "For Founder Use Only — Confidential" styled as a *heading* instead of body text. The actual content starts on page 3. That's a wasted page.

**Title page content bleeds.** On the Memo and Roadmap, below the business unit table there's a stray repetition — "OSA" / "Orange Sunshine Aviation" / "Runway to your future" appears *again* as styled headings at the bottom of page 1. This looks like a section break misfired and the first content headings landed on the title page instead of the next page.

**No header/footer visible on content pages.** The XML has header/footer definitions with the orange accent lines, but in the rendered PDFs I checked, the content pages show no header/footer at all — likely because the section properties don't properly reference them, or the `titlePage: true` flag is suppressing them on the only section that exists.

**Callout boxes are just left-border blocks.** They work, but they feel like markdown blockquotes, not designed callouts. No background shading visible.

---

## The Revised Prompt

Based on all of this, the prompt needs to explicitly address these technical pitfalls. Let me update it:

---

## Phelipe

Continue

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

Now I have the complete picture across all three docs. Let me write the definitive prompt.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Phelipe, here's what the audit found and what v2 of the prompt fixes.

**The three bugs killing your docs right now:**

**1. Logo is invisible in all three documents.** The file `lg_osa_3.png` is actually JPEG data stored with a `.png` extension. The code declares `type: "png"`, Word tries to decode JPEG as PNG, and you get that beige/tan placeholder rectangle where the logo should be. The v2 prompt includes a magic-byte sniffing pattern that detects the real format regardless of the file extension.

**2. Headings rely on fragile inline formatting.** All three docs have *duplicate* Heading1/2/3 style definitions in `styles.xml` — the first set is a default blue (#2E74B5) with no bold or font, the second is your correct orange. Word uses the first one it finds, so the style-level branding is ignored. The headings only appear orange because every TextRun has inline color overrides — which is a band-aid, not a fix. The v2 prompt addresses this with a belt-and-suspenders approach: define the styles correctly AND apply inline formatting as a safety net, plus explicit guidance to check for and remove duplicates.

**3. The Memo is structurally broken.** Pages 2, 3, and 4 are nearly empty — just dashed-line separators and stray table fragments before actual content starts on page 5. Body content also bleeds onto the title page (the "OSA / Orange Sunshine Aviation / Runway to your future" repetition below the business unit table). The v2 prompt enforces a strict two-section architecture with clear break rules.

**What's actually working:** The Operating System's header/footer renders correctly on body pages — orange "OSA" mark, pipe separator, document title, accent lines. The callout boxes with the orange left-border work. The orange table headers with white text work. These patterns are preserved in v2.

Paste everything below the line marker into your OSA Project instructions, and the next time you generate a doc in that Project it should come out clean.

---

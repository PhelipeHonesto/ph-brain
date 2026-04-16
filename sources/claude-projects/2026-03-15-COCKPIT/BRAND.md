---
title: BRAND.md
project: COCKPIT
doc_uuid: 98c4f816-8e42-4c1c-a90c-24b5adc266f5
source: claude-project-doc
type: source
---

# OSA Connect — Visual Identity Reference
**Source:** Orange Sunshine Aviation Brand Book
**Scope:** OSA Connect sub-brand ONLY. This is the charter brokerage platform.
**Note:** The parent brand (Orange Sunshine Aviation) and other sub-brands (Loud Hawk, OSA Aircraft) have their own visual hierarchies. This file does NOT cover those — it will be expanded into a full multi-brand system later.

---

## Color Hierarchy — OSA Connect

OSA Connect flips the parent brand's color priority. Where OSA institutional leads with orange, OSA Connect leads with beige for readability and uses orange as an accent.

### Application Order (how colors are used, not swatch number)

| Priority | Color           | HEX       | How It's Used in OSA Connect                    |
|----------|-----------------|-----------|-------------------------------------------------|
| **1st**  | Light Beige     | `#e4e4d3` | Neutral base, canvas, readability foundation    |
| **2nd**  | Dark Gray       | `#1a1a1a` | Text, contrast, grounding, dark-mode backgrounds |
| **3rd**  | Purple          | `#432a7a` | Wordmark, distinction, exclusivity signals      |
| **4th**  | Vibrant Orange  | `#e74b1d` | CTA buttons, accents, energy moments — NOT dominant |
| **5th**  | Lilac           | `#8767a9` | Supporting tone, secondary UI elements          |
| **6th**  | Salmon/Peach    | `#f29569` | Warmth, approachability, soft accents           |
| **7th**  | Light Blue      | `#a9d6e5` | Lightness, freedom, informational highlights    |
| **8th**  | Yellow          | `#ffc431` | Awareness, visibility, alerts, sparse accents   |

### Key Rule
**Orange is an accent in OSA Connect, not the canvas.** Beige leads. Dark gray grounds. Purple distinguishes. Orange draws the eye to actions (CTAs, key moments).

---

## Full Color Specs

### Primary Colors

| Swatch | Name            | HEX       | RGB            | CMYK          |
|--------|-----------------|-----------|----------------|---------------|
| 01     | Vibrant Orange  | `#e74b1d` | 231, 75, 29    | 1, 81, 93, 0  |
| 02     | Dark Gray       | `#1a1a1a` | 26, 26, 26     | 0, 0, 0, 90   |
| 03     | Light Beige     | `#e4e4d3` | 236, 228, 211  | 9, 10, 20, 0  |

### Secondary Colors

| Swatch | Name            | HEX       | RGB            | CMYK          |
|--------|-----------------|-----------|----------------|---------------|
| 04     | Purple          | `#432a7a` | 67, 42, 122    | 92, 98, 11, 3 |
| 05     | Lilac           | `#8767a9` | 135, 103, 169  | 56, 65, 1, 0  |
| 06     | Salmon/Peach    | `#f29569` | 242, 149, 105  | 0, 51, 59, 0  |
| 07     | Light Blue      | `#a9d6e5` | 169, 214, 229  | 38, 4, 10, 0  |
| 08     | Yellow          | `#ffc431` | 255, 196, 49   | 0, 26, 85, 0  |

### Opacity Scale

All colors can be used at these opacity levels for depth, hierarchy, and texture:
`100% → 90% → 81% → 72% → 63% → 54% → 45% → 36% → 27% → 18% → 9%`

---

## CSS Variables

```css
:root {
  /* OSA Connect — Application hierarchy order */

  /* Canvas & Structure */
  --osa-beige: #e4e4d3;          /* 1st — neutral base */
  --osa-dark: #1a1a1a;           /* 2nd — contrast, text */

  /* Brand Identity */
  --osa-purple: #432a7a;         /* 3rd — wordmark, distinction */
  --osa-orange: #e74b1d;         /* 4th — CTA, accent ONLY */

  /* Supporting Palette */
  --osa-lilac: #8767a9;          /* 5th */
  --osa-salmon: #f29569;         /* 6th */
  --osa-blue: #a9d6e5;           /* 7th */
  --osa-yellow: #ffc431;         /* 8th */

  /* Semantic Tokens */
  --osa-bg-light: #e4e4d3;       /* Default page background */
  --osa-bg-dark: #1a1a1a;        /* Dark sections / dark mode */
  --osa-text-on-light: #1a1a1a;  /* Body text on beige */
  --osa-text-on-dark: #e4e4d3;   /* Body text on dark gray */
  --osa-cta: #e74b1d;            /* Buttons, links, action elements */
  --osa-cta-hover: #f29569;      /* CTA hover state — softer warmth */
  --osa-highlight: #432a7a;      /* Special emphasis, badges, tags */
}
```

---

## Typography

### Primary Typeface: Lexend
- **Role:** Primary typeface for ALL OSA Connect interfaces
- **Why:** High legibility, cognitive accessibility
- **Use:** Body text, UI elements, navigation, forms, labels, all content
- **Weights:** Regular (400) body, Medium (500) emphasis, Bold (700) headings
- **Source:** Google Fonts — `https://fonts.google.com/specimen/Lexend`

### Display Typeface: Coolvetica
- **Role:** Titles and visual highlights ONLY
- **Use:** Hero headlines, section headers, marketing callouts — sparingly
- **Rule:** Lexend is the default. Coolvetica adds personality but does not dominate.

### CSS Implementation

```css
@import url('https://fonts.googleapis.com/css2?family=Lexend:wght@400;500;700&display=swap');

body {
  font-family: 'Lexend', sans-serif;
}

h1, .hero-headline, .brand-display {
  font-family: 'Coolvetica', sans-serif;
}
```

---

## Logo — OSA Connect

### Structure
- **Icon:** Stylized aviation motif (compass rose / signal waves) — left of wordmark
- **Wordmark:** "osa" in custom letterforms + "connect" below in clean sans-serif
- **Default colors:** Icon = orange (#e74b1d) + purple (#432a7a). Wordmark = purple (#432a7a)

### Approved Background Variations

| Background       | Icon Color      | Wordmark Color | Use Case                     |
|------------------|----------------|----------------|------------------------------|
| Light Beige      | Orange + Purple | Purple         | Primary / default            |
| Dark Gray        | Orange          | White/Beige    | Dark mode / website header   |
| Vibrant Orange   | White           | White          | High-energy applications     |
| Purple           | Orange          | White          | Accent contexts              |
| Light Blue       | Purple          | Purple         | Light secondary              |
| Salmon           | Dark Gray       | Dark Gray      | Warm contexts                |
| Yellow           | Dark Gray       | Dark Gray      | High-visibility              |
| Lilac            | Orange          | Dark Gray      | Soft secondary               |

---

## Design Rules — OSA Connect

1. **Beige first** — #e4e4d3 is the default canvas
2. **Dark gray for dark sections** — #1a1a1a for headers, footers, hero blocks, dark mode
3. **Orange is a verb, not a noun** — Use it for CTAs and action moments, never as background fill
4. **Purple = brand signature** — The wordmark is purple; use it for distinction, not decoration
5. **Lexend everywhere, Coolvetica sparingly** — Accessibility over style
6. **Opacity for depth** — Use the 9-step scale to create hierarchy within a single color
7. **Secondary colors support, never lead** — Lilac, salmon, blue, yellow enrich but don't dominate

---

## Scope & Future

This file covers OSA Connect only. Future brand reference files will be created for:
- **OSA (institutional)** — Parent brand, orange-dominant
- **Loud Hawk** — Media/intelligence layer, dark background system
- **OSA Aircraft** — Advisory sub-brand

These will be organized into a unified brand system when ready.

---

## File Placement

Drop this file into any project building OSA Connect UI:
- `~/Desktop/design-skills-lab/BRAND.md`
- `~/Desktop/OSA-connect-site/BRAND.md`
- Referenced in `CLAUDE.md` with: `Before generating any UI, read BRAND.md and follow all specifications.`

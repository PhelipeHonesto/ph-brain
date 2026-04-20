---
title: SKILLS-STACK.md
project: COCKPIT
doc_uuid: db225c02-94a6-42b1-838d-be411bec82d9
source: claude-project-doc
type: source
---

# OSA Skills Stack — Master Research Document
**Compiled:** March 15, 2026
**Purpose:** Best-in-class Claude Code skills for building OSA Connect website, Loud Hawk content system, and Orange Sunshine Aviation brand

---

## TIER 1 — CORE STACK (Install First)

### 1. Owl-Listener/designer-skills ✅ INSTALLED
- **What:** 63 skills, 27 commands across 8 plugins (research, systems, strategy, UI, interaction, prototyping, ops, toolkit)
- **Why for OSA:** Full UX research workflow — personas, journey maps, empathy maps, design system audits, handoff specs
- **Install:** Already done
- **Source:** https://github.com/Owl-Listener/designer-skills
- **Stars:** ~300+ | **License:** MIT

### 2. UI/UX Pro Max (v2.1)
- **What:** Design intelligence engine — 50 UI styles, 97 color palettes, 57 font pairings, 99 UX guidelines, 25 chart types, 9 tech stacks. Includes Python CLI with searchable design database and AI-powered Design System Generator
- **Why for OSA:** Auto-generates complete design systems based on product type. Run `--design-system -p "OSA Connect"` and get tailored palette, typography, layout patterns, anti-patterns. Persistent design systems with Master + page overrides
- **Install:** `/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill` then `/plugin install ui-ux-pro-max@ui-ux-pro-max-skill`
- **Source:** https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- **Stars:** 41,400+ | **License:** MIT

### 3. Anthropic frontend-design ✅ AVAILABLE IN MARKETPLACE
- **What:** Anthropic's official anti-generic-AI design skill. Forces bold aesthetic direction before writing code. Covers typography, color, motion, spatial composition, backgrounds
- **Why for OSA:** Ensures the OSA Connect site doesn't look like every other AI-generated page. Pushes distinctive brand identity
- **Install:** `/plugin marketplace add anthropics/claude-code` or `/plugin install frontend-design@claude-plugins-official`
- **Source:** https://github.com/anthropics/skills + https://github.com/anthropics/claude-code
- **Stars:** 65,800+ | **License:** Custom

### 4. Superpowers (obra)
- **What:** Complete agentic software development workflow — brainstorm → design spec → implementation plan → subagent-driven execution → review → merge. 20+ battle-tested skills including TDD, debugging, collaboration patterns
- **Why for OSA:** When you move from prototyping to actually building the OSA Connect web app, this structures the entire development process. /brainstorm → /write-plan → /execute-plan
- **Install:** `/plugin marketplace add obra/superpowers-marketplace` then `/plugin install superpowers@superpowers-marketplace`
- **Source:** https://github.com/obra/superpowers
- **Stars:** 42,000+ | **License:** Open source

### 5. Marketing Skills (Corey Haines)
- **What:** Full marketing skill suite — CRO, copywriting, SEO audit, AI SEO, email sequences, social media, landing page optimization, signup flow CRO, analytics tracking, pricing strategy, competitor analysis, and more
- **Why for OSA:** Directly relevant to Loud Hawk content, OSA Connect landing page optimization, email sequences, and overall growth strategy. Built by a real marketer (Corey Haines / Conversion Factory)
- **Install:** `/plugin marketplace add coreyhaines31/marketingskills` then `/plugin install marketing-skills`
- **Source:** https://github.com/coreyhaines31/marketingskills
- **Stars:** Growing | **License:** Open contributions

---

## TIER 2 — QUALITY & ENGINEERING (Install When Building the Web App)

### 6. Vercel Web Design Guidelines
- **What:** 100+ rules for UI/UX quality — accessibility, performance, UX best practices. Works like a linter for design
- **Why for OSA:** Quality gate before shipping. Catches WCAG violations, missing ARIA attributes, keyboard nav issues
- **Install:** `/plugin marketplace add vercel-labs/agent-skills` then select `web-design-guidelines`
- **Source:** https://github.com/vercel-labs/agent-skills
- **Stars:** 19,500+ | **License:** MIT

### 7. Vercel React Best Practices
- **What:** 57 performance rules across 8 categories (waterfalls, bundle size, server-side, client-side, re-renders, rendering, JS performance, advanced patterns)
- **Why for OSA:** When OSA Connect moves to Next.js/React via Cursor, this ensures performance is built in from the start
- **Install:** Same marketplace as above, select `react-best-practices`
- **Source:** https://github.com/vercel-labs/agent-skills

### 8. Vercel Composition Patterns
- **What:** React component architecture — compound components, context providers, explicit variants, state management. Kills boolean prop proliferation
- **Why for OSA:** Clean, scalable component architecture for OSA Connect's UI (pipeline views, contact cards, quote builders)
- **Install:** Same marketplace as above, select `composition-patterns`
- **Source:** https://github.com/vercel-labs/agent-skills

### 9. AccessLint
- **What:** Dedicated accessibility toolkit — contrast checker, WCAG refactoring, color-only detection, link purpose auditing. Includes MCP server for programmatic contrast analysis
- **Why for OSA:** Charter clients include people with disabilities. Accessibility isn't optional for a service brand
- **Install:** `/plugin marketplace add accesslint/claude-marketplace` then `/plugin install accesslint@accesslint`
- **Source:** https://github.com/accesslint/claude-marketplace
- **Stars:** Small but high quality | **License:** MIT

### 10. Bencium UX Designer
- **What:** Comprehensive UX fundamentals — design thinking, visual standards, interaction design, accessibility. Two variants: "innovative" (bold/creative) and "controlled" (consistent/systematic). 28,000+ character reference doc
- **Why for OSA:** Deep UX reference for complex flows like booking, quoting, operator selection
- **Install:** `git clone https://github.com/bencium/bencium-claude-code-design-skill.git` then copy to `~/.claude/skills/`
- **Source:** https://github.com/bencium/bencium-claude-code-design-skill
- **Stars:** 72 | **License:** Not specified

---

## TIER 3 — SPECIALIZED / EXPLORE LATER

### 11. Alirezarezvani/claude-skills (180+ Skills Mega-Pack)
- **What:** 180+ production-ready skills across engineering, marketing, product, compliance, C-level advisory, finance. Includes agent personas (startup-cto, growth-marketer, solo-founder)
- **Why for OSA:** The "solo-founder" persona + marketing skills + launch strategy could be useful for OSA's growth phase
- **Install:** `/plugin marketplace add alirezarezvani/claude-skills`
- **Source:** https://github.com/alirezarezvani/claude-skills

### 12. SEO Machine (TheCraigHewitt)
- **What:** Specialized Claude Code workspace for long-form SEO content. Custom commands (/research, /write, /analyze-existing, /optimize). Integrates GA4 + Google Search Console + DataForSEO
- **Why for OSA:** When Loud Hawk needs SEO-optimized long-form content beyond the newsletter
- **Source:** https://github.com/TheCraigHewitt/seomachine

### 13. Context7 MCP Server
- **What:** Up-to-date, version-specific library documentation delivered into Claude Code sessions. Replaces stale training data with actual current docs
- **Why for OSA:** When building with React/Next.js, ensures Claude uses correct API references
- **Install:** Available in official marketplace
- **Source:** Upstash (open source)
- **Stars:** 168,800+ installs

---

## KEY RESOURCE HUBS

| Resource | URL | What It Is |
|---|---|---|
| **Awesome Claude Skills** | https://github.com/travisvn/awesome-claude-skills | Curated list of skills + resources |
| **Awesome Claude Plugins** | https://github.com/ComposioHQ/awesome-claude-plugins | Plugin adoption metrics |
| **Awesome Claude Plugins (quemsah)** | https://github.com/quemsah/awesome-claude-plugins | Automated metrics tracking |
| **Claude Code Skills Hub** | https://claudecodeplugins.io/ | 1,399 skills across 343 plugins, searchable |
| **Claude Marketplaces** | https://claudemarketplaces.com/ | Plugin marketplace directory |
| **Agent Skills Spec** | https://agentskills.io/specification | Open standard (works across Claude, Codex, Cursor, Gemini CLI) |
| **Snyk Top 8 Skills** | https://snyk.io/articles/top-claude-skills-ui-ux-engineers/ | Best curated article on UI/UX skills |

---

## INSTALLATION PRIORITY ORDER

For a solo operator building a charter aviation brand + website + content system:

```
Phase 1 — Research & Design (NOW)
  ✅ Owl-Listener/designer-skills (installed)
  → UI/UX Pro Max
  → Anthropic frontend-design

Phase 2 — Marketing & Content
  → Marketing Skills (coreyhaines31)
  → SEO Machine (optional, for long-form)

Phase 3 — Development Workflow
  → Superpowers (obra)
  → Vercel agent-skills (web-design-guidelines + react-best-practices + composition-patterns)
  → Context7 MCP

Phase 4 — Quality & Polish
  → AccessLint
  → Bencium UX Designer
```

---

## SECURITY NOTE

Per Snyk's ToxicSkills research:
- 36% of tested skills contained prompt injection
- 1,467 malicious payloads found across the ecosystem
- **Always review SKILL.md and bundled scripts before installing**
- Skills from Anthropic, Vercel, and well-known maintainers = lower risk
- Community skills = read the code first

---

## HOW SKILLS LAYER (They Don't Conflict)

```
┌─────────────────────────────────────────────────┐
│              YOUR PROMPT / TASK                  │
├─────────────────────────────────────────────────┤
│ Owl-Listener    → Research & Strategy layer     │
│ UI/UX Pro Max   → Design Intelligence layer     │
│ frontend-design → Aesthetic Direction layer      │
│ Vercel          → Quality & Performance layer   │
│ AccessLint      → Accessibility layer           │
│ Superpowers     → Development Process layer     │
│ Marketing       → Growth & Content layer        │
└─────────────────────────────────────────────────┘
Each activates when relevant. No conflicts.
```

---
title: Finding designer skills via terminal
created: 2026-03-28T22:21:32.902500Z
updated: 2026-03-28T23:55:07.403218Z
uuid: 0f090b69-4aea-405e-bd44-b891633338f8
source: claude-conversation
type: source
message_count: 10
---

# Finding designer skills via terminal

*Summary: **Conversation Overview**

The person was troubleshooting and navigating their local Claude plugins directory structure to locate designer and copywriting-related skills. The conversation focused on finding the correct terminal commands to explore skill files stored in `~/.claude/plugins/`, specifically within the `designer-skills` and `marketingskills` plugin folders.

The person encountered a "No such file or directory" error when attempting to `cat` a skill file at a path suggested by Claude, which revealed that the actual files are stored under a cache subdirectory (`~/.claude/plugins/cache/`) rather than directly in `~/.claude/plugins/`. Through this troubleshooting process, the correct paths were identified: designer skills live at `~/.claude/plugins/cache/designer-skills/designer-toolkit/1.0.0/skills/` and marketing skills at `~/.claude/plugins/cache/marketingskills/marketing-skills/9d4d29a79511/skills/`.

The person was specifically looking for copywriting-related skills and was directed to three relevant files: `copywriting/SKILL.md` and `copy-editing/SKILL.md` in marketingskills, and `ux-writing/SKILL.md` in designer-skills. The conversation ended with the person requesting commands to list all designer-skill markdown files and directories, for which Claude provided several `find`, `grep`, and `tree`-based terminal commands. The person's plugin stack also includes an `osa-brand-voice` skill relevant to OSA/Loud Hawk brand work.*

## Phelipe

can you give me prompt to find designer skills on terminal

---

## Claude

The user wants a terminal command/prompt to find designer skills. Let me look at the uploaded file first.
```
This block is not supported on your current device yet.
```

The user wants terminal commands to find designer skills. Based on the catalog, designer skills are in `~/.claude/plugins/designer-skills` (57 skills) and also `ui-ux-pro-max-skill` (7 skills). Let me give them grep/find commands to explore these.Based on your catalog, designer skills live in two plugin folders. Here are the terminal commands:

**List all designer skill files:**
```bash
ls ~/.claude/plugins/designer-skills/
```

**Also check UI/UX Pro Max:**
```bash
ls ~/.claude/plugins/ui-ux-pro-max-skill/
```

**Search by keyword across both:**
```bash
grep -r "design" ~/.claude/plugins/designer-skills/ --include="*.md" -l
```

**Find a specific skill by name (e.g., "typography"):**
```bash
find ~/.claude/plugins/designer-skills/ -name "*typography*"
```

**Preview a skill's description quickly:**
```bash
head -20 ~/.claude/plugins/designer-skills/SKILL_NAME.md
```

**Search across ALL plugin skills at once:**
```bash
grep -rl "design" ~/.claude/plugins/ --include="*.md"
```

The 57 skills in `designer-skills` are grouped into: Visual Design, UX/Research, Interaction Design, Prototyping & Testing, Design Ops, and Designer Toolkit — so if you want to filter by category you can also grep for category headers:

```bash
grep -r "typography\|color\|layout" ~/.claude/plugins/designer-skills/ --include="*.md" -l
```

---

## Phelipe

find the one the help with copywritting

---

## Claude

The user wants to find a skill related to copywriting from their designer skills catalog. Looking at the catalog content I already have, I can search through it.

From the catalog, I can see `ux-writing` under Designer Toolkit: "Microcopy, error messages, empty states, onboarding copy, CTAs."

There's also `osa-brand-voice` in Layer 1 custom skills.

And in marketing skills there might be copywriting skills too. Let me check the truncated section.

The relevant ones visible are:
- `ux-writing` (Designer Toolkit) — "Microcopy, error messages, empty states, onboarding copy, CTAs"


- `osa-brand-voice` (Custom OSA) — "OSA brand voice and copy guidelines"

The truncated section likely contains marketing-specific copywriting skills, but from what I can see, `ux-writing` is the closest match in the designer skills.From your catalog, the closest match in the designer skills is:

**`ux-writing`** — under the **Designer Toolkit** section of `designer-skills`
> *Microcopy, error messages, empty states, onboarding copy, CTAs*

To pull it up in terminal:
```bash
cat ~/.claude/plugins/designer-skills/ux-writing.md
```

That said, for pure copywriting (ads, brand copy, campaigns), you actually have better-fit skills elsewhere in your stack:

| Skill | Location | Best for |
|-------|----------|----------|
| `osa-brand-voice` | `~/osa/skills/` | Any OSA/Loud Hawk copy |
| `ad-creative` | `~/.claude/plugins/marketingskills/` | Ad copy |
| `ux-writing` | `~/.claude/plugins/designer-skills/` | UI microcopy, CTAs |

To confirm what's in marketing skills:
```bash
ls ~/.claude/plugins/marketingskills/ | grep -i "copy\|writ\|content"
```

---

## Phelipe

cat ~/.claude/plugins/designer-skills/ux-writing.md
cat: /Users/phelipehonesto/.claude/plugins/designer-skills/ux-writing.md: No such file or directory

---

## Claude

The user is getting a "No such file or directory" error. The skill file might have a different name or be in a different location. Let me suggest some discovery commands.The file path or name might be slightly different. Try these to locate it:

**Find the actual folder name:**
```bash
ls ~/.claude/plugins/ | grep -i design
```

**Then list what's inside:**
```bash
ls ~/.claude/plugins/<actual-folder-name>/
```

**Or do a broad search for anything with "writing" in the name:**
```bash
find ~/.claude/plugins/ -name "*writ*" -o -name "*copy*" 2>/dev/null
```

**Nuclear option — find every .md file and grep for "copy":**
```bash
grep -rl "copy\|writing" ~/.claude/plugins/ --include="*.md" 2>/dev/null
```

The catalog may list skill names that don't match the actual filenames 1:1. Once you run `ls ~/.claude/plugins/` and see the real folder structure, paste it here and I'll point you to the exact file.

---

## Claude

The user wants to find copywriting skills. From the results, the best candidates are:

1. `copywriting` skill in marketingskills
2. `copy-editing` skill in marketingskills
3. `ux-writing` in designer-skills

The actual active paths (not cache/marketplace) for the copywriting skill would be in the cache. Let me point them to the right ones.You have two dedicated copywriting skills in `marketingskills`. Here are the exact paths:

**Main copywriting skill:**
```bash
cat ~/.claude/plugins/cache/marketingskills/marketing-skills/9d4d29a79511/skills/copywriting/SKILL.md
```

**Copy editing skill:**
```bash
cat ~/.claude/plugins/cache/marketingskills/marketing-skills/9d4d29a79511/skills/copy-editing/SKILL.md
```

**And the UX writing one from designer-skills:**
```bash
cat ~/.claude/plugins/cache/designer-skills/designer-toolkit/1.0.0/skills/ux-writing/SKILL.md
```

For OSA/Loud Hawk work specifically, the priority order would be:

| Priority | Skill | Use case |
|----------|-------|----------|
| 1st | `osa-brand-voice` | Any OSA copy — brand voice first |
| 2nd | `copywriting` (marketingskills) | Campaigns, landing pages, sales copy |
| 3rd | `copy-editing` (marketingskills) | Refining/tightening existing copy |
| 4th | `ux-writing` (designer-skills) | In-product microcopy only |

---

## Phelipe

i want to show all the designer-skill md and skill

---

## Claude

The user wants to see all the designer-skills markdown files and skills. Let me give them the right terminal commands.Run this:

```bash
find ~/.claude/plugins/cache/designer-skills/ -name "*.md" -o -type d | sort
```

Or more organized — **skills only:**
```bash
find ~/.claude/plugins/cache/designer-skills/ -type d | sort
```

**All `.md` files only:**
```bash
find ~/.claude/plugins/cache/designer-skills/ -name "*.md" | sort
```

**With file previews (first line of each):**
```bash
find ~/.claude/plugins/cache/designer-skills/ -name "*.md" | sort | while read f; do echo "---"; echo "$f"; head -1 "$f"; done
```

**Tree view (cleanest):**
```bash
tree ~/.claude/plugins/cache/designer-skills/
```

If `tree` isn't installed:
```bash
brew install tree && tree ~/.claude/plugins/cache/designer-skills/
```

Paste the output here and I'll map it all out for you cleanly.

---

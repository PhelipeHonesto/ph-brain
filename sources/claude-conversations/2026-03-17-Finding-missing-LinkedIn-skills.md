---
title: Finding missing LinkedIn skills
created: 2026-03-17T20:24:58.164159Z
updated: 2026-03-17T20:28:35.790774Z
uuid: 7e856e92-9ef1-47bf-a308-809bb890a7a4
source: claude-conversation
type: source
message_count: 10
---

# Finding missing LinkedIn skills

## Phelipe

i cant find my lh-linkedin skills

---

## Claude

Check this path:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Not on disk in the expected places. A few places to check:

1. **In your Loud Hawk project folder:** `~/Desktop/OSA/loud-hawk/skills/` or `~/Desktop/OSA/loud-hawk/docs/`
2. **In the marketing skills plugin:** The `coreyhaines31/marketingskills` plugin has social media skills. Your LinkedIn content may live there as a skill invocation, not a standalone file.
3. **In a Claude Project context:** If you drafted it in the Loud Hawk + Marketing Project (not COCKPIT), it won't be visible here.

What do you remember about where you built it? Was it a SKILL.md file, a prompt template, or a content strategy doc? That'll narrow it down fast.

---

## Phelipe

i need to do a search on terminal

---

## Claude

Open Warp and run:

```bash
find ~/Desktop/OSA -type f | xargs grep -ril "linkedin" 2>/dev/null
```

That'll search file contents across the entire OSA folder. If it was named something non-obvious, it'll still surface it.

---

## Claude

Found it:

```
~/Desktop/OSA/loud-hawk/docs/LH-Carousel-Automation-Pipeline-v3-FINAL.md
```

It's not a skills file, it's your LinkedIn carousel automation pipeline doc. Open it with:

```bash
open ~/Desktop/OSA/loud-hawk/docs/LH-Carousel-Automation-Pipeline-v3-FINAL.md
```

Or in Claude Code:

```bash
cat ~/Desktop/OSA/loud-hawk/docs/LH-Carousel-Automation-Pipeline-v3-FINAL.md
```

---

## Phelipe

wait we build a skill to make post on linked in

---

## Claude

Run a broader search:

```bash
find ~/Desktop/OSA -type f | xargs grep -ril "skill\|linkedin" 2>/dev/null | grep -i "skill"
```

And also check your Claude skills directory directly:

```bash
ls ~/.claude/skills/ 2>/dev/null && find ~/.claude -type f -name "*.md" 2>/dev/null
```

---

## Claude

No `~/.claude/skills/` directory exists on your machine. The skill isn't in the standard Claude Code skills location.

Try this — search for the actual skill file by name patterns:

```bash
find ~/Desktop/OSA -type f -name "*skill*" -o -name "*SKILL*" | grep -i "linkedin\|social\|post"
```

And broader:

```bash
find ~/Desktop/OSA -type d -name "*skill*" -o -type d -name "*skills*"
```

It's possible it was built inside the Owl-Listener plugin directory or inside the `loud-hawk/docs/` folder under a different name. The carousel pipeline doc we found earlier might actually be it, just named differently than you remembered.

---

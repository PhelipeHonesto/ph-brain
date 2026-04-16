---
title: Design system evaluation workflow across 8 skills
created: 2026-03-17T04:38:09.544892Z
updated: 2026-03-17T04:38:20.987984Z
uuid: 9ff4b82e-c2ed-440e-8c9c-35614815fc21
source: claude-conversation
type: source
message_count: 2
---

# Design system evaluation workflow across 8 skills

## Phelipe

you will be getting all the outputs for this Smart. Let me build a comprehensive design evaluation document that you can feed to each skill. This needs to be specific enough that the skills can audit the actual decisions, not just rubber-stamp them.Save that to `~/osa-marketing/` then run it through all 8 skills in sequence. Here's the exact terminal workflow for tab 4:
Step 1: Save the file

```
cp ~/Downloads/LH-Design-System-Evaluation-Brief.md ~/osa-marketing/

```

Step 2: Start a fresh Claude Code session

```
cd ~/osa-marketing && claude

```

Step 3: Run each skill in sequence. Paste each one, wait for output, then paste the next:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(design-systems). Focus on the evaluation questions in the "For design-systems skills" section. Output findings as keep/change/add.

```

After that completes:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(ui-design). Focus on the "For ui-design skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(interaction-design). Focus on the "For interaction-design skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(design-ops). Focus on the "For design-ops skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(prototyping-testing). Focus on the "For prototyping-testing skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(designer-toolkit). Focus on the "For designer-toolkit skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(ux-strategy). Focus on the "For ux-strategy skills" section. Output findings as keep/change/add.

```

Then:

```
Read LH-Design-System-Evaluation-Brief.md and evaluate using Skill(design-research). Focus on the "For design-research skills" section. Output findings as keep/change/add.

```

That's 8 skill passes. Each one has specific questions tailored to what that skill is best at evaluating. Paste the outputs back here and we'll merge all findings into a final pre-build decision log.
Go run them. This is the last validation pass before you open Figma.

---

## Claude

Phelipe, I need to build the evaluation brief first before you can run those skills against it. Let me create the document.

Let me check what exists in the project files to make sure I reference the right design decisions for Loud Hawk's site.
```
This block is not supported on your current device yet.
```

---

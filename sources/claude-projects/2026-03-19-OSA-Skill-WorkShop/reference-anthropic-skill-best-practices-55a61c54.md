---
title: reference-anthropic-skill-best-practices.md
project: OSA Skill WorkShop
doc_uuid: 55a61c54-9a62-4558-b3ae-40b0642b5f6b
source: claude-project-doc
type: source
---

# Anthropic Skill Authoring Best Practices (Reference)

Source: platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
Last updated: March 2026

This is a condensed reference of Anthropic's official guidelines for writing effective skills. Use this as a checklist and reference when building or reviewing skills.

---

## Frontmatter Requirements

The SKILL.md frontmatter requires exactly two fields:

**name:**
- Maximum 64 characters
- Lowercase letters, numbers, and hyphens only
- No XML tags
- Cannot contain reserved words: "anthropic", "claude"

**description:**
- Maximum 1024 characters
- Non-empty
- No XML tags
- Must describe what the skill does AND when to use it
- Write in third person always ("Processes files" not "I process files")

The description is critical for skill selection. Claude uses it to choose the right skill from potentially 100+ available skills.

---

## Progressive Disclosure

SKILL.md serves as an overview that points Claude to detailed materials as needed, like a table of contents.

**How it works:**
- At startup, only name + description from all skills are loaded into context
- SKILL.md body is loaded only when the skill is triggered
- Additional files (references, examples) are loaded only when Claude needs them
- Scripts are executed without loading their code into context

**Rules:**
- Keep SKILL.md body under 500 lines
- Keep file references one level deep from SKILL.md
- For reference files over 100 lines, include a table of contents at the top
- Name files descriptively (form_validation_rules.md, not doc2.md)

**Pattern 1: High-level guide with references**

```
# PDF Processing

## Quick start
[Core instructions here]

## Advanced features
**Form filling**: See [FORMS.md](FORMS.md) for complete guide
**API reference**: See [REFERENCE.md](REFERENCE.md) for all methods
```

**Pattern 2: Domain-specific organization**

```
bigquery-skill/
  SKILL.md (overview and navigation)
  reference/
    finance.md (revenue, billing)
    sales.md (pipeline, accounts)
    product.md (usage, features)
```

**Pattern 3: Conditional details**

Show basic content in SKILL.md, link to advanced content in separate files. Claude reads the advanced files only when the user needs those features.

---

## Degrees of Freedom

Match specificity to the task's fragility:

**High freedom (text instructions, multiple valid approaches):**
Good for: content creation, research, analysis
Example: "Analyze the code structure and suggest improvements"

**Medium freedom (pseudocode, scripts with parameters):**
Good for: data processing, report generation
Example: Provide a template with customizable parameters

**Low freedom (exact scripts, no parameters):**
Good for: database migrations, destructive operations, exact formatting
Example: "Run exactly this command. Do not modify."

---

## Feedback Loops

The pattern: do the thing, validate the thing, fix if needed, repeat.

This dramatically improves output quality. Always include a validation step for critical tasks.

Example:
1. Make edits
2. Validate immediately
3. If validation fails, review error, fix, validate again
4. Only proceed when validation passes

---

## Common Anti-Patterns

**Don't offer too many options.** Provide one default approach with an escape hatch for edge cases.

**Don't use time-sensitive information.** Avoid "if before August 2025, use X." Use "current method" and "old patterns" sections instead.

**Don't use inconsistent terminology.** Pick one term and use it throughout. Don't mix "API endpoint," "URL," "API route," and "path."

**Don't deeply nest references.** Keep all reference files one level deep from SKILL.md.

**Don't assume tools are installed.** List required packages explicitly and include installation commands.

---

## The Iterative Build Process (Anthropic's Recommendation)

1. **Do the task without a skill first.** Work through it in a normal conversation. Notice what context you repeatedly provide.

2. **Identify the reusable pattern.** What information would be useful for similar future tasks?

3. **Ask Claude to create the skill.** "Create a skill that captures this pattern we just used."

4. **Review for conciseness.** Remove unnecessary explanations. Ask: "Does Claude already know this?"

5. **Test on real tasks.** Use the skill with a fresh Claude instance on actual work, not toy examples.

6. **Watch where Claude struggles.** Note where it misses steps, produces inconsistent output, or goes off-track.

7. **Iterate based on observation.** Return to Claude with specifics: "It forgot to filter test accounts. How should we fix the skill?"

8. **Repeat.** Each iteration improves the skill based on real behavior, not assumptions.

---

## Workflow Pattern

For complex tasks, provide a checklist Claude can track:

```
Task Progress:
- [ ] Step 1: [description]
- [ ] Step 2: [description]
- [ ] Step 3: [description]
```

Clear steps prevent Claude from skipping critical validation.

---

## Utility Scripts

Pre-made scripts in the skill folder are better than having Claude generate code because:
- More reliable than generated code
- Save tokens (no code in context)
- Save time (no generation needed)
- Ensure consistency across uses

Make clear whether Claude should EXECUTE the script (most common) or READ it as reference.

---

## MCP Tool References

If your skill uses MCP tools, always use fully qualified names:
Format: ServerName:tool_name
Example: "Use the BigQuery:bigquery_schema tool to retrieve schemas"

Without the server prefix, Claude may fail to locate the tool.

---

## Final Checklist (from Anthropic)

**Core quality:**
- Description is specific with key terms and trigger contexts
- SKILL.md body under 500 lines
- Additional details in separate files if needed
- No time-sensitive information
- Consistent terminology
- Concrete examples (not abstract)
- File references one level deep
- Clear workflow steps

**Testing:**
- At least three evaluation scenarios created
- Tested with real usage scenarios
- Feedback incorporated from actual use

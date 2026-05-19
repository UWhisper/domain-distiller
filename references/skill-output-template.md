# SKILL.md Output Template

> Reference for Phase 5 of the domain-distiller methodology.
> Use this skeleton when compiling the final SKILL.md for the distilled domain skill.

## Template Skeleton

```markdown
---
name: [SKILL-NAME]
description: [One paragraph describing what the skill does and when to trigger. Be specific about keywords and scenarios. Write in third person: "This skill should be used when..."]
---

# [Skill Title]

[1-2 sentences explaining what this skill enables.]

## Trigger Conditions

Activate this skill when the user:
- [Specific trigger scenario 1]
- [Specific trigger scenario 2]
- Mentions keywords: [keyword1], [keyword2], [keyword3], ...
- [Specific trigger scenario 3]

## Role & Tone

You are a [persona description]. Your tone is:
- **[Trait 1]** — [what this means in practice]
- **[Trait 2]** — [what this means in practice]
- **[Trait 3]** — [what this means in practice]
- **[Trait 4]** — [what this means in practice]

## Core Decision Framework

When a user asks for [domain action], work through this decision tree:

### Step 1: Gather Context

Ask about any missing dimensions from:
1. **[Dimension 1]** — [possible values]
2. **[Dimension 2]** — [possible values]
3. **[Dimension 3]** — [possible values]
... (up to 5-6 dimensions)

### Step 2: Apply [Dimension A] × [Dimension B] Matrix

| [Dim A \ Dim B] | [Value 1] | [Value 2] | [Value 3] | [Value 4] |
|-----------------|-----------|-----------|-----------|-----------|
| [Value A] | [recommendation] | ... | ... | ... |
| [Value B] | ... | ... | ... | ... |

### Step 3: Apply [Constraint/Taboo] Filter

**Absolute constraints (never recommend):**
- [Constraint 1] — [reason]
- [Constraint 2] — [reason]
...

**Soft constraints (caution):**
- [Constraint 1] — [reason]
...

### Step 4: Recommend

Provide **3-5 specific suggestions** organized as:
1. **Recommended** (best match) — with reasoning
2. **Alternative A** — different category at similar budget
3. **Alternative B** — lower-budget option
4. **Wildcard** — unexpected/creative option
5. **Experience add-on** — complementary experience

For each suggestion, include:
- [Key attribute 1]
- [Key attribute 2]
- Why it fits this context
- Any watch-outs

## Quick Reference Tables

### [Table 1 Name]

| [Column 1] | [Column 2] | [Column 3] | [Column 4] | [Column 5] |
|------------|------------|------------|------------|------------|
| ... | ... | ... | ... | ... |

### [Table 2 Name]

...

## The [N] Core Rules

These [N] rules are distilled from the research references. They are the backbone of this skill's recommendations.

### [Category 1] (Rules 1-X)
1. [Rule 1]
2. [Rule 2]
...

### [Category 2] (Rules X-Y)
...

## Special Scenario Handling

### [Special Scenario 1]

- [Key consideration]
- [Recommended approach]
- [Common mistakes]

### [Special Scenario 2]

...

## Reference Files

For deeper context on specific dimensions, consult these research files:

| File | Content |
|------|---------|
| `references/research/[dim-1]/[file].md` | [Description] |
| `references/research/[dim-2]/[file].md` | [Description] |
...

## Interaction Examples

### Example 1: [Scenario Description]

**User:** [Example query]

**Response flow:**
1. [Step taken]
2. [Step taken]
3. [Recommendations]
4. [Follow-up question to narrow down]

### Example 2: [Edge Case]

**User:** [Example query]

**Response flow:**
1. [Warning/flag raised]
2. [Alternative offered]
3. [Explanation]
```

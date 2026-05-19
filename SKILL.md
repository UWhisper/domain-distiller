---
name: domain-distiller
description: This skill should be used when the user wants to distill a domain of knowledge into a reusable Claude Code skill. Triggers on requests like "蒸馏一个关于X的skill", "把X知识做成技能", "distill X into a skill", or when the user describes a domain with scattered knowledge sources and wants structured, decision-ready output. Also use when the user has seen a successful skill distillation and wants to replicate the process for another domain.
---

# Domain Distiller

Distill any knowledge domain into a structured Claude Code skill through orthogonal decomposition, parallel multi-agent collection, cross-source verification, and decision framework compilation.

## Overview

This skill provides a repeatable 7-phase methodology for converting scattered domain knowledge into a Claude Code skill. It was generalized from multiple successful skill distillations across diverse domains.

The core insight: any knowledge domain can be decomposed into 3-5 orthogonal dimensions, researched in parallel, cross-verified, and compiled into a decision framework. The methodology works for any domain with external signal sources — restaurant recommendations, travel planning, home renovation, pet care, interview preparation, legal advice, etc.

## Prerequisite Check: Is Distillation Worth It?

Before activating the full methodology, run the LLM Baseline Test:

1. Ask Claude (without any skill loaded) a representative question from the domain
2. Evaluate the response for: accuracy, specificity, structure, actionability
3. If the response is already excellent, distillation's marginal value comes only from:
   - **Timeliness** — information newer than training cutoff
   - **Structured decisions** — multi-branch decision trees beyond what the LLM spontaneously generates
   - **User preference memory** — persisting user-specific context across sessions

If the domain lacks ALL three of these, recommend against distillation. A pure prompt might suffice.

## Phase 1: Domain Audit

### 1.1 Define the Domain Boundary

Work with the user to specify:
- **What decisions** should this skill help with? (Not "everything about X" — be specific)
- **Who is the user** and what context do they bring?
- **What is the output format** — recommendations, checklists, decision trees, comparisons?

### 1.2 Map the Signal Topology

Determine where knowledge lives in this domain:
- **Concentrated signals** — expert-authored content, official guidelines, textbooks, authoritative sources
- **Distributed signals** — social media discussions, user reviews, forum threads, community consensus
- **Tacit signals** — unwritten rules, cultural norms, practitioner intuition

The signal topology determines the verification strategy: concentrated signals need expert consensus checking; distributed signals need cross-source frequency weighting; tacit signals need pattern extraction across many anecdotes.

### 1.3 Define the Target Skill Scope

Output a one-paragraph scope statement. Example (restaurant recommendation):

> "A Claude Code skill that recommends restaurants in Chinese cities. Analyzes diner type, cuisine preference, occasion, budget, dietary constraints, and location to suggest specific restaurants with dishes, price estimates, and reservation tips."

## Phase 2: Orthogonal Decomposition

### 2.1 The Orthogonality Principle

Decompose the domain into 3-5 dimensions that are **mutually independent** — information in one dimension does not substantially overlap with information in another. Good decomposition means parallel agents work without conflict; bad decomposition produces redundant content requiring costly deduplication.

**Test for orthogonality**: Can you describe what unique information each dimension contributes without referencing any other dimension? If dimensions bleed into each other, re-split.

### 2.2 Decomposition Patterns

Choose from these proven patterns (detailed examples in `references/decomposition-patterns.md`):

| Pattern | Structure | Example Domains |
|---------|-----------|-----------------|
| **Context × Action** | User context dimensions × action/decision dimensions | Restaurant recs (diner type×cuisine×scene×budget), Travel planning (traveler type×destination×season×purpose) |
| **Rule × Resource** | Constraints/rules dimension × options/resources dimension | Renovation (taboos/regulations×materials×rooms), Legal advice (jurisdiction×case type×remedies) |
| **Principle × Practice** | Theory/principles dimension × application/technique dimension | Interview prep (evaluation criteria×question types×answers), Fitness (physiology×exercise types×nutrition) |
| **Static × Dynamic** | Stable knowledge dimension × time-sensitive dimension | Investment (asset class principles×current market), Tech stack (CS fundamentals×framework versions) |
| **Supply × Demand** | Provider/seller dimension × consumer/buyer dimension | Pet care (breed needs×owner lifestyle), Travel (destination×traveler type) |

### 2.3 Generate the Dimension Map

For the chosen pattern, generate specific dimensions. Each should have:
- **Name** — short label
- **Scope** — what knowledge falls under this dimension
- **Key sources** — where to find information for this dimension
- **Output file target** — where collected knowledge will be written

Present the dimension map to the user for approval before proceeding.

## Phase 3: Parallel Collection

### 3.1 Generate Agent Prompts

For each dimension, create an agent prompt following this template (full template in `references/agent-prompt-template.md`):

```
You are a research assistant. Your task is to collect knowledge about [DIMENSION] for [DOMAIN].

Search for the following topics (use WebSearch, mix languages as appropriate):
1. [Specific topic with keywords]
2. [Specific topic with keywords]
...

Write findings to: /path/to/output/dimension-name.md

Format requirements:
- Use tables for structured rules/data
- Each rule/data point must include: [field1], [field2], ...
- Minimum [N] rules/data points
- Label sources (even if based on training data, note "待后续核实")
```

### 3.2 Launch and Monitor

- Launch one agent per dimension in parallel (background mode)
- If agents lack WebSearch permissions, instruct them to use training data as fallback, labeled "基于训练数据，待后续核实"
- Monitor for completion; agents that stall on permission checks need explicit instruction to proceed without web access

### 3.3 Fallback Strategy

If all agents are blocked from web access:
1. Send explicit instruction: "Proceed with training data. Label accordingly. Write files NOW."
2. If agents still stall, write the reference files directly using the current Claude instance's knowledge
3. Prioritize writing the most critical dimension files first; skip non-essential ones if needed

## Phase 4: Cross-Source Verification

### 4.1 Signal Weighting

For each rule or data point collected:

| Confidence | Criteria |
|-----------|----------|
| **High** ✅ | Confirmed by 3+ independent sources or authoritative consensus |
| **Medium** ⚠️ | Confirmed by 2 sources or strong single authoritative source |
| **Low** ⚡ | Single source or training-data-only without external confirmation |
| **Speculative** ❓ | Inferred from pattern but not directly attested |

### 4.2 Cross-Reference Rules Across Dimensions

Rules from different dimensions should not contradict each other. If dimension A says "always do X in situation Y" and dimension B says "never do X in situation Y," flag the contradiction and determine which has stronger signal.

### 4.3 Deduplication

Same rule appearing in multiple collected files = strong signal. Merge duplicates into a single canonical form rather than repeating.

### 4.4 Verification Without Live Web Access

When agents operated entirely from training data (no live web search), shift the verification strategy:

- **Within-dimension consistency** — rules within a single dimension's output must not contradict each other
- **Cross-dimension consistency** — rules from different dimensions must not conflict (e.g., culture dimension says "never do X" but occasion dimension recommends X)
- **LLM consensus check** — rules consistent with widely-known, cross-cultural knowledge are higher confidence; idiosyncratic or surprising claims without corroboration are flagged speculative

Even without live sources, this multi-angle consistency check catches contradictions and overclaims that a single pass would miss.

## Phase 5: Decision Framework Compilation

### 5.1 Extract Core Rules

From the verified reference files, extract 50+ specific, actionable rules. Each rule should be:
- **Atomic** — one clear directive, not a compound
- **Falsifiable** — can be verified or disproven with data
- **Decision-relevant** — affects what recommendation or output is produced
- **Domain-specific** — not generic advice the LLM already knows

### 5.2 Build the Decision Tree

Structure the decision flow as:

```
Input context → [Dimension 1 filter] → [Dimension 2 filter] → ... → [Taboo/Constraint filter] → Output recommendations
```

The decision tree should be explicit enough that, given the same inputs, two independent runs produce the same reasoning path.

### 5.3 Create Quick-Reference Tables

For the most common decision points, create lookup tables that compress many rules into a scannable format. These speed up recommendations by avoiding full tree traversal for simple cases.

### 5.4 Write the SKILL.md

Compile everything into the target skill's SKILL.md following this structure (template in `references/skill-output-template.md`):

1. **YAML frontmatter** — name, description with trigger conditions
2. **Role & Tone** — 3-4 sentences defining persona
3. **Core Decision Framework** — step-by-step decision tree
4. **Quick Reference Tables** — condensed lookup tables for common scenarios
5. **Core Rules** (50+) — the verified rule set, organized by dimension
6. **Special Scenario Handling** — edge cases and high-stakes situations
7. **Reference Files Index** — pointers to the detailed research files
8. **Interaction Examples** — 2-3 annotated example conversations

## Phase 6: Validation

### 6.1 The 50-Rule Test

Count the domain-specific, actionable rules in the compiled skill. If fewer than 50:
- The domain may be too narrow for a dedicated skill
- Or the decomposition may have missed important dimensions
- Or the collection didn't go deep enough — revisit Phase 3

### 6.2 The Baseline Comparison

Run the same query through:
1. Pure Claude (no skill loaded)
2. Claude with the distilled skill loaded

The skill should produce **measurably better** output on at least 3 of these axes:
- Specificity (concrete vs. generic)
- Accuracy (reflects verified domain knowledge vs. plausible-sounding guess)
- Structure (organized decision flow vs. stream of consciousness)
- Safety (flags pitfalls/taboos vs. silent about risks)
- Personalization (adapts to user context vs. one-size-fits-all)

### 6.3 Edge Case Stress Test

Test the skill against:
- Extreme values (zero budget, maximum complexity)
- Contradictory constraints (high romance expectation + minimal budget)
- High-stakes scenarios (scenarios where wrong advice has real consequences)
- Cross-cultural or regional variations

## Phase 7: Packaging

### 7.1 Directory Structure

The final skill follows the standard structure:

```
skill-name/
├── SKILL.md                    # Core skill with decision framework
├── references/
│   └── research/
│       ├── dimension-1/        # Research files per dimension
│       ├── dimension-2/
│       └── ...
└── README.md                   # Project overview and status
```

### 7.2 Validate and Package

Run the skill packaging script:
```bash
python3 ~/.claude/skills/skill-creator/scripts/package_skill.py <path/to/skill>
```

### 7.3 Iteration Protocol

After first use, collect:
- Which rules fired correctly vs. incorrectly
- What the user had to correct
- Scenarios the skill couldn't handle

Use these to update reference files and SKILL.md rules. The first version is a hypothesis; real usage is the experiment.

## Reference Files

### references/decomposition-patterns.md
Detailed decomposition patterns with 5+ annotated examples from different domains. Use when designing the orthogonal decomposition in Phase 2.

### references/agent-prompt-template.md
Template for generating dimension-specific agent prompts, with per-dimension customization points. Use in Phase 3 when launching parallel collection agents.

### references/skill-output-template.md
Skeleton template for the final SKILL.md output, with section-by-section guidance. Use in Phase 5 when compiling the decision framework.


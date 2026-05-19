<div align="center">

# Domain Distiller

<p align="center">
  <em>Meta-skill for distilling domain knowledge into decision-capable Claude Code skills</em>
</p>

> *"The next domain you want to master doesn't need to be learned from scratch."*

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Skill-blueviolet)](https://claude.ai/code)
[![Skills](https://img.shields.io/badge/skills.sh-Compatible-green)](https://skills.sh)

<br>

**Domain Distiller turns scattered knowledge into structured, decision-ready Claude Code skills — through orthogonal decomposition, parallel multi-agent research, and cross-source verification.**

<br>

[Install](#install) · [How It Works](#how-it-works) · [Decomposition Patterns](#the-5-decomposition-patterns) · [When NOT to Use](#when-not-to-use)

<br>

[中文版](README_CN.md)

</div>

---

## Install

```bash
npx skills add UWhisper/domain-distiller
```

Then in Claude Code:

```
> distill travel planning into a skill
> turn personal knowledge management into a skill
> distill "how to choose consumer products" into a skill
```

After distillation, invoke the skill directly:

```
> plan a 7-day Tokyo trip with a $1500 budget
> help me decide between Obsidian and Logseq
> which laptop should I buy for development?
```

---

## Skills Distilled with Domain Distiller

Domain Distiller has been used to produce multiple verified skills:

| Skill | Domain | Install |
|------|---------|---------|
| 🔥 **Travel Guide** | Travel planning with 5-dimension research | `npx skills add UWhisper/travel-guide` |
| 🔥 **PKM Advisor** | Personal knowledge management tool selection | `npx skills add UWhisper/pkm-advisor` |
| **Consumer Decision** | Product comparison with constraint modeling | `npx skills add UWhisper/consumer-decision` |

Each skill includes structured decision frameworks, taboo/risk filtering, and user preference memory. Quality verified against bare Claude baselines.

---

## How It Works

Input a domain name. Domain Distiller runs a 7-phase pipeline:

**1. Domain Audit** — Is this domain worth distilling? Map the information topology. Identify signal sources and their reliability. Skip domains where bare Claude already excels.

**2. Orthogonal Decomposition** — Split the domain into 3–5 mutually independent dimensions. This is the core insight: true independence enables parallel research without redundant output.

**3. Parallel Collection** — Launch one agent per dimension. All research runs concurrently. Each agent archives its findings independently.

**4. Cross-Source Verification** — Weight signals by source quality. Resolve contradictions between sources. Deduplicate overlapping findings.

**5. Decision Framework** — Extract 50+ atomic, falsifiable, domain-specific rules. Build decision trees. Compile into a structured SKILL.md.

**6. Validation** — 50-rule completeness test. Side-by-side comparison against bare Claude. Edge case stress testing. Must beat baseline on specificity, accuracy, structure, safety, and personalization.

**7. Packaging** — Finalize structure. Ship as an installable skill.

Full methodology in `references/decomposition-patterns.md` and `references/agent-prompt-template.md`.

---

## The 5 Decomposition Patterns

The hardest and most important step is splitting the domain into independent dimensions. Choose from 5 proven patterns:

| Pattern | Structure | When to Use | Example |
|---------|-----------|-------------|---------|
| **Context × Action** | User situation × What to do | Recommendation problems | Travel planning (budget × destination × season) |
| **Rule × Resource** | Constraints × Options | Constrained choice | PKM tools (requirements × available tools) |
| **Principle × Practice** | Theory × Application | Skill-building | Learning a framework (concepts × exercises) |
| **Static × Dynamic** | Fundamentals × Time-sensitive | Fast-changing domains | Crypto investing (core principles × market data) |
| **Supply × Demand** | Provider × Consumer | Two-sided matching | Job hunting (candidate profile × market openings) |

---

## Key Design Decisions

**50-rule minimum** — A forcing function that pushes beyond surface-level knowledge. If you can't extract 50 atomic, falsifiable, domain-specific rules, the domain may not need a dedicated skill.

**Parallel agents with fallback** — Agents launch in parallel for speed. When WebSearch is unavailable, the pipeline falls back to training data with explicit source labeling — transparent about what it does and doesn't know.

**Constraint dimension is mandatory** — Every domain has taboos, common mistakes, and things to avoid. This dimension is almost always the highest-ROI part of the distillation.

**Validation against bare Claude** — The skill must produce measurably better output across 5 axes: specificity, accuracy, structure, safety, and personalization. If it doesn't beat the baseline, it's not done.

---

## When NOT to Use

Not every domain needs a skill. Run the **LLM Baseline Test** first:

1. Ask bare Claude a representative question from the domain
2. Rate the response on specificity, accuracy, structure, actionability, and safety
3. If it's already excellent on all 5 — distillation's marginal value comes only from timeliness, structured decisions, and preference memory

If the domain lacks all three additional value dimensions, a pure prompt may suffice.

---

## Repository Structure

```
domain-distiller/
├── SKILL.md                              # The skill itself (loaded by Claude Code)
├── README.md                             # This file
├── README_CN.md                          # Chinese version
├── references/
│   ├── decomposition-patterns.md         # 5 patterns with multi-domain examples
│   ├── agent-prompt-template.md          # Dimension-specific prompt generator
│   └── skill-output-template.md          # SKILL.md skeleton with section guidance
├── assets/
└── scripts/
```

---


## License

MIT

---


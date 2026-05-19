# Domain Distiller

> Turn any knowledge domain into a structured, decision-capable Claude Code skill — through orthogonal decomposition, parallel multi-agent research, and cross-source verification.

Domain Distiller is a **meta-skill**: a repeatable 7-phase methodology for distilling scattered domain knowledge into high-quality Claude Code skills. It was generalized from multiple successful skill distillations across diverse domains — including travel planning, personal knowledge management, and consumer decision support — and works for any domain with external signal sources.

## The Problem

Claude knows a lot, but raw LLM knowledge has sharp limits:

- **Generic** — plausible-sounding but unspecific advice
- **Unstructured** — stream of consciousness, not decision trees
- **Unsafe** — no systematic taboo/risk filtering
- **Stateless** — no user preference memory across sessions
- **Stale** — training cutoff means missing time-sensitive information

A well-distilled skill transforms this into specific, structured, verified, personalized output.

## The Methodology

```
Phase 1: Domain Audit        →  Is distillation worth it? Map signal topology.
Phase 2: Orthogonal Decomposition  →  Split domain into 3–5 independent dimensions.
Phase 3: Parallel Collection  →  Launch one agent per dimension. Research concurrently.
Phase 4: Cross-Source Verification →  Weight signals, resolve contradictions, deduplicate.
Phase 5: Decision Framework  →  Extract 50+ rules. Build decision trees. Compile SKILL.md.
Phase 6: Validation          →  50-rule test. Baseline comparison. Edge case stress test.
Phase 7: Packaging           →  Finalize structure. Ship.
```

### Core Insight: Orthogonal Decomposition

The hardest and most important step. Split the domain into dimensions that are **mutually independent** — information in one dimension does not overlap with another. This enables true parallel research without redundant output.

Choose from 5 proven decomposition patterns:

| Pattern | Structure | When to Use |
|---------|-----------|-------------|
| **Context × Action** | User situation × What to do | Recommendation problems |
| **Rule × Resource** | Constraints × Options | Constrained choice problems |
| **Principle × Practice** | Theory × Application | Learning/skill-building domains |
| **Static × Dynamic** | Stable fundamentals × Time-sensitive | Fast-changing domains |
| **Supply × Demand** | Provider × Consumer | Two-sided matching problems |

## Key Design Decisions

**50-rule minimum** — A forcing function that pushes beyond surface-level knowledge into real domain nuance. If you can't extract 50 atomic, falsifiable, domain-specific rules, the domain may not need a dedicated skill.

**Parallel agents with fallback** — Agents launch in parallel for speed, but the methodology handles the case where WebSearch is unavailable by falling back to training data with explicit labeling.

**Constraint dimension is mandatory** — Every domain has taboos, common mistakes, or things to avoid. This dimension is almost always the highest-ROI part of the distillation.

**Validation against bare Claude** — The skill must produce measurably better output on specificity, accuracy, structure, safety, and personalization. If it doesn't beat the baseline, it's not done.

## Repository Structure

```
domain-distiller/
├── SKILL.md                              # The skill itself (loaded by Claude Code)
├── README.md                             # This file
├── references/
│   ├── decomposition-patterns.md         # 5 patterns with multi-domain examples
│   ├── agent-prompt-template.md          # Dimension-specific prompt generator
│   └── skill-output-template.md          # SKILL.md skeleton with section guidance
├── assets/                               # Visual assets (placeholder)
└── scripts/                              # Packaging scripts (placeholder)
```

## Quick Start

1. Load the skill: `/domain-distiller` or mention "distill X into a skill"
2. The skill walks you through Phase 1 (Domain Audit) — define the boundary, map signals, assess whether distillation is worth it
3. Phase 2 (Orthogonal Decomposition) produces a dimension map for your approval
4. Phases 3–6 execute the research and compilation pipeline
5. Phase 7 packages the final skill

## When NOT to Use

Not every domain needs a skill. Run the **LLM Baseline Test** first: ask bare Claude a representative question from the domain. If the response is already excellent on specificity, accuracy, structure, actionability, and safety, distillation's marginal value comes only from timeliness, structured decisions, and preference memory. If the domain lacks all three, a pure prompt may suffice.

## License

MIT

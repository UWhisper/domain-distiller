# Agent Prompt Template

> Reference for Phase 3 of the domain-distiller methodology.
> Use this to generate dimension-specific prompts for parallel collection agents.

## Template

Copy this template, replace `[PLACEHOLDERS]`, and send one agent per dimension.

```
You are a research assistant. Your task is to collect knowledge about [DIMENSION_NAME] for the domain of [DOMAIN_NAME].

Search for the following topics using WebSearch (mix languages as appropriate for the domain):
1. [SPECIFIC_TOPIC_WITH_KEYWORDS]
2. [SPECIFIC_TOPIC_WITH_KEYWORDS]
3. [SPECIFIC_TOPIC_WITH_KEYWORDS]
... (5-10 topics, be specific about what to search)

After searching, organize all findings into structured Markdown files. Write to:
- [OUTPUT_FILE_PATH_1]
- [OUTPUT_FILE_PATH_2] (if this dimension needs multiple files)

Format requirements:
- Use tables for structured rules/data with columns: [COLUMN_1], [COLUMN_2], [COLUMN_3], ...
- Each rule/data point must include: [REQUIRED_FIELD_1], [REQUIRED_FIELD_2]
- Minimum [N] specific, actionable rules/data points
- For each rule, note the information source (specific platform, or "基于训练数据，待后续核实" if from training data)

[DOMAIN_SPECIFIC_INSTRUCTIONS]

Do NOT write code. Only do research and file writing.
```

## Per-Dimension Customization

### For Rule/Constraint Dimensions (culture, taboos, regulations)

Add to domain-specific instructions:
```
- Rate each rule by severity: 禁忌/必知/建议/可选
- Include the reasoning behind each rule, not just the rule itself
- Note regional or contextual variations
- Include "破解方法" (mitigation strategies) for rules that have exceptions
```

### For Resource/Catalog Dimensions (products, options, categories)

Add to domain-specific instructions:
```
- Include price ranges or equivalent resource metrics
- Note which options are best for which scenarios/contexts
- Include "safety" ratings or beginner-friendly markers
- List both mainstream and niche/creative options
```

### For Temporal/Occasion Dimensions (calendars, timelines)

Add to domain-specific instructions:
```
- Organize chronologically (calendar format preferred)
- Tag each entry with priority level (必做/建议做/可选)
- Include typical budgets or resource requirements
- Note dependencies (e.g., "需要提前X天准备")
```

### For Gender/Persona Split Dimensions

Add to domain-specific instructions:
```
- Use comparison tables to highlight differences
- Include specific "翻车案例" (failure cases) for each side
- Note where common stereotypes are wrong or misleading
```

## Fallback Instructions

If agents report that WebSearch is unavailable, send this follow-up:

```
Proceed with your training data. Write the files directly using the Write tool. Label all content "基于训练数据中的通用知识，待后续核实" (for Chinese domains) or "Based on training data, pending verification" (for English domains). Do NOT wait for WebSearch to become available. Write the files NOW.
```

## Agent Count Guidelines

| Domain complexity | Recommended agents | Notes |
|------------------|-------------------|-------|
| Simple (1-2 dimensions) | 1-2 agents | Can often be done inline without parallel agents |
| Medium (3-4 dimensions) | 3-4 agents | Standard case; launch all in parallel |
| Complex (5+ dimensions) | 4-5 agents max | Beyond 5 dimensions, consider splitting into sub-domains |

## Generic Agent Prompt Example

This is a filled-out example for a "cultural constraints" dimension in a food recommendation domain:

```
You are a research assistant. Your task is to collect knowledge about dietary restrictions and food culture for restaurant recommendations in China.

Search for the following topics (mix languages as appropriate):
1. Common dietary restrictions in China - religious, health, and lifestyle
2. Regional food taboos and preferences across Chinese provinces
3. Dining etiquette rules that affect restaurant choice
4. Food allergy prevalence and handling in Chinese restaurants
5. Cultural preferences around spice levels, ingredients, and cooking methods

After searching, organize all findings into structured Markdown files. Write to:
- /path/to/references/research/culture/dietary-restrictions.md
- /path/to/references/research/culture/dining-etiquette.md

Format requirements:
- Use tables with columns: Rule, Applicable Scenario, Severity (Absolute/Strong/Preference), Source
- Each rule must include: rule description, reason, applicable scenario, severity
- Minimum 15 specific, actionable rules per file
- Label sources (e.g., "government guideline", "authoritative cookbook", or "based on general cultural knowledge, pending verification")

Do NOT write code. Only do research and file writing.
```

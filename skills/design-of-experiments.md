---
name: design-of-experiments
description: Design of Experiments (DOE / תכנון ניסויים) and ANOVA for Shkhina experimentation — A/B testing demo variants, prompt-engineering ablations, hyperparameter studies, factorial designs, blocking, response surface methodology. Sourced from BGU IE&M elective 364-1-1071. Use when comparing multiple variants (post hooks, demo flows, model configs, message templates), running multi-factor experiments, controlling for nuisance variables, or testing if a difference is real vs noise.
---

# Design of Experiments (תכנון ניסויים) & ANOVA

The science of running experiments that actually answer your question — without fooling yourself with random noise.

## When to use
- "A/B test this LinkedIn hook vs the old one"
- "Compare 3 prompt variants for the Editor agent"
- "Test 5 model temperatures × 3 max_tokens configs — minimum runs?"
- "Did demo conversion change because of the new copy or because of seasonality?"
- "Hyperparameter sweep — but I can only afford 12 runs"
- "Is my Sharpe improvement real, or did I just get lucky?"

## Core methods

### One-factor experiments (basic A/B)
- **Sample size** — power analysis: n ≈ 16/(effect size)² for 80% power, α=0.05
- **Test:** two-sample t-test (continuous) or χ² (proportion)
- **Common Shkhina effect sizes:** "small" 0.2, "medium" 0.5 (need ~64), "large" 0.8 (need ~25)

### Multi-factor (factorial designs)
- **Full factorial (2^k):** test all combinations of k factors at 2 levels each
- **Fractional factorial (2^(k-p)):** test 1/2^p of combinations, accept some confounding — when full is too expensive
- **Plackett-Burman:** screen many factors quickly to find the few that matter

### ANOVA (Analysis of Variance)
Tests whether group means differ. Multi-factor variant tests interactions too.
- **One-way ANOVA:** k groups, one factor → F-test
- **Two-way ANOVA:** 2 factors + interaction
- **Randomized Block Design:** control for known nuisance (week-of-year, prospect segment)

### Response Surface Methodology (RSM)
For continuous factors with optimum somewhere — fit quadratic surface, find max/min via gradient. Used for hyperparameter optimization.

### Blocking & randomization
- **Block** what you can't control but know matters (day-of-week, batch ID, prospect segment) → removes that variance from "noise"
- **Randomize** within blocks → eliminates lurking variable bias
- **Replication** → estimate within-condition variability

## Shkhina-specific applications

### LinkedIn post variants
- Factors: hook variant (3), CTA variant (2), image vs no-image (2) = 12 conditions
- Block by: posting hour, day-of-week
- Response: views, reactions, comments, profile visits
- ANOVA → main effects + interactions

### Demo conversion experiment
- Factors: demo entry copy (2), CTA placement (2), pre-demo email vs none (2) = 8 conditions
- Sample: 25-50 prospects per condition
- Response: conversion rate
- 2-way + interaction ANOVA

### Prompt-engineering ablation
- Factors: system prompt length (3), few-shot examples (3), temperature (3) = 27 → reduce via fractional factorial
- Response: agent quality score (per `agent-evals`)
- Run on held-out eval set for unbiased estimate

### Pricing experiment (with care)
- Variants: $X / $Y / $Z anchor in proposal
- Block: prospect segment, deal size class
- Response: close rate, deal size
- Caveat: ethical issues + small N → bayesian methods preferable

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Design experiment for Shkhina question: [question]
   1. Identify factors + levels
   2. Pick design (full / fractional / Plackett-Burman / RSM)
   3. Compute required sample size for desired power
   4. Identify blocking factors + nuisance variables
   5. Specify analysis (which ANOVA, post-hoc tests)
   6. Output: experiment-plan.md + Python script for analysis"
- Tools: Bash (scipy.stats / statsmodels), Write
```

## Skill chain
- Pairs with [`agent-evals`](../agent-evals/SKILL.md) (eval = experiment with response variable = score)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (DOE for DMAIC's Improve phase)
- Pairs with [`simulation-modeling`](../simulation-modeling/SKILL.md) (Monte Carlo for power analysis when analytics intractable)
- Pairs with [`afml-methodology`](../afml-methodology/SKILL.md) (DSR, deflated Sharpe = formal hypothesis tests on experiments)
- Pairs with [`scoring-awareness`](../scoring-awareness/SKILL.md) (post variants → DOE)

## Course origin
- BGU 364-1-1071 — תכנון ניסויים ו-ANOVA (elective)
- Builds on: 364-1-1041 Probability, 364-1-1291 Hypothesis Testing, 364-1-1061 Linear Regression

## References
- `references/sample-size-calculator.md` — power formulas + Python
- `references/factorial-design-templates.md` — 2^k, 2^(k-p), Plackett-Burman matrices
- `references/anova-recipes.md` — Python statsmodels code
- `references/blocking-checklist.md` — common Shkhina nuisance variables
- `references/rsm-template.md` — response surface workflow

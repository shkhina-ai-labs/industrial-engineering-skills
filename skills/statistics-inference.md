---
name: statistics-inference
description: Foundational statistics & inference for Shkhina — probability distributions, estimation (MLE, MoM), hypothesis testing (t-test, χ², Mann-Whitney, bootstrap), confidence intervals, linear/logistic regression, multiple-comparison correction. Consolidates BGU IE&M mandatory courses 364-1-1041 (הסתברות), 364-1-1291 (אמידה ומבחני השערות), 364-1-1061 (מודלים ברגרסיה לינארית). Use when claims need statistical backing — A/B test significance, model performance comparison, survey results, drift detection, anomaly thresholds, sample-size sufficiency.
---

# Statistics & Inference (הסתברות, אמידה, רגרסיה)

The foundation under almost every other IE skill. Replaces "I think this number went up" with "the difference is 3.2σ, p=0.001, here's the 95% CI".

## When to use
- "Demo conversion went from 8% to 12% — real or noise?"
- "Onkolos rolling Sharpe dropped — should I shut down the strategy?"
- "Impilo accuracy on 13 cases — is 11/13 vs 8/13 a real improvement?"
- "Ran 50 prompt variants — which winners are real vs noise (multiple comparisons)?"
- "Linear model: which features actually predict demo conversion?"
- "How many samples do I need to detect a 5% effect?"

## Core methods

### Distributions (when each)
| Distribution | Use for |
|---|---|
| Normal (Gaussian) | Continuous, symmetric, CLT applies |
| Bernoulli / Binomial | 0/1 outcomes (conversion, win/loss) |
| Poisson | Counts of independent events (alerts/day) |
| Exponential | Wait times (memoryless) |
| LogNormal | Positive, right-skewed (deal size, latency) |
| Beta | Bounded 0-1 (conversion rate prior) |
| Gamma | Positive, flexible shape (cycle time) |
| t / χ² / F | Test statistics |

### Estimation
- **Sample mean / proportion** — point estimate
- **Maximum Likelihood Estimation (MLE)** — argmax L(θ|data)
- **Method of Moments** — match sample moments to theoretical
- **Confidence interval:** point ± z × SE (z=1.96 for 95%)
- **Bootstrap CI:** resample with replacement → percentile CI (works without distribution assumption)

### Hypothesis testing decision tree
```
Continuous data, 2 groups, normal-ish → two-sample t-test (or Welch's if variances differ)
Continuous data, 2 groups, non-normal → Mann-Whitney U
Continuous data, 3+ groups → ANOVA (per `design-of-experiments`)
Continuous, paired (before/after) → paired t-test or Wilcoxon
Proportion, 2 groups → χ² test or Fisher's exact (small N)
Counts, expected vs observed → χ² goodness-of-fit
Distribution comparison → Kolmogorov-Smirnov
Time-to-event → log-rank test
```

### Critical gotchas
- **p-value ≠ probability hypothesis is true** (it's P(data|null))
- **Statistical significance ≠ practical significance** (huge N → tiny effects significant)
- **Multiple comparisons:** if you test 20 things at α=0.05, you expect 1 false positive. Correct via Bonferroni (α/k) or Benjamini-Hochberg (FDR per `afml-methodology`)
- **p-hacking** — pre-register hypotheses, don't fish

### Regression
- **Linear (OLS):** continuous y, linear in parameters
- **Logistic:** binary y, log-odds linear
- **Multiple regression:** multiple predictors, watch multicollinearity (VIF > 10 = problem)
- **Diagnostics:** residual plots (linearity), QQ plot (normality), Breusch-Pagan (homoscedasticity), Durbin-Watson (autocorrelation)
- **Coefficient interpretation:** unit change in x → β unit change in y, holding others constant

## Shkhina-specific applications

### A/B test significance
- Per `design-of-experiments` workflow
- Use proportion z-test or χ² for conversion-rate comparisons
- Always report: estimated lift + 95% CI + p-value + practical-significance threshold

### Demo accuracy comparison (Impilo case)
- 13 Tzachi cases, V8 = 11/13, candidate = 8/13
- McNemar's test (paired binary) → significance of difference
- Beta(11,2) vs Beta(8,5) posterior — Bayesian alternative

### Onkolos drift detection (methodology only, 🔒)
- Rolling Sharpe distribution under null
- Detect drift via cumulative-sum (CUSUM) or Western Electric rules per `quality-engineering`
- Pair with deflated Sharpe ratio (`afml-methodology`)

### Prompt-variant winner selection (multiple comparisons)
- Run 50 variants, take top-1 → likely overfit
- Apply Bonferroni or Benjamini-Hochberg
- Better: hold out 30% as confirmation set

### Sample-size pre-checks
- Power formula: n ≈ 16/(effect size)² for 80% power, α=0.05
- Pair with `simulation-modeling` for power simulation when analytic form intractable

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run statistical analysis for Shkhina question: [question]
   1. Identify data type + distribution assumption
   2. Pick appropriate test (decision tree above)
   3. Compute test statistic, p-value, effect size, 95% CI
   4. Apply multiple-comparison correction if relevant
   5. Translate to plain-language conclusion + caveats
   6. Suggest follow-up if marginal
   Output: stats-report.md + Python code"
- Tools: Bash (scipy.stats, statsmodels), Write
```

## Skill chain
- Foundation under [`design-of-experiments`](../design-of-experiments/SKILL.md), [`quality-engineering`](../quality-engineering/SKILL.md), [`simulation-modeling`](../simulation-modeling/SKILL.md), [`operations-research`](../operations-research/SKILL.md), [`agent-evals`](../agent-evals/SKILL.md), [`afml-methodology`](../afml-methodology/SKILL.md)
- Pairs with [`process-mining`](../process-mining/SKILL.md) (statistical conformance)

## Course origin (consolidated)
- BGU 364-1-1041 (3.5 נק"ז) — הסתברות (Probability)
- BGU 364-1-1291 (3.5 נק"ז) — אמידה ומבחני השערות (Estimation & Hypothesis Testing)
- BGU 364-1-1061 (3.5 נק"ז) — מודלים ברגרסיה לינארית (Linear Regression Models)

## References
- `references/distribution-cheatsheet.md`
- `references/test-decision-tree.md`
- `references/sample-size-formulas.md`
- `references/multiple-comparison-correction.md`
- `references/regression-diagnostics-checklist.md`
- `references/scipy-statsmodels-recipes.md`

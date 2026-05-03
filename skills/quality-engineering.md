---
name: quality-engineering
description: Quality engineering and process improvement (הנדסת איכות) for Shkhina services — DMAIC for systematic improvement, Statistical Process Control (SPC) for monitoring demos/agents/deploys, FMEA for risk analysis, root-cause analysis (5 Whys, fishbone, Pareto), control charts. Sourced from BGU IE&M course 364-1-1091 (Quality Engineering & Process Improvement). Use when something keeps breaking, when quality is drifting, when launching a new service that needs guard-rails, or when a vendor/supplier needs a quality contract.
---

# Quality Engineering (הנדסת איכות)

The discipline of **making things consistently good, then proving it with data**. Six Sigma's superpower: separating signal from noise so you fix real problems, not phantoms.

## When to use
- "Demo conversion dropped this month — real problem or random noise?"
- "Onkolos win rate is variable — when do I act vs ignore?"
- "Impilo accuracy on Tzachi cases — what counts as a regression?"
- "Vendor X had a 4hr outage last week — is this acceptable?"
- "Setting up SLA for a new client — what to monitor?"
- "Demo broke for 3 prospects in a row — root cause?"
- "Six Sigma project for the outreach pipeline"

## DMAIC — the universal improvement loop

The Six Sigma backbone. Apply to ANY process you want to improve:

| Phase | What you do | Outputs |
|---|---|---|
| **D**efine | Frame the problem precisely. Who hurts? What's the gap from goal? | Problem statement, business case, scope |
| **M**easure | Quantify current state. Baseline metrics, sample data. | Baseline KPI, measurement system check (Gage R&R if it matters) |
| **A**nalyze | Find root causes (NOT symptoms). Use 5 Whys, fishbone, Pareto. | Root-cause hypotheses + statistical evidence (correlation, regression, t-test) |
| **I**mprove | Test a fix. Small experiment, measure, compare. | Validated change + before/after data |
| **C**ontrol | Lock in the gain. SPC chart, ownership, escalation triggers. | Control plan, control chart, alert rules |

**Rule:** never skip Measure or Analyze to jump to Improve. Most fixes fail because they treated a symptom.

## Statistical Process Control (SPC)

Distinguishes **common cause** variation (noise — leave alone) from **special cause** (signal — investigate).

### Control charts (which one for what)
| Chart | Data type | Use for |
|---|---|---|
| X̄-R chart | Continuous, subgroups | Demo response time, model accuracy on a held-out set |
| I-MR chart | Continuous, single observations | Daily revenue, daily lead count |
| p-chart | Proportion (0/1) | Demo success rate, deploy success rate |
| c-chart | Count of defects | Bugs/week, complaints/month |
| u-chart | Defects per unit | Errors per output, alerts per server |

### Western Electric rules — when a point is "special cause"
1. 1 point > 3σ from centerline
2. 9 points in a row on same side of centerline
3. 6 points in a row trending up or down
4. 14 points in a row alternating up/down
5. 2 of 3 consecutive points > 2σ on same side

If any rule fires → STOP, investigate the cause, do NOT just adjust the chart.

### Process capability — Cp / Cpk
- **Cp** = (USL - LSL) / (6σ) — process spread vs spec spread (assumes centered)
- **Cpk** = min((USL-μ)/(3σ), (μ-LSL)/(3σ)) — accounts for off-center
- Rules: Cpk ≥ 1.33 = capable; ≥ 1.67 = highly capable; < 1 = incapable

## FMEA (Failure Mode & Effects Analysis)

Proactive risk analysis BEFORE launch. For each potential failure:

| Column | What |
|---|---|
| Process step | What part of the process |
| Potential failure | What could go wrong |
| Effect | What the customer/system feels |
| Severity (S) | 1-10 |
| Cause | Root cause of the failure |
| Occurrence (O) | 1-10 |
| Current controls | What catches it today |
| Detection (D) | 1-10 (10 = won't catch) |
| **RPN** | S × O × D — prioritize by RPN, fix top 20% |
| Action | What to do |

Use FMEA before:
- Launching a new demo / product
- Onboarding a new vendor (paired with [`vendor-management`](../vendor-management/SKILL.md))
- Major infrastructure change
- New client engagement (paired with [`compliance-check`](../compliance-check/SKILL.md))

## Root-cause analysis tools

### 5 Whys
Keep asking "why" until you hit a root cause (usually 5 levels deep). Stop when you reach something actionable + systemic, not a person.

### Fishbone (Ishikawa) diagram
Categorize potential causes into 6M's: **M**an, **M**achine, **M**aterial, **M**ethod, **M**easurement, **M**other Nature (environment).

### Pareto analysis
80/20 rule — chart defects by category, fix the top 20% of categories that cause 80% of pain.

## Shkhina-specific applications

### Demo health monitoring (paired with [`demo-audit`](../demo-audit/SKILL.md))
- p-chart of demo success rate per week
- Western Electric rule fires → run [`demo-audit`](../demo-audit/SKILL.md)
- Track which demos drift most → DMAIC them

### Outreach campaign quality
- I-MR chart on daily reply rate
- DMAIC when reply rate drops: define (which segment?), measure (sample), analyze (message variant? time-of-day? prospect quality?), improve (test variant), control (SPC + auto-rotate)

### Agent reliability (Shkhina, BizDev, Poster)
- c-chart on errors per day
- FMEA before deploying agent changes — what could go wrong, what's RPN
- Cpk calculation on response latency vs SLA

### Onkolos strategy quality (methodology only, 🔒 specifics)
- I-MR chart on rolling Sharpe per strategy
- Western Electric rules → re-evaluate strategy
- Pairs with AFML's deflated Sharpe (formal hypothesis test for Sharpe drift)

### Vendor SLA enforcement
- Track each vendor against documented SLA
- p-chart on vendor uptime
- FMEA → contractual remedies in [`contract-drafting`](../contract-drafting/SKILL.md)

## Sub-agent leverage

For full DMAIC on a real Shkhina problem:

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run DMAIC on Shkhina problem: [problem statement]
   Step 1 (Define): write 1-paragraph problem statement, name the hurt
   Step 2 (Measure): identify 3 KPIs to baseline; specify how to collect 30 data points
   Step 3 (Analyze): apply 5 Whys + fishbone; rank root causes by data
   Step 4 (Improve): propose 1 small change with measurable hypothesis
   Step 5 (Control): design the control chart + alert rules
   Return: structured DMAIC report"
- Tools: WebSearch (for benchmark / industry SPC norms), Read (for prior data)
```

For SPC chart implementation: pairs with `data-scientist` skill for plotting.

## Skill chain
- Pairs with [`operations-research`](../operations-research/SKILL.md) (process optimization, capacity)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (when DMAIC's Improve step has multi-criteria decisions)
- Feeds [`vendor-management`](../vendor-management/SKILL.md) (FMEA → vendor SLA)
- Feeds [`compliance-check`](../compliance-check/SKILL.md) (audit-grade quality records)
- Pairs with [`agent-evals`](../agent-evals/SKILL.md) (eval drift = SPC)

## Skill manifest
- BGU 364-1-1091 (3.5 נק"ז) — Quality Engineering & Process Improvement
- Builds on: 364-1-1041 Probability, 364-1-1291 Estimation & Hypothesis Testing
- Optional companion: 364-1-1071 Design of Experiments & ANOVA (DOE) — TODO `design-of-experiments` skill

## References
- `references/dmaic-template.md` — fillable DMAIC report template
- `references/control-chart-recipes.md` — when to use which chart, sample sizes
- `references/fmea-template.md` — FMEA worksheet
- `references/western-electric-rules.md` — full WE rule set + examples
- `references/spc-python-recipes.md` — code for control charts (matplotlib + scipy)

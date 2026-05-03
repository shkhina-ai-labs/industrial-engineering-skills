---
name: simulation-modeling
description: Discrete-Event Simulation (DES) and Monte Carlo simulation (סימולציה) for Shkhina capacity planning, what-if analysis, and revenue/cost forecasting. Use when an analytical OR model is intractable (complex queueing networks, multi-stage pipelines), when comparing operational scenarios (hire timing, demo capacity, GPU sizing), or when a forecast needs probabilistic ranges instead of point estimates. Sourced from BGU IE&M course 364-1-3091 (סימולציה).
---

# Simulation Modeling (סימולציה)

When the math gets too messy or the system has too many moving parts, **simulate it.** Run thousands of synthetic worlds, look at the distribution of outcomes, decide.

## When to use
- "What's the throughput of my outreach pipeline if I add a hire in 3 months?"
- "If I take 1 more client at $30K, will I miss the Impilo deadline? What's the probability?"
- "How many GPU-hours do I really need for the next quarter?"
- "Revenue forecast for 2026 — what's the 80% confidence band?"
- "Demo capacity — at what prospect-volume do I break?"
- "Compare strategy A vs B under uncertainty — full distributions, not point estimates"

When NOT to use:
- Closed-form analytic answer exists (use [`operations-research`](../operations-research/SKILL.md) — faster + provable)
- 1-2 variables and linear → spreadsheet sensitivity is enough

## Two simulation flavors

### Flavor 1 — Monte Carlo (random sampling)
For: probabilistic forecasts, sensitivity analysis, propagating uncertainty through formulas.

**Workflow:**
1. Identify uncertain inputs and their distributions (revenue per deal, # deals/quarter, costs)
2. Define output metric (annual revenue, profit, deadline date)
3. Sample inputs N times (10,000+), compute output each time
4. Look at output distribution: mean, median, 5th/95th percentile

**Tools:** Python with numpy + scipy.stats. ~30 lines of code per sim.

**Common Shkhina distributions:**
| Variable | Distribution | Why |
|---|---|---|
| Deal close probability per qualified prospect | Beta(α, β) | Bounded 0-1, can be skewed |
| Deal size $ | LogNormal | Bounded > 0, can have fat right tail |
| Time to close (days) | LogNormal or Gamma | Bounded > 0 |
| Hours per engagement (vs estimate) | Triangular(O, M, P) | Matches PERT 3-point |
| Demo conversion rate | Beta | Sample size + prior beliefs |
| Vendor outage frequency | Poisson | Counts of independent events |
| Vendor outage duration | Exponential | Memoryless waits |

### Flavor 2 — Discrete-Event Simulation (DES)
For: queues, pipelines, multi-stage workflows where events happen at distinct times and entities (prospects, jobs, requests) flow through.

**Concepts:**
- **Entity** — what flows (prospect, GPU job, demo request)
- **Resource** — what's consumed (you, GPU, DB connection)
- **Event** — discrete time-stamped occurrence (arrival, service complete)
- **Clock** — simulation time advances event-to-event (not in fixed steps)

**Tools:** Python `simpy` is the standard. AnyLogic / Arena for fancier visual models (overkill for Shkhina).

**Skeleton (simpy):**
```python
import simpy, random
def prospect_lifecycle(env, name, you_resource):
    yield env.timeout(random.expovariate(1/30))  # discovery wait
    with you_resource.request() as req:
        yield req
        yield env.timeout(random.lognormvariate(2, 0.5))  # discovery call
    # ...
env = simpy.Environment()
you = simpy.Resource(env, capacity=1)  # +1 when hire lands
for i in range(50):
    env.process(prospect_lifecycle(env, f'P{i}', you))
env.run(until=180)  # 180 days
```

## Shkhina-specific simulation models

### Model 1 — Outreach pipeline throughput
- Entity: prospect
- Stages: queue → outreach → reply → discovery → SOW → closed-won/lost
- Resource: Yossi (capacity 1, +1 when hire #1 closes)
- Outputs: deals closed per quarter, lost-due-to-wait %, avg cycle time, Yossi utilization
- Decision: at what prospect-volume / hire-timing does the pipeline break?

### Model 2 — GPU capacity (vast)
- Entity: training/inference job (Impilo iteration, ad-factory render, surveillance fine-tune)
- Resource: 4090 (capacity 1)
- Job arrival distribution: Poisson with rate per project
- Service time distribution: LogNormal per job type
- Output: queue length p95, expected wait, utilization
- Decision: when does adding a 2nd GPU pay back?

### Model 3 — Multi-engagement schedule risk
- Entity: engagement deliverable
- Stages: each engagement's WBS leaf nodes (from [`ie-project-management`](../ie-project-management/SKILL.md))
- Resource: Yossi-hours/week
- Sample: actual hours per leaf from triangular distribution
- Output: probability of hitting each engagement's deadline
- Decision: which engagement to renegotiate / push first

### Model 4 — Annual revenue forecast (Monte Carlo)
- Inputs: pipeline by stage with conversion probs (Beta), expected deal size (LogNormal), close timing (Gamma)
- Sample 10,000 paths
- Output: P10, P50, P90 of annual revenue
- Pair with [`engineering-economy`](../engineering-economy/SKILL.md) (TODO) for cost side → profit distribution
- Decision: feed pricing strategy, hiring approval, runway analysis

### Model 5 — Demo health drift (paired with quality-engineering SPC)
- Monte Carlo: assume true demo accuracy = 95%, with daily noise
- How long until a Western Electric rule fires? (false-alarm rate)
- Tune SPC chart parameters via simulation

### Model 6 — Onkolos strategy comparison (methodology only, 🔒 specifics)
- Bootstrap historical returns under different strategy parameters
- Output: distribution of Sharpe, max drawdown, terminal wealth
- Pair with AFML deflated Sharpe (formal tests)

## Standard workflow

```
1. Frame: what's the decision? what metric matters?
2. Pick flavor: Monte Carlo (formula + uncertainty) or DES (entities + queues + resources)
3. List inputs: distribution + parameters per uncertain variable
4. Build model in Python (simpy for DES, numpy for Monte Carlo)
5. Validate against known cases (set inputs to known scenario, check output matches)
6. Run N replications (10K for Monte Carlo, 100+ for DES)
7. Analyze output distribution: mean, median, P5, P95, histogram
8. Sensitivity: vary one input at a time, see which moves the output most
9. Translate result back to operational decision + confidence
```

## Sub-agent leverage

For building a full simulation:

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build simulation for Shkhina: [problem statement]
   Step 1: Frame — decision, metric, scope
   Step 2: Pick flavor (Monte Carlo / DES) with rationale
   Step 3: Specify inputs (distribution + parameters per variable)
   Step 4: Implement Python script (numpy or simpy)
   Step 5: Run + report distribution of outputs
   Step 6: Sensitivity analysis — top 3 inputs that drive the output
   Step 7: Operational recommendation
   Output: model.py + report.md"
- Tools: Bash (to run sim), Write (to save script + report)
```

## Skill chain
- Pairs with [`operations-research`](../operations-research/SKILL.md) (when analytic model is feasible, OR is faster; when not, simulate)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (validate SPC chart parameters via simulation)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (PERT estimates → Monte Carlo critical-path simulation)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (decision tree EMV computed via simulation when analytic too hard)
- Pairs with `data-scientist` skill (visualization, distribution fitting)

## Course origin
- BGU 364-1-3091 (4.0 נק"ז) — סימולציה (Simulation)
- Builds on: 364-1-1041 Probability, 364-1-3061 Stochastic OR

## References
- `references/monte-carlo-template.py` — generic Monte Carlo skeleton (numpy + scipy.stats)
- `references/des-simpy-template.py` — generic DES skeleton (simpy)
- `references/distribution-fitting-recipe.md` — how to pick distributions from sparse data
- `references/validation-checklist.md` — how to validate a simulation before trusting it
- `references/output-analysis-recipes.md` — confidence intervals, ANOVA on sim runs

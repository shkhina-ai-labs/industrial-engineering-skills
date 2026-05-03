---
name: operations-research
description: Operations Research methods (חקר ביצועים) for Shkhina business optimization — linear/integer programming for resource allocation, network optimization for prospect-to-demo matching, queueing theory for outreach throughput, Markov chains for demo conversion funnels, decision trees for negotiation paths. Sourced from BGU IE&M courses 364-1-3051 (Deterministic OR), 364-1-3061 (Stochastic OR), 364-1-3031 (Production Optimization), 364-1-3041 (Algorithms for Production). Use when allocating finite resources, sizing capacity, modeling waiting/queueing systems, or making structured trade-off decisions.
---

# Operations Research (חקר ביצועים)

The IE foundation. **OR turns "I think we should..." into "the optimum given constraints X, Y, Z is...".**

## When to use
- "How should I split my week across 5 clients?" (LP — resource allocation)
- "If I send 50 LinkedIn DMs/day and reply rate is X, what's my queue depth?" (queueing)
- "Which prospect should I pitch which demo?" (assignment / network optimization)
- "How many GPU hours do I need to hit deadline?" (capacity sizing)
- "Should I take Deal A or Deal B?" (decision tree under uncertainty)
- "What's the bottleneck in my prospect→cash pipeline?" (TOC / network analysis)

## The 4 OR families (BGU course mapping)

### Family 1 — Deterministic optimization (LP/IP/Network)
Source: BGU 364-1-3051 (Deterministic OR Models), 364-1-3031 (Production Optimization).

**Use when:** decisions, constraints, and objective are all numerically definable.

| Problem shape | Method | Tool |
|---|---|---|
| Continuous resource split (hours, $) with linear constraints | Linear Programming (LP) | `scipy.optimize.linprog`, `pulp` |
| Yes/no decisions (which clients to take, which servers to keep) | Integer Programming (IP / MILP) | `pulp`, `mip`, `cvxpy` |
| Assignment (N agents to N tasks) | Hungarian algorithm / IP | `scipy.optimize.linear_sum_assignment` |
| Shortest path / max flow / min cut | Network optimization | `networkx` |
| Production scheduling | Job-shop / flow-shop | OR-tools `cp_model` |

**Workflow:**
```
1. Decision variables — what am I choosing? (hours per client, demos to pitch)
2. Objective — what am I maximizing/minimizing? (revenue, cost, time)
3. Constraints — what are the limits? (40 hr/wk, $500/mo API budget, 1 of me)
4. Solve — LP/IP solver
5. Sensitivity analysis — which constraint is binding? where's the slack?
```

### Family 2 — Stochastic models (Queueing / Markov)
Source: BGU 364-1-3061 (Stochastic OR Models).

**Use when:** randomness matters — arrival rates, service times, transitions.

| Problem shape | Method |
|---|---|
| Server with random arrivals + service times | M/M/1 queue (Little's law: L = λW) |
| Multiple servers (you + future hires) | M/M/c queue |
| Demo→lead→deal pipeline with conversion rates | Markov chain (absorbing states = won/lost) |
| Throughput limited by slowest stage | Theory of Constraints (TOC) |

**Key formulas to remember:**
- **Little's Law:** L = λ × W (long-run avg # in system = arrival rate × avg time in system). Universal.
- **M/M/1 utilization:** ρ = λ/μ; if ρ ≥ 1 the queue blows up to infinity
- **M/M/1 avg wait:** W = 1/(μ-λ); explodes as ρ → 1

### Family 3 — Sequencing & scheduling
Source: BGU 364-1-3041 (Algorithms for Production Optimization).

**Use when:** order matters — what to do first, second, third.

| Problem | Method |
|---|---|
| Minimize total time across N tasks on 1 machine | SPT (shortest processing time first) |
| Minimize lateness | EDD (earliest due date first) |
| 2 machines, N jobs | Johnson's rule |
| N machines, complex constraints | OR-tools `cp_model` constraint programming |

### Family 4 — Decision under uncertainty
Source: complements 364-1-4241 (Decision Making — see [`decision-analysis`](../decision-analysis/SKILL.md)).

Decision trees with EMV (expected monetary value), risk-adjusted utility, value of information.

## Shkhina-specific applications

### Outreach throughput as a queue
- Inputs: λ = LinkedIn DMs sent/day, μ = replies you can handle/day, c = number of operators (1 today, +1 if hire #1 made)
- Outputs: queue depth, reply latency, utilization
- Decision: at what λ does a hire pay back? (Little's law + cost of waiting × lost-deal probability)

### Prospect-to-demo assignment
- 5 active prospects × 22 demos = which demo each prospect should see first
- Bipartite matching with weights = expected conversion × deal size
- Solver: `scipy.optimize.linear_sum_assignment`

### GPU capacity sizing on vast
- Fine-tuning jobs queue on the vast 4090
- Job arrivals (Impilo iterations, Compass safety re-runs, Ad-factory videos)
- Decision: M/M/1 utilization gives expected wait → if > target, justify second GPU

### Onkolos position-sizing under constraint
- Max $35/trade, multiple strategies competing for the cash pool
- LP: maximize expected return s.t. capital constraint, max-loss constraint, correlation matrix
- (Methodology only — Onkolos specifics stay 🔒)

### Client-week resource allocation
- 5 clients, 40 hr/week, varying $/hr and deadline pressure
- LP: maximize revenue s.t. hours/client ≤ scope, total ≤ 40, deadlines met
- Re-solve weekly as conditions change

## Workflow template

```
1. Frame: what type? (LP, IP, queue, schedule, decision tree)
2. Decision variables: what are you choosing?
3. Constraints: what limits apply?
4. Objective: what to optimize?
5. Solve with the right tool (Python script or hand calc)
6. Sensitivity check: which constraint binds? what changes the answer?
7. Implement the chosen action + log assumptions for next iteration
```

## Sub-agent leverage

For complex models (multi-period IP, large queueing networks, simulation-coupled OR), spawn a sub-agent:

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build an OR model for [Shkhina problem]:
   1. Identify variables, constraints, objective
   2. Pick the right OR family (LP/IP/queue/schedule)
   3. Implement in Python (scipy, pulp, OR-tools, or networkx)
   4. Run + report optimum + sensitivity analysis
   5. Translate the answer back to operational language
   Constraints: <list>
   Inputs: <list>"
- Tools: Bash (for solver runs), Read/Write (for code)
```

For very large/specialized problems, the [`quant-analyst`](../../agents/quant-analyst.md) agent has AFML methodology that overlaps OR (FDR controls = multiple testing, deflated Sharpe = decision under uncertainty).

## Skill chain
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (when objective is multi-criteria)
- Pairs with [`simulation-modeling`](../simulation-modeling/SKILL.md) (when analytic OR model is intractable)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (process optimization → DMAIC pairing)
- Feeds [`ie-project-management`](../ie-project-management/SKILL.md) (resource leveling = OR problem)

## References
- `references/lp-templates.md` — common LP formulations (resource allocation, blending, transportation)
- `references/queueing-cheatsheet.md` — formulas for M/M/1, M/M/c, M/G/1
- `references/bgu-364-1-3051-notes.md` — course notes from Deterministic OR
- `references/bgu-364-1-3061-notes.md` — course notes from Stochastic OR
- `references/python-or-tools-recipes.md` — code recipes for scipy/pulp/OR-tools

## Course origin
- BGU 364-1-3051 (4.5 נק"ז) — Deterministic OR Models
- BGU 364-1-3061 (3.5 נק"ז) — Stochastic OR Models
- BGU 364-1-3031 (4.0 נק"ז) — Optimization for Production Planning
- BGU 364-1-3041 (3.5 נק"ז) — Algorithms for Production Optimization
- Total: 15.5 נק"ז of OR coursework distilled

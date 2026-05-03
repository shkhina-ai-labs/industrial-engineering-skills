---
name: ie-project-management
description: IE-grade project management for Shkhina — CPM/PERT critical path analysis, work breakdown structure (WBS), RACI matrix, resource leveling, earned value management (EVM), risk register. Sourced from BGU IE&M course 364-1-1251 (ניהול פרויקטים). Distinct from agile/dev workflows; this is the analytical PM toolkit for client engagements, multi-week deliverables, and any project with hard dependencies and resource constraints. Use when planning a client SOW, scheduling a complex deliverable, allocating limited time across competing projects, or tracking earned value vs spend.
---

# IE Project Management (ניהול פרויקטים)

The analytical PM toolkit. Where agile says "iterate fast," IE-PM says "let me see your network diagram, your critical path, and your resource histogram before you commit a delivery date."

For consulting work where deadlines are real and Yossi is one resource — this matters more than agile rituals.

## When to use
- "Drafting an SOW for [client] — what's a realistic delivery date?"
- "5 active engagements, 40 hr/week — what's slipping?"
- "Track EVM on the Impilo engagement"
- "Build the WBS for the Compass safety project"
- "Critical path on the Shkhina-website rebuild"
- "Risk register for [vendor] migration"
- "RACI for the multi-stakeholder [client] integration"

## Core tools

### 1. Work Breakdown Structure (WBS)
Decompose deliverable → phases → tasks → activities. Rule: every leaf node has exactly one owner and a clear "done" definition.

```
Engagement (project)
├── Phase 1 — Discovery
│   ├── Stakeholder interviews
│   ├── Data exploration
│   └── Scope confirmation memo
├── Phase 2 — Build
│   ├── Data pipeline
│   ├── Model fine-tune
│   └── Eval suite
├── Phase 3 — Pilot
│   ├── Deploy to staging
│   ├── Client UAT
│   └── Bug-fix cycle
└── Phase 4 — Handoff
    ├── Documentation
    ├── Training session
    └── Maintenance contract
```

Each leaf gets: owner, estimate (h), dependencies, deliverable.

### 2. CPM / PERT — Critical Path
Build a precedence network from the WBS, compute earliest/latest start, find critical path.

| Concept | Formula / definition |
|---|---|
| Earliest start (ES) | max(EF of all predecessors) |
| Earliest finish (EF) | ES + duration |
| Latest finish (LF) | min(LS of all successors) |
| Latest start (LS) | LF - duration |
| Slack / float | LS - ES (or LF - EF). Critical path = activities with 0 slack |

**PERT** adds 3-point estimates per activity (optimistic O, most likely M, pessimistic P):
- Expected: te = (O + 4M + P) / 6
- Variance: σ² = ((P - O) / 6)²
- Project completion is normally distributed around sum of te on critical path

**Practical:** for each activity, ask "best/likely/worst hours". Use PERT te. The critical path tells you which slips kill the deadline.

### 3. Gantt + Resource Histogram
Plot activities on a timeline. Then plot **who** works on **what when**. Spikes above capacity (e.g. > 40 hr/week for Yossi) → resource conflict → must level.

### 4. Resource Leveling
When the resource histogram exceeds capacity:
- **Within slack:** delay non-critical activities to flatten peaks
- **Critical path:** must extend deadline OR add resource OR cut scope
- **Decision rule:** never silently push critical path; surface the choice

### 5. Earned Value Management (EVM)
The 3 EVM numbers (measured at any point in time):
| Metric | What | Formula |
|---|---|---|
| **PV** Planned Value | Budget cost of work scheduled by now | from baseline |
| **EV** Earned Value | Budget cost of work actually completed | %complete × budget |
| **AC** Actual Cost | Money/hours actually spent | from time log |

Derived:
- **CPI** Cost Performance Index = EV / AC. > 1 = under budget; < 1 = over
- **SPI** Schedule Performance Index = EV / PV. > 1 = ahead; < 1 = behind
- **EAC** Estimate at Completion = BAC / CPI (extrapolated final cost)

**Use:** weekly check on every active engagement. If CPI or SPI < 0.85, escalate.

### 6. RACI Matrix
For each WBS leaf, assign: **R**esponsible (does the work), **A**ccountable (signs off, exactly one), **C**onsulted (input), **I**nformed (notified).

Useful for multi-stakeholder engagements (client lead, client tech, Shkhina, vendor).

### 7. Risk Register
| ID | Risk | Probability (1-5) | Impact (1-5) | Score (P×I) | Mitigation | Owner | Trigger |
|---|---|---|---|---|---|---|---|

Top-5 by score = active monitoring. Any score ≥ 15 = mandatory mitigation plan before Go.

## Standard Shkhina engagement template

For a typical 4-8 week client engagement, here's the WBS skeleton (apply [`client-delivery-lifecycle`](../client-delivery-lifecycle/SKILL.md) for the lifecycle phases):

```
Week 1 — Discovery (PV ~25%)
  ├─ Kickoff call (1h, R: Yossi, A: Yossi, I: client lead)
  ├─ Data sample review (4h)
  ├─ Scope memo + acceptance criteria (4h)
  └─ SOW signed (gate)

Week 2-3 — Build (PV ~50% cumulative)
  ├─ Data pipeline (8h)
  ├─ Model/agent build (16h)
  ├─ Eval suite + baseline (8h)
  └─ Internal demo with client (gate)

Week 4 — Pilot (PV ~75% cumulative)
  ├─ Deploy to staging (4h)
  ├─ UAT cycle (8h, R: client, A: Yossi)
  └─ Bug fixes (8h)

Week 5+ — Handoff (PV 100%)
  ├─ Docs (8h)
  ├─ Training session (2h)
  ├─ Maintenance contract signed (gate)
  └─ Final invoice
```

## Cross-portfolio view

When 5 engagements run concurrently, build a **cross-project critical path**:
- For each engagement, identify its critical path
- For each Yossi-week, sum hours across all engagement critical paths
- If sum > 40h, at least one engagement WILL slip → which one?
- Use [`decision-analysis`](../decision-analysis/SKILL.md) (AHP) to decide which slip is most acceptable
- Surface the slip to the affected client BEFORE the deadline arrives

## Sub-agent leverage

For building a full project plan from a SOW or scope statement:

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build IE-grade project plan for: [scope statement]
   Step 1: WBS (3 levels deep)
   Step 2: 3-point estimates per leaf (O/M/P)
   Step 3: Precedence network + CPM critical path
   Step 4: Resource histogram (Yossi-hours/week)
   Step 5: Risk register (top 5)
   Step 6: RACI matrix
   Step 7: PV curve (weekly cumulative)
   Output: project-plan.md"
- Tools: Write (project-plan.md to client folder)
```

For visualization: [`d3-visualization`](../d3-visualization/SKILL.md) or [`canvas-design`](../canvas-design/SKILL.md) for Gantt charts.

## Skill chain
- Pairs with [`client-delivery-lifecycle`](../client-delivery-lifecycle/SKILL.md) (lifecycle phases) — this skill is the analytical layer; that one is the lifecycle layer
- Pairs with [`operations-research`](../operations-research/SKILL.md) (resource leveling = LP problem)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (which engagement gets the limited resource)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (FMEA on critical-path risks)
- Feeds [`contract-drafting`](../contract-drafting/SKILL.md) (delivery dates in SOW must come from CPM)

## Why "ie-" prefix?
Distinguishes from agile/dev `pr` and `feature-dev` skills. This is the analytical PMI/PMBOK + IE blend, not the agile sprint-planning kind.

## Course origin
- BGU 364-1-1251 (3.0 נק"ז) — ניהול פרויקטים (Project Management)
- Augmented with PMBOK 7th edition principles (EVM, RACI, risk register)

## References
- `references/wbs-template.md` — generic WBS skeleton
- `references/cpm-pert-cheatsheet.md` — formulas + worked example
- `references/evm-formulas.md` — CPI/SPI/EAC reference
- `references/raci-template.md` — fillable RACI worksheet
- `references/risk-register-template.md` — fillable risk register
- `references/shkhina-engagement-skeleton.md` — the 4-8 week template above, fillable

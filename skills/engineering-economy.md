---
name: engineering-economy
description: Engineering economics + managerial accounting (כלכלת הנדסה + חשבונאות ניהולית) for Shkhina pricing, deal evaluation, and cost-to-serve analysis. NPV, IRR, payback, equivalent annual cost, ABC (activity-based) costing, contribution margin, break-even, sensitivity analysis. Sourced from BGU IE&M service courses 142-1-3141 (Intro to Economics for IE&M, 3.5 נק"ז) + 681-1-5081 (Financial & Managerial Accounting, 3.0 נק"ז). Use when pricing a new engagement, deciding to take a deal, evaluating a vendor switch, sizing an investment (hire, GPU, infra), or computing the real cost-to-serve of a demo.
---

# Engineering Economy & Managerial Accounting (כלכלת הנדסה)

How to put a number on "is this worth it?". Without this, pricing is gut-feel and deals look bigger than they are.

## When to use
- "What's the actual cost to serve a $20K Impilo-class engagement?"
- "Do I take this deal at $15K or hold for higher?"
- "Should I rent a 2nd GPU for $X/month?"
- "What's the NPV of hiring Sales Operator now vs 6 months out?"
- "Am I underpricing? — break-even on different price points"
- "Vendor A is $X upfront + $Y/year, Vendor B is $Z/month — which is cheaper over 3 years?"
- "Sensitivity: at what client churn rate does the engagement become unprofitable?"

## Core methods

### Time value of money
- **Present Value (PV):** PV = FV / (1+r)^n
- **Net Present Value (NPV):** Σ(cash flow_t / (1+r)^t) — invest if NPV > 0
- **Internal Rate of Return (IRR):** discount rate where NPV = 0; invest if IRR > hurdle rate
- **Payback period:** time to recoup initial investment (ignores time value — use as sanity check only)
- **Equivalent Annual Cost (EAC):** annualized cost of project — use to compare projects with different lifespans
- **Hurdle rate for Shkhina:** ~15-20% (small business risk premium over treasury)

### Cost classification (managerial accounting)
| Type | Definition | Shkhina example |
|---|---|---|
| **Fixed** | Doesn't change with volume | Rent, software subscriptions, fixed salary |
| **Variable** | Scales with output | API tokens per inference, GPU-hours per training |
| **Semi-variable** | Mix | Vast.ai (fixed monthly + per-hour usage) |
| **Direct** | Traceable to a specific output | Hours on Impilo deliverable |
| **Indirect (overhead)** | Shared across outputs | wiki-sync time, infra maintenance |
| **Sunk** | Already spent, irreversible | Past R&D — IGNORE in forward decisions |
| **Opportunity** | What you give up by choosing X | Hours on Client A you can't spend on Client B |

### Activity-Based Costing (ABC)
Traditional costing allocates overhead by labor hours. ABC allocates by activity drivers — more accurate for service businesses.

**Workflow:**
1. List activities (outreach, demo prep, discovery call, build, deploy, support)
2. Identify cost driver per activity (hours, # demos, # API calls, # support tickets)
3. Allocate total overhead per activity per driver unit
4. Sum activities per engagement → true cost-to-serve

### Contribution margin & break-even
- **Contribution margin (CM):** Price − Variable Cost per unit
- **Break-even units:** Fixed Cost / CM
- **Break-even revenue:** Fixed Cost / CM Ratio (where CM Ratio = CM / Price)
- **Operating leverage:** % change in profit / % change in revenue (high = volatile)

### Sensitivity & scenario analysis
- **One-way sensitivity:** vary one input ±20%, see output change
- **Tornado chart:** rank inputs by sensitivity (visual)
- **Scenario:** best / base / worst — compute output for each
- Pair with [`simulation-modeling`](../simulation-modeling/SKILL.md) for full Monte Carlo distributions

## Shkhina-specific applications

### Pricing a new engagement
```
1. Estimate hours (per [`ie-project-management`](../ie-project-management/SKILL.md) WBS)
2. Compute ABC cost: hours × loaded rate + variable costs (API, GPU, vendor) + allocated overhead
3. Add target margin (40-60% for consulting)
4. Check against [`pricing/`](../../../Code/business/sales-marketing/pricing/) tiers
5. Sensitivity: at what hours overrun does margin go negative?
```

### Deal go/no-go
```
1. Project monthly cash flows over engagement life
2. Compute NPV at 18% hurdle
3. Compute IRR
4. Compute payback period
5. Compare to next-best alternative (BATNA from [`negotiation-playbook`](../negotiation-playbook/SKILL.md))
6. Decision: take if NPV > 0 AND IRR > 18% AND no better BATNA
```

### Hire timing analysis
- Cost: salary + benefits + onboarding overhead + equipment
- Benefit: revenue unlock + Yossi-hours freed × hourly value + risk reduction
- NPV over 24 months, varying hire-date scenarios
- Sensitivity on revenue ramp assumptions

### Vendor switch / lock-in cost
- Stay-with-current: ongoing $/month × 36 months, present value
- Switch: migration $ + new vendor $/month × 36 months, present value
- Decision: switch if PV(switch) < PV(stay) AND non-financial factors agree

### Cost-to-serve per demo
- Variable: API tokens per demo session × token cost × monthly sessions
- Fixed allocated: server slice × % usage
- Total: sum / total demo sessions = $/session
- Decision: which demos cost > revenue per lead they generate?

## Sub-agent leverage

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build engineering-economy analysis for Shkhina decision: [decision]
   1. Layout all cash flows (year 0..N), classify fixed/variable/sunk
   2. Compute NPV at 18%, IRR, payback
   3. Sensitivity on top 3 inputs (±20%)
   4. Scenario analysis (best/base/worst)
   5. Compare to BATNA / next-best alternative
   6. Recommendation with confidence + key assumption
   Output: analysis.md + Excel-equivalent CSV"
- Tools: Bash (Python with numpy_financial), Write
```

## Skill chain
- Pairs with [`negotiation-playbook`](../negotiation-playbook/SKILL.md) (deal go/no-go, BATNA pricing)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (cost = hours × rate; from EVM CPI)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (multi-criteria — NPV is one of N criteria)
- Pairs with [`simulation-modeling`](../simulation-modeling/SKILL.md) (Monte Carlo NPV when inputs uncertain)
- Pairs with [`vendor-management`](../vendor-management/SKILL.md) (vendor TCO comparison)
- Pairs with [`business-admin-ops`](../business-admin-ops/SKILL.md) (cost categorization, accounting alignment)

## Course origin
- BGU 142-1-3141 (3.5 נק"ז) — מבוא לכלכלה להנדסת תעשייה וניהול
- BGU 681-1-5081 (3.0 נק"ז) — חשבונאות פיננסית וניהולית

## References
- `references/npv-irr-cheatsheet.md` — formulas + Python snippets
- `references/abc-costing-template.md` — activity-based costing worksheet
- `references/break-even-template.md`
- `references/sensitivity-recipe.md` — tornado charts via Python
- `references/shkhina-loaded-rate.md` — Yossi-hour cost-loaded calculation (TODO — fill from real data)

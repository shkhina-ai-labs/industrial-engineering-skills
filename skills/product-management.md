---
name: product-management
description: High-tech product management (ניהול מוצרי היי-טק) for Shkhina internal products and client deliverables — discovery, MVP framing, roadmapping, prioritization (RICE/ICE/Kano), product-market fit signals, lifecycle management, sunset criteria. Sourced from BGU IE&M elective 364-1-3400. Use when launching a new Shkhina product/demo, prioritizing the backlog across products, deciding to kill a feature/product, or advising clients on their AI product roadmap.
---

# Product Management (ניהול מוצרי היי-טק)

The discipline of deciding **what to build, for whom, why, and when** — and ruthlessly killing the rest. For Shkhina with 22 demos + multi-product portfolio, this is critical.

## When to use
- "Should we build feature X next?"
- "Demo Y has zero traffic — kill it?"
- "Roadmap for Impilo for next quarter"
- "Client wants 5 features — which should be MVP?"
- "Is this product idea worth a paid pilot?"
- "PMF signal check — are we there yet?"

## Core methods

### Discovery (continuous, not one-shot)
- **Customer interviews** — find unmet need, not validate solution
- **Jobs-to-be-Done (JTBD):** "When [situation], I want to [motivation], so I can [outcome]"
- **Problem validation BEFORE solution validation**
- **Mom Test** — ask about past behavior, not future intentions

### Prioritization frameworks
| Method | Formula | Best for |
|---|---|---|
| **RICE** | (Reach × Impact × Confidence) / Effort | Backlog ranking with data |
| **ICE** | (Impact + Confidence + Ease) / 3 | Quick scoring, less data |
| **Kano** | Basic / Performance / Delight per feature | Deciding feature ROI |
| **MoSCoW** | Must / Should / Could / Won't (this release) | MVP scoping |
| **Value vs Effort 2×2** | Quick wins / big bets / fill-ins / time sinks | Visual prioritization |
| **Cost of Delay / WSJF** | (Value + Time-Crit + Risk-Reduc) / Job-size | When sequence matters |

Pair with [`decision-analysis`](../decision-analysis/SKILL.md) AHP for multi-criteria.

### MVP framing (Lean Startup)
- **Build → Measure → Learn** loop, minimize time-per-loop
- **MVP** = smallest thing that tests a real hypothesis (not "barely-functional product")
- **Pivot** = change one of (problem, solution, segment); persist on the rest

### PMF signals (Sean Ellis, Rahul Vohra)
- "Very disappointed if you couldn't use it" ≥ 40% → strong PMF
- Net Revenue Retention > 110% (for SaaS)
- Organic growth > paid
- Users explain product to other users

### Roadmapping
- **Now / Next / Later** (3 buckets, not Gantt)
- **Outcome-based** (move metric X by Y) not output-based (ship feature Z)
- **Quarterly themes** + monthly bets + weekly tactics
- Communicate uncertainty: "Now" = high confidence, "Later" = directional

### Lifecycle management
| Stage | Indicators | Action |
|---|---|---|
| **Idea** | Hypothesis, no data | Discovery interviews |
| **MVP** | Built, in test market | Measure leading indicators |
| **PMF search** | Some users, churning | Iterate on problem-solution fit |
| **Growth** | PMF, scaling | Optimize funnel, cost-to-serve |
| **Mature** | Stable revenue, slow growth | Operational excellence, expansion |
| **Decline** | Falling usage / margin | Sunset (per `products/playbooks/deprecation.md`) |

### Sunset criteria (apply quarterly)
Per [`business/products/playbooks/deprecation.md`](../../../Code/business/products/playbooks/deprecation.md):
- 0 traffic 60+ days AND no outreach pipeline
- Replaced by newer demo with overlapping value
- Cost-to-serve > value
- Compliance/safety blocker

## Shkhina-specific applications

### Demo portfolio prioritization (22 demos!)
- Score each via RICE: reach (prospects who'd see), impact (conversion lift), confidence (eval evidence), effort (maintenance)
- Cull bottom quartile per quarter
- Pair with [`demo-audit`](../demo-audit/SKILL.md)

### Internal product roadmap (Shkhina, Poster, BizDev, Wingmain, etc.)
- Quarterly: Now/Next/Later per product
- Outcome metric per product (e.g., Poster: posts ≥ 75/100 weekly; BizDev: qualified leads/week)
- Ruthless about "Later" → most should die there

### Client product strategy advisory
- Apply same frameworks for clients
- Output: their roadmap doc + RICE-scored backlog
- Pair with [`is-strategy-mgmt`](../is-strategy-mgmt/SKILL.md), [`contract-drafting`](../contract-drafting/SKILL.md)

### MVP scoping for new client engagement
- Discovery interviews → JTBD framing
- Smallest thing that tests THE riskiest hypothesis (usually: "will users actually use this?")
- 4-week MVP, not 6-month launch

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run product analysis for Shkhina/client: [product or backlog]
   1. Frame JTBD per main user segment
   2. Score backlog via RICE
   3. Apply Now/Next/Later
   4. PMF signal check (if applicable)
   5. Sunset candidates (if applicable)
   Output: product-analysis.md + prioritized backlog CSV"
```

## Skill chain
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (RICE = simplified MCDM)
- Pairs with [`offer-creation`](../offer-creation/SKILL.md) (offer = packaged product value)
- Pairs with [`engineering-economy`](../engineering-economy/SKILL.md) (NPV per product)
- Pairs with [`demo-audit`](../demo-audit/SKILL.md) (demo health = product health)
- Pairs with [`is-strategy-mgmt`](../is-strategy-mgmt/SKILL.md) (product roadmap = IS strategy execution)
- Pairs with [`design-of-experiments`](../design-of-experiments/SKILL.md) (validate product hypotheses)

## Course origin
- BGU 364-1-3400 — ניהול מוצרי היי-טק (High-Tech Product Management, elective)

## References
- `references/rice-template.md`
- `references/jtbd-template.md`
- `references/now-next-later-template.md`
- `references/pmf-survey-template.md`
- `references/sunset-criteria.md` (mirrors products/playbooks/deprecation.md)

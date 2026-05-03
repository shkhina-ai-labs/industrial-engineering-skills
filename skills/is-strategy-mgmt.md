---
name: is-strategy-mgmt
description: IS strategy & management (אסטרטגיה וניהול של מערכות מידע) — IT governance, IS strategy alignment with business strategy, COBIT/ITIL frameworks, IT portfolio management, IS investment justification, IS organization structure. Sourced from BGU IE&M course 364-1-1911. Use when advising clients on IS strategy, designing Shkhina's own IS roadmap, building an IT governance argument for a deal, or making the "should we build / buy / partner" call.
---

# IS Strategy & Management (אסטרטגיה וניהול של מערכות מידע)

The strategic layer above [`is-analysis-design`](../is-analysis-design/SKILL.md). Where IS analysis says "how to build it right", IS strategy asks "should we build it at all, and how does it fit the business".

## When to use
- "Client asks: AI strategy for next 24 months — what's the framework?"
- "Build vs buy vs partner for [capability]?"
- "How to structure a small IT/AI org?"
- "Justify IS investment to client CFO"
- "Roadmap a digital-transformation engagement"
- "IT governance for a regulated client"

## Core methods

### Business-IT alignment (Henderson-Venkatraman SAM)
Four domains: business strategy / IT strategy / org infrastructure / IT infrastructure. Two cross-perspectives:
- **Strategy execution** — business strategy drives IT (typical)
- **Technology potential** — IT capability creates new business strategy (AI consultancy POV)

### IS strategy frameworks
- **Porter's Value Chain** — where in the chain does IS create value?
- **5-Forces** — IS as defensive/offensive moat (already in `analysis/business/porter-five-forces`)
- **McFarlan Strategic Grid** — Support / Factory / Turnaround / Strategic quadrants per system

### IT governance (COBIT / ITIL summarized)
- **Decision rights** — who decides (architecture, infra, apps, biz process)
- **Investment review board** — gate for IT spend > threshold
- **Service management (ITIL)** — incident / problem / change / release management
- **Risk management** — IT risk register feeding [`compliance-check`](../compliance-check/SKILL.md)

### IT portfolio management
- All IT investments classified: Run / Grow / Transform
- Budget split target (typical): 60/30/10 → 40/40/20 → 30/40/30 (mature org)
- Each project: NPV per `engineering-economy`, strategic alignment score, risk

### Build / buy / partner decision
For each capability:
| Lens | Build | Buy | Partner |
|---|---|---|---|
| Strategic differentiation | High | Low | Medium |
| Time-to-value | Slow | Fast | Medium |
| TCO | Higher control, higher fixed | Lower fixed, ongoing | Variable |
| Lock-in risk | Low | High | Medium |
| Skill required | Yes (build/keep) | No | Some |

Pair with [`decision-analysis`](../decision-analysis/SKILL.md) AHP.

### Digital-transformation roadmapping
Phases: Assess → Vision → Design → Pilot → Scale → Optimize.
- Assess: current state, capability gaps, regulatory landscape
- Vision: 2-3 year north star
- Design: target architecture, governance, sourcing model
- Pilot: 1-2 high-leverage use cases, measurable outcomes
- Scale: roll out winners, kill losers
- Optimize: continuous improvement (DMAIC per `quality-engineering`)

## Shkhina-specific applications

### Client AI-strategy engagement
- Deliverable: 24-month AI roadmap document
- Structure: business context → maturity assessment → capability map → priority matrix → roadmap → governance → investment plan
- Pair with [`contract-drafting`](../contract-drafting/SKILL.md) for SOW + [`compliance-check`](../compliance-check/SKILL.md) for regs

### Shkhina's own IT roadmap
- Apply same methods to ourselves
- Current strategic-grid position: Factory (we run on IT) → moving toward Strategic (IT IS our product)
- Build/buy/partner per capability: AI = build, infra = buy (vast/Hostwinds), CRM = buy (EspoCRM)

### Vendor-of-vendor analysis
- For client engagements: who's their IT vendor stack and how does Shkhina fit?
- Position Shkhina as strategic vs commodity (premium tier per `offer-creation`)

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build IS strategy for [client/Shkhina-internal]:
   1. Assess current state (capability inventory, maturity)
   2. Apply McFarlan grid to existing systems
   3. Identify strategic gaps
   4. Build/buy/partner analysis per gap
   5. 24-month roadmap with milestones
   6. Governance recommendation
   7. Investment plan with NPV per project
   Output: is-strategy-<client>.md"
```

## Skill chain
- Pairs with [`is-analysis-design`](../is-analysis-design/SKILL.md) (strategy → analysis → design)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (build/buy/partner)
- Pairs with [`engineering-economy`](../engineering-economy/SKILL.md) (investment NPV)
- Pairs with [`compliance-check`](../compliance-check/SKILL.md) (regulatory dimension)
- Pairs with [`contract-drafting`](../contract-drafting/SKILL.md) (turn strategy → SOW)

## Course origin
- BGU 364-1-1911 — אסטרטגיה וניהול של מערכות מידע (track 2 mandatory)

## References
- `references/mcfarlan-grid-template.md`
- `references/build-buy-partner-decision.md`
- `references/it-portfolio-template.md`
- `references/transformation-roadmap-template.md`

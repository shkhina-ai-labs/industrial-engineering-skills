---
name: supply-chain-management
description: Supply chain management (ניהול שרשרת אספקה) for Shkhina vendor portfolio — supplier selection, network design, bullwhip-effect mitigation, single-source risk diversification, SLA management, dual-sourcing strategy, prepaid-credit inventory policy. Sourced from BGU IE&M course 364-1-1931. Extends `vendor-management` with IE-grade analytical methods. Use when designing the vendor stack, mitigating single-supplier risk, optimizing inventory of prepaid resources (API quotas, GPU hours, credits), or modeling demand variability through the supplier chain.
---

# Supply Chain Management (ניהול שרשרת אספקה)

Shkhina's "supply chain" is **API providers + cloud infra + data sources + creative tools**. Same dynamics as physical supply chains — bullwhip, single-source risk, lead-time variability — applied to the digital stack.

## When to use
- "Should we add a 3rd LLM provider for redundancy?"
- "Anthropic raised prices — switching cost analysis?"
- "Vast.ai has been flaky — what's our diversification plan?"
- "Image-gen tools: keep all 6, or consolidate?"
- "How much pre-paid credit per vendor?"
- "Vendor cascade risk: if X dies, what else fails?"

## Core methods

### Supplier selection (multi-criteria)
Pair with [`decision-analysis`](../decision-analysis/SKILL.md) AHP. Typical criteria for SaaS/API suppliers:
- Quality on Shkhina eval set (25%)
- Price per unit (20%)
- Reliability — uptime SLA, p95 latency (20%)
- Switching cost / lock-in (15%)
- Geographic / data-residency (10%)
- Contract terms per [`contract-review`](../contract-review/SKILL.md) (10%)

### Bullwhip effect (digital variant)
Small change in end-user demand → amplified swing in upstream resource demand.

**Shkhina pattern:** prospect surge → demo surge → API tokens 3-10× normal → vendor rate-limits → prospect drop-off.

Mitigations: information sharing (forecast pipeline to vendor), throttle to smooth demand, vendor-managed elastic scaling (vast.ai), reduce variability via Little's Law (`operations-research`).

### Network design
Map workload → primary / secondary / tertiary vendor. Any single-source critical dependency = active risk.

| Workload | Primary | Secondary | Tertiary |
|---|---|---|---|
| LLM inference | Anthropic | OpenAI | self-host vLLM-Gemma on vast |
| GPU training | vast 4090 | HF Jobs | (none) |
| Image gen | nano-banana / Gemini Pro | DALL-E 3 | local SDXL |
| Hosting | Hostwinds VPS | (single — RISK) | (none) |

### Single-source risk score
Risk = (time-to-switch) × (data lock-in) × (replacement availability) × (cost-to-switch), each 1-5. Anything ≥ 100 = active risk.

### Prepaid-credit inventory
- Demand forecast per vendor (next 30/90 days)
- Lead time to refill (instant → weeks)
- Safety stock = √(demand variance × lead time) × z
- Reorder point = (avg demand × lead time) + safety stock

### Cascade-failure analysis
What chain reaction if vendor X dies? Direct hits → indirect hits → time horizon → fallback exists?

## Shkhina-specific applications
- **Annual diversification review** — score each vendor; top-3 risk get diversification plans + quarterly drills
- **Pre-launch supply check** — every external dep gets fallback + SLA match + cascade trace
- **Price-shock absorption** — pair with `engineering-economy` NPV(absorb vs pass-through vs switch)

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Build supply-chain analysis for Shkhina:
   1. Map current vendor → workload matrix
   2. Score single-source risk per vendor
   3. Identify top-3 cascade-failure paths
   4. Recommend diversification + cost
   5. Draft switching playbook for top-1 risk
   Output: supply-chain-analysis-<date>.md"
```

## Skill chain
- Extends [`vendor-management`](../vendor-management/SKILL.md) with IE analytical methods
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (multi-criteria selection), [`engineering-economy`](../engineering-economy/SKILL.md) (TCO, switching NPV), [`compliance-check`](../compliance-check/SKILL.md) (sub-processor disclosure), [`dual-provider-llm`](../dual-provider-llm/SKILL.md) (a Shkhina supply-chain pattern in code), [`operations-research`](../operations-research/SKILL.md) (Little's Law for demand smoothing)

## Course origin
- BGU 364-1-1931 — ניהול שרשרת אספקה (elective)
- Builds on: 364-1-1041 Probability, 364-1-3061 Stochastic OR (queueing/inventory)

## References
- `references/supplier-selection-ahp.md`
- `references/single-source-risk-template.md`
- `references/inventory-policy-eoq.md`
- `references/cascade-analysis-template.md`
- `references/shkhina-vendor-map-2026.md` (TODO from real state)

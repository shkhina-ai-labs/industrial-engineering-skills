---
name: game-theory-agents
description: Game theory & intelligent agent design (תורת המשחקים ועיצוב סוכנים חכמים) — Nash equilibrium, mechanism design, auction theory, multi-agent coordination, principal-agent problems, repeated games, evolutionary stable strategies. Sourced from BGU IE&M elective 364-1-1311. Use when designing multi-agent systems with conflicting incentives, modeling negotiations, designing pricing/bidding mechanisms, or analyzing strategic interactions (with clients, partners, competitors, or between Shkhina's own agents).
---

# Game Theory & Intelligent Agent Design (תורת המשחקים)

When multiple agents (humans, AI, organizations) make interdependent decisions. Pricing decisions, negotiations, multi-agent pipelines, partnership terms — all are games.

## When to use
- "Pricing — match competitor or differentiate? what does Nash say?"
- "Designing the multi-agent Poster pipeline — how to align Editor and Creator incentives?"
- "Partner negotiation: when does cooperation beat competition?"
- "Auction-style allocation of Yossi-hours across clients"
- "Repeated game with this client — should I trust their next promise?"
- "Mechanism design: how to incentivize prospects to qualify themselves?"

## Core methods

### Game classification
- **Cooperative vs non-cooperative**
- **Zero-sum vs non-zero-sum** — most business games are non-zero-sum
- **Simultaneous vs sequential** (game tree vs payoff matrix)
- **Complete vs incomplete information** (Bayesian games)
- **One-shot vs repeated** (folk theorems enable cooperation)

### Nash equilibrium
A strategy profile where no player can improve by unilaterally deviating. Solve via:
- **Pure strategy:** check each cell for stability
- **Mixed strategy:** indifference principle
- **Sequential games:** backward induction (subgame-perfect equilibrium)

### Famous games (with Shkhina mappings)
| Game | Lesson | Shkhina application |
|---|---|---|
| Prisoner's Dilemma | Defect dominates one-shot; cooperate emerges in repeated | Vendor relationships (repeated → trust) |
| Stag Hunt | Coordination on payoff-dominant equilibrium hard | Partnership LOI (signal commitment) |
| Battle of the Sexes | Multiple equilibria, distribution conflict | Splitting joint-venture revenue |
| Ultimatum | Fairness > strict rationality | Take-it-or-leave-it pricing |
| Chicken | Brinkmanship | Negotiation walk-away signaling |
| Public Goods | Free-riding without enforcement | Open-source contributions |

### Mechanism design (reverse game theory)
Design rules so self-interested agents produce desired outcome:
- **VCG (Vickrey-Clarke-Groves) auctions** — second-price reveals true valuations
- **Revelation principle** — any equilibrium achievable with truthful reporting
- **Incentive compatibility** — best to tell the truth
- **Budget balance + efficiency + IC** — pick 2 (impossibility result)

### Multi-agent system design
- **Coordination mechanisms:** explicit (contracts) vs implicit (norms, conventions)
- **Communication protocols:** speech acts (request, inform, propose, accept, reject)
- **Trust & reputation:** track historical reliability per agent
- **Conflict resolution:** voting, market mechanisms, hierarchical arbitration

### Principal-agent problem
When delegator (you) and delegate (agent) have conflicting incentives + asymmetric info. Solutions: monitoring, performance contracts, signaling/screening.

## Shkhina-specific applications

### Multi-agent pipeline incentive design (Poster, BizDev, Shkhina)
- Each sub-agent's "reward" (quality score) shapes behavior
- Misalignment example: Critic optimizes for low score → blocks everything → fix by aligning scores to outcomes (post engagement)
- Design: aggregate quality score must match real-world success metric (engagement, conversion)

### Partner negotiation (paired with `negotiation-playbook`)
- Repeated game with reputation effects
- Tit-for-tat: cooperate first, then mirror partner's last move
- Build cooperation through small reciprocal commitments (LOI → revenue share → joint product)

### Pricing as game
- vs competitors: don't race to bottom (Bertrand → zero profit) — differentiate (Hotelling)
- vs client: ultimatum game — leave some surplus on table for closing
- vs vendor: monopolistic supplier (Anthropic) → diversify per `supply-chain-management`

### Auction-style resource allocation
- Yossi-hours scarce → clients implicitly bid via deal size + urgency
- Make explicit: capacity-constrained quarters → auction with rush-fee tiers
- VCG-inspired: highest-payer wins, pays second-highest's bid (truthfulness)

### Lead qualification as mechanism design
- Want prospects to self-reveal seriousness
- Design: paid pilot ($X) reveals serious-vs-tire-kicker
- Costly signal → only serious prospects pay

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Apply game theory to Shkhina situation: [situation]
   1. Frame as game: players, strategies, payoffs, info structure
   2. Find equilibria (Nash / subgame-perfect / Bayesian)
   3. Identify mechanism-design alternatives if equilibrium suboptimal
   4. Recommend strategy + watch-outs
   Output: game-analysis.md"
```

## Skill chain
- Pairs with [`negotiation-playbook`](../negotiation-playbook/SKILL.md) (every negotiation = repeated game)
- Pairs with [`offer-creation`](../offer-creation/SKILL.md) (mechanism design for pricing tiers)
- Pairs with [`multi-agent-pipeline`](../multi-agent-pipeline/SKILL.md) (multi-agent design)
- Pairs with [`agent-security-patterns`](../agent-security-patterns/SKILL.md) (principal-agent → confirmation gates)
- Pairs with [`decision-analysis`](../decision-analysis/SKILL.md) (game payoffs feed decision tree)

## Course origin
- BGU 364-1-1311 — תורת המשחקים ועיצוב סוכנים חכמים (Intelligent Systems track elective)

## References
- `references/nash-equilibrium-recipes.md`
- `references/mechanism-design-patterns.md`
- `references/repeated-games-strategies.md`
- `references/multi-agent-coordination.md`

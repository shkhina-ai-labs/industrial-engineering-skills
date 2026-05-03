---
name: decision-analysis
description: Structured decision analysis (קבלת החלטות) for Shkhina prioritization — Analytic Hierarchy Process (AHP) for multi-criteria choices, decision trees with Expected Monetary Value (EMV) and utility, MCDM methods (TOPSIS, weighted sum), value of information (VOI), behavioral decision-bias guards. Sourced from BGU IE&M course 364-1-4241 (קבלת החלטות). Use when stuck between multiple options, when prioritizing prospects/demos/features, when picking between deals with different risk profiles, or when a high-stakes decision needs to be defended later.
---

# Decision Analysis (קבלת החלטות)

When the call really matters: get it out of your head, structure it on paper, and let the numbers + your intuition argue. Decision analysis isn't about removing judgment — it's about **knowing exactly where the judgment enters**.

## When to use
- "Which 3 prospects should I focus on this month?"
- "Demo A or Demo B for [prospect]?"
- "Take the [client] deal at $X with these terms, or hold out?"
- "Which vendor should we pick — Anthropic, OpenAI, or both?"
- "Hire Sales Operator first, or DevOps first?"
- "Build feature A, B, or C next?"
- "Should we accept the partnership LOI from [company]?"

## Three core methods

### Method 1 — AHP (Analytic Hierarchy Process)
For ranking N options against M weighted criteria.

**Workflow:**
1. **List options** (A, B, C, D)
2. **List criteria** (revenue potential, fit, risk, urgency, strategic value)
3. **Pairwise-compare criteria** for importance — fill the matrix using 1-9 scale (1=equal, 9=extreme)
4. **Compute criterion weights** (eigenvector of comparison matrix; or just normalize each row's sum)
5. **Score each option on each criterion** (1-10 or 1-5)
6. **Final score** = Σ (criterion weight × option's criterion score)
7. **Rank** options by final score

**Consistency check:** AHP gives a CR (Consistency Ratio). If CR > 0.10, your pairwise comparisons are inconsistent — re-do them.

**Use when:** several criteria matter, weights aren't obvious, decision needs to be defensible.

### Method 2 — Decision tree with EMV
For decisions with sequential choices and probabilistic outcomes.

**Workflow:**
1. Draw nodes: ◯ = chance node, □ = decision node, △ = terminal payoff
2. Estimate probabilities at each chance node (must sum to 1.0)
3. Estimate payoff at each terminal
4. **Roll back from right to left:**
   - At chance nodes: EMV = Σ (probability × downstream value)
   - At decision nodes: pick the branch with max EMV, mark others ✗
5. The retained path = optimal decision strategy

**Variant — risk-adjusted utility:** if you're risk-averse, replace dollar payoff with utility u($) (concave function). Maximize **expected utility** instead of EMV. For Shkhina ($10K-$50K deals), risk neutrality is usually fine; for $100K+ commitments, use utility.

**Value of Information (VOI):** before paying for more info (a paid pilot, a market study), compute VOI = EMV(with info) - EMV(without info). If VOI < cost of info, don't buy it.

### Method 3 — TOPSIS (or weighted-sum MCDM)
Lighter than AHP. Useful for quick prioritization.

**Workflow:**
1. Build score matrix: rows = options, columns = criteria, cells = score
2. Normalize each column (divide by column max, or by Euclidean norm)
3. Apply weights: each cell × column weight
4. **Ideal best** = column max for each criterion; **Ideal worst** = column min
5. For each option compute: distance to ideal best (D+), distance to ideal worst (D-)
6. **Score** = D- / (D+ + D-) — higher is better
7. Rank

Faster than AHP for "I just need a defensible ranking."

## Behavioral bias guards

The IE course covers cognitive biases. Watch for:

| Bias | What it does | Counter |
|---|---|---|
| **Anchoring** | First number dominates | List 3 anchors before settling |
| **Confirmation bias** | Seek info that confirms preferred option | Pre-mortem: "this option failed — why?" |
| **Loss aversion** | Overweight downside vs upside (~2x) | Frame both gains AND losses; use utility curve |
| **Sunk cost** | "We already invested X" | Decide based on forward-looking value only |
| **Availability** | Recent / vivid examples dominate | Look at base rates, not anecdotes |
| **Status quo bias** | Inertia | Force "do nothing" to compete head-to-head with alternatives |
| **Overconfidence** | Probabilities too tight | Use 90%-confident range; widen if you've ever been wrong |

If a decision matters: pre-mortem ("imagine it's 6 months later and this failed") before committing.

## Shkhina-specific decision templates

### Template A — Prospect prioritization (which 3 to focus on)
- **Criteria (typical weights):** Revenue potential 35% / Fit with current capability 25% / Conversion probability 20% / Strategic value (case study, sector entry) 15% / Effort 5%
- **Method:** AHP across all qualified prospects
- **Output:** ranked list, top 3 get the focus
- Source data: [`outreach-strategy`](../outreach-strategy/SKILL.md), CRM scoring, [`negotiation-playbook`](../negotiation-playbook/SKILL.md) BATNA file

### Template B — Demo selection (which demo for which prospect)
- **Criteria:** Sector match, complexity match, "wow" factor, evidence depth
- **Method:** weighted-sum or TOPSIS (faster for repeated use)
- **Output:** demo ranking per prospect → feeds [`outreach-strategy`](../outreach-strategy/SKILL.md)

### Template C — Vendor pick (Anthropic vs OpenAI for new agent)
- **Criteria:** quality on Shkhina eval set, latency p95, cost per 1M tokens, ToS terms (per [`contract-review`](../contract-review/SKILL.md)), redundancy
- **Method:** decision tree (we already use [`dual-provider-llm`](../dual-provider-llm/SKILL.md), so the question is "which is primary")
- Pair with cost-of-info: a 1-week side-by-side eval costs X; is it worth it?

### Template D — Feature/product priority (build A or B next?)
- **Criteria:** Demo conversion lift, addressable use cases, dev effort, vendor risk, methodology reuse
- **Method:** AHP
- **Output:** ranked feature backlog

### Template E — Hire which role first
- **Criteria (per [`hr-hiring`](../hr-hiring/SKILL.md)):** revenue unlock, key-person risk reduction, cost-to-serve impact, time-to-value
- **Method:** decision tree (because each hire changes the available criteria for the next)
- **Output:** confirms or revises the order in `analysis/business/hr.md`

### Template F — Take this deal (with these terms) — yes/no
- **Method:** decision tree with utility (because deal sizes vary widely)
- Branches: accept current terms / counter / walk away
- Probabilistic outcomes per branch (deal closes / pushes / dies / goes elsewhere)
- Pair with [`negotiation-playbook`](../negotiation-playbook/SKILL.md) walk-away triggers

## Sub-agent leverage

For complex multi-criteria decisions or when the input data needs gathering:

```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run decision analysis for [Shkhina decision]:
   1. Frame: list options + decision criteria
   2. Pick method (AHP / decision tree / TOPSIS) with rationale
   3. Gather inputs (scores, probabilities, payoffs) — ask me for any I can't infer
   4. Compute the recommendation
   5. Run pre-mortem on the recommended choice
   6. Report: ranked options + top recommendation + key sensitivity (which input change flips the answer)"
- Tools: WebSearch (if external data needed), Bash (for solver runs)
```

## Skill chain
- Often paired with [`operations-research`](../operations-research/SKILL.md) (when criteria are quantitative + constraint-based, OR is more direct)
- Pairs with [`negotiation-playbook`](../negotiation-playbook/SKILL.md) (every offer/counter is a decision)
- Pairs with [`offer-creation`](../offer-creation/SKILL.md) (which offer variant to lead with)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (which engagement gets the limited week)
- Pairs with [`vendor-management`](../vendor-management/SKILL.md) (vendor selection)
- Pairs with [`hr-hiring`](../hr-hiring/SKILL.md) (which role first)

## Course origin
- BGU 364-1-4241 (3.0 נק"ז) — קבלת החלטות (Decision Making)
- Augmented with: classical MCDM (Saaty's AHP, Hwang & Yoon's TOPSIS), Kahneman behavioral economics

## References
- `references/ahp-template.xlsx-equivalent.md` — AHP worksheet (criteria-vs-criteria + options-vs-criteria matrices)
- `references/decision-tree-template.md` — fillable tree structure
- `references/topsis-recipe.md` — Python recipe for TOPSIS scoring
- `references/bias-checklist.md` — pre-decision bias-guard checklist
- `references/utility-curves.md` — risk-tolerance utility function options

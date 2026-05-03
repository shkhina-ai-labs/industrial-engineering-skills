---
name: methods-engineering
description: Methods engineering & organizational process design (הנדסת שיטות ותהליכים ארגוניים) — work-method analysis, time studies, motion economy, work standardization, MTM (methods-time measurement), workflow optimization. Sourced from BGU IE&M course 364-1-1721. Use when standardizing recurring tasks, eliminating waste in personal/agent workflows, time-studying how long things actually take, or designing the "right way" to do a repeated activity.
---

# Methods Engineering (הנדסת שיטות ותהליכים ארגוניים)

The discipline of finding the **best way** to do recurring work — then standardizing it so it stays the best way. Pre-Lean Toyota / Frederick Taylor / Frank & Lillian Gilbreth.

## When to use
- "How long does it ACTUALLY take to onboard a client?"
- "Standardize the demo deployment process"
- "Time-study the outreach wave creation cycle"
- "Eliminate motion waste in the daily check-in flow"
- "Design the standard work for [recurring task]"

## Core methods

### Work measurement
- **Time study** — observe N reps, record cycle time, compute mean + std
- **Sample size:** n ≥ (1.96 × s / (0.05 × x̄))² for ±5% precision at 95%
- **Synthetic times (MTM-1, MTM-2):** decompose motion into TMU (Time Measurement Units, 0.036s) — Reach + Move + Grasp + Position + Release
- **Work sampling:** snapshot observations to estimate % time on each activity

### Methods analysis (the 5-step Gilbreth process)
1. **Select** task to study (high frequency × high variation = high payoff)
2. **Record** existing method (operation chart, flow process chart, two-handed chart)
3. **Examine** — apply the 5W2H + Why × 5: eliminate, combine, rearrange, simplify
4. **Develop** improved method
5. **Install + Maintain** — write standard work, train, monitor

### Motion economy principles
- Both hands begin/end motion simultaneously
- Both hands work in opposite + symmetric directions
- Tools/materials in fixed locations
- Smooth continuous curves > zigzag
- Minimize distance moved
- Apply gravity / momentum where possible

### Standard work
For each recurring task: standard work sheet with steps, takt time, in-process inventory, quality checkpoints. Lives next to the work.

## Shkhina-specific applications

### Outreach wave standard work
- Currently: ~varies — time-study to baseline
- Standard: Yossi opens DNC list (5min) → pulls top-N from CRM (5min) → Composer drafts (10min) → review + edit (15min) → send (5min) = takt 40min/wave
- Pair with `process-mining` to compare standard vs actual

### Demo deployment standard work
- Steps: pull main → build → deploy → smoke test → publish products.json → verify
- Each step: target time + quality gate
- Standard work sheet posted at `business/infrastructure/runbooks/`

### Client kickoff standard work
- Per [`client-delivery-lifecycle`](../client-delivery-lifecycle/SKILL.md): kickoff call → memo → SOW
- Standard time per step → flag deviations as outliers in `quality-engineering` SPC

### Skill-build standard work (this skill)
- Per pattern: dirs → SKILL.md → references TODO → manifest entry → wiki log
- Time-study: how long per skill? what's the bottleneck step?

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Apply methods engineering to Shkhina task: [task]
   1. Decompose to elemental steps
   2. Time-study via existing log data (or design a sampling plan)
   3. Identify waste: motion / waiting / over-processing / defects
   4. Propose redesigned method (eliminate / combine / rearrange / simplify)
   5. Draft standard work document
   Output: standard-work-<task>.md"
- Tools: Read (logs), Bash (analysis)
```

## Skill chain
- Pairs with [`process-mining`](../process-mining/SKILL.md) (mined process = baseline; methods-eng = redesign)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (DMAIC's Improve = methods redesign; standard work = Control)
- Pairs with [`operations-research`](../operations-research/SKILL.md) (after methods optimized, sequence/schedule with OR)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (better estimates from time-study data)

## Course origin
- BGU 364-1-1721 — הנדסת שיטות ותהליכים ארגוניים (mandatory, 3.5 נק"ז)

## References
- `references/time-study-template.md`
- `references/standard-work-template.md`
- `references/motion-economy-checklist.md`
- `references/work-sampling-recipe.md`

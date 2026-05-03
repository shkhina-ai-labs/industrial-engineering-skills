---
name: process-mining
description: Process mining (כריית תהליכים) — discover the actual process from event logs, vs the documented one. Conformance checking, bottleneck detection, variant analysis. Sourced from BGU IE&M elective 364-1-1781. Use when you have logs (CRM, demo telemetry, agent traces, server logs) and want to see what's REALLY happening — not what you think happens. Critical for debugging "why isn't conversion working" or "where do prospects drop off".
---

# Process Mining (כריית תהליכים)

Reverse-engineer the actual process from event logs. **Documented process is what you wrote; mined process is what actually happens.** Usually wildly different.

## When to use
- "Where do prospects actually drop off in the outreach funnel?"
- "What's the real demo flow vs what we designed?"
- "Why does the multi-agent pipeline get stuck?"
- "Discover variants in client engagements — which is most successful?"
- "Conformance: are we following the playbook, or improvising?"
- "Bottleneck analysis on cycle time per stage"

## Core methods

### Process discovery
Input: event log (case_id, activity, timestamp, [resource]). Output: process map (Petri net, BPMN, directly-follows graph).
- **Algorithms:** Alpha miner, Heuristics miner, Inductive miner (most robust), Fuzzy miner
- **Tool:** PM4Py (Python), Disco (commercial), Apromore (open-source)

### Conformance checking
Compare event log → reference model. Find:
- **Skipped activities** (model says X happens, log shows it didn't)
- **Inserted activities** (log shows steps not in model)
- **Wrong order** (log violates model's ordering)
- **Fitness metric** = % of log explainable by model (>0.9 good)

### Variant analysis
Group cases by behavior pattern. Find:
- Most common variant (the "happy path")
- Rare variants — investigate (broken or innovative?)
- Performance per variant (cycle time, conversion)

### Bottleneck detection
For each activity: avg duration, queue time before, throughput. Stage with highest queue+duration = bottleneck (per Theory of Constraints).

## Shkhina-specific applications

### Outreach funnel mining
- Event log: CRM activities (LinkedIn DM sent → reply → call booked → call held → demo sent → SOW sent → signed)
- Mine: actual stage-to-stage flow + drop-off rates
- Variant analysis: which sequence converts best?
- Pair with [`outreach-strategy`](../outreach-strategy/SKILL.md) for actionable changes

### Multi-agent pipeline mining
- Event log: agent_id, step, timestamp, output_quality
- Mine Poster pipeline (Scout → Strategist → Tech Context → Research → Creator → Critic → Editor → Fact Checker)
- Find: where does work back-flow? where are retries clustered?

### Demo session mining
- Event log: demo loaded → interacted → tried-feature → completed → bounced
- Mine: which demos have stickiest engagement, where do users abandon?

### Client engagement mining
- Event log per engagement: discovery → scope → SOW → kickoff → milestone → review → sign-off
- Compare actual cycle time per stage vs [`ie-project-management`](../ie-project-management/SKILL.md) plan
- Find which engagements deviated and why

### Onkolos strategy execution mining (methodology only, 🔒)
- Event log: signal → analysis → order → fill → exit
- Detect: latency between stages, broken handoffs, missed signals

## Workflow
```
1. Find the event log (CRM table, server logs, agent traces)
2. Format: case_id, activity, timestamp [, resource, attributes]
3. Use PM4Py to discover process map
4. Compare to documented model → conformance gaps
5. Variant analysis → find happy path + outliers
6. Bottleneck analysis → which stage costs the most cycle time
7. Output: process-mining-report.md with diagrams + recommendations
```

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run process mining for Shkhina log: [log path]
   1. Profile log: # cases, activities, time range
   2. Discover process map (Inductive miner via PM4Py)
   3. Conformance check vs documented model: [model description]
   4. Variant analysis: top 3 variants + performance
   5. Bottleneck: where does cycle time concentrate?
   6. Output: PNG of process map + analysis.md"
- Tools: Bash (Python + pm4py), Read (logs), Write
```

## Skill chain
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (mined process feeds DMAIC's Measure phase)
- Pairs with [`operations-research`](../operations-research/SKILL.md) (bottleneck = TOC constraint)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (engagement-mining → CPM accuracy improvement)
- Pairs with [`outreach-strategy`](../outreach-strategy/SKILL.md) (funnel mining → outreach changes)
- Pairs with [`agent-evals`](../agent-evals/SKILL.md) (multi-agent pipeline diagnostics)

## Course origin
- BGU 364-1-1781 — כריית תהליכים (elective)

## References
- `references/event-log-format.md` — required schema for PM4Py
- `references/pm4py-recipes.md` — discovery, conformance, variant code
- `references/shkhina-log-sources.md` — where each Shkhina event log lives (CRM, server, agent traces)
- `references/process-mining-report-template.md`

---
name: knowledge-management
description: Knowledge management (ניהול ידע) — capturing, organizing, retrieving, and reusing organizational knowledge. Tacit-vs-explicit conversion (SECI model — Socialization, Externalization, Combination, Internalization), knowledge graphs, communities of practice, lessons-learned cycles. Sourced from BGU IE&M elective 364-1-3309. Distinct from `wiki-knowledge` (which is the operational tool) — this skill is the *strategy* of what to capture, why, and how to keep it usable. Use when designing knowledge systems, deciding what to wiki vs forget, or running a post-mortem to extract reusable lessons.
---

# Knowledge Management (ניהול ידע)

Why some teams compound knowledge over time and others reinvent the wheel every quarter. The methodology layer above the wiki tool.

## When to use
- "Should this go in the wiki, code comments, or just my head?"
- "Run a post-mortem on the [client] engagement"
- "Why does Claude forget things between sessions?" → KM design
- "Onboarding a new hire — what's the knowledge transfer plan?"
- "Audit: which wiki pages are dead, which are alive?"
- "Extract lessons from 5 client engagements into reusable methodology"

## Core methods

### SECI model (Nonaka)
Knowledge cycles between tacit (in heads) and explicit (written):

| From → To | Mode | Shkhina example |
|---|---|---|
| Tacit → Tacit | **Socialization** | Pair-coding, shadowing, demos |
| Tacit → Explicit | **Externalization** | Writing a SKILL.md from experience |
| Explicit → Explicit | **Combination** | Synthesizing 5 client retros into a playbook |
| Explicit → Tacit | **Internalization** | Reading the playbook, applying it instinctively |

Healthy KM: all 4 happen continuously. Most orgs only do Combination (slides about slides) or fail Externalization (everything stays in heads).

### Knowledge taxonomy
| Type | Where it lives | Decay rate |
|---|---|---|
| **Procedural** (how to do X) | SKILLS, runbooks, scripts | Slow if maintained |
| **Conceptual** (what X means) | Wiki concepts/, glossaries | Slow |
| **Episodic** (what happened) | Wiki log.md, retros | Fast (loses context) |
| **Relational** (who knows X) | CRM, [`hr/`](../../../Code/business/hr/) | Medium |
| **Strategic** (why we do X) | CLAUDE.md, governance.md | Slow if explicit |

### What to capture vs forget
**Capture:**
- Decisions + rationale (why)
- Surprises (counter-intuitive findings)
- Templates (next time, start from here)
- Failure modes (don't repeat)
- Per-client/vendor "watch out" notes

**Forget (don't burden the system):**
- Routine ops with no learning
- One-off troubleshooting that won't recur
- Outdated approaches (archive, don't delete — but unindex)

### Lessons-learned cycle (after every engagement / launch / incident)
1. **What happened** — facts, timeline
2. **What worked** — keep doing
3. **What didn't** — stop doing
4. **What we'd do differently** — change
5. **Generalizable lesson** — pattern (becomes a SKILL or playbook update)
6. **Where this lives** — wiki/SKILLS/agent-leverage update

### Knowledge graph (Obsidian)
Shkhina's wiki is a knowledge graph. Connect via:
- Wikilinks `[[entity]]`
- Tags `#topic`
- Dataview queries (lists/tables across pages)
- Graph view (visualize knowledge clusters)

## Shkhina-specific applications

### Post-engagement retro (after each client wraps)
- Run lessons-learned cycle
- Update [`client-services/playbooks/`](../../../Code/business/client-services/playbooks/) with generalizable lesson
- Update relevant SKILL.md if methodology evolved
- Update wiki entity page for client

### Wiki health audit (quarterly)
- Pages not edited in 12 months → mark stale, decide: archive / refresh / delete
- Pages with 0 inbound links → orphans, integrate or remove
- Run `wiki-knowledge` skill audit

### Knowledge transfer to new hire
- Day 1: read CLAUDE.md, [`firm-structure`](../../../Code/llm-wiki/analysis/firm-structure.md), product wiki entities
- Day 2-3: shadow Yossi on actual work (Socialization)
- Day 4-5: write a SKILL.md from what they learned (Externalization)
- Week 2: own a small project applying the methodology (Internalization)

### Multi-agent memory design
- Per-agent: short-term context (session) + long-term (vector DB / wiki)
- Knowledge handoff between agents = explicit (passed data) vs implicit (shared corpus)
- Avoid: each agent building its own incompatible knowledge silo

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Knowledge audit / extraction for Shkhina topic: [topic]
   1. Inventory current state across wiki, SKILLS, agents
   2. Identify gaps (knowledge that exists but unwritten)
   3. Identify staleness (written but outdated)
   4. Propose consolidation or new capture targets
   5. Draft post-mortem template if relevant
   Output: km-audit-<topic>.md"
- Tools: Read, Glob, Grep
```

## Skill chain
- Pairs with [`wiki-knowledge`](../wiki-knowledge/SKILL.md) (the tool — this skill is the strategy)
- Pairs with [`claude-md-management`](../claude-md-management/SKILL.md) (CLAUDE.md is strategic knowledge)
- Pairs with [`hr-hiring`](../hr-hiring/SKILL.md) (onboarding = KM transfer)
- Pairs with [`client-delivery-lifecycle`](../client-delivery-lifecycle/SKILL.md) (retros)
- Pairs with [`process-mining`](../process-mining/SKILL.md) (mined process = explicit knowledge of actual)

## Course origin
- BGU 364-1-3309 — ניהול ידע (Knowledge Management, IS-track elective)
- Augmented with: Nonaka SECI, Davenport-Prusak, Drucker

## References
- `references/seci-cycle-template.md`
- `references/lessons-learned-template.md`
- `references/wiki-audit-checklist.md`
- `references/onboarding-km-plan.md`

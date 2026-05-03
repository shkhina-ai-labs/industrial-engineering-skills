---
name: is-analysis-design
description: Information Systems analysis & design (ניתוח ועיצוב מערכות מידע) — requirements engineering, UML modeling (use-case, class, sequence, activity), SDLC variants (waterfall/agile/iterative), data modeling (ER, dimensional), system architecture documentation. Sourced from BGU IE&M course 364-1-1411. Use when designing a new client system, scoping a build deliverable, documenting an existing system for handoff, or producing the architecture artifacts needed in a SOW.
---

# IS Analysis & Design (ניתוח ועיצוב מערכות מידע)

Turn fuzzy "we need a system" into precise specs that engineers can build and clients can sign off on.

## When to use
- "Scope this client engagement — what's the system architecture?"
- "Document the Shkhina agent for handoff to a new dev"
- "Generate use-cases from this client conversation"
- "Build ER diagram for the new feature DB"
- "Sequence diagram for the multi-agent pipeline"
- "Requirements doc for the SOW appendix"

## Core methods

### Requirements engineering
- **Functional requirements** — what the system DOES (use cases, user stories)
- **Non-functional** — how WELL (performance, security, scalability, reliability)
- **Acceptance criteria** — testable definition of "done" per requirement
- **MoSCoW prioritization** — Must / Should / Could / Won't (this release)

### UML diagrams (when each)
| Diagram | What it shows | Use for |
|---|---|---|
| **Use-case** | Actors × system interactions | Scoping, SOW appendix |
| **Class** | Static structure (entities, relationships, attributes) | Domain model, code structure |
| **Sequence** | Object interactions over time | API flows, multi-step processes |
| **Activity** | Workflow with branches/joins | Business process flow |
| **State machine** | Object lifecycle (states + transitions) | Order/ticket/lead state |
| **Component** | Code modules + dependencies | Architecture overview |
| **Deployment** | Hardware/server topology | Infra diagram |

### Data modeling
- **Conceptual ER** — entities + relationships, no implementation
- **Logical** — normalize to 3NF (or break for performance)
- **Physical** — tables, indexes, partitioning per chosen DB
- **Dimensional (Kimball)** — for analytics / BI (facts + dimensions)

### SDLC variant selection
- **Waterfall** — when requirements are stable + compliance needed (rare for AI)
- **Iterative/Spiral** — when uncertainty is high (typical Shkhina engagements)
- **Agile/Scrum** — small-team, frequent client feedback (Shkhina default for client work)
- **Lean Startup** — when product-market fit unknown

### Architecture documentation (the "C4 model")
- **L1 Context** — system + external actors
- **L2 Containers** — apps/services/DBs
- **L3 Components** — modules within a container
- **L4 Code** — class diagrams (rare to maintain)

## Shkhina-specific applications

### Client engagement scoping
- Use-case diagram → SOW Appendix A (signed scope)
- Class/ER diagram → Appendix B (data model)
- Sequence diagram → Appendix C (key flows)
- Pair with [`contract-drafting`](../contract-drafting/SKILL.md) — these become contractual scope

### Internal system documentation
- Each Shkhina product entity page (wiki) gets a C4 context + container diagram
- Pair with [`figma:figma-generate-diagram`](../figma:figma-generate-diagram/) for visuals
- Stored at `business/knowledge/architecture-diagrams/`

### New feature scoping
- Generate use-cases → MoSCoW prioritize → estimate (per `ie-project-management`) → SOW change order

### Handoff documentation
- For client engagements ending in handoff: full UML pack + runbook + maintenance contract
- Pair with [`client-delivery-lifecycle`](../client-delivery-lifecycle/SKILL.md)

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Run IS analysis on Shkhina need: [scope description]
   1. Extract functional + non-functional requirements
   2. Build use-case diagram (textual + draft Mermaid)
   3. Domain class/ER model
   4. Top-3 sequence diagrams
   5. C4 L1+L2 architecture
   6. MoSCoW prioritization
   7. Output: requirements-spec.md + diagrams in Mermaid"
- Tools: Write
```

## Skill chain
- Pairs with [`figma:figma-generate-diagram`](../figma:figma-generate-diagram/) (UML rendering)
- Pairs with [`contract-drafting`](../contract-drafting/SKILL.md) (SOW appendices = these artifacts)
- Pairs with [`ie-project-management`](../ie-project-management/SKILL.md) (use-case → WBS)
- Pairs with [`api-design`](../api-design/SKILL.md), [`database-prisma`](../database-prisma/SKILL.md) (data model implementation)

## Course origin
- BGU 364-1-1411 — ניתוח ועיצוב מערכות מידע (mandatory, 3.5 נק"ז)

## References
- `references/requirements-template.md`
- `references/uml-mermaid-snippets.md`
- `references/c4-template.md`
- `references/moscow-template.md`

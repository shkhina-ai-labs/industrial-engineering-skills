---
title: Industrial Engineering — Skill Curriculum (COMPLETE)
type: index
created: 2026-05-03
updated: 2026-05-03
parent: r-and-d
status: 17 skills built; full BGU IE&M curriculum mapped
source: BGU IE&M Yearbook תשפ"ו (2025-26)
---

# Industrial Engineering — Skill Curriculum

The full **BGU Industrial Engineering & Management (תעשייה וניהול)** undergraduate curriculum, distilled into 17 Claude skills that work across Shkhina's 9 business departments.

**Source:** [BGU IE&M Yearbook 2025-26 PDF](https://www.bgu.ac.il/media/bvnhtwad/364-2026.pdf) (verified primary).

## The 17 IE skills (all built and synced)

### Quantitative core (foundation under everything)
| Skill | BGU course(s) | Use |
|---|---|---|
| [`statistics-inference`](../../../.claude/skills/statistics-inference/SKILL.md) | 364-1-1041 הסתברות + 364-1-1291 אמידה ומבחני השערות + 364-1-1061 רגרסיה | Hypothesis tests, CI, regression — foundation under all IE skills |
| [`operations-research`](../../../.claude/skills/operations-research/SKILL.md) | 364-1-3051/3061/3031/3041 (15.5 נק"ז of OR) | LP, queueing, network opt, scheduling |
| [`simulation-modeling`](../../../.claude/skills/simulation-modeling/SKILL.md) | 364-1-3091 סימולציה | Monte Carlo + DES |
| [`design-of-experiments`](../../../.claude/skills/design-of-experiments/SKILL.md) | 364-1-1071 DOE & ANOVA | A/B tests, factorial designs |

### Quality, process, methods
| Skill | BGU course(s) | Use |
|---|---|---|
| [`quality-engineering`](../../../.claude/skills/quality-engineering/SKILL.md) | 364-1-1091 הנדסת איכות | DMAIC, SPC, FMEA, root cause |
| [`methods-engineering`](../../../.claude/skills/methods-engineering/SKILL.md) | 364-1-1721 הנדסת שיטות | Time studies, work standardization |
| [`process-mining`](../../../.claude/skills/process-mining/SKILL.md) | 364-1-1781 כריית תהליכים | Discover real process from logs |
| [`human-factors-design`](../../../.claude/skills/human-factors-design/SKILL.md) | 364-1-4311 גורמי אנוש | Ergonomics for UX, alert design |

### Management, strategy, decisions
| Skill | BGU course(s) | Use |
|---|---|---|
| [`ie-project-management`](../../../.claude/skills/ie-project-management/SKILL.md) | 364-1-1251 ניהול פרויקטים | CPM/PERT, EVM, RACI |
| [`decision-analysis`](../../../.claude/skills/decision-analysis/SKILL.md) | 364-1-4241 קבלת החלטות | AHP, decision trees, MCDM |
| [`engineering-economy`](../../../.claude/skills/engineering-economy/SKILL.md) | 142-1-3141 כלכלה + 681-1-5081 חשבונאות | NPV, IRR, ABC costing |
| [`game-theory-agents`](../../../.claude/skills/game-theory-agents/SKILL.md) | 364-1-1311 תורת המשחקים | Nash, mechanism design, multi-agent |
| [`supply-chain-management`](../../../.claude/skills/supply-chain-management/SKILL.md) | 364-1-1931 שרשרת אספקה | Vendor portfolio, single-source risk |
| [`product-management`](../../../.claude/skills/product-management/SKILL.md) | 364-1-3400 ניהול מוצרי היי-טק | RICE, PMF, lifecycle |

### Information Systems
| Skill | BGU course(s) | Use |
|---|---|---|
| [`is-analysis-design`](../../../.claude/skills/is-analysis-design/SKILL.md) | 364-1-1411 ניתוח ועיצוב מערכות מידע | UML, requirements, C4 |
| [`is-strategy-mgmt`](../../../.claude/skills/is-strategy-mgmt/SKILL.md) | 364-1-1911 אסטרטגיה וניהול IS | McFarlan grid, build/buy/partner |
| [`knowledge-management`](../../../.claude/skills/knowledge-management/SKILL.md) | 364-1-3309 ניהול ידע | SECI, lessons-learned, KM strategy |

## Other BGU IE&M courses — coverage map

### Foundational math (used by other skills, no separate skill needed)
- 214-1-9711 חדו"א 1 — Calculus 1
- 214-1-9621 חדו"א 2 — Calculus 2
- 214-1-9321 אלגברה לינארית — Linear Algebra
- 214-1-9481 משוואות דיפרנציאליות רגילות — ODEs
- 214-1-9661 מתמטיקה דיסקרטית — Discrete Math

These underpin OR, simulation, statistics, ML — invoked transitively when needed.

### Covered by existing Shkhina skills
| BGU course | Existing skill |
|---|---|
| 364-1-1191 אלגוריתמים | (existing dev skills: `code-reviewer`, `refactorer`, `systematic-debugging`) |
| 364-1-1301 תכנות JAVA + 364-1-1421 OOP | (existing dev skills: `backend`, `frontend`, language-specific LSPs) |
| 364-1-1901 בסיסי נתונים + 364-1-1541 NoSQL | [`database-prisma`](../../../.claude/skills/database-prisma/SKILL.md), [`postgres-best-practices`](../../../.claude/skills/postgres-best-practices/SKILL.md) |
| 364-1-1811 למידת מכונה + 364-1-2030 Deep Learning | [`train-model`](../../../.claude/skills/train-model/SKILL.md), [`evaluate-model`](../../../.claude/skills/evaluate-model/SKILL.md), [`llm-finetuning`](../../../.claude/skills/llm-finetuning/SKILL.md) |
| 364-1-1441 יסודות AI | (existing AI skills: `ai-agents-builder`, `claude-api`, `gemini-api`) |
| 364-1-1171 Business Intelligence | [`bi-developer`](../../../.claude/skills/bi-developer/SKILL.md) |
| 364-1-1731 HCI | [`ui-ux-design`](../../../.claude/skills/ui-ux-design/SKILL.md), [`accessibility-auditor`](../../../.claude/skills/accessibility-auditor/SKILL.md), `human-factors-design` |
| 364-1-1841 IT Infrastructure + 364-1-1371 Cloud | [`devops`](../../../.claude/skills/devops/SKILL.md), [`cloud-infrastructure`](../../../.claude/skills/cloud-infrastructure/SKILL.md), [`docker-kubernetes`](../../../.claude/skills/docker-kubernetes/SKILL.md), [`systemd-deploy`](../../../.claude/skills/systemd-deploy/SKILL.md) |
| 364-1-5001 אבטחת מידע | [`cybersecurity`](../../../.claude/skills/cybersecurity/SKILL.md), [`security-review`](../../../.claude/skills/security-review/SKILL.md), [`agent-security-patterns`](../../../.claude/skills/agent-security-patterns/SKILL.md), [`web-security-audit`](../../../.claude/skills/web-security-audit/SKILL.md) |
| 364-1-1711 Text-as-Data, NLP | [`nlp-expert`](../../../.claude/skills/nlp-expert/SKILL.md) |
| 364-1-1381 WEB systems | (existing frontend/backend skills) |
| 681-1-2071/0049 HR / Marketing | [`hr-hiring`](../../../.claude/skills/hr-hiring/SKILL.md), [`outreach-strategy`](../../../.claude/skills/outreach-strategy/SKILL.md), [`lead-generation`](../../../.claude/skills/lead-generation/SKILL.md), [`offer-creation`](../../../.claude/skills/offer-creation/SKILL.md) |

### Not relevant for an AI consultancy (skipped intentionally)
- 203-1-1391/1491 פיסיקה 1+2 — physics
- 364-1-1211 הנדסת ייצור ומכניחה — manufacturing/mechanics
- 364-1-3151 הנדסת חשמל ומערכות ספרתיות — EE & digital systems
- 364-1-3321 אוטומציה ומערכות משולבות — factory automation
- 364-1-1791 יסודות מדעי המוח — neuroscience
- 364-1-1481 / 364-1-1871 רובוטיקה / רובוטיקה קוגניטיבית — robotics

### Soft skills / workshops
- 364-1-1501 מיומנויות בתקשורת בינאישית — covered by [`internal-comms`](../../../.claude/skills/internal-comms/SKILL.md)
- 364-1-3241 כתיבה ומיומנויות למידה — covered by [`documentation-writer`](../../../.claude/skills/documentation-writer/SKILL.md), [`doc-coauthoring`](../../../.claude/skills/doc-coauthoring/SKILL.md)

### Capstone
- 364-1-4091/4101 פרויקט מסכם — not a skill, an integrative artifact. The Shkhina equivalent is any client engagement applying multiple skills end-to-end (use [`workflow-ml-pipeline`](../../../.claude/skills/workflow-ml-pipeline/SKILL.md) or [`workflow-ai-agent`](../../../.claude/skills/workflow-ai-agent/SKILL.md))

## Build status

| Wave | Date | Skills |
|---|---|---|
| Cornerstones | 2026-05-03 | operations-research, quality-engineering, ie-project-management, decision-analysis, simulation-modeling |
| Full curriculum | 2026-05-03 | engineering-economy, supply-chain-management, design-of-experiments, process-mining, human-factors-design, methods-engineering, is-analysis-design, is-strategy-mgmt, game-theory-agents, statistics-inference, knowledge-management, product-management |
| **Total** | | **17 IE skills** |

## Folder structure

```
industrial-engineering/
├── README.md                      ← this file (curriculum complete map)
├── topics/                        ← per-topic bridge READMEs (TODO as patterns emerge)
│   ├── operations-research/
│   ├── quality-engineering/
│   ├── project-management/
│   ├── decision-analysis/
│   └── simulation-modeling/
├── playbooks/                     ← cross-topic operational playbooks (TODO)
└── references/
    └── bgu-curriculum-2026.md     ← yearbook excerpt (sourced data)
```

Skill code lives at `~/.claude/skills/<skill-name>/SKILL.md`. Topic folders here hold the **bridge** between BGU course material and Shkhina's operational use.

## See also
- [`business/skills/r-and-d.md`](../../skills/r-and-d.md) — R&D dept skill manifest (IE skills listed here)
- [`business/r-and-d/README.md`](../README.md)
- [`business/_visualizations/05-rnd-tech-radar.jpeg`](../../_visualizations/05-rnd-tech-radar.jpeg)

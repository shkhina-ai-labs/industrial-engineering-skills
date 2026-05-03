---
name: human-factors-design
description: Human factors engineering and ergonomics (הנדסת גורמי אנוש) for Shkhina UX — cognitive load, attention, error-prevention, fitts' law, hick's law, mental models, accessibility, designing for high-stress users (incident response, trading, medical). Sourced from BGU IE&M course 364-1-4311. Use when designing demo flows, agent UX, dashboards, alert systems, or any human-facing interface where user error or cognitive overload is a risk.
---

# Human Factors Design (הנדסת גורמי אנוש)

The science of designing for the human in the loop. Why some interfaces feel effortless and others feel like they're fighting you.

## When to use
- "Designing the new Shkhina dashboard — what's the cognitive load budget?"
- "Onkolos health alerts: 50/day — alert fatigue?"
- "Demo flow: where do prospects hesitate or click wrong button?"
- "Agent confirmation gates: when do users blindly approve?"
- "Impilo clinical UI — how to prevent medication errors?"

## Core methods

### Hick's Law
Decision time = a + b · log₂(N+1). More choices = exponentially slower decisions. Cap menu options at 7±2.

### Fitts' Law
Time-to-target = a + b · log₂(distance/size + 1). Big, close targets are faster. Apply to demo CTAs, primary buttons.

### Cognitive load (Sweller)
Working memory holds ~7 chunks. Three load types:
- **Intrinsic** — inherent task complexity (can't reduce, only chunk)
- **Extraneous** — bad design (eliminate aggressively)
- **Germane** — schema-building (encourage)

Goal: maximize germane, minimize extraneous, manage intrinsic via chunking.

### Attention & vigilance
- **Sustained attention degrades after ~20 min** — design for breaks/recoveries
- **Alert fatigue:** > 1 alert/hour = users learn to ignore. Calibrate severity tiers.
- **Salience hierarchy:** color > motion > size > position. Use sparingly.

### Error prevention (Norman)
- **Slips** — right plan, wrong execution → make affordances clear
- **Mistakes** — wrong plan → improve mental model
- **Constraints:** physical (can't), logical (won't), cultural (don't)
- **Forcing functions** — confirmation gates, undo windows
- **Affordances** — visual cues for what's clickable/editable

### Mental models
Match the system to user's existing mental model. If you must break it, train explicitly.

### Accessibility (intersects with `accessibility-auditor`)
Color contrast (WCAG AA = 4.5:1), keyboard nav, screen reader, motion-reduce, font size.

## Shkhina-specific applications

### Demo UX (high-leverage — first impression)
- Hick's: keep visible options ≤ 5 in initial demo state
- Fitts': primary CTA = big, central, contrasting color
- Cognitive load: progressive disclosure — reveal complexity as user demonstrates readiness
- Error prevention: confirm destructive actions, allow undo
- Pair with [`demo-audit`](../demo-audit/SKILL.md) — add HF criteria to scoring

### Shkhina agent confirmation gates
- Per agent-security-patterns: destructive ops need 5-min confirm window
- HF angle: rate of "blind confirm" = error mode → require active typed phrase for critical, vary phrasing to prevent muscle memory

### Alert design (Onkolos health, Shkhina ops)
- Severity tiers: INFO / WARN / CRITICAL with different channels
- WARN/CRITICAL volume budget: < 5/day each — anything more = re-tune thresholds (with `quality-engineering` SPC)
- Each alert = (what + why + suggested action + acknowledge button)

### Dashboard design (paired with `dashboard-design`)
- Above-fold: ≤ 5 KPIs, freshest data first
- Color: red/yellow/green only for alerts (don't decorate)
- Drill-down progressive (one click = +1 detail layer)

### Hebrew RTL considerations
- Reading order R-to-L → primary action on LEFT (visual end)
- Number direction stays L-to-R (numerical)
- Mixed-language fields: explicit direction marks

## Sub-agent leverage
```
Use the Agent tool with subagent_type=general-purpose:
- prompt: "Apply human factors review to Shkhina interface: [interface description or screenshot path]
   1. Cognitive load assessment (intrinsic / extraneous / germane)
   2. Hick's + Fitts' on key interactions
   3. Error-prevention audit (slips, mistakes, missing constraints)
   4. Attention/alert budget if relevant
   5. Mental-model match check
   6. Output: prioritized list of HF issues + specific fixes"
- Tools: Read (for screenshots/specs), WebFetch (for live UI)
```

## Skill chain
- Pairs with [`ui-ux-design`](../ui-ux-design/SKILL.md), [`accessibility-auditor`](../accessibility-auditor/SKILL.md) (operational layer for HF principles)
- Pairs with [`demo-audit`](../demo-audit/SKILL.md) (HF criteria added to demo scoring)
- Pairs with [`agent-security-patterns`](../agent-security-patterns/SKILL.md) (confirmation gate UX)
- Pairs with [`quality-engineering`](../quality-engineering/SKILL.md) (alert tuning via SPC)
- Pairs with [`dashboard-design`](../dashboard-design/SKILL.md)

## Course origin
- BGU 364-1-4311 — הנדסת גורמי אנוש (Human Factors Engineering)

## References
- `references/cognitive-load-checklist.md`
- `references/hicks-fitts-cheatsheet.md`
- `references/error-prevention-patterns.md`
- `references/alert-fatigue-tuning.md`
- `references/rtl-design-notes.md`

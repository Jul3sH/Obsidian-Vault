---
type: reference
created: 2026-05-18
---

# Sprint Planning (DSDM Timebox Planning)

**Open this when you want to understand how sprints are planned and committed.** This covers the MoSCoW prioritisation rules, capacity allocation, and the timebox planning process. In DSDM terms, a sprint is a Timebox.

For the skill that runs the sprint planning ceremony, see [[../skills/sprint-plan/_index|sprint-plan]].
For how Epics are prioritised (WSJF), see [[wsjf|WSJF Reference]].
For the full planning hierarchy, see [[agile-workflow|Agile Workflow]].

---

## Overview

Sprint planning uses a **DSDM/Scrum hybrid**: stories are sized using adapted Fibonacci (1/2/3/5/8) during story definition, then prioritised using MoSCoW at sprint planning time. The MoSCoW classification drives a capacity-based commitment model — Must Haves are guaranteed, the rest is flex.

This approach replaces WSJF at the story level. WSJF is used at the Epic level only (deciding which initiative receives investment). Within an Epic, the Product Owner uses MoSCoW to decide what gets done this sprint.

---

## DSDM MoSCoW Rules for Timebox Planning

### Rule 1: Apply MoSCoW at Three Levels

Every requirement must carry a MoSCoW priority at three levels — Project, Increment, and Timebox. The Timebox priority is set fresh at the start of each sprint and may differ from the project-level rating. Never assume a project-level Must Have automatically becomes a Timebox Must Have.

### Rule 2: Enforce the 60% Must Have Cap

Must Have effort must never exceed **60% of Timebox capacity** (velocity in story points or hours). If Musts exceed 60%, scope must be negotiated before the Timebox begins — not during it.

### Rule 3: Reserve the Remaining 40% as Flex

Structure the remaining capacity as follows:
- **~20%** Should Have — important but deliverable next Timebox if needed
- **~20%** Could Have — desirable; first to be dropped if Musts overrun
- **Won't Have** items are explicitly parked — documented but out of scope for this Timebox

### Rule 4: Guarantee the Musts

The commitment to deliver all Must Have stories by the end of the Timebox is unconditional. If a Must is at risk mid-sprint, Could Haves are dropped first, then Should Haves — **never** reduce a Must to protect optional scope.

### Rule 5: Re-evaluate at Every Timebox Boundary

MoSCoW priorities are not inherited from the previous Timebox. At the start of each planning session, review all candidate stories and re-apply MoSCoW in the context of current goals, dependencies, and remaining project scope.

### Rule 6: "Won't Have" is Not Rejection

Won't Have means *not this Timebox*. Every Won't Have must be explicitly returned to the backlog with a note. This prevents scope from silently disappearing and ensures the PO can re-prioritise it in a future Timebox.

### Rule 7: MoSCoW Ratings Require Team Agreement

MoSCoW categories are set **collaboratively** between the PO (who owns value/priority) and the team (who own effort estimates). A story cannot be labelled Must Have if the team has not confirmed it is feasible within the Timebox.

**Solo operator adaptation:** As both PO and team, the collaborative check becomes a self-check: "Am I labelling this Must because it genuinely must be done this sprint, or because it feels urgent?" Apply the same anti-mood-bias discipline used in WSJF scoring.

### Rule 8: Validate Against the Timebox Goal

Every Must Have must have a clear, traceable link to the Timebox goal. If a Must Have cannot be connected to the goal, its rating should be challenged — it may actually be a Should Have or Could Have.

---

## Quick Reference Card

| Category | Commitment | Capacity Target | Can Be Dropped? |
|----------|------------|-----------------|-----------------|
| Must Have | Unconditional | Max 60% | Never |
| Should Have | Strong intent | ~20% | Only if Musts at risk |
| Could Have | Best effort | ~20% | First to drop |
| Won't Have | Explicitly out | 0% | N/A — parked for later |

---

## MoSCoW Classification Criteria

The Product Owner assigns MoSCoW based on five factors:

1. **Business value** — how much does this move the needle on the sprint goal or a wider 3-month objective?
2. **Dependencies** — stories that unblock others (or other teams) get pulled up
3. **Risk** — high-uncertainty stories go early in the sprint (fail fast principle)
4. **Urgency vs importance** — conscious separation; urgency without importance is a backlog trap
5. **Stakeholder input from Sprint Review** — the backlog gets re-ordered after each review based on live feedback

---

## Capacity Planning

Sprint capacity is calculated in story points (size numbers, not hours):

1. **Determine total capacity** — based on available hours mapped to story points
2. **Apply the 60/20/20 split:**
   - Must Haves ≤ 60% of capacity
   - Should Haves ≈ 20%
   - Could Haves ≈ 20%
3. **Validate:** sum all Must Haves. If > 60%, negotiate scope before committing.

**Example:** If sprint capacity is 20 points:
- Must Haves: max 12 points
- Should Haves: ~4 points
- Could Haves: ~4 points

---

## Jira Implementation

MoSCoW is tracked in Jira via a custom field on Story issue types:
- **Field:** MoSCoW (single-select: Must / Should / Could / Won't)
- **Dashboard/filter:** calculate % of sprint capacity allocated to Must Have stories before the sprint is committed
- **Board:** BWS (Development Sprints)

---

## Links

- [[wsjf|WSJF Reference]] — Epic-level prioritisation (upstream of MoSCoW)
- [[../skills/sprint-plan/_index|sprint-plan skill]] — the ceremony that applies these rules
- [[portfolio-kanban|Portfolio Kanban]] — how Epics flow through the system
- [[epic|Epic Reference]] — Epic definition and WSJF scoring

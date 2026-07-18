---
type: reference
created: 2026-05-18
updated: 2026-06-09
---

# Timebox Planning (DSDM)

**Open this when you want to understand how timeboxes are planned and committed.** This covers the MoSCoW prioritisation rules, capacity allocation, and the timebox planning process. This workflow is DSDM-derived: a timebox is the core unit of delivery.

For the skill that runs the timebox planning ceremony, see [[../skills/timebox-plan/_index|timebox-plan]].
For how Projects are prioritised (WSJF), see [[wsjf|WSJF Reference]].
For the full planning hierarchy, see [[project-workflow|Project Workflow]].

---

## Overview

Timebox planning uses a **DSDM/Scrum hybrid**: deliverables are sized using adapted Fibonacci (1/2/3/5/8) during deliverable definition, then prioritised using MoSCoW at timebox planning time. The MoSCoW classification drives a capacity-based commitment model — Must Haves are guaranteed, the rest is flex.

This approach replaces WSJF at the deliverable level. WSJF is used at the Project level only (deciding which initiative receives investment). Within a Project, the Product Owner uses MoSCoW to decide what gets done this timebox.

---

## DSDM MoSCoW Rules for Timebox Planning

### Rule 1: Apply MoSCoW at Three Levels

Every requirement must carry a MoSCoW priority at three levels — Project, Increment, and Timebox. The Timebox priority is set fresh at the start of each timebox and may differ from the project-level rating. Never assume a project-level Must Have automatically becomes a Timebox Must Have.

### Rule 2: Enforce the 60% Must Have Cap

Must Have effort must never exceed **60% of Timebox capacity** (velocity in story points or hours). If Musts exceed 60%, scope must be negotiated before the Timebox begins — not during it.

### Rule 3: Reserve the Remaining 40% as Flex

Structure the remaining capacity as follows:
- **~20%** Should Have — important but deliverable next Timebox if needed
- **~20%** Could Have — desirable; first to be dropped if Musts overrun
- **Won't Have** items are explicitly parked — documented but out of scope for this Timebox

### Rule 4: Guarantee the Musts

The commitment to deliver all Must Have deliverables by the end of the Timebox is unconditional. If a Must is at risk mid-timebox, Could Haves are dropped first, then Should Haves — **never** reduce a Must to protect optional scope.

### Rule 5: Re-evaluate at Every Timebox Boundary

MoSCoW priorities are not inherited from the previous Timebox. At the start of each planning session, review all candidate deliverables and re-apply MoSCoW in the context of current goals, dependencies, and remaining project scope.

### Rule 6: "Won't Have" is Not Rejection

Won't Have means *not this Timebox*. Every Won't Have must be explicitly returned to the backlog with a note. This prevents scope from silently disappearing and ensures the PO can re-prioritise it in a future Timebox.

### Rule 7: MoSCoW Ratings Require Team Agreement

MoSCoW categories are set **collaboratively** between the PO (who owns value/priority) and the team (who own effort estimates). A deliverable cannot be labelled Must Have if the team has not confirmed it is feasible within the Timebox.

**Solo operator adaptation:** As both PO and team, the collaborative check becomes a self-check: "Am I labelling this Must because it genuinely must be done this timebox, or because it feels urgent?" Apply the same anti-mood-bias discipline used in WSJF scoring.

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

1. **Business value** — how much does this move the needle on the timebox goal or a wider 3-month objective?
2. **Dependencies** — deliverables that unblock others get pulled up
3. **Risk** — high-uncertainty deliverables go early in the timebox (fail fast principle)
4. **Urgency vs importance** — conscious separation; urgency without importance is a backlog trap
5. **Stakeholder input from Timebox Review** — the backlog gets re-ordered after each review based on live feedback

---

## Capacity Planning

Timebox capacity is calculated in story points (size numbers, not hours):

1. **Determine total capacity** — based on available hours mapped to story points
2. **Apply the 60/20/20 split:**
   - Must Haves ≤ 60% of capacity
   - Should Haves ≈ 20%
   - Could Haves ≈ 20%
3. **Validate:** sum all Must Haves. If > 60%, negotiate scope before committing.

**Example:** If timebox capacity is 20 points:
- Must Haves: max 12 points
- Should Haves: ~4 points
- Could Haves: ~4 points

---

## Jira Implementation

MoSCoW is tracked in Jira via a custom field on Story issue types:
- **Field:** MoSCoW (single-select: Must / Should / Could / Won't)
- **Dashboard/filter:** calculate % of timebox capacity allocated to Must Have deliverables before the timebox is committed
- **Board:** BWS (Development Sprints)

---

## Links

- [[wsjf|WSJF Reference]] — Project-level prioritisation (upstream of MoSCoW)
- [[portfolio-kanban|Portfolio Kanban]] — how Projects flow through the system
- [[project|Project Reference]] — Project definition and WSJF scoring

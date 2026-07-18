---
created: 2026-05-07
updated: 2026-05-20
type: reference
---

# Agile Workflow

**Open this document when you want to understand the planning hierarchy, sprint cadence, ceremonies, and operating guardrails.** This is the process — how work flows from goals to execution.

For the Jira configuration that supports this workflow (project structure, field mapping, labels, cron expressions), see [[jira-system-design|Jira System Design]].

For Epic-specific guidance — Objectives, Business Outcomes/Key Results, WSJF scoring at Epic level, the commitment gate — see [[epic|Epic Reference]].

For Story and Enabler guidance — types, sizing, acceptance criteria, and scope discipline — see [[story|Story Reference]].

For the WSJF scoring methodology — formula, components, counter-factual questioning, anti-mood-bias check — see [[wsjf|WSJF Reference]].

For how sprints are planned and committed (MoSCoW, capacity split, DSDM rules) — see [[sprint-planning|Sprint Planning (DSDM Timebox Planning)]].

For how the AI OS itself is architected — working memory, skill structure, two-layer design — see [[system-design-principles|System Design Principles]].

---

## Planning Hierarchy

```
Goals (6 workstreams, quarterly)
  SMART Goals --- wellbeing, relationships, finance, personal
  OKRs        --- career, performance
     |
Epics --- Objective + BOs/KRs + WSJF                    /epic-planner
           Gate: is this initiative worth starting?
     |
Stories --- story, enabler                              /define-user-story
           created in wiki/stories/                     /define-enabler
           Gate: scoped + sized + value-linked?
     |
Sprint --- MoSCoW committed and tracked                /sprint-plan + /jira-sync
```

Goals set direction. Epics answer "is this worth the commitment?" Stories answer "is this well-defined enough to build?" Sprint planning answers "what delivers the most value this timebox?"

For the goals methodology (SMART vs OKR split, quarterly cadence, guard rails), see [[workstream-framework|Workstream Framework]].

**Prioritisation happens at two levels, using different methods:**
- **Epic level** (in `/epic-planner`) — WSJF ranks Epics against each other to decide which initiative to pursue. See [[wsjf|WSJF Reference]].
- **Sprint level** (in `/sprint-plan`) — MoSCoW prioritises stories within a timebox using the 60/20/20 capacity split. See [[sprint-planning|Sprint Planning]].

Stories are **not** scored with WSJF. They are sized during definition (effort, complexity, uncertainty → adapted Fibonacci 1/2/3/5/8) and prioritised by the Product Owner at sprint planning time using MoSCoW.

---

## Sprint & Ceremonies

- **Sprint length:** 1 week
- **Capacity:** 40 hours (full working week)
- **Maximum story size:** 5 (17-40h) fits in one sprint. Stories at the top of the range (~40h) are candidates for splitting at sprint planning time.

| Ceremony | When | Duration | Trigger |
|----------|------|----------|---------|
| Daily stand-up | 6:00 AM HKT, Mon-Fri | ~5 min | Scheduled (auto) |
| Sprint planning | Weekend (Sat or Sun) | ~45 min | Manual (`/sprint-plan`) |
| Retrospective | 4:00 PM HKT, Friday | ~20 min | Scheduled (auto) |

### Ceremony skills

| Skill | Status |
|-------|--------|
| `/jira-sync` | Active --- push wiki epics/stories to Jira BWS |
| `/standup` | Someday --- 5-min daily check-in; 3 questions only |
| `/sprint-plan` | Someday --- manual; MoSCoW commitment, DSDM timebox rules |
| `/retro` | Someday --- hard cap 20 min; 1 win, 1 improvement, 1 change |

---

## Operating Guardrails

- **Ceremonies must be frictionless.** Any ceremony that feels like overhead will get dropped. Hard time caps are non-negotiable.
- **Don't over-commit sprint capacity.** Over-commitment feeds the guilt spiral. Budget 38h execution + 2h ceremony.
- **Sprint planning is manual by design.** Weekend schedule varies --- auto-triggering creates pressure, not structure.
- **BAU Kanban stays gut-driven.** Adding WSJF to tasks under ~2h is pure overhead. Deadlines (today / this week / this month) are sufficient prioritisation at that granularity.
- **Must Haves never exceed 60%.** The MoSCoW 60/20/20 split protects against over-commitment. See [[sprint-planning|Sprint Planning]].

---

## Links

- [[jira-system-design|Jira System Design]] --- Jira project structure, field mappings, labels
- [[wsjf|WSJF Reference]] --- Epic-level prioritisation methodology
- [[sprint-planning|Sprint Planning (DSDM Timebox Planning)]] --- MoSCoW rules, capacity split
- [[epic|Epic Reference]] --- Epic definition and WSJF scoring
- [[story|Story Reference]] --- Story/Enabler types and sizing
- [[portfolio-kanban|Portfolio Kanban]] --- Epic flow stages

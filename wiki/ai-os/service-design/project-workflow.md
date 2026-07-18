---
created: 2026-05-07
updated: 2026-06-09
type: reference
---

# Project Workflow

**Open this document when you want to understand the planning hierarchy, timebox cadence, ceremonies, and operating guardrails.** This is the process — how work flows from goals to execution.

For the Jira configuration that supports this workflow (project structure, field mapping, labels, cron expressions), see [[jira-system-design|Jira System Design]].

For Project-specific guidance — Objectives, Outcomes/Outputs, WSJF scoring at Project level, the commitment gate — see [[project|Project Reference]].

For Deliverable and Enabler guidance — types, sizing, acceptance criteria, and scope discipline — see [[deliverable|Deliverable Reference]].

For the WSJF scoring methodology — formula, components, counter-factual questioning, anti-mood-bias check — see [[wsjf|WSJF Reference]].

For how timeboxes are planned and committed (MoSCoW, capacity split, DSDM rules) — see [[timebox-planning|Timebox Planning (DSDM)]].

For how the AI OS itself is architected — working memory, skill structure, two-layer design — see [[system-design-principles|System Design Principles]].

> **Vocabulary note:** This workflow uses domain-neutral terms (Project / Deliverable / Timebox) rather than Agile-specific ones (Epic / Story / Sprint). The mechanics are DSDM/Scrum/SAFe-derived and unchanged. See [[_archived/agile-workflow-retired/_index|Agile Workflow (retired)]] for the vocabulary map and lineage.

---

## Planning Hierarchy

See [[planning-hierarchy.excalidraw|Planning Hierarchy diagram]] for a visual of the flow below plus the ceremony cadence, prioritisation methods, and guardrails.

```
Capture --- raw, unclassified ideas               raw/brain-dump.md
             Zero evaluation. "Will I lose this?"
             │  triage routes each item out ↓
     ├──────────────┬───────────────┬─────────────┐
     ▼              ▼               ▼             ▼
  Project        Deliverable      Wiki         Discard
  funnel         (BAU someday)   (reference)
     |
Goals (6 workstreams, quarterly)
  SMART Goals --- wellbeing, relationships, finance, personal
  OKRs        --- career, performance
     |
Projects --- Objective + Outcomes/Outputs + WSJF       /project-planner
             Funnel gate: hypothesis + trigger?
             Commitment gate: is this worth starting?
     |
Deliverables --- user-facing, enablers, generic items  /define-user-story
             created in wiki/deliverables/             /define-enabler
             Gate: scoped + sized + value-linked?
     |
Timebox --- MoSCoW committed and tracked               /timebox-plan + /jira-sync
```

Capture comes first and sits **outside** the hierarchy: a zero-evaluation inbox
([[brain-dump|raw/brain-dump.md]]) where any raw idea lands so it stops pulling
focus. Items there are unclassified — triage later routes each one to the Project
funnel (including standalone deliverable ideas, captured as XXS Project
candidates), to the wiki (reference), or to the bin. Nothing is a project until
it earns a hypothesis + trigger in the [[funnel|funnel]]. See
[[prioritization-framework|Prioritization Framework]] for the capture → funnel →
scheduled logic.

Goals set direction. Projects answer "is this worth the commitment?" Deliverables answer "is this well-defined enough to build?" Timebox planning answers "what delivers the most value this week?"

**One raw tier.** Capture ([[brain-dump|raw/brain-dump.md]]) is the only dump
that sits before a structured stage — it precedes the [[funnel|funnel]], and
covers both Project-sized ideas and standalone deliverable ideas (the latter
enter the funnel as XXS Project candidates rather than as a separate
deliverable-level tier). Capture is not synced to Jira — a POR card is only
created once an item passes into the funnel.

For the goals methodology (SMART vs OKR split, quarterly cadence, guard rails), see [[workstream-framework|Workstream Framework]].

**Prioritisation happens at two levels, using different methods:**
- **Project level** (in `/project-planner`) — WSJF ranks Projects against each other to decide which initiative to pursue. See [[wsjf|WSJF Reference]].
- **Timebox level** (in `/timebox-plan`) — MoSCoW prioritises deliverables within a timebox using the 60/20/20 capacity split. See [[timebox-planning|Timebox Planning]].

Deliverables are **not** scored with WSJF. They are sized during definition (effort, complexity, uncertainty → adapted Fibonacci 1/2/3/5/8) and prioritised by the Product Owner at timebox planning time using MoSCoW.

---

## Timebox & Ceremonies

- **Timebox length:** 1 week
- **Capacity:** 40 hours (full working week)
- **Maximum deliverable size:** 5 (17-40h) fits in one timebox. Deliverables at the top of the range (~40h) are candidates for splitting at timebox planning time.

| Ceremony         | When                 | Duration | Trigger                  |
| ---------------- | -------------------- | -------- | ------------------------ |
| Daily stand-up   | 6:00 AM HKT, Mon-Fri | ~5 min   | Scheduled (auto)         |
| Timebox planning | Weekend (Sat or Sun) | ~45 min  | Manual (`/timebox-plan`) |
| Retrospective    | 4:00 PM HKT, Friday  | ~20 min  | Scheduled (auto)         |

### Ceremony skills

| Skill | Status |
|-------|--------|
| `/jira-sync` | Active --- push wiki projects/deliverables to Jira BWS |
| `/standup` | Someday --- 5-min daily check-in; 3 questions only |
| `/timebox-plan` | Someday --- manual; MoSCoW commitment, DSDM timebox rules |
| `/retro` | Someday --- hard cap 20 min; 1 win, 1 improvement, 1 change |

---

## Operating Guardrails

- **Ceremonies must be frictionless.** Any ceremony that feels like overhead will get dropped. Hard time caps are non-negotiable.
- **Don't over-commit timebox capacity.** Over-commitment feeds the guilt spiral. Budget 38h execution + 2h ceremony.
- **Timebox planning is manual by design.** Weekend schedule varies --- auto-triggering creates pressure, not structure.
- **BAU Kanban stays gut-driven.** Adding WSJF to tasks under ~2h is pure overhead. Deadlines (today / this week / this month) are sufficient prioritisation at that granularity.
- **Must Haves never exceed 60%.** The MoSCoW 60/20/20 split protects against over-commitment. See [[timebox-planning|Timebox Planning]].

---

## Links

- [[jira-system-design|Jira System Design]] --- Jira project structure, field mappings, labels
- [[wsjf|WSJF Reference]] --- Project-level prioritisation methodology
- [[timebox-planning|Timebox Planning (DSDM)]] --- MoSCoW rules, capacity split
- [[project|Project Reference]] --- Project definition and WSJF scoring
- [[deliverable|Deliverable Reference]] --- Deliverable/Enabler types and sizing
- [[portfolio-kanban|Portfolio Kanban]] --- Project flow stages

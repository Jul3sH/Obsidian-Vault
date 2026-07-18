---
created: 2026-05-20
type: reference
---

# Jira System Design

**Open this document when you want to understand the Jira configuration: project structure, field mappings, labels, and sync conventions.** This is the system design for the execution layer.

For the project workflow that this Jira setup supports (planning hierarchy, ceremonies, guardrails), see [[project-workflow|Project Workflow]].

For the Portfolio Kanban board configuration, see [[portfolio-kanban|Portfolio Kanban]].

---

## Connection Details

- **Site:** agileict.atlassian.net
- **Cloud ID:** `bbbb75d2-e2e4-44fe-a329-e506d1128c29`

---

## Project Structure

| Project | Key | Type | Purpose |
|---------|-----|------|---------|
| Development Sprints | BWS | Software (next-gen) | Sprint-based execution. Wiki-managed Epics and Stories. 40h/week capacity. |
| Portfolio Kanban | POR | Software (classic Kanban) | Epic flow tracking. Board 48. See [[portfolio-kanban|Portfolio Kanban]]. |
| BAU Kanban | PERF | Software (classic Kanban) | Day-to-day tasks. Gut-prioritised by deadline. No WSJF --- overhead exceeds value at this task size. |
| My Discovery Project | MDP | Product Discovery | Ideas only. Not used for execution tracking. |

---

## Backlog Semantics by Board

"Backlog" means something different on each board — both meanings matter:

| Board | Backlog view holds | Wiki equivalent | Jira presence |
|-------|--------------------|------------------|----------------|
| POR (Portfolio Kanban) | Epics with status `Funnel` — Project ideas that haven't passed the commitment gate | [[funnel|funnel.md]] | Every funnel.md row gets a card (label `funnel`, status `Funnel`) |
| BWS (Agile Sprints) | Stories/Enablers/Tasks that passed the admission gates (scoped, sized, value-linked) but aren't yet in a sprint | each Project's `## Deliverables` section | Only once admitted via `/define-user-story`, `/define-enabler`, or `/define-task` |
| *(no board)* | Deliverable ideas tied to a Project that haven't passed admission gates yet | each Project's `## Funnel` section | None — not synced until promoted |

See [[portfolio-kanban|Portfolio Kanban]] for how the POR Backlog mirrors the Project funnel.

---

## Wiki to Jira Mapping (BWS)

- Wiki **Project** -> Jira **Epic** in BWS (note: "Epic" is the Jira issue type; the wiki uses "Project")
- Wiki **Deliverable** (story/enabler) -> Jira **Story** in BWS, linked to its parent Epic

The wiki is the **source of truth** for planning. Jira is the **execution layer** (status, sprint assignment, board view). Run `/jira-sync` after each `/project-planner` session to push changes. Changes always flow wiki -> Jira, never the reverse.

**Exception:** Portfolio Kanban flow status is pulled Jira -> wiki by `/jira-pull`. See [[portfolio-kanban|Portfolio Kanban]] for details.

### Why the wiki is the source of truth

Jira provides the visual Kanban and task tracking but lacks structured planning context (KRs, WSJF rationale, definition of done). The wiki captures the *why* behind every prioritisation decision. If Jira were the source of truth, that reasoning would be lost and WSJF scores would become meaningless numbers disconnected from their rationale.

---

## Label Design

Every synced story receives standard labels:

| Label | Purpose |
|-------|---------|
| `wiki-sync` | Marks the issue as wiki-managed --- edit in the wiki, not directly in Jira |
| `career` (workstream) | Enables filtering by workstream across the board |
| `size-N` | Adapted Fibonacci size (1/2/3/5/8) for capacity planning |

---

## Story Points

1 SP = 1 hour. This makes sprint capacity immediately readable on the board --- 40 SP committed = a full sprint. The `hours` field in wiki frontmatter is the source; `/jira-sync` writes it to Jira's story points field (`customfield_10016`) on every sync.

Traditional unitless story points add a translation layer that serves no purpose when one person plans their own sprints.

---

## MoSCoW Field

MoSCoW priority is tracked via a custom field on Story issue types:
- **Field:** MoSCoW (single-select: Must / Should / Could / Won't)
- **Set during:** `/sprint-plan` (not during story definition)
- **Dashboard/filter:** calculate % of sprint capacity allocated to Must Have stories before the sprint is committed

---

## Scheduled Tasks (Cron)

**HKT = UTC+8**

| Task | Cron (UTC) | Local Time |
|------|-----------|------------|
| Daily stand-up | `0 22 * * 0-4` | 6:00 AM Mon-Fri HKT |
| Retrospective | `0 8 * * 5` | 4:00 PM Friday HKT |

---

## Links

- [[project-workflow|Project Workflow]] --- planning hierarchy, ceremonies, guardrails
- [[portfolio-kanban|Portfolio Kanban]] --- Project flow stages and POR board mapping
- [[timebox-planning|Timebox Planning]] --- MoSCoW rules and capacity planning

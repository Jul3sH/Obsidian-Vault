---
type: archived
archived: 2026-06-09
replaced-by: project-workflow
---

# Agile Workflow — Retired (9 June 2026)

> This cluster of documents defined the Agile Workflow vocabulary used before 9 June 2026. Preserved verbatim. The live replacement is the **Project Workflow** cluster in the parent `service-design/` folder.

## Why it was retired

Vocabulary replaced for two reasons:
1. **Solopreneur fit:** "Epic" and "Sprint" are Scrum/SAFe terms that overstate scale for a solo operator. "Project" and "Timebox" are accurate and self-explanatory at that scale.
2. **Portability:** The AI OS is designed to be cloned for non-technical teams. "Project / Deliverable / Timebox" requires no Agile literacy to understand.

The *mechanics* are unchanged. This remains a DSDM/Scrum/SAFe-derived workflow with WSJF prioritisation, MoSCoW timebox planning, and Portfolio Kanban flow control. Only the vocabulary changed.

## Vocabulary map

| Old term (retired) | New term (live) | Notes |
|--------------------|-----------------|-------|
| Epic | Project | Top-level initiative with Objective + KRs + WSJF |
| Story / User Story | Deliverable | Child work item, user-facing |
| Enabler | Enabler | Unchanged |
| Sprint | Timebox | The weekly execution cycle |
| Agile Workflow | Project Workflow | The spine document |
| Epic Reference | Project Reference | Definition + WSJF guide |
| Stories & Enablers Reference | Deliverable Reference | Child item guide |
| Sprint Planning (DSDM Timebox Planning) | Timebox Planning (DSDM) | MoSCoW + capacity planning |
| wiki/epics/ | wiki/projects/ | Folder for all Projects |
| /epic-planner | /project-planner | Skill for defining Projects |

**Unchanged:** Backlog, Story Points, Portfolio Kanban, WSJF, Portfolio Backlog, MoSCoW, Definition of Done, Acceptance Criteria, Success Criteria, /define-user-story, /define-enabler.

**Jira note:** Jira issue types are NOT renamed. Jira "Epic" = wiki "Project". The wiki vocabulary and Jira issue types are deliberately decoupled to avoid Jira project configuration changes. wiki Project = Jira Epic issue type.

## Archived documents (verbatim)

Only the four renamed documents are archived here. `portfolio-kanban.md` and `portfolio-backlog.md` were updated in place (their basenames did not change) and are not duplicated here.

- [[agile-workflow]] (this folder) - replaced by `service-design/project-workflow.md`
- [[epic]] (this folder) - replaced by `service-design/project.md`
- [[story]] (this folder) - replaced by `service-design/deliverable.md`
- [[sprint-planning]] (this folder) - replaced by `service-design/timebox-planning.md`

## To reinstate Agile vocabulary

1. Copy the 4 archived files back to `wiki/ai-os/service-design/`
2. Copy `project-workflow.md` → `agile-workflow.md` (or delete new versions)
3. Update `service-design/_index.md` to point to the old file names
4. Update `taxonomy.md` worked-examples table
5. Reverse the vocab map in CLAUDE.md, the skill, and memory

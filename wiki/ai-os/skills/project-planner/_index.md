---
type: skill-index
created: 2026-05-07
updated: 2026-07-09
skill-path: ~/.claude/skills/project-planner/SKILL.md
---

# Project Planner Skill

Guides the user through defining a new Project (initiative with OKRs), scores it with WSJF at the project level, and writes it to the wiki.

## Trigger phrases
"Plan a new initiative", "define a project", "I want to structure my goals", "WSJF scoring", "what should I work on next"

## What this skill does - and does not do

**Does:**
- Defines the Project (objective, KRs, t-shirt size)
- Scores the Project with WSJF (counter-factual questioning, anti-mood-bias checks)
- Creates `wiki/projects/[project-slug].md` - the project file with WSJF scoring table
- Adds a `## Project Summary File Map` so the Project page links to all live supporting evidence files
- Updates `wiki/projects/_index.md` - the project ranked list
- Captures a rough work breakdown (informal, for sizing context only)

**Does not:**
- Create deliverable or enabler files in `wiki/deliverables/` - that is the job of `/define-user-story` or `/define-enabler`
- Score individual deliverables with WSJF - that happens during deliverable definition
- Write to `wiki/deliverables/_index.md` - deliverable definition skills own the deliverable queue

The deliverable definition skills create and score the deliverables. Project Planner hands off to them at the end of the session.

## Phases
1. **Define the Project** - workstream, objective (outcome not activity), max 3 KRs, t-shirt size
2. **WSJF Scoring (Project level)** - rough work breakdown for sizing, then WSJF scoring via counter-factual questioning; anti-mood-bias checks on Time Criticality
3. **Write to Wiki** - project file + project index only; hands off to `/define-user-story` / `/define-enabler`

> **Jira note:** wiki "Project" = Jira "Epic" issue type. Jira issue types are not renamed - this skill creates POR Epics in Jira.

## Links
- **Skill file:** `~/.claude/skills/project-planner/SKILL.md`
- **Mirror:** [[SKILL|SKILL.md]]
- **Outputs:** [[../../projects/_index|Projects]]
- **Design principles:** [[../../service-design/project-workflow|Project Workflow]] - planning hierarchy and prioritisation model

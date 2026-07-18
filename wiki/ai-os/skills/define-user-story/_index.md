---
type: skill-index
created: 2026-05-08
skill-path: ~/.claude/skills/define-user-story/SKILL.md
---

# Define User Story Skill

Defines a user story with story statement (As a / I want / So that), acceptance criteria, Definition of Done, and WSJF scoring. Writes the story file to `wiki/projects/` and updates the WSJF priority queue.

## Trigger phrases
"Define a story", "create a user story", "I want to work on [X]", "acceptance criteria", "define the DoD", or after running `/project-planner` to break a project into stories.

## What this skill does — and does not do

**Does:**
- Guides the user through story statement, acceptance criteria, and DoD
- Scores the story with WSJF (counter-factual questioning, anti-mood-bias checks)
- Creates `wiki/projects/[story-slug].md`
- Updates `wiki/projects/_index.md` — the WSJF priority queue
- Guards against scope creep, XL stories, and bundled stories

**Does not:**
- Create Jira issues — that is `/jira-sync`'s job
- Define enablers — use `/define-enabler` for technical/architectural work
- Define projects — use `/project-planner` for that

## Steps
1. **Identify the story** — which project, story statement, acceptance criteria (3–5), Definition of Done
2. **T-shirt size** — guard against XL (must split) and XS (may be sub-task)
3. **WSJF scoring** — counter-factual questions, rank in queue context
4. **Write to wiki** — story file + index update + log entry
5. **Next steps** — hand off to `/jira-sync`, more stories, or `/sprint-plan`

## Links
- **Skill file:** `~/.claude/skills/define-user-story/SKILL.md`
- **Mirror:** [[SKILL|SKILL.md]]
- **Outputs:** [[../../projects/_index|Projects — WSJF Queue]]
- **Design principles:** [[../../service-design/project-workflow|Project Workflow]] — planning hierarchy and sizing

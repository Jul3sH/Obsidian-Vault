---
type: skill-index
created: 2026-06-14
skill-path: ~/.claude/skills/define-task/SKILL.md
---

# Define Task Skill

Defines a generic deliverable (`type: task`) that doesn't fit the User Story
or Enabler shapes, runs it through the same three backlog admission gates
(Scoped, Sized, Value-linked), and writes it to `wiki/deliverables/`.

## Trigger phrases
"Define a task", "add this as a task", "create a deliverable for [X]" where X
isn't user-facing value or technical runway, or any administrative/operational/
reference work that needs a completion definition, a size, and a Project link
before it enters the backlog.

## What this skill does — and does not do

**Does:**
- Guides the user through a one-sentence Task Description, 2-4 Completion
  Criteria, and a Definition of Done
- Sizes the task (Effort/Complexity/Uncertainty, portfolio comparison)
- Creates `wiki/deliverables/[task-slug].md` with `type: task`
- Updates `wiki/deliverables/_index.md` only if all three admission gates pass
- Redirects to `/define-user-story` or `/define-enabler` if the work is
  actually a story or an enabler in disguise

**Does not:**
- Score with WSJF — that's Project-level only
- Create Jira issues — that is `/jira-sync`'s job

## Steps
1. **Identify the task** — which Project, value-link gate, duplicate check, task description, completion criteria (2-4), Definition of Done
2. **Sizing** — Effort/Complexity/Uncertainty walkthrough, portfolio comparison, guard rails
3. **Confirm and place** — show the Project's backlog section
4. **Write to wiki** — task file + index update (gated) + log entry
5. **Next steps** — hand off to `/jira-sync`, more items, or `/timebox-plan`

## Links
- **Skill file:** `~/.claude/skills/define-task/SKILL.md`
- **Mirror:** [[SKILL|SKILL.md]]
- **Outputs:** [[../../../deliverables/_index|Deliverables — Backlog]]
- **Design principles:** [[../../service-design/deliverable|Deliverables — Reference Guide]]

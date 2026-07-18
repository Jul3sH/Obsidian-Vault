---
type: skill
skill-path: ~/.claude/skills/jira-pull/SKILL.md
---

# jira-pull

Pulls Project flow status from the Portfolio Kanban board in Jira (project PK, board 47) and updates the `flow` field in corresponding wiki Project files. The only skill that writes from Jira → wiki. All other Project fields remain wiki-authoritative.

## Trigger

Run after moving a Project card on the Portfolio Kanban board in Jira:
- `/jira-pull`
- "pull from Jira"
- "sync from Jira"

## What it does

1. Fetches all Epics from board 47 with their current column
2. Maps column name → `flow` value (Funnel/Analyzing/Backlog/Active/Done)
3. Matches each Jira Epic to its wiki file (by `pk-key` frontmatter, then by title)
4. Updates `flow` in frontmatter if changed; adds `pk-key` if absent
5. Updates `wiki/projects/_index.md` Flow column
6. Reports what changed

## What it does NOT touch

Everything except `flow` and `pk-key` — Objective, KRs, WSJF score, size, `status`, `jira-key` are all untouched. Wiki is authoritative for those fields.

## Related skills

- [[../jira-sync/_index|jira-sync]] — pushes wiki → Jira BWS (opposite direction, different board)
- [[../project-planner/_index|project-planner]] — creates new Projects and sets initial `flow: backlog`

## Files

- `SKILL.md` — full skill definition (mirrored from `~/.claude/skills/jira-pull/SKILL.md`)

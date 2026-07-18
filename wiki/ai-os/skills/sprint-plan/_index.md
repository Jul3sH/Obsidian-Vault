---
type: skill-index
created: 2026-05-07
skill-path: ~/.claude/skills/sprint-plan/SKILL.md
---

# Sprint Planning Skill

Runs the weekly sprint planning ceremony for Jira BWS. Reads the WSJF-ranked backlog, guides a prioritisation discussion, creates a Jira sprint, assigns committed stories, and presents a summary for manual review before the user starts the sprint.

## Trigger phrases
"Sprint planning", "plan my sprint", "what should I work on this sprint", "start a new sprint", `/sprint-plan`

## What it does
1. Reads all unstarted BWS stories via JQL, sorted by WSJF priority
2. Presents a ranked table with running capacity total (40h cap)
3. Guides a discussion — challenges over-commitment, flags L stories, resists mood-driven re-ordering
4. Creates the Jira sprint (not started) and assigns committed stories
5. Presents a summary and hands off for manual review
6. User starts the sprint manually in Jira

## Design principles
- **Proposal first, commitment second.** Sprint is created but never started by Claude — that's always a manual user action.
- **Capacity is a hard constraint, not a guideline.** Stories that exceed 40h are flagged, not silently dropped.
- **L stories at the top of their range are surfaced.** A 40h L story is a full sprint — the skill asks for a specific sprint goal rather than a blind commitment.
- **WSJF order is the default.** Deviations require a stated reason — the skill asks for one rather than accepting gut overrides silently.

## Key fields
- Sprint capacity: 40h (1 SP = 1 hour)
- Sprint length: 1 week
- JQL: `project = BWS AND issuetype = Story AND status = "To Do" AND sprint is EMPTY`
- Sprint field in Jira: `customfield_10020`

## Links
- **Skill file:** `~/.claude/skills/sprint-plan/SKILL.md`
- **Agile Workflow:** [[../../service-design/agile-workflow|Agile Workflow]] — sprint cadence and ceremonies
- **Sprint Planning:** [[../../service-design/sprint-planning|Sprint Planning]] — DSDM MoSCoW rules
- **Backlog:** [[../../../projects/_index|Projects — WSJF Queue]]
- **Jira board:** https://agileict.atlassian.net/jira/software/projects/BWS/boards

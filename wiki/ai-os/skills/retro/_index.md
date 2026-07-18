---
type: skill-index
created: 2026-05-07
skill-path: ~/.claude/skills/retro/SKILL.md
---

# Retro Skill

Weekly retrospective ceremony. Runs every Friday at 4 PM HKT. Hard-capped at 20 minutes. Reads the closing sprint from Jira, presents a sprint summary, asks for 1 win / 1 problem / 1 change, and logs the retro.

## What It Does

1. **Reads the sprint** — Fetches story statuses from Jira and this week's standup log.
2. **Shows sprint summary** — Completed vs. carried forward, completion rate.
3. **Asks 3 questions** — One sentence each: win / problem / change.
4. **Logs the retro** — Appends one row to `wiki/ai-os/logs/retro-log.md`.
5. **Actions the change (optional)** — Creates a Jira story or updates a process doc if the change requires it.

## Format: 1-1-1

| Question | Purpose |
|----------|---------|
| 1 win | Anchor on what worked — reinforces good patterns |
| 1 problem | Name what got in the way — honest, not defensive |
| 1 change | One specific, actionable thing for next sprint |

One sentence per answer. The skill enforces this gently.

## Trigger & Scheduling

| Trigger | Type | Time |
|---------|------|------|
| Manual | `/retro` | On demand, anytime |
| Automatic | Cron | 4 PM HKT, Fridays |

## Design Principles

1. **20 minutes hard cap.** Identification only — not resolution. Resolution happens in sprint planning.
2. **One sentence per answer.** Forces distillation. The detail lives in the standup log; the retro captures the headline.
3. **The change must be specific.** "Be more focused" is rejected. "Block 7–12 AM, decline calls before noon" is accepted.
4. **Honest completion rates.** If the sprint was 0% complete, the retro says so. No softening.
5. **The change is optionally actioned.** If the change requires a Jira story or a process update, the skill can create it right there.

## Key Files

- **Skill:** `~/.claude/skills/retro/SKILL.md`
- **Retro Log:** `wiki/ai-os/logs/retro-log.md`
- **Standup Log:** `wiki/ai-os/logs/standup-log.md` (context for the week)
- **Jira Board:** https://agileict.atlassian.net/jira/software/projects/BWS/boards

## Key Takeaways

- Runs every Friday at 4 PM — closes the sprint week
- 20-min hard cap; 3 questions; 1 sentence each
- Change must be specific and actionable
- Optionally actions the change as a Jira story or process update
- Feeds context into Monday's sprint planning

## Links

- **Agile Workflow:** [[../../../service-design/agile-workflow|Agile Workflow]]
- **Retro Log:** [[../../logs/retro-log|retro-log]]
- **Related Ceremonies:** [[../sprint-plan/_index|Sprint Plan]], [[../standup/_index|Standup]]

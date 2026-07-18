---
type: skill-index
created: 2026-05-07
skill-path: ~/.claude/skills/standup/SKILL.md
---

# Standup Skill

End-of-day review ceremony. Runs at 4 PM HKT on weekdays to close out the day before context is lost. Reads the active Jira sprint, asks 3 questions, updates story statuses, and logs the review.

## What It Does

1. **Reads the active sprint** — Fetches current story statuses from Jira BWS.
2. **Asks 3 questions** — What got done? What's in progress? Any blockers?
3. **Updates Jira** — Transitions stories to Done or In Progress; adds comments for blockers and where you left off.
4. **Logs the standup** — Appends one row to `wiki/ai-os/logs/standup-log.md`.

## Why End of Day (Not Morning)

As a solo operator, there's no team to sync with in the morning. The value is in capturing what happened *before you forget it* — status, blockers, and where you left off. That context then feeds the next day naturally when you open Jira.

## Trigger & Scheduling

| Trigger | Type | Time |
|---------|------|------|
| Manual | `/standup` | On demand, anytime |
| Automatic | Cron | 4 PM HKT, weekdays (Mon–Fri) |

Run manually after a late flow-state session to capture progress before context is lost.

## Key Files

- **Skill:** `~/.claude/skills/standup/SKILL.md`
- **Standup Log:** `wiki/ai-os/logs/standup-log.md`
- **Jira Board:** https://agileict.atlassian.net/jira/software/projects/BWS/boards

## Design Principles

1. **5 minutes max.** Three questions. No fluff. The point is capture, not reflection.
2. **Confirm before writing.** The skill summarises its Jira updates and waits for confirmation before touching anything.
3. **No judgment on unproductive days.** If nothing got done, log it and move on. `/retro` is where patterns get examined.
4. **Flow state is a valid trigger.** Running at 6 PM after a late session is just as valid as the 4 PM cron.

## Key Takeaways

- Runs at end of day — captures status before context is lost
- 3 questions: done, in progress, blockers
- Updates Jira story statuses and adds progress comments
- Logs to standup-log.md for reference

## Links

- **Agile Workflow:** [[../../../service-design/agile-workflow|Agile Workflow]]
- **Standup Log:** [[../../logs/standup-log|standup-log]]
- **Related Ceremonies:** [[../sprint-plan/_index|Sprint Plan]], [[../retro/_index|Retro]]

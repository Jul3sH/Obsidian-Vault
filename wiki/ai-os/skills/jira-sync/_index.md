---
type: skill-index
created: 2026-05-07
skill-path: ~/.claude/skills/jira-sync/SKILL.md
---

# Jira Sync Skill

Pushes the Obsidian wiki planning layer to Jira BWS (Development Sprints). Wiki is the source of truth; Jira is the execution and visual layer.

## Trigger phrases
"Sync to Jira", "push to Jira", "update Jira", "jira-sync", or after any `/project-planner` session

## What it does
1. Reads all active Projects from `wiki/projects/`
2. Finds their linked deliverables from `wiki/deliverables/`
3. Creates or updates Jira Epics and Stories in BWS
4. Writes `jira-key: BWS-X` back to each wiki file's frontmatter
5. Reports a clean summary of what was created vs updated

## Mapping
| Wiki | Jira |
|------|------|
| Project | Epic (BWS) |
| Deliverable | Story (BWS), parented to its Epic |

## Connection details
- **Site:** agileict.atlassian.net
- **Cloud ID:** `bbbb75d2-e2e4-44fe-a329-e506d1128c29`
- **Project:** BWS (Development Sprints)

## Label Design

Every synced issue receives a standard set of labels. These are the canonical definitions:

| Label | Applied to | Purpose |
|-------|-----------|---------|
| `wiki-sync` | All issues | Marks the issue as wiki-managed. Don't edit title/description directly in Jira — edit the wiki and re-sync. |
| `career` (workstream) | All issues | Which life workstream this belongs to. Enables filtering by workstream when multiple Epics are active across career, finance, performance, etc. |
| `S` / `M` / `L` / `XL` (size) | Stories / Epics | T-shirt size from WSJF scoring. Used during sprint planning to gauge capacity — S = ~1 day, M = few days, L = full sprint or more. |
| `wsjf-4.5` etc. (score) | Stories | WSJF priority score. Jira has no native WSJF field, so the score lives here for reference. Superseded by the Priority field for day-to-day filtering — see WSJF → Priority mapping below. |

## WSJF → Jira Priority Mapping

Jira's Priority field (Highest / High / Medium / Low / Lowest) is more visible in the board and backlog than labels. The skill sets Priority from WSJF score using this mapping, calibrated to the full WSJF range of 0.375–9.0:

| WSJF score | Jira Priority |
|-----------|--------------|
| > 6.0 | Highest |
| 4.0 – 6.0 | High |
| 2.0 – 4.0 | Medium |
| 1.0 – 2.0 | Low |
| < 1.0 | Lowest |

**Current stories:**
- BWS-2 Integrate platform (4.5) → **High**
- BWS-3 Run campaign (3.0) → **Medium**
- BWS-4 Enrichment skills (1.4) → **Low**

The `wsjf-X.X` label is retained as an audit trail — it shows the exact score, whereas Priority only shows the band.

## Story Points

Story points in Jira are set to the project's hour estimate (1 SP = 1 hour). This makes sprint capacity immediately readable on the board — 40 SP = a full sprint. The `hours` field in wiki frontmatter is the source; jira-sync writes it to the Jira story points field on every sync.

## What is and isn't updated on re-sync
- **Updated:** description, labels, priority, story points
- **Never touched:** status, assignee, sprint assignment, comments

## Jira key caching
After first sync, each wiki file gets `jira-key: BWS-X` in its frontmatter. Re-syncs use this key directly — fast and no risk of duplicates.

## Eval results (iteration 1 — 2026-05-07)
10/10 assertions passed on first run. No iteration needed.

- Full sync: 1 Epic + 3 Stories created, keys written to all 4 wiki files
- Re-sync: 0 created, 4 updated — no duplicates

## Links
- **Skill file:** `~/.claude/skills/jira-sync/SKILL.md`
- **Jira System Design:** [[../system-design/jira-system-design|Jira System Design]] — Jira project structure, field mappings, labels
- **Project Workflow:** [[../service-design/project-workflow|Project Workflow]] — timebox rhythm and ceremonies
- **Conventions:** [[../system-design/skill-conventions|Skill Conventions]]

---
name: jira-pull
description: >
  Pulls Project flow status from the Jira Portfolio Kanban board (POR, board 48)
  and updates the corresponding wiki Project files. Also checks content
  discrepancies between Jira (POR and BWS) and the wiki — wiki always wins,
  so any discrepancy results in Jira being corrected, not the wiki. Use this
  skill whenever the user says "jira-pull", "pull from Jira", "sync from Jira",
  or has just moved a Project card on the Portfolio Kanban board and wants the
  wiki updated. Direction: Jira Portfolio Kanban → wiki (flow status only).
  Content discrepancies: wiki → Jira (wiki wins). Step 0 is a cheap pre-check
  that skips the full pull on days with no board activity.
---

# Jira Pull Skill

Pulls Project flow status from the Portfolio Kanban board in Jira and updates
`flow` in each wiki Project's frontmatter. Also corrects any content discrepancies
between Jira (POR and BWS) and the wiki — the wiki is the single source of truth
for all content. Flow status is the only thing Jira is authoritative for.

---

## Authoritative Sources

| Data type | Source of truth | Direction on conflict |
|-----------|----------------|----------------------|
| Flow status (which column) | Jira POR board | Jira → wiki (update wiki) |
| All content (Objective, Outcomes, Hypothesis, description) | Wiki | Wiki → Jira (correct Jira) |

---

## Connection Details

- **Site:** agileict.atlassian.net
- **Cloud ID:** `bbbb75d2-e2e4-44fe-a329-e506d1128c29`
- **Portfolio Kanban project:** POR
- **Board ID:** 48
- **Board URL:** https://agileict.atlassian.net/jira/software/c/projects/POR/boards/48
- **Sprint project:** BWS (Epics checked for content discrepancies)

---

## Column → Flow Mapping

| Jira status | Wiki `flow` value | SAFe stage |
|------------|-----------------|------------|
| Funnel | `funnel` | Funnel |
| Ready | `ready` | Reviewing + Analyzing + Portfolio Backlog (collapsed) |
| Implementing | `implementing` | Implementing |
| Done | `done` | Done |

Note: there is no `Review` column. A solo operator defines, scores, and approves
a Project in one `/project-planner` pass, so SAFe's Review/Analyzing stages are
collapsed into `Ready`. If a legacy `Review` status is encountered on the board,
treat it as `ready`.

Column names are case-insensitive. If an unrecognised column name is encountered,
flag it to the user and skip that issue rather than writing an invalid flow value.

---

## Step-by-Step Process

### Step 0 — Cheap pre-check (skip if no board activity)

Before doing a full pull, check whether anything on the POR board has changed
today. This makes a daily automatic run cost almost nothing on days with no
activity.

Use `searchJiraIssuesUsingJql` with:
```
jql: project = POR AND updated >= startOfDay()
fields: ["key"]
maxResults: 1
```

- **If zero results:** no Project on the POR board has changed today. Skip
  Steps 1-6 entirely and go to Step 7 to log a "no changes" row.
- **If one or more results:** proceed to Step 1 for a full pull as normal.

### Step 1 — Fetch board issues from Jira

Use `searchJiraIssuesUsingJql` with:
```
jql: project = POR
fields: ["summary", "status", "description"]
maxResults: 50
```

For each issue extract:
- `key` — e.g. `POR-1`
- `fields.summary` — the issue title
- `fields.status.name` — the current column name
- `fields.description` — the current Jira description (for discrepancy check in Step 5)

### Step 2 — Load wiki Projects

Read `wiki/projects/project-priorities.md` to get all Project slugs.
For each slug, read `wiki/projects/[slug].md` and extract:
- `por-key` from frontmatter
- `jira-key` from frontmatter (used in Step 5b for BWS check)
- `flow` from frontmatter (current value)
- H1 title (for name matching if no `por-key`)

### Step 3 — Match Jira issues to wiki files

For each Jira issue:

1. If a wiki file has a matching `por-key`: use it — fast and reliable.
2. If no `por-key` match: search wiki Project files for a case-insensitive title match against `fields.summary`.
3. If no Project file match found:
   - **If `fields.status.name` is "Funnel":** this is likely a new idea captured via the Jira-first workflow. Check `wiki/projects/funnel.md` for a matching row (case-insensitive title match).
     - If a funnel.md row already exists: note it in the report as "in funnel.md, no Project file yet — correct". No action needed.
     - If no funnel.md row exists: this is a new capture. Draft a funnel.md row using the Jira description as the hypothesis, leave Trigger as `[to be defined]`, and ask the user to confirm before writing. Report as "new Jira capture — drafted funnel.md row, awaiting confirmation".
   - **If `fields.status.name` is anything other than "Funnel":** flag to user — "POR-N ([summary]) has no matching wiki Project file and is not in Funnel status. Run `/project-planner` to define it, or check the title matches."

### Step 4 — Update flow status (Jira → wiki)

For each matched pair:

1. Map `fields.status.name` to a flow value using the column mapping above.
2. If flow value has changed (or was absent): update `flow` in frontmatter using Edit tool.
3. If `por-key` is absent from frontmatter: add it now.
4. If flow value is unchanged: skip — no write needed.

Note: `status` (active/done) is NOT touched — it is used by `/jira-sync` and must not be overwritten. Only `flow` changes.

### Step 5 — Content discrepancy check (wiki → Jira, wiki wins)

For each matched pair, check whether the Jira description matches what the wiki
would generate. If it doesn't, Jira is corrected — never the wiki.

**5a. Check POR description:**

Build the expected POR description from the wiki file using the same format as `/jira-sync` Step 2b.

For active Projects:
```
## Objective
[objective]

## Outcomes / Outputs
1. ...

## Hypothesis
[if present — omit for Output-only Projects]

---
Workstream: [ws] | Size: [t-shirt] | WSJF: [score] | Wiki: wiki/projects/[slug].md
```

For funnel Projects (`flow: funnel`):
```
## Hypothesis
[hypothesis]

## Trigger
[trigger]

---
Workstream: [ws] | Size: [t-shirt] | Wiki: wiki/projects/[slug].md
```

Compare the expected description against `fields.description` fetched in Step 1.
If they differ: call `editJiraIssue` on the `por-key`, updating `description` only. Record as a correction in the report.

**5b. Check BWS Epic description (if `jira-key` exists):**

Fetch the BWS Epic: call `getJiraIssue` on the `jira-key`, fields `["summary", "description"]`.

Build the expected BWS description from the wiki file (same format as `/jira-sync` Step 2d):
```
## Objective
[objective]

## Outcomes / Outputs
1. ...

---
Workstream: [ws] | Size: [t-shirt] | Wiki: wiki/projects/[slug].md
```

If the BWS description differs from expected: call `editJiraIssue` on the `jira-key`, updating `description` only. Record as a correction in the report.

**Tolerance for minor differences:** whitespace, trailing newlines, and markdown rendering differences are ignored. Only flag substantive content differences (changed objective, missing outcomes, wrong workstream).

### Step 6 — Update `project-priorities.md`

Re-read `wiki/projects/project-priorities.md` and update the Flow column for any
Projects whose `flow` changed. Sort rows by WSJF descending (Projects with no
WSJF score go last).

### Step 7 — Report

```
Jira Pull — Portfolio Kanban → Wiki
═══════════════════════════════════════

Flow status updates:
  POR-3  TTI Role              ready → implementing    ✓ wiki updated

Content corrections (wiki wins):
  POR-1  Agile Claw MVP        POR description was empty   ✓ Jira corrected
  POR-2  Cold Outreach RE      BWS Epic description stale  ✓ Jira corrected

No changes:
  POR-6  Hong Kong Runway      flow: funnel, content: match

2 flow updates · 2 content corrections · 1 unchanged

Wiki: wiki/projects/project-priorities.md
Board: https://agileict.atlassian.net/jira/software/c/projects/POR/boards/48
```

### Step 8 — Log

Append one row to `wiki/ai-os/logs/log-2026-Q2.md`:
- Normal run: `| [date] | Maintenance | jira-pull: updated flow for [N] Projects; corrected [N] content discrepancies (wiki wins). |`
- No-activity skip: `| [date] | Maintenance | jira-pull: pre-check found no POR board activity today — skipped full pull. |`

---

## Edge Cases

- **Issue not an Epic/Project:** skip silently — the POR board should only contain Projects.
- **Unrecognised column name:** flag to user, skip that issue, continue with others.
- **No wiki match by por-key or title:** flag to user, skip. Do not create wiki files — that is `/project-planner`'s job.
- **API error:** report the error clearly, abort gracefully. Do not partially update files.
- **flow field already matches and content matches:** skip all writes — don't touch files that haven't changed.
- **funnel.md entries without a full wiki Project file:** flag as "in Funnel, no wiki file" if unmatched.
- **`jira-key` absent (no BWS Epic yet):** skip BWS content check for that Project — no Epic to compare against.

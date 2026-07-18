---
name: jira-sync
description: >
  Syncs the Obsidian wiki planning layer to both the POR Portfolio Kanban and
  the BWS Development Sprints board in Jira. Use this skill whenever the user
  says "sync to Jira", "push to Jira", "update Jira", "jira-sync", or has just
  finished a project-planner session and wants their projects and deliverables
  reflected in Jira. Maps wiki Projects → POR (content) AND BWS Epic
  (execution). Maps wiki Deliverables → BWS Stories. Wiki is always the source
  of truth. Jira is the execution/visual layer.
---

# Jira Sync Skill

The wiki is the planning source of truth. This skill pushes it to Jira so the
user gets a visual Kanban and sprint board without manually re-entering anything.

## Connection Details

- **Site:** agileict.atlassian.net
- **Cloud ID:** `bbbb75d2-e2e4-44fe-a329-e506d1128c29`
- **Portfolio Kanban project:** POR (strategic layer — Projects)
- **Sprint project:** BWS (execution layer — Epics + Stories)
- **Issue type mapping:**
  - Wiki Project → POR issue (description sync via `por-key`)
  - Wiki Project → BWS Epic (description sync + parent for Stories via `jira-key`)
  - Wiki Deliverable → BWS Story (child of BWS Epic)

## What Gets Synced

### POR (Portfolio Kanban — per Project)
| Wiki field | Jira field |
|-----------|-----------|
| Project H1 | POR issue summary |
| Objective + Outcomes/Outputs + Hypothesis | POR issue description |
| Workstream, t-shirt, WSJF | Footer in description |
| Workstream (frontmatter) | POR labels (workstream label always present; additive only) |

### BWS (Development Sprints — per Project)
| Source | Jira field |
|--------|-----------|
| **POR card summary** (source of truth for naming) | Epic summary |
| Wiki Objective + Outcomes/Outputs | Epic description |
| Wiki Workstream, t-shirt size | Epic labels |

**Naming rule:** BWS Epic names must always match their corresponding POR card name exactly. POR is the source of truth for project names across both boards. Never use the wiki H1 as the BWS Epic summary — always read the POR card summary and copy it verbatim. A project must exist in POR before a BWS Epic can be created.

### BWS (Development Sprints — per Deliverable)
| Wiki field | Jira field |
|-----------|-----------|
| Deliverable title (H1) | Story summary |
| "What this delivers" + "Definition of Done" | Story description |
| WSJF score, size | Story labels |
| WSJF score (banded) | Story priority (Highest/High/Medium/Low/Lowest) |
| size (frontmatter) | Story Points (adapted Fibonacci: 1/2/3/5/8) |

**Never touched on update:** status, assignee, sprint assignment, comments.
Description, labels, priority, and story points are overwritten on every sync to stay in line with the wiki.

## WSJF → Priority Mapping

| WSJF score | Jira Priority |
|-----------|--------------|
| > 6.0 | Highest |
| 4.0 – 6.0 | High |
| 2.0 – 4.0 | Medium |
| 1.0 – 2.0 | Low |
| < 1.0 | Lowest |

## Jira Key Caching

After creating or finding a Jira issue, write the key back to the wiki file's YAML frontmatter:
- `por-key: POR-N` — the Portfolio Kanban card (set by `/project-planner`; verified here)
- `jira-key: BWS-N` — the BWS Epic (set here on first sync)

Example frontmatter after first sync:
```yaml
---
workstream: career
status: active
t-shirt: XL
por-key: POR-2
jira-key: BWS-12
---
```

---

## Step-by-Step Process

### Step 1 — Identify what to sync

By default, sync all Projects where `status: active` in their frontmatter.
If the user specifies a project slug (e.g. "sync cold-outreach-real-estate"), sync only that one.

Read `wiki/projects/project-priorities.md` to get the list of active Projects, then read each Project file.

### Step 2 — Sync each Project to POR and BWS

For each active Project file:

**2a. Extract fields from the wiki file:**
- **Title** — the H1 heading
- **Objective** — the Objective section
- **Outcomes / Outputs** — the numbered list
- **Hypothesis** — if present (Outcome-type Projects only)
- **Workstream**, **t-shirt**, **wsjf** from frontmatter
- **por-key** and **jira-key** from frontmatter (may be absent on first sync)

**2b. Build the POR description:**
```
## Objective
[objective text]

## Outcomes / Outputs
1. [Outcome/Output 1]
2. [Outcome/Output 2]
3. [Outcome/Output 3]

## Hypothesis
[if present — omit section for Output-only Projects]

---
Workstream: [workstream] | Size: [t-shirt] | WSJF: [score] | Wiki: wiki/projects/[slug].md
```

**2c. Sync to POR:**
- If `por-key` exists: call `editJiraIssue` on that key, updating `description` only.
- If no `por-key`: search `project = POR AND summary ~ "[title]"`. If found, write key to frontmatter and update. If not found, warn the user — POR cards are created by `/project-planner`, not here.
- After the description update, fetch the POR issue's current labels. If the workstream value (e.g. `career`) is not already in the list, add it — additive only; do NOT remove `funnel` or any other existing labels. If the label was already present, skip the labels write.

**2d. Build the BWS Epic description:**
```
## Objective
[objective text]

## Outcomes / Outputs
1. [Outcome/Output 1]
2. [Outcome/Output 2]
3. [Outcome/Output 3]

---
Workstream: [workstream] | Size: [t-shirt] | Wiki: wiki/projects/[slug].md
```

**2e. Sync to BWS Epic:**
- **Gate: if `por-key` is absent**, do NOT create or update a BWS Epic. Warn the user: "No POR card exists for [project]. Create it via `/project-planner` first, then re-run `/jira-sync`." Skip this project entirely for BWS.
- **Fetch the POR card summary** by calling `getJiraIssue` on the `por-key`. Use that summary verbatim as the BWS Epic summary — never use the wiki H1.
- If `jira-key` exists: call `editJiraIssue` updating `summary` (to match POR), `description`, and `labels`. This corrects any naming drift.
- If no `jira-key`: search `project = BWS AND issuetype = Epic AND summary ~ "[por-summary]"`. If found, use that key, update (including summary to match POR exactly), write to frontmatter. If not found, create with `issueTypeName: "Epic"` and `summary` = POR card summary, write returned key to frontmatter.

**2f. Write both keys back to the wiki file** using Edit tool if they changed or were absent.

### Step 3 — Find linked Deliverables

Read `wiki/deliverables/_index.md` — this is the sprint-ready backlog. Collect
all deliverables listed under the current project's section.

**Only sync deliverables from `_index.md`.** Items in a Project's `## Funnel`
section are never pushed to Jira — they have not passed the backlog admission
gates (scoped + sized + value-linked) and are not ready for execution tracking.

Sort by size ascending within each Project section (smallest first) before syncing.

### Step 4 — Sync each Deliverable as a BWS Story

For each deliverable file:

1. Read the file. Extract:
   - **Title** — the H1 heading
   - **What this delivers** section
   - **Definition of Done** section
   - **WSJF Scoring** table
   - **size**, **hours**, **workstream**, **jira-key** from frontmatter

2. Build the Jira description:
   ```
   ## What this delivers
   [what this delivers text]

   ## Definition of Done
   [definition of done text]

   ## WSJF Scoring
   Value: [v] | Time Criticality: [tc] | Risk/Opp: [ro] | Size: [size] | **WSJF: [score]**

   ---
   Project: [project title] | Wiki: wiki/deliverables/[slug].md
   ```

3. Build labels: `["wiki-sync", "[workstream]", "wsjf-[score]", "[size]"]`

4. If `jira-key` exists: call `editJiraIssue` updating `description`, `labels`, `priority`, and `customfield_10016` (story points = `size` value, NOT hours).
5. If no `jira-key`: search `project = BWS AND issuetype = Story AND summary ~ "[title]"`. If found, use that key; if not found, create with `parent: [bws-epic-key]`. Write key to frontmatter.

### Step 5 — Report

```
Jira sync complete.

POR updates:  2 descriptions updated
BWS Epics:    1 created, 1 updated
BWS Stories:  2 created, 1 updated

POR:
  POR-1  Agile Claw MVP               ✓ description updated
  POR-2  Cold Outreach Real Estate    ✓ description updated

BWS Epics:
  BWS-14  Cold Outreach Real Estate   ✓ created
  BWS-3   TTI Role                    ✓ updated

BWS Stories:
  BWS-15  Integrate Platform          ✓ created
  BWS-16  Run Campaign & Measure      ✓ created
  BWS-17  Build Enrichment Skills     ✓ updated

Portfolio board: https://agileict.atlassian.net/jira/software/c/projects/POR/boards/48
Sprint board:    https://agileict.atlassian.net/jira/software/projects/BWS/boards
```

---

## Edge Cases

- **POR card missing (`por-key` absent and no title match):** block BWS Epic creation entirely. Warn the user: "No POR card found for [project]. A project must be created in POR first via `/project-planner` before a BWS Epic can exist." POR cards are only created by `/project-planner`, not here.
- **Funnel Projects (`flow: funnel` in frontmatter):** sync the POR description (hypothesis + trigger) but do NOT create or update a BWS Epic — funnel items are not execution-ready.
- **Funnel deliverables** (a Project's `## Funnel` section): skip entirely.
- **Completed projects** (`status: done` in frontmatter): sync both POR and BWS but add label `"done"`.
- **BWS Epic name drift:** if BWS Epic summary does not match POR card summary, update the BWS summary on every sync. POR is always the source of truth for naming.
- **Projects with no BWS Epic match and no `jira-key`:** create the BWS Epic (using POR summary as the name), warn user to assign sprint.
- **Jira API error on a single issue:** log the error, continue with remaining issues, report failures at the end.
- **Title contains special characters:** strip or escape before using in JQL `~` search.

---

## After Syncing

Remind the user:
- Status changes (To Do → In Progress → Done) are managed in Jira, not the wiki.
- Sprint assignment is done in Jira during `/sprint-plan`.
- Re-run `/jira-sync` any time a new Project or deliverable is added via `/project-planner`.
- The wiki `por-key` and `jira-key` fields are now set — future syncs will be faster.

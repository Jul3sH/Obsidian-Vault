---
type: reference
created: 2026-06-15
updated: 2026-06-16
tags: [ai-os, system-design, wiki, convention]
absorbs: [wiki-folder-structure]
aliases: [wiki-folder-structure, wiki-folder-structure-and-linking]
---

# Documentation Conventions

> *How wiki content is written, structured, foldered, and linked. The single reference for creating or editing any wiki document, deciding how something is filed or formatted, and how active project/workstream folders are organised. (Absorbed the former `wiki-folder-structure` doc on 2026-06-16, so there is one place to look.)*

The wiki has two readers at once: Claude (the LLM that maintains and navigates it) and Julian (a visual thinker who reads it directly). A convention that serves one but not the other is incomplete. These principles keep both working as the wiki grows.

---

## Part 1 - Content principles

### 1. Dual audience: succinct for the model, navigable for the human
- Bullets over paragraphs. Lead with the point.
- Every document earns its length. If a line helps neither reader decide nor understand, cut it.
- Notes are operational *and* human reference at the same time. Write so both uses work.

### 2. Visual-first where an image is faster
- Use **tables** for anything comparative or multi-dimensional: options, scales, mappings, stages. A table beats prose whenever there is more than one axis.
- Use **Excalidraw diagrams** when structure or flow lands faster as a picture than as text: hierarchies, pipelines, lifecycles, relationships. Keep the text doc as the source of truth and link the diagram as its visual companion.
- Julian is a visual thinker: when a concept gets hard to follow in prose, that is the signal to draw it, not to write more.

### 3. Balance human navigation against LLM flatness (the core tension)
Flat structures (few folders, everything cross-linked) suit the LLM: fewer files to update, less duplication, cheaper traversal. Deeper hierarchy suits the human: a clear tree to navigate. These pull in opposite directions, and the wiki will only get bigger.

**The rule:** optimise for human navigability by default, and accept modestly more update overhead to get it. **But Claude must challenge any hierarchy that would materially hurt LLM efficiency or burn excessive tokens.** This is a two-way guardrail:

| Situation | Claude's job |
|-----------|--------------|
| Structure that aids human navigation, at the cost of a few more updates | Build it. Don't resist reasonable update overhead. |
| Hierarchy that forces heavy duplication, many-level traversal, or large token overhead on every read | Say so. Name the cost, propose the lighter alternative, let Julian decide. Do not silently comply. |

Julian owns the call. Claude owns surfacing the cost.

### 4. Deliverables are clearly associated with their Projects
The motivating case for principle 3. A flat deliverables backlog cross-linked to projects is efficient for the model but hard for a human to see at a glance. Deliverables should be clearly grouped under, or visibly associated with, their parent Project, so a human can view a Project and its deliverables together. Each Project file holds a `## Deliverables` table as the single source of truth for its deliverables; `wiki/deliverables/_index.md` is pure navigation (type reference, admission criteria, links to each Project's `## Deliverables` section). Standalone deliverables (not linked to a Project) get a `## Standalone Deliverables` table in `wiki/deliverables/_index.md` instead.

### 5. Standard recurring artefacts have a fixed name and shape
Long-running work uses named artefacts with a defined structure, so a reader (human or LLM) always knows which file holds what without opening several to find out. The first standardised one is the **engagement-strategy doc** (see Part 3). When a recurring artefact type appears across two or more areas, give it a standard name and a documented shape here, rather than letting each area invent its own.

### When adding hierarchy - Claude's check
Before creating new folders, nesting, or per-item files, sanity-check:
- Does this measurably help human navigation? If not, keep it flat.
- Does it force the same fact to live in multiple places (sync burden)? If yes, flag it.
- Would every read now traverse extra levels or pull large overhead? If yes, notify Julian and offer the lighter option.

---

## Part 2 - Folder structure & linking

> *How project/workstream folders are organised by workflow state, and why we use bare wikilinks. Established 2026-06-02 after restructuring `wiki/career/tti/`; that folder is the reference implementation.*

**Key points:**
- **Active project folders organise by workflow state**, not by type.
- **Root holds only the `_index.md`.** The engagement-strategy doc is a `_wip` record; current-position state lives in that doc and the project Status surface, never duplicated into indexes.
- The folders do **two different jobs**: *hide* (`_on-hold`, `_archived`) and *tidy* (`_reference`, `_wip`).
- **Use bare `[[wikilinks]]`, never path links** - bare links survive file moves; path links break on every move and force link surgery.
- **Structure emerges as a project grows** - don't pre-build empty folders.
- The per-state-move cost is just **updating the indexes**; links don't need touching (because they're bare).

### The state-folder model

For an **active project / workstream folder** (one with live work and drafts that change state, e.g. a career workstream, an epic, a deliverables area):

| Location | Holds | Purpose |
|----------|-------|---------|
| **(root)** | The folder `_index.md` only | Start here |
| **`_wip/`** | Active drafts + the engagement-strategy doc (live, must-stay-current records) | *Tidy* - spotlight current focus |
| **`_reference/`** | Stable knowledge consulted **while working** (profiles, research, sent artefacts) | *Tidy* - keep a large reference set out of the root, but in sightline |
| **`_on-hold/`** | Paused artefacts, may be repurposed | *Hide* - out of working sightline |
| **`_archived/`** | Done or dead, kept for record | *Hide* - audit trail only |

### The two jobs (don't conflate them)
1. **Hide - `_on-hold` + `_archived`.** These get paused/dead material *out of your working sightline*. This is the core value; items **move into** them when they change state.
2. **Tidy - `_reference` + `_wip`.** Purely organisational. Reference stays fully in sightline; the folder just stops a large set cluttering the root.

### When to use each folder

| Folder | Use it when… |
|--------|--------------|
| `_archived/`, `_on-hold/` | **Always** - the moment a first item is superseded or paused. This is the point of the system. |
| `_reference/` | Only when the reference set is big enough to clutter the root (rule of thumb: ~8-10+ files). Small project, keep reference flat at root. |
| `_wip/` | Only when there are several active drafts. One draft, leave it at root. |

### Structure emerges - don't pre-build

A new project starts almost flat: a few notes + maybe one draft at root.
- First item paused, create `_on-hold/`, move it.
- First item dies/superseded, create `_archived/`, move it.
- Root gets noisy (~8-10+ files), create `_reference/`, tuck the stable stuff in.

Folders appear **as the project grows**. Because links are bare, foldering later costs nothing.

### What this applies to - and what it doesn't
- **Apply to:** active project / workstream folders with a real WIP to done lifecycle.
- **Do NOT apply to pure reference libraries** (`wiki/technology/`, `wiki/enterprise-architecture/`). They're 100% reference, organise them **by topic**, not by state. Add an `_archived/` only if something there gets superseded.

### Linking convention (non-negotiable for this to work)
- **Prefer bare `[[note-name]]`.** Obsidian resolves by filename regardless of folder, so a bare link keeps working when the file moves between state folders. This is what makes state-moves free.
- **Use a path link only to disambiguate a duplicate filename.** Better still: keep basenames **unique across the vault** so disambiguation is never needed. (Known collision to clean up: `tti-ai-leadership-brief` / `tti-consulting-brief` exist in both `career/tti/_on-hold/` and `deliverables/`.)
- Path links (`[[../../area/file]]`) are the thing that made the one-time TTI migration expensive. Avoid creating new ones.

### The cost model
- **Day-one cost: ~zero.** A file created in the right folder with bare links needs no fixing.
- **Per-state-move cost: small.** Move the file, then update the source `_index`, the destination `_index`, and the master `_index` if it lists the item. **Links are not touched** (bare links don't break). The librarian does the index update as part of the move.
- **The index update is mandatory** - skip it and the folders drift out of sync with the indexes, which is how state-based filing rots.
- **One-time migration cost (retrofitting a flat folder) is the expensive case** - mass moves + converting existing path links to bare. Paid once, only when adopting the structure for an existing flat area. Born-right projects never pay it.

---

## Part 3 - Current-position surfaces

Folder state answers *"which files are live?"*. It does **not** answer *"where am I at right now?"*. That is the job of the two surfaces below.

### The project-file Status surface

For a project in `wiki/projects/`, the current position lives in a **`## Status` block at the top of the project file** (`wiki/projects/[slug].md`), the single go-to surface, so a reader never reconciles the strategy, comms, and history docs just to get the current position.

**Why on the project file:** it is already the per-project hub `wiki/projects/_index.md` points to, status sits next to the Objective it serves, and the `flow` field (written by `/jira-pull`) already lives there. One place, every project, identical shape.

**Shape - three parts:**
1. **Snapshot** (overwrites, always *now*): Position, Next action, Waiting on, and a **Detail-tier** line linking down to the deep working docs. A few lines only.
2. **Project Summary File Map** (living navigation table): grouped links to all live project-critical supporting files, with one-line roles.
3. **Status log** (append-only, newest first): `| Date | Update |`, one terse row per project-level milestone. Links out to detailed logs (the engagement-strategy doc, engagement history); does **not** restate them.

Frontmatter carries `status-updated: [date]` so staleness is visible at a glance.

### The Project Summary File Map

Every Project file in `wiki/projects/` must include a `## Project Summary File Map` near the top, after the Status snapshot and before the Status log.

**Purpose:** make the Project page the human navigation hub for all live evidence without moving domain files out of their natural homes.

**Shape:**

| Column | Holds |
|---|---|
| Area | Group such as Decision control, Finance, Career, Relationships and family, Delivery, Source-of-truth, or Reviews. |
| File | Bare `[[wiki link]]` to the supporting file. |
| Role | One-line description of what the file is for in this Project. |

**Rules:**
- Include all live supporting files a human would need to understand, audit, or resume the Project.
- Group by area, not by folder path.
- Use bare `[[note-name]]` links.
- Keep each Role to one line.
- Update the file map when creating, renaming, archiving, or superseding project-critical files.
- Do not duplicate mutable status inside the file map. It says what each file is for, not what the file currently concludes.

**Maintenance rule:** any operation that materially changes a project's state updates the snapshot, bumps `status-updated`, and adds one log row. This mirrors the mandatory-index-update discipline above; skip it and the surface rots.

**Scope:** real projects in `wiki/projects/` only. Parking-lot lists (`funnel.md`, `someday.md`) are not projects and take no Status block. Defined and templated in the `/project-planner` skill (Step 3.2).

### The engagement-strategy doc

**What it is:** the command-centre living strategy doc for a long-running engagement (a campaign, negotiation, relationship, or workstream that evolves over weeks or months and accumulates decisions). It is the **open-first** file: current position + standing plan + the dated reasoning behind each call. It complements, never duplicates, the chronological logs (which record *what happened*) and the reference docs (profiles, research, drafts).

**Name:** `<area>-engagement-strategy.md`, prefixed with the folder/area name so the basename is unique across the vault (bare-link rule). Title: `<Area> - Engagement Strategy (living document)`. Frontmatter: `type: strategy`, `status: living`.

**Where it lives:** at the folder root while the folder is flat; in `_wip/` once the folder adopts state-folders (it is a live, must-stay-current record, not reference). Bare links mean the move costs nothing.

**Standard structure (the template):**

| Section | Holds | Update mode |
|---|---|---|
| Purpose blockquote + companion-doc map | One-line statement of what the doc is, plus links to the logs/reference it sits on top of. Doubles as a nav hub. | Rarely |
| **Snapshot** (dated) | Current position in one screen: where things stand, what is live, what is pending / waiting-on. | Overwrites, always *now* |
| **Standing Strategy** | The settled layer that does not change per update: non-negotiables, guardrails, the pitch, standing risks. | Rarely; changes are themselves logged |
| **Decision Log** (newest first) | One entry per material call: date, trigger, decision, rationale, and any watch item. The "why", preserved. | Append-only |
| **Open Loops / Watch Items** | Live threads to act on when they move; pre-decided responses held in reserve. (Optional, fold into Snapshot for simple engagements.) | Living |
| **Related** | Bare links to companion docs. | Rarely |

**Section-name discipline:** use these exact headings (Snapshot, Standing Strategy, Decision Log, Open Loops / Watch Items) so the same information sits under the same heading in every engagement, whatever the domain. This is the point of standardising: you always know which section to open.

**Relationship to the Status surface:**
- If the engagement is a formal Project in `wiki/projects/`, the project-file `## Status` block is the brief top-level surface and its Detail-tier line links *down* to this doc; this doc's Snapshot is the deep current position.
- If the engagement is a workstream folder not in `wiki/projects/` (e.g. `relationships/Dad`, `career/tti`), there is no project Status block, so this doc's Snapshot is the sole current-position surface.

**Maintenance rule:** any operation that materially changes the engagement updates the Snapshot (and its date) and adds a Decision Log row. Same discipline as the mandatory index update; skip it and the doc rots.

---

## Reference implementations
- **Folder structure:** `wiki/career/tti/` - root (index only), `_wip/` (the engagement-strategy doc + active drafts), `_reference/`, `_on-hold/`, `_archived/`, each with its own `_index.md`, master index as a folder map.
- **Engagement-strategy docs:** [[tti-engagement-strategy]] (conversion/sales engagement) and [[dad-engagement-strategy]] (defensive/relationship engagement) - the two shapes the template is designed to fit.

## Related
- [[system-design-principles|System Design Principles]] - the working-memory model (why enforced rules live in the always-on layer, not only here)
- [[agent-instruction-architecture|Agent Instruction Architecture]] - the three-layer model: `AGENTS.md` (canonical universal rules), agent wrappers (`CLAUDE.md` and future Codex/OpenCode files), and this wiki (deep doctrine)

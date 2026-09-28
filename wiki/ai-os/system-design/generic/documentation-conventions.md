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
Long-running work uses named artefacts with a defined structure, so a reader (human or LLM) always knows which file holds what without opening several to find out. The first standardised one is the **engagement-strategy doc** (see Part 3); the second is the **mental model** (below). When a recurring artefact type appears across two or more areas, give it a standard name and a documented shape here, rather than letting each area invent its own.

### 6. Headline status is current-only; history goes to a Document Log

Any file that carries a status banner shows **one** entry at the top: the current
position, dated, in a few lines a reader can take in at a glance ("where is this
at"). It is rewritten in place when the position changes. It never accumulates.

Every superseded status, and every dated note of what changed in the file, goes to
a `## Document Log` section at the **bottom** of the file: one row per entry,
newest first, columns Date and Entry. The Document Log records the history of the
document; the Time and Token Log (where the file has one) records effort only, and
the two are not merged.

Why: a headline that lists every change since the file opened stops telling the
reader where the file is at. *(Rule set by Julian, 27 Sep 2026.)* This is the
in-document form of the [[#The project-file Status surface]] rule: newest position
first, history below.

### The mental-model format (six slots, any workstream)

A mental model is a compressed decision aid Julian holds in his head, with the
evidence pushed down to a detail article. Every mental model, in any workstream
(GenAI, finance, wellbeing, relationships, performance, personal, technical), uses
the same six slots in the same order:

| # | Slot | Holds | Ages |
|---|---|---|---|
| 1 | **One-liner** | The model in a single speakable sentence. The thing recalled under pressure. | Never |
| 2 | **Reach for it when** | The trigger situation, one line. Prevents the common failure: non-use when the situation arrives. | Rarely |
| 3 | **Principles** | 3-6 bold one-line invariants, statements of the form *this input decides this thing*. The understanding layer. | Slowly |
| 4 | **Guidelines** | Actionable advice, each traceable to a principle. The action layer. | With tools and context |
| 5 | **Limitations** | Where the model stops applying. Every model overapplied becomes a bias; this slot is the boundary of validity. Operating restrictions belong in Guidelines, not here. | Slowly |
| 6 | **Detail** | Bare link(s) to the article carrying the evidence. | On refactor |

**Rules:**
- **Naming:** a mental model's filename starts `mm-` (e.g. `mm-rule-layering.md`)
  and its H1 title starts `MM: ` (e.g. `MM: Rule Layering`), so a model is
  recognisable as one both in a file listing and wherever its title appears. The
  title uses a colon and the filename a hyphen because Obsidian forbids `:` in
  filenames.
- **Key Takeaways sit above Principles:** the order in a mental-model file is
  purpose block, One-liner, Reach for it when, Key Takeaways, then Principles,
  Guidelines, Limitations, Detail. The takeaways are the summary a reader gets
  before deciding whether to read on.
- Principles and Guidelines are kept separate because they age differently:
  principles survive tooling changes, guidelines do not. Refresh Guidelines without
  touching Principles. The rationale is its own mental model: [[mm-rule-layering]].
- The same skeleton applies at both altitudes: a recall-card section holds the six
  slots compressed; the detail article may expand under the same headings. Reader
  always knows where a thing lives.
- The fixed skeleton is itself a deterministic check: a missing slot is visibly
  missing.
- **One model, one file.** A mental model is never a section inside a collection
  file: collections drift against the detail articles and duplicate the index's
  job. Reference implementations: [[mm-verification]] (model plus separate detail
  articles) and [[mm-steering]] (model and detail in one file, where the evidence
  is external). Where a model summarises a detail article and the two disagree,
  the article wins and the model file is corrected.
- Every mental model is listed in [[mental-models-index]] (under
  `wiki/performance/`), grouped by workstream, with its one-liner as the
  description. Adding the index row is part of creating the model, not a separate
  step.
- **Every documented personal bias has, at minimum, an mm card** with "bias" in
  the filename (e.g. `mm-recency-bias.md`); detail articles exist only where the
  evidence warrants one. The bias card and its countermeasure card are separate
  files that link to each other and never restate each other's content. Every
  bias card also gets a row in [[biases-index]] (trigger situation + card link),
  and adding that row includes checking the row's situation type is covered by
  the `behaviour-check` skill's trigger, widening it if not - in the same operation.
  *(Rule agreed 19 Sep 2026 during [[bias-history-review]].)*

### The BRAIND format (one question, one file)

A BRAIND file is the working file for one decision run through the six
B-R-A-I-N-D steps ([[brain-brand-framework]]). There is one format. When an
option's B and R rows outgrow the decision file, they may be split into their own
`<Option>-BRAIND.md` (as [[HK-BRAIND]], [[London-BRAIND]] and [[Malvern-BRAIND]]
were in August 2026); a split file holds only the B and R sections for that
option, follows the same section rules, and opens with a pointer to the decision
file it belongs to. It is not a different kind of document.

**Naming and location.** `<Question>-BRAIND.md`, H1 the same, in the decision's
workspace folder under `wiki/performance/decision-journal/`. Frontmatter:
`type: decision-workspace`, `status: open | committed | reviewed`, `created`,
`project`, `decision` (the question in one line).

**Fixed sections, in this order.** A missing section is visibly missing.

| # | Section | Holds | Rules |
|---|---|---|---|
| 1 | Purpose | A `## Purpose` heading and one sentence only: the question (or, for a split file, the option whose B and R rows it holds). No section map: the BRAIND sections are self-explanatory | Per the AGENTS.md purpose rule: the question is the what and the why. Why the file was opened and how it is used go to the Document Log as a dated row (rule set 27 Sep 2026) |
| 2 | Status | A `## Status` heading, then the banner: the current position of this document only, dated, opening `⚠ Status (date):`, a few lines. Decision and project state go to the project status surface | Rewritten in place when the position changes. Superseded entries move to the Document Log (Part 1 item 6). The project page carries the cross-project view and links here |
| 3 | B - Benefits | Opens with a dated summary against the questions in the Purpose, one bullet per question (bold question, then whether it is answered and where it is tested; bullets not a table, so the answer is not restricted). Then rows by workstream (Wellbeing, Relationships, Finance, Career, Performance, Personal), each row opening with a **bold headline** and then the detail | Each row says its source: carried from an earlier BRAIND file, carried and changed, or new and dated |
| 4 | R - Risks | Opens with a dated summary against the questions in the Purpose (bullets, as in B). Then the risks grouped by **event**: each event is a ### heading stating the event in Julian's words (ranked events first, rank and date in the heading; unranked after), with why-it-could-happen, workstream and rating as bullets. Under each event an **Effects** list, each effect opening with a **bold headline** and naming its workstream and source. Under each effect a **Mitigations** sub-bullet, marked candidate or adopted, or "none identified". Analysis notes that are not risks of the option sit in a closing block. Bullets throughout, no tables | Only the risks of the option under question live here. Risks of an alternative live in that alternative's own BRAIND file, with a pointer. The event, effect, mitigation chain is the AGENTS.md Risk Framework's cause, event, effect, response chain; mitigation is that framework's response. Structure set 28 Sep 2026 at Julian's instruction, for [[HK-Return-BRAIND]] and every later BRAIND; the August split files keep their 27 Sep form |
| 5 | A - Alternatives | Every alternative, always including "hold the committed choice". An alternative already covered by an earlier BRAIND file gets a differences table here, not a new file | Warnings the model adds are marked as the model's judgement |
| 6 | I - Intuition Log | Append-only dated blocks in Julian's words, recorded before the analysis | The model never rewrites, summarises away, or labels an entry. Later entries may contradict earlier ones; both stand |
| 7 | What the intuition asks the analysis to check | Numbered table: the claim the gut relies on, Fact / Assumption / Belief, where it gets tested | A resolved claim is marked resolved with the date and Julian's words, never deleted. Referred to by number plus what it says, never number alone |
| 8 | N - Need time / Nothing | What doing nothing means, and the date on which waiting ends | Bounded, so it closes into D |
| 9 | D - Decision | The committed choice, dated, written by Julian | Never model-drafted ([[mm-commitment-by-proxy-bias]]). Mirrored to the `dec-*.md` entry and the project page in the same operation |
| 10 | Links | Bare links to the journal entry, related BRAIND files, canonical model, protocol | |
| 11 | Document Log | Dated rows, newest first: superseded statuses and what changed in the file | History only; effort goes in the Time and Token Log |
| 12 | Time and Token Log, Session Synopsis | Per the AGENTS.md rules | A BRAIND file is a deliverable: the Prompt Zero gate applies |

**Rules.**
- One question, one file. The first BRAIND run (July 2026, [[performance/decision-journal/uk-move/_index|UK relocation workspace]]) was spread across seven files, which is why the single-file form exists.
- Julian's words, no coined labels. A risk, claim or option is recorded in the words he used; if a shorter handle is needed, ask him for one.
- Earlier BRAIND files are inputs to a later run and are never rebuilt inside it. Rows are carried with their source named; rows not carried are listed with the reason at the time of carrying.
- Every status claim inside the file is dated (AGENTS.md rule). The banner holds the current position only; on every edit, rewrite it and move what it replaced to the Document Log.
- Numbers come from the canonical model file and say so; a figure computed outside the model is marked derived and the model change it implies is logged as an open task.

Reference implementation: [[HK-Return-BRAIND]] (opened 24 Sep 2026). Split B-and-R files: [[HK-BRAIND]], [[London-BRAIND]], [[Malvern-BRAIND]] (August 2026; brought to this convention 27 Sep 2026).

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

#### Exemption: structurally-named files always use path links

Some filenames are **fixed by a convention, not chosen for uniqueness**, so they collide by design and can never be linked bare. This is not a defect to clean up; it is forced.

| Structural name | Why it is fixed | Count |
|---|---|---|
| `SKILL.md` | Mirror filename must match `~/.claude/skills/[name]/SKILL.md` exactly | 22 |
| `_index.md` | Index convention, one per folder | many |
| `TESTING.md`, `architecture.md`, `capabilities.md`, `pricing.md` | Fixed slot names inside a skill or vendor folder | several each |

**A skill's name is a folder, not a file.** `[[commitment-guard]]` can never resolve, because the file is `commitment-guard/SKILL.md`. `[[SKILL]]` is ambiguous across all 22.

**Canonical form, always use this:**

```
[[ai-os/skills/commitment-guard/SKILL|commitment-guard]]
```

Path from `wiki/`, plus a pipe alias so the rendered text stays readable. Inside a table, escape the pipe: `\|`.

**The rule in one line:** names you *choose* get bare links and must be unique; names fixed by *convention* get path links with an alias.

### File lifecycle: which operations break links

The bare-link convention makes **moves** free. It does nothing for renames or deletions, and the ease of moving makes those feel free too. They are not: this is how link rot happens.

| Operation | Inbound links | Indexes |
|---|---|---|
| **Create** | n/a | Add to the destination `_index` |
| **Move** between state folders | **Untouched.** Bare links survive | Update source `_index`, destination `_index`, and master if listed |
| **Rename** | **Repoint every inbound link.** Bare links break on a basename change | Update every index that lists it |
| **Delete** | **Repoint or remove every inbound link.** Decide per link | Remove from every index |
| **Supersede / merge** | **Repoint inbound links to the successor**, never leave them dangling | Remove the old entry; confirm the successor is listed |

**Before any rename, delete, or merge, find the inbound links first:**

```bash
grep -rnE "\[\[[^]]*old-note-name" wiki/
```

**Do not anchor the pattern to `[[`.** A bare link starts with the name, but a path link starts with the *path* (`[[ai-os/skills/commitment-guard/SKILL|…]]`), so an anchored grep silently misses every path link. The unanchored form above catches both.

**Also grep the plain filename, unbracketed.** A name can appear as a backticked filename in a table or prose (`` `old-note-name` ``) without ever being a wikilink. Obsidian does not track these, so they never show as broken, but they still go stale the moment the target is renamed.

```bash
grep -rn "old-note-name" wiki/
```

Run both searches. The bracketed one finds live links to repoint; the plain one finds mentions to update by hand, since there is nothing to repoint automatically.

Do this *before* the operation, not after, so the lists are still accurate. For a delete, each hit is a decision: repoint it to the successor, or remove the link and its sentence.

**Why this matters:** an audit on 2026-07-31 found 51 broken links across 12 missing targets, one deleted note accounting for 21 of them. Every one was a rename or delete performed as if it were a move. A rename on 2026-08-01 then caught a second gap the same way: the bracketed-only search missed a backticked filename reference in a table, found only by a manual follow-up check.

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
- **BRAIND file**: [[HK-Return-BRAIND]] (single-file B-R-A-I-N-D run; format in Part 1).
- **Folder structure:** `wiki/career/tti/` - root (index only), `_wip/` (the engagement-strategy doc + active drafts), `_reference/`, `_on-hold/`, `_archived/`, each with its own `_index.md`, master index as a folder map.
- **Engagement-strategy docs:** [[tti-engagement-strategy]] (conversion/sales engagement) and [[dad-engagement-strategy]] (defensive/relationship engagement) - the two shapes the template is designed to fit.

## Related
- [[system-design-principles|System Design Principles]] - the working-memory model (why enforced rules live in the always-on layer, not only here)
- [[agent-instruction-architecture|Agent Instruction Architecture]] - the three-layer model: `AGENTS.md` (canonical universal rules), agent wrappers (`CLAUDE.md` and future Codex/OpenCode files), and this wiki (deep doctrine)

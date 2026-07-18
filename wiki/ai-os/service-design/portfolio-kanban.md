---
type: reference
created: 2026-05-18
---

# Portfolio Kanban — Workflow Reference

**Open this when you want to understand how Projects flow through the system: what the stages are, what triggers transitions, and how Jira and the wiki stay in sync.** This is the workflow layer — for what a Project *is* and how to define one, see [[project|Project Reference]].

For the skill that syncs Jira → wiki, see [[../skills/jira-pull/_index|jira-pull]].
For the parked ideas backlog, see [[portfolio-backlog|Portfolio Backlog]].

---

## Overview

The Portfolio Kanban controls which Projects receive investment. It limits work in progress at the strategic level so that a small number of initiatives get completed rather than many getting started.

Every Project carries a `flow` field in its frontmatter reflecting its current stage. This field is the only one written from Jira → wiki (via `/jira-pull`). All other Project fields (Objective, Outcomes/Outputs, WSJF, size) are wiki-authoritative.

---

## Stages

| Flow value | Jira column | SAFe stage | Meaning |
|-----------|------------|------------|---------|
| `funnel` | Funnel | Funnel | Raw idea captured, not yet through the commitment gate |
| `ready` | Ready | Reviewing + Analyzing + Portfolio Backlog | Commitment gate passed; defined, scored, approved in one `/project-planner` pass — waiting to be pulled into implementation |
| `implementing` | Implementing | Implementing | In execution — stories broken out, sprint work underway |
| `done` | Done | Done | All Outcomes/Outputs achieved, Project closed |

> **No `review` stage.** SAFe separates "Reviewing/Analyzing" (a project being defined and evaluated) from "Portfolio Backlog" (approved, waiting). That separation only earns its place when reviewing has *duration* — when work sits in an analysis queue waiting on other people. For a solo operator, definition is a single discrete act: one `/project-planner` pass runs the commitment gate, defines the Project, scores WSJF, and approves it. Nothing dwells "in review", so the stage was removed (20 Jun 2026). The `funnel` → `ready` transition *is* the review.

### Stage definitions

**Funnel (`funnel`)**
Project candidates that have a **hypothesis + trigger** but haven't passed the commitment gate. The [[portfolio-backlog|Portfolio Backlog file]] (`funnel.md`) holds structured rows for parked candidates — enough information to make a go/no-go decision without re-researching — each backed by a POR card.

The funnel is fed by triage from the **capture inbox** ([[brain-dump|raw/brain-dump.md]]) — a zero-evaluation dump of raw, unclassified ideas that sits *before* the funnel and outside the projects folder (an idea there might become a project, a BAU task, wiki reference, or nothing). An idea only enters the funnel once it earns a hypothesis + trigger. See [[prioritization-framework|Prioritization Framework]].

There is no WIP limit on the funnel — it's a parking tier, not active work.

**Ready (`ready`)**
The Project has passed the commitment gate and has been defined, WSJF scored, and approved — all in one `/project-planner` pass. This is where `/project-planner` operates: running the commitment gate, then defining the Objective, Outcomes or Outputs, T-shirt size, and WSJF score. The result is a fully scored Project waiting to be pulled into implementation when there's capacity. This is the equivalent of a backlog for stories: the ranked queue you pull from.

A Project enters this stage by passing the commitment gate (see below). It exits forward when stories are broken out and sprint capacity is committed, or backward to `funnel` if it turns out not to be ready after all.

**Implementing (`implementing`)**
The Project is in execution. User stories and enablers have been broken out (via `/define-user-story` and `/define-enabler`), committed to sprints on the BWS board, and work is underway.

**WIP limit: 2 implementing Projects.** A solo operator cannot meaningfully execute more than 2 Projects simultaneously. If a third Project needs to go active, one of the existing two must be paused or completed first. This constraint prevents context-switching and half-finished work.

**Done (`done`)**
All Outcomes and Outputs have been achieved (or a deliberate decision has been made to close the Project). The Project file remains in `wiki/projects/` for reference but is no longer active.

---

## Information Progression

Each stage requires progressively more detail. This prevents over-planning ideas that may never be committed, while ensuring Projects are fully defined before execution begins.

| Stage | Artefact | Required information |
|-------|----------|---------------------|
| **Funnel** | Row in [[portfolio-backlog\|portfolio-backlog.md]] | Title, hypothesis (the need or opportunity), trigger |
| **Ready** | Full Project file in `wiki/projects/` (via `/project-planner`) | Outcomes or Outputs, Leading Indicators (M+ only), t-shirt size, WSJF score with rationale — defined, scored, approved, waiting for capacity |
| **Implementing** | Project file + deliverables in `wiki/deliverables/_index.md` | Deliverables broken out (scoped + sized + value-linked), MoSCoW committed (via `/sprint-plan`) |

### Outcomes vs Outputs

When a Project is defined (the `funnel` → `ready` transition), the Project interview asks:

> "Is success measured by an external effect, or by completion of the thing itself?"

- **External effect** → write an **Outcome** — a measurable change in the world
  - "Inbound recruiter messages increase by 2x within 60 days"
  - "Pipeline generates 5 qualified leads per month"
  - "Consulting revenue reaches $X by end of quarter"
- **Completion** → write an **Output** — binary proof the thing is built and working
  - "AI OS skills documented, mirrored, and passing evals"
  - "Sending domain configured with DKIM/SPF/DMARC passing"
  - "WSJF scoring framework operational and used for 3+ Projects"

An Project may have a mix of both. The distinction determines how you'll evaluate success: did it *matter*, or is it *done*? See [[project#Outcomes and Outputs|Project Reference]] for the full rationale.

### Leading Indicators (M+ Projects only)

For Projects sized M (a week) or above, the interview asks:

> "This Project will take at least a week. What's the earliest signal — within the first sprint — that your approach is working?"

Leading Indicators are early signals that value is emerging before the Project is complete — so you can course-correct mid-flight rather than waiting until all outcomes are delivered. XS/S Projects skip this — they complete fast enough that the result is the indicator.

### MVP Question (M+ Projects only)

For Projects sized M or above, the interview asks:

> "Can you test this hypothesis with a smaller first pass before committing the full Project?"

If yes, the MVP becomes a story under the Project — prioritised first via MoSCoW at sprint planning, delivered, and evaluated before the remaining stories are committed. If no, proceed normally.

### Lean Business Case

The WSJF scoring (Value + Time Criticality + Risk/Opportunity ÷ Job Size) serves as the Lean Business Case. Each component carries a rationale in the Project file — the reasoning behind the score, not just the number. No additional narrative field is needed.

---

## The Commitment Gate

The commitment gate is the transition from `funnel` → `ready`. It exists to prevent the ADHD pattern of planning everything rather than committing to anything.

Before a full Project interview begins, `/project-planner` asks two questions:

> "In one sentence each: what's the concrete payoff if this Project gets done, and what happens if you ignore it for 3 months?"

**What this tests:**
- Is the payoff specific enough to be real? Vague answers ("it would be good") signal the Project isn't ready.
- Is the 3-month consequence a real cost, or just anxiety? Discomfort is not a consequence.

**If answers are compelling:** proceed with the full interview → Project is defined and scored, entering `ready` in the same pass.

**If answers are vague or the case isn't clear:** park it in [[portfolio-backlog|portfolio-backlog.md]] with a structured row rather than forcing a definition that isn't ready.

---

## Transitions

```
              Commitment gate + define + score
       Funnel ─────────────────────────────────► Ready
      (funnel)              pass                 (ready)
                            fail ◄─────────────── return if not ready
                                                     │
                                                     │ Stories broken out;
                                                     │ sprint capacity committed
                                                     ▼
                                                Implementing
                                               (implementing)
                                                     │
                                                     │ All Outcomes/Outputs achieved
                                                     ▼
                                                   Done
                                                  (done)
```

| Transition | Trigger | Who/what |
|-----------|---------|----------|
| `funnel` → `ready` | Passes the commitment gate, then defined and WSJF scored in the same pass | `/project-planner` (interactive) |
| `ready` → `funnel` | Not ready after all; parked | Manual decision / `/project-planner` Stage Regression |
| `ready` → `implementing` | Stories broken out, sprint capacity committed | `/sprint-plan` or manual |
| `implementing` → `done` | All Outcomes/Outputs achieved or deliberately closed | Manual decision |

---

## Jira ↔ Wiki Sync

**Board:** [POR board 48](https://agileict.atlassian.net/jira/software/c/projects/POR/boards/48)

The Portfolio Kanban lives in Jira as a Kanban board. The wiki mirrors the board state via the `flow` field.

- **Jira → wiki:** `/jira-pull` reads each Project's Jira status and updates the `flow` field in the wiki frontmatter. This is the only Jira → wiki write.
- **Wiki → Jira:** `/project-planner` automatically creates the POR Project card after writing the wiki file, transitions it to "Ready", and writes `por-key` back to the wiki frontmatter.
- **`por-key`:** the Jira issue key (e.g. `POR-1`), written to the Project's frontmatter by `/project-planner` on creation (or by `/jira-pull` on first run if creation failed and the card was added manually).

**Column mapping:**

| Jira column | Wiki `flow` value |
|------------|-----------------|
| Funnel | `funnel` |
| Ready | `ready` |
| Implementing | `implementing` |
| Done | `done` |

**"Funnel" is the board's Backlog view, not a visible column.** Cards with status `Funnel` sit in the POR board's Backlog view rather than on the active Kanban columns — this is deliberate, it's how the [[portfolio-backlog|Project funnel]] (`funnel.md`) is represented in Jira: a drag-to-reorder list that doesn't clutter the board. See [[portfolio-backlog#Jira representation|Portfolio Backlog — Jira representation]] for the mechanism, and the note there on how this differs from the BWS board's Backlog.

**Labels**

Every POR Project carries two types of label, enabling workstream filtering on both the board and the backlog view:

| Label | Example | Applied by | Purpose |
|-------|---------|------------|---------|
| Workstream | `career`, `performance` | `/jira-sync` (additive, never removes) | Marks which workstream a Project belongs to. Present on all POR Projects. Use the label filter on the board or backlog to view one workstream at a time. |
| `funnel` | `funnel` | `/project-planner` | Marks a parked idea not yet through the commitment gate. Added when the POR card is first created; removed when the Project graduates via `/project-planner`. Gate-qualified Projects carry only the workstream label. |

To filter by workstream: use the **Label** filter on the POR board or backlog and select the workstream label. You can toggle between workstreams without any board configuration changes.

**Direction rule:** Jira is authoritative for `flow` (board position). The wiki is authoritative for everything else (Objective, Outcomes/Outputs, WSJF, size, stories).

---

## SAFe Context

This is a simplified version of SAFe's Portfolio Kanban. The key adaptations for a solo operator:

| Our stage | Flow value | SAFe equivalent(s) | What we compressed |
|-----------|-----------|--------------------|--------------------|
| Funnel | `funnel` | Funnel | Direct mapping — raw ideas not yet through the commitment gate |
| Ready | `ready` | Reviewing + Analyzing + Portfolio Backlog | Three SAFe stages collapsed — a solo operator runs the commitment gate, defines, scores, and approves in one `/project-planner` session, then the Project waits for capacity |
| Implementing | `implementing` | Implementing | Direct mapping |
| Done | `done` | Done | Direct mapping |

The main compression: SAFe's Reviewing → Analyzing → Portfolio Backlog collapses into one `ready` stage because the commitment gate, Project interview, and WSJF scoring are all handled by one person in one `/project-planner` session. There is no separate Review column — it only earns its place when "reviewing" has duration (a queue waiting on other people), which never happens for one operator. See the note under [[#Stages]] for the full rationale.

**On "Portfolio Backlog":** SAFe's "Portfolio Backlog" isn't really a single stage — it's an umbrella covering Funnel → Reviewing/Analyzing → Ready (everything not yet Implementing). If forced to pick one stage as the closest match, it's `ready` — Projects fully defined and scored, waiting to be pulled into implementation. See [[portfolio-backlog#SAFe Terminology: "Portfolio Backlog" Isn't One Thing|Portfolio Backlog]] for the full explanation.

---

## Links

- [[project|Project Reference]] — what a Project is and how to define one
- [[portfolio-backlog|Portfolio Backlog]] — the parked ideas list
- [[agile-workflow|Agile Workflow]] — how the Portfolio Kanban fits into the full planning hierarchy
- [[wsjf|WSJF Reference]] — scoring methodology used to rank Projects
- [[../skills/jira-pull/_index|jira-pull skill]] — Jira → wiki sync

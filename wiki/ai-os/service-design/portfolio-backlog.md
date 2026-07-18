---
type: reference
updated: 2026-06-15
---

# Portfolio Backlog — Process Reference

**Open this when you want to understand how the Project Funnel works: what goes in, what the fields mean, and how ideas graduate to full Projects.**

> **Scope:** this file describes funnel mechanics only - what the Funnel is, how
> items graduate, and field definitions. It holds no live Project or deliverable
> state. Live state lives in [[../../projects/project-priorities|Project Priorities]]
> (ranking/flow) and each Project's own file.

For actual funnel items, see [[funnel|Project Funnel]].
For how Projects flow through stages, see [[portfolio-kanban|Portfolio Kanban]].
For how to define a Project, see [[project|Project Reference]].

---

## SAFe Terminology: "Portfolio Backlog" Isn't One Thing

In SAFe, "Portfolio Backlog" is often misread as a single backlog artifact — an ordered pile of approved work waiting for delivery, like a product backlog. It isn't.

- **"Portfolio Backlog" is an umbrella term** for Projects that have entered the portfolio kanban but haven't reached Implementing — i.e. everything across SAFe's **Funnel → Reviewing/Analyzing → Ready**. In our compressed flow that is just two stages: `funnel` and `ready` (SAFe's Reviewing/Analyzing is folded into `ready` — there is no separate `review` stage).
- A backlog usually means "an ordered list of work items sitting and waiting." At portfolio level the emphasis is on *progressing* Projects through validation and approval, not maintaining a queue of committed work — it's a flow, not a pile.
- **If forced to name the single closest state, it's `ready`** — approved, scored Projects waiting for capacity. That's the mapping used in [[portfolio-kanban#SAFe Context|Portfolio Kanban's SAFe Context table]].

This file is named for that umbrella sense — "the backlog of stuff not yet in flight." Its content below covers the **Funnel**: the entry point into that umbrella, where ideas sit before the commitment gate.

---

## What is the Funnel?

The Funnel is the inbox for Project-sized ideas that haven't passed the commitment gate. It exists to capture ideas with enough context to make a fast go/no-go decision later — without re-researching from scratch, and without forcing a full definition on something that isn't ready.

**Funnel items live at:** [[funnel|wiki/projects/funnel.md]]

---

## Capture Methods — How to get an idea into the Funnel

There are two ways to capture a new Project idea. The **Jira-first method is preferred** — it keeps the Portfolio Kanban board as the primary capture surface, which is faster and more visual.

### Method 1 — Jira-first (preferred)

1. **Create a Project on the POR board** — write a rough description in the issue body (goals, rationale, anything you know). Label is not required at this stage.
2. **Transition it to `Funnel` status immediately** — new Project cards default to `Backlog` status, which is NOT mapped to the POR board. A card in `Backlog` status will show "work item not visible" on the board. Open the issue and transition it to `Funnel` before doing anything else.
3. **Run `/jira-pull`** — the skill detects the new Funnel Project with no matching wiki row and prompts you to add it to `funnel.md`, using the Jira description as a hypothesis draft.
4. **Run `/project-planner`** when ready to gate-qualify — the commitment gate is Step 0. If it passes, the POR card is promoted (relabelled, transitioned to Ready) and a full Project file is created. If it fails, the funnel row and card stay in place with a sharpened hypothesis.

### Method 2 — Wiki-first (alternative)

1. **Add a row to `wiki/projects/funnel.md`** with hypothesis and trigger.
2. **Run `/project-planner`** which creates the POR card at the end of the funnel entry (if not gate-qualified) or at the end of the full interview (if gate-qualified).

### What you don't need to do

- Don't worry about hypothesis/trigger wording when creating the Jira card — rough notes are fine. `/jira-pull` will draft the funnel row from the description, and `/project-planner` will sharpen the hypothesis during the interview.
- Don't create a wiki Project file manually — that is `/project-planner`'s job.

### Common gotcha

New Project cards default to `Backlog` status in Jira. `Backlog` is NOT one of the POR board's statuses — the board only knows Funnel, Ready, Implementing, Done. If you skip the transition step you will see "Changes saved, but work item not visible" on the board. Fix: open the issue and transition to `Funnel`.

---

## What goes in the Funnel?

Any initiative that:
- Is too large to be a single user story (≥5h of work)
- Has a plausible payoff but hasn't been validated yet
- Isn't ready for the commitment gate (the payoff or timing isn't compelling enough right now)

**The funnel is the *first* project tier — but not the rawest place an idea can sit.**
Truly unclassified ideas (no hypothesis yet, might not even be a project) live one
step earlier in the capture inbox at [[brain-dump|raw/brain-dump.md]]. An idea earns
a funnel slot only once it has a **hypothesis + trigger**; before that it's just a
capture. There is no separate "project someday" tier — the capture inbox is shared
across projects, BAU tasks, and wiki reference, because a raw idea isn't yet known
to be any of them. See [[prioritization-framework|Prioritization Framework]].

---

## Funnel Item Fields

| Field | Purpose |
|-------|---------|
| **Item** | Name of the idea — short, descriptive |
| **Hypothesis** | One sentence: the concrete payoff if this gets done. Must be specific enough to evaluate, not vague ("it would be good") |
| **Trigger** | What needs to be true for this to move to Ready (be defined and scored via `/project-planner`) — a dependency, a milestone, a date, or "anytime" |
| **Added** | Date parked |
| **Jira** | Linked POR board card — see "Jira representation" below |

---

## Jira representation

Each funnel row also gets a lightweight card on the [POR board](https://agileict.atlassian.net/jira/software/c/projects/POR/boards/48):

- **Issue type:** Epic, **Project:** POR
- **Label:** `funnel` — distinguishes these from real Projects (which carry no label and have their own `por-key`)
- **Status:** `Funnel` — this status sits in the board's **Backlog view**, not on the active columns, so it doesn't clutter the board
- **Description:** Hypothesis + Trigger, copied from the wiki row

This gives a visual, drag-to-reorder view of funnel ideas in Jira's Backlog alongside the structured wiki row — the wiki row is the source of truth for content, the Jira card is the visual reminder.

**This "Backlog" is not the same as the BWS (Agile Sprints) board's Backlog.** The POR Backlog holds `Funnel`-status Projects — not-yet-committed Project ideas, the portfolio-level "someday" pile (this now includes XXS standalone deliverable ideas, not just Project-sized ones). The BWS Backlog holds Stories/Enablers/Tasks that have already passed the admission gates (scoped, sized, value-linked — see [[../../deliverables/_index|deliverables/_index]]) and are waiting for sprint capacity; it is not a someday pile. Not-yet-admitted deliverable ideas tied to a Project live in that Project's own `## Funnel` section, which has no Jira presence until an item is promoted via `/define-user-story` or `/define-enabler`.

---

## How items graduate

1. A trigger fires (or the user decides to evaluate the idea)
2. Run `/project-planner` — the commitment gate is the first step
3. If the gate passes: full interview → Project file created in `wiki/projects/` → flow set to `ready` → the POR funnel card is reused (relabel: remove `funnel`, transition to `Ready`, becomes the Project's `por-key`) rather than creating a second card
4. If the gate fails: item stays in the Funnel with a sharpened hypothesis and updated trigger; its POR card stays as-is
5. Remove the row from `funnel.md` once it has its own Project file (regardless of which flow stage it enters)

---

## How items regress

Projects that have been through the commitment gate but need to return to the Funnel (e.g. hypothesis invalidated, scope needs rethinking) keep their own Project file — they don't go back into `funnel.md`. The Project file is updated with a sharpened hypothesis and trigger under the Stage Regression process (see `/project-planner`).

---

## Links

- [[funnel|Project Funnel]] — the actual funnel items
- [[../../projects/project-priorities|Project Priorities]] — defined Projects ranked by WSJF
- [[../../projects/_index|Projects — Master List]] — navigation index of all Project files
- [[portfolio-kanban|Portfolio Kanban]] — how Projects flow through stages
- [[project|Project Reference]] — what a Project is and how to define one

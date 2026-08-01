---
type: reference
updated: 2026-08-01
---

# Systems Register

A live inventory of every **system, process, or tool** Julian has built for himself, and whether it is actually being *used*. Its job is accountability, not design: the ADHD reward is in *building* a system, not *running* it, so systems get created and silently abandoned the moment they stop being novel. This register makes that abandonment visible.

**The load-bearing column is Status.** An `Abandoned` or `Lapsed` label next to days of build effort is the uncomfortable signal that does the work. Review this register regularly and force each row to a decision: re-adopt (with a forcing-function) or deliberately retire.

**Why this exists:** see [[adhd-aware-work-patterns]] (§ *Build vs Adopt — a system isn't done when it's designed, it's done when it's used*) and [[self-sabotage-and-fear]] (§ *The false prerequisite*). Sits alongside [[goals-register]] and [[habits-register]].

---

## How to read this table

- **ID** — short reference (SYS-n)
- **System** — the thing built (process, tool, integration, framework)
- **Built** — roughly when it was created
- **Purpose** — what it was meant to do
- **Adoption forcing-function** — the mechanism that should make you actually use it (scheduled first-use, a trigger, an accountability surface). If blank, that's the gap — the system has no reason to survive contact with boredom
- **Last used** — when it was last genuinely run
- **Status** — **New** (built, adoption not yet proven) / **Live** (used regularly) / **Lapsed** (built and adopted but has drifted) / **Abandoned** (built, never truly adopted) / **Retired** (deliberately stopped)

A **New** row is not a pass. It is a row on the clock: if it has not moved to **Live** within roughly two weeks of real use, it moves to **Abandoned**.

---

## The Rule for Adding a System

Every time a new system is built, it gets a row here **at creation**, with its adoption forcing-function named. A system with no forcing-function is a system that will be abandoned — decide the forcing-function before you consider the build finished. A system is not "done" when designed; it is done when it has been used for two weeks and survived the boredom.

---

## Register

| ID | System | Built | Purpose | Adoption forcing-function | Last used | Status |
|----|--------|-------|---------|--------------------------|-----------|--------|
| SYS-1 | Jira sprint system (BWS Development Sprints + Claude integration; ceremony skills: `/sprint-plan`, `/standup`, `/retro`, `/morning`, `/jira-sync`, `/jira-pull`) | 2026 (mid) | Run personal work as sprints — plan, track, review deliverables against WSJF priority | Ceremony skills scheduled at fixed times (morning 6am, standup/retro 4pm) — but no habit was formed to honour them | Shortly after build | **Lapsed** — overcomplicated the start ("needs a perfect sprint plan first"), then dropped it. The ceremonies exist as a ready-made re-adoption forcing-function if restarted |
| SYS-2 | Payoff Test gate (see [[payoff-vs-prestige-bias]]) — embedded in `/define-task`, `/define-user-story`, `/define-enabler`, `/project-planner`, `/sprint-plan`, `/retro` | 1 Aug 2026 | Stop Career/Performance work being selected because it would be impressive to explain rather than because it produces something. Three questions: payoff route, silence test, "good enough when" | **Automatic** — fires inside skills already run; nothing new to remember. Accountability surface is the `/retro` question *"what did you spend time on this week you couldn't invoice for?"*, and the 5 SP speculative cap checked at `/sprint-plan` | Not yet — first use is the next `/define-*` run | **New** — not yet adopted. Adopted only once it has survived two consecutive retros without being skipped |

---

## Notes

- SYS-1 is the founding case study for this register. The lesson that created the register: *building the system was the easy, rewarding part; the resistance was to adopting a boring, novel, context-switching routine.* The false blocker was "I need to design the perfect sprint before I can start" — untrue; you just start the sprint and move items in and out.
- Populate the rest of the register by listing other systems built and dropped (prioritisation frameworks, capture inboxes, tracking spreadsheets, automations).

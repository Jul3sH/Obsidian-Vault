---
type: reference
updated: 2026-09-03
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
| SYS-3 | Prompt Zero (`/prompt-zero` skill + the `## Prompt Zero` section in every deliverable file) | 5 Aug 2026 | Force Julian to write the grounding brief for a piece of work **in his own words** before any model touches it, using the Seven Questions (outcome, stakes, done, wrong, unwritten context, pieces, hard part). Stops the work quietly becoming the model's idea of the task | **Automatic** - the gate is in `AGENTS.md` Deliverable-First Step 2, so every agent checks it on every session that starts or resumes a deliverable. No ceremony to remember. Backstop is the `/standup` Step 3.5 check, which logs a miss when work was done without a brief. Waiver allowed only at size 1, and it is written down | Not yet: first use is the next deliverable started | **New** - not yet adopted. Adopted only once three consecutive deliverables have started with a brief written before the work, not backfilled after |
| SYS-2 | Payoff Test gate (see [[payoff-vs-prestige-bias]]) — embedded in `/define-task`, `/define-user-story`, `/define-enabler`, `/project-planner`, `/sprint-plan`, `/retro` | 1 Aug 2026 | Stop Career/Performance work being selected because it would be impressive to explain rather than because it produces something. Three questions: payoff route, silence test, "good enough when" | **Automatic** — fires inside skills already run; nothing new to remember. Accountability surface is the `/retro` question *"what did you spend time on this week you couldn't invoice for?"*, and the 5 SP speculative cap checked at `/sprint-plan` | Not yet — first use is the next `/define-*` run | **New** — not yet adopted. Adopted only once it has survived two consecutive retros without being skipped |
| SYS-4 | Agent-fired guard skills (`commitment-guard`, `decision-visualisation-check`) | Aug 2026 | Catch behavioural failure modes in-session: emotional U-turns on locked decisions; incomplete mental images when evaluating options by feel | **Automatic** - Claude fires them on trigger phrases; no habit required of Julian | Not yet observed firing in a live session | **New** - adopted once each has fired and been useful in a real session |
| SYS-5 | On-demand tools (`ats-checker`, `resume-tailor`, `storm-research`, `llm-council`, `notebooklm-py`, `youtube-notebook`, `whatsapp-someday`) | Jun-Aug 2026 | Invoked when a matching job arises; no recurring loop to abandon | None needed - value is per-invocation, not habitual. Risk is forgetting they exist, which this row now covers | Various (whatsapp-someday and youtube-notebook ran Aug; resume-tailor/ats-checker ran Jun for SHL) | **Live (on-demand)** |
| SYS-6 | Claude memory system (user.md + feedback-*.md + MEMORY.md index) | Jul 2026 | Persist behavioural corrections and profile across sessions | **Automatic** - harness loads it every session; writes are agent-prompted at correction time | Every session | **Live** |
| SYS-7 | Systems-register review loop (`/retro` Step 3.5) | 3 Sep 2026 | Close this register's own missing read loop: weekly walk of the rows at retro, forcing re-adopt / retire / no change | Every retro (Sunday), inside the retro skill; the retro's own trigger is a SessionStart hook that reminds on any Sunday session where no retro is logged yet. **Caveat: fires only if Julian opens Claude on a Sunday** - no session, no reminder. **Caveat: rides on SYS-1, which is Lapsed** - if retros do not run, this does not either | Not yet | **New** |

---

## Notes

- SYS-1 is the founding case study for this register. The lesson that created the register: *building the system was the easy, rewarding part; the resistance was to adopting a boring, novel, context-switching routine.* The false blocker was "I need to design the perfect sprint before I can start" — untrue; you just start the sprint and move items in and out.
- Backfilled 3 Sep 2026 (SYS-4 to SYS-7, aggregate rows). Anything new gets its own row at creation per the rule above; the monthly retro check (SYS-7) is the read loop.

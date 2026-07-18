---
type: reference
created: 2026-05-14
updated: 2026-06-09
---

# Deliverables — Reference Guide

**Open this when you want to understand how Deliverables and Enablers work: what they are, how to define them, how to size and score them, and how scope discipline is enforced.** This covers everything from deliverable type selection through to Definition of Done and timebox execution.

For Project-level guidance, see [[project|Project Reference]].
For the WSJF scoring methodology — formula, components, and rationale — see [[wsjf|WSJF Reference]].
For the full planning hierarchy and ceremonies, see [[project-workflow|Project Workflow]]. For Jira configuration, see [[jira-system-design|Jira System Design]].
For the skills that run the deliverable interviews, see [[../skills/define-user-story/_index|define-user-story]], [[../skills/define-enabler/_index|define-enabler]], and [[../skills/define-task/_index|define-task]].

---

## Deliverable Types

Every deliverable in the backlog must be defined as a **User-facing Deliverable**, an **Enabler**, or a **Task** before it enters a timebox. This happens after `/project-planner` and before `/timebox-plan`.

### User-facing Deliverable

A deliverable where a human receives something useful. Written in the standard format:

> *As a [role], I want [capability] so that [benefit].*

User-facing deliverables have **Acceptance Criteria** — 3–5 binary, testable conditions that define done. Use `/define-user-story` to create the `.md` file.

### Enabler

Technical work that creates the architectural runway for future deliverables. Enablers are not user-facing — they exist to unblock or de-risk future work.

| Type | Purpose |
|------|---------|
| **Exploration** | A spike — time-boxed research or prototype to reduce uncertainty |
| **Architecture** | Structural or design work that future deliverables depend on |
| **Infrastructure** | Platform, tooling, or environment work |
| **Compliance** | Regulatory or security requirements |

Enablers have **Success Criteria** rather than acceptance criteria — what must be true for the enabler to be considered complete. Use `/define-enabler` to create the `.md` file.

### Task

Everything else — admin, reference material, one-off setup, periodic maintenance. Not user-facing value, and not technical runway for future deliverables, but it still produces a concrete result.

Tasks have **Completion Criteria** (2-4, binary and outcome-framed) in place of acceptance or success criteria. Use `/define-task` to create the `.md` file.

### Choosing between a User-facing Deliverable, an Enabler, and a Task

| Signal | Deliverable type |
|--------|-----------------|
| A human gets something useful from this | User-facing Deliverable |
| This unblocks or de-risks future work | Enabler |
| This is research to reduce uncertainty | Enabler (Exploration) |
| This wires up infrastructure nobody directly uses | Enabler (Infrastructure) |
| This changes something the user experiences | User-facing Deliverable |
| Generic backlog work — produces a result but isn't value or runway | Task |

When in doubt: would someone outside the technical team notice if this wasn't done? If yes, User-facing Deliverable. Does the next deliverable depend on it? If yes, Enabler. Otherwise, Task.

---

## Deliverable Files

The `.md` files in `wiki/deliverables/` — one per deliverable or enabler — are the source of truth for deliverable content. They feed into `/jira-sync` (which pushes to Jira) and `/timebox-plan` (which reads DoD and hours at commit time).

`/project-planner` does **not** create deliverable files. Deliverable, enabler, and task files are created by `/define-user-story`, `/define-enabler`, or `/define-task` when the user is ready to elaborate and execute.

---

## Sizing

### Story Points

Story points are the primary sizing unit. They capture three dimensions — not just how long something takes, but how hard and how uncertain it is:

- **Effort** — how much raw work is involved?
- **Complexity** — how technically intricate or difficult is the implementation?
- **Uncertainty** — how well-understood is the work? Poorly-defined tasks score higher because the unknown space is real cost.

Story points use a modified Fibonacci scale (1, 2, 3, 5, 8) — the same unified scale used for Project sizing (see [[wsjf|WSJF Reference]]). Deliverables do not use t-shirt labels; the number is the authoritative value for timebox capacity planning:

| Size | Hours | Duration | Gate |
|------|-------|----------|------|
| 1 | 1–4h | Up to half a day | |
| 2 | 5–8h | Up to a day | |
| 3 | 9–16h | Up to 2 days | |
| 5 | 17–40h | Up to a week | |
| 8 | 41–80h | Up to 2 weeks | Must be split |

**Hours are an anchor, not a contract.** A deliverable estimated at 8 hours of effort but with high uncertainty might be a 3 (not a 2) because the uncertainty inflates the real cost. Over time, the portfolio of completed deliverables becomes the primary reference for relative sizing — not the hours column.

**1 SP = 1 hour** for Jira purposes. This makes timebox capacity immediately readable on the board — 40 SP committed = a full timebox.

### Estimation Process

When sizing a deliverable, `/define-user-story` and `/define-enabler` prompt three questions:

1. **Effort:** "Ignoring complexity and unknowns — how much straightforward work is this?"
2. **Complexity:** "How technically difficult is the implementation? Any tricky integrations, unfamiliar APIs, or architectural decisions?"
3. **Uncertainty:** "How well do you understand what needs to be built? Are there unknowns that could expand the scope?"

After answering, the skill proposes a story point value and compares against completed deliverables of similar scope from the portfolio in `wiki/deliverables/`. This relative comparison improves accuracy over time.

### Why a Fibonacci-like scale

The jump from M=3 to L=5 (rather than 4) reflects the real non-linearity of effort: a 17–40h deliverable is not just "a bit more" than a 9–16h deliverable — it's a qualitatively different commitment with compounding uncertainty. The gaps in the scale force honest decisions rather than allowing "it's about a 4" hedging.

### XL rule

XL (8 points) is valid at Project level. At deliverable level, XL is a flag — the work must be split into smaller deliverables before timebox planning. L (5 points) is the practical maximum for a single deliverable.

### Velocity

Velocity is the number of story points completed per timebox. It replaces fixed hours as the capacity measure once enough data exists:

- **Timeboxes 1–3:** Use the hours anchor as a rough guide. Commit ~25–30 points per timebox (based on 40h capacity and the hours mapping).
- **Timebox 4+:** Use rolling average velocity from the last 3 timeboxes. The `/retro` skill tracks points committed vs completed; `/timebox-plan` reads velocity to set capacity.

Velocity naturally absorbs the difference between estimated and actual effort — including interruptions, context-switching, and estimation bias. It's the self-correcting mechanism that makes story points work over time.

### Completed Deliverable Portfolio

Every completed deliverable retains its original estimate and actual outcome in `wiki/deliverables/`. Over time, this portfolio becomes the primary reference for relative sizing:

- "Last time you estimated an API integration at 3 points, it took a full timebox. Should this similar one be a 5?"
- "You've completed three XS deliverables in a single day before — does this feel like another one of those?"

The `/retro` skill maintains this data. The `/define-user-story` and `/define-enabler` skills read it during estimation.

---

## Outcome Framing — Acceptance & Success Criteria

### The principle

Every criterion — whether an Acceptance Criterion on a user-facing deliverable or a Success Criterion on an enabler — must describe what **exists or is true** when the work is done, not what you **did**.

| Activity-framed (wrong) | Outcome-framed (right) |
|------------------------|----------------------|
| "Research completed" | "Tool recommendation documented at wiki/[path] with rationale and cost breakdown" |
| "Integration built" | "Google Sheets row updates within 30s of enrichment script completing end-to-end" |
| "Spike done within 4h" | "Spike completed within 4h; recommendation exists at wiki/[path] regardless of outcome" |
| "Tests reviewed" | "All tests passing in CI with zero failures on main" |

### Why this matters

Activity-framed criteria have no natural stopping point. "Research completed" is done whenever you decide to stop — which means it's done whenever you're bored, tired, or distracted, not when something meaningful exists. For an ADHD operating style, this is a direct path to either never finishing (endless research) or declaring done too early (nothing was produced).

Outcome-framed criteria are binary: either the artifact exists or it doesn't. Either the system does the thing or it doesn't. Someone else could walk in and verify them without asking questions.

### The signal to watch for

**Past-tense action verbs** are the primary indicator of activity-framing: "completed", "reviewed", "researched", "built", "done". When you see one, ask: "What artifact or state exists as a result?" That's the criterion.

The time cap for exploration spikes is a partial exception — "spike completed within 4h" is a valid constraint — but it must always be paired with an artifact criterion: *"within 4h; [output] exists at [location]."* A time cap alone tells you when to stop, not what exists when you do.

### Where this applies

- **User-facing deliverables** → Acceptance Criteria (3–5, enforced by `/define-user-story`)
- **Enablers** → Success Criteria (2–4, enforced by `/define-enabler`)
- **Tasks** → Completion Criteria (2-4, enforced by `/define-task`)
- **Definition of Done** → applies to all three; the DoD is the end-state paragraph that wraps the criteria

---

## Deliverable Scope Discipline

### The core principle

**Deliverable scope is fixed. Timebox scope is flexible.**

A deliverable's Definition of Done is a contract — it defines exactly what "done" means before work begins. It doesn't change during the timebox. The tasks inside a deliverable are simply the steps to reach that fixed outcome.

Timebox scope is where flexibility lives. If something takes longer than estimated, or a higher priority emerges, you negotiate *which deliverables* to complete — not what any individual deliverable delivers.

### Why this matters for planning accuracy

WSJF scores and capacity planning only work if deliverable sizes are trustworthy. A deliverable estimated at 8h that quietly becomes a 16h deliverable corrupts velocity data, breaks the morning skill's hour allocations, and makes future timebox planning unreliable. Fixed deliverable scope is what makes the whole system predictable.

### The ADHD risk: scope creep is silent and fast

Scope creep within a deliverable is particularly tempting with ADHD because it feels like progress — you're working, you're engaged, you're building something. But you're building something *different* from what was agreed. By the time the timebox ends, the deliverable is either unfinished (because the expanded scope took longer) or "done" in a way that wasn't defined upfront and can't be measured.

The antidote is structural, not willpower-based. The Definition of Done must be:
- **Written before the hours estimate** — you can't estimate what you haven't defined
- **Binary or testable** — "can I answer yes or no to whether this is done?"
- **Specific enough to have a stopping point** — vague DoDs have no finish line

**Bad DoD (no stopping point):** "Improve the LinkedIn enrichment pipeline"
**Good DoD (binary, specific):** "LinkedIn enrichment script processes 100 contacts end-to-end and writes results to the Google Sheet without manual intervention"

### What to do when scope expands mid-timebox

Discovery during execution is normal — you find something that needs doing that wasn't in the original DoD. The correct response is not to quietly expand the deliverable. It's one of:

1. **Trivial addition (< 30 min):** absorb it, note it at standup
2. **Meaningful addition:** create a new Jira deliverable, add it to the backlog, size it at the next timebox planning
3. **Deliverable was mis-scoped:** flag at retro — the DoD was wrong upfront, not discovered mid-timebox

### Ceremony accountability

The ceremonies enforce this discipline systematically:

**Timebox planning (`/timebox-plan`):**
- Definition of Done is written and confirmed *before* the hours estimate is committed
- The skill will ask: "What specifically will done look like for this deliverable?" — answer must be binary/testable
- If the DoD can't be stated clearly, the deliverable isn't ready to commit

**Daily standup (`/standup`):**
- Includes a scope check: "Did you work on anything today outside the current deliverable's Definition of Done?"
- Yes → name it. Either it's trivial (note it), or it needs a new deliverable (create it before standup ends)
- This surfaces scope drift daily, before it compounds into a timebox failure

**Retrospective (`/retro`):**
- Reviews completion rate as a leading indicator — deliverables consistently running over their hours estimate signals scope creep, not bad estimation
- Asks: "Did any deliverable deliver beyond its original Definition of Done?" If yes, that's scope that should have been a separate deliverable
- The "1 change" output from each retro is a direct input to tightening DoDs at the next timebox planning

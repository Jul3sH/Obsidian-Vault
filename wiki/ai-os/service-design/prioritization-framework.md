---
type: reference
created: 2026-06-08
status: draft
---

# Prioritization Framework

> *How to decide what to work on and when — across workstreams, sprints, and the day.*

For the workstream priority hierarchy (the "why" behind the ordering), see [[workstream-framework]].
For how Projects are scored and ranked within a workstream, see [[wsjf]].
For how Projects flow through the portfolio, see [[portfolio-kanban]].

---

## Why This Pipeline Exists (the ADHD focus problem)

The constraint this whole framework solves: **ambition consistently exceeds bandwidth.** There is no shortage of ideas, only of time. The system's job is not to evaluate everything well, it is to keep the single most impactful thing in front of you and hold everything else somewhere safe so it does not pull focus. Guiding rule: **every evaluation step must pay for itself in better focus, or it gets cut.** An hour spent scoring is an hour not spent doing.

### Three stages, three different questions

| Stage | Question it answers | Evaluation cost |
|-------|--------------------|-----------------|
| **Capture** ([[brain-dump\|raw/brain-dump.md]]) | "Will I lose this idea?" | Zero. Capture only. |
| **Funnel** ([[funnel]]) | "Should this become a commitment at all?" | Light. Expected value. |
| **Scheduled** (Project + WSJF) | "Given I've committed, in what order?" | Full. WSJF score. |

- **Capture = zero evaluation.** Its only job is to silence the "I'll lose this idea" anxiety so you can let it go for now. Cheap on purpose. The capture inbox is **unclassified** — an item there is not yet a project; it might become one, or a BAU task, or wiki reference, or nothing.
- **Funnel = candidate evaluation.** "Should this become a commitment at all?"
- **Scheduled (Project + WSJF) = committed and sequenced.** "Given I've committed, in what order?"

Capture is **pre-hierarchy** and feeds multiple destinations by triage — project-sized ideas *and* standalone deliverable ideas (the latter as XXS Project candidates) graduate into the Funnel. The rest route to the wiki (reference/learning), or to the bin. Funnel items graduate to Scheduled only when they earn a commitment. Most ideas should die in Capture or Funnel. That is the system working, not failing.

> **Naming note:** the capture stage used to be called "Someday" and lived at `wiki/projects/someday.md`. It was renamed and moved to [[brain-dump\|raw/brain-dump.md]] because the items aren't projects — filing them under `projects/` mislabelled them. There is no separate deliverable-level "someday" tier — standalone deliverable ideas are XXS Project candidates and live in the Funnel alongside Project-sized ideas.

### Two decisions, two tools

The funnel and the schedule answer different questions, so they use different tools. Conflating them is the classic mistake.

- **Selection (funnel admission)** uses **expected value**: roughly payoff multiplied by probability of success. This is decision-tree thinking: identify the options, the desired outcomes, the payoffs, and the likelihood of achieving them. Probability belongs here because the entire question is whether an uncertain bet is worth committing to.
- **Sequencing (scheduling)** uses **WSJF**: `(Value + Time Criticality + Risk/Opportunity) ÷ Job Size`. WSJF assumes the work is already committed and only orders it. It deliberately carries no probability term. See [[wsjf]].

Bolting probability onto WSJF would corrupt a clean sequencing tool with false precision. Keep probability upstream, at the admission gate.

### Confidence, not percentages

Probability enters at the commitment gate (`/project-planner` Step 0.3) and **only for Outcome-type payoffs**: bets on how the world or someone else responds. Output-type payoffs (a deliverable within your control) are effectively certain once built, so they skip it.

It is recorded as a **band (High / Medium / Low), never a percentage.** A made-up "65%" feels rigorous but is fiction you cannot calibrate. A band is honest and fast.

Confidence is a **gate modifier, not a score**:
- **High** confidence Outcomes proceed normally.
- **Medium / Low** confidence Outcomes must be framed cheapest-test-first. The MVP and Leading Indicators become the real gate: the bet earns a full Project slot only after the smallest test fires.

This is the **"commit small, kill fast"** principle, and it is why the Hypothesis and Leading Indicators steps exist. They are the lean, ADHD-friendly substitute for explicit probability weighting: instead of guessing a number up front, you commit small and let an early signal either fire or kill the idea. Real signal beats invented precision.

---

## The Two-Axis Model

Every piece of work sits on two axes:

1. **Workstream priority** — which layer of the hierarchy does this serve? (Wellbeing first, Personal last)
2. **WSJF score** — within a workstream, how urgent and valuable is this item relative to others?

When deciding between competing items, resolve workstream priority first. Only compare WSJF scores within the same workstream layer, or when workstream priority is equal.

---

## Workstream Priority (top to bottom)

| Priority | Workstream | Type |
|----------|-----------|------|
| 1 | Wellbeing | SMART |
| 2 | Relationships | SMART |
| 3 | Finance | SMART |
| 4 | Career | OKR |
| 5 | Performance | OKR |
| 6 | Personal | SMART |

A Wellbeing goal outranks any Career goal. A Relationships goal outranks a Finance goal. This is the tiebreaker when time or energy is scarce.

The chain is complete: Personal feeds Performance, which sharpens Career, which produces Finance, which enables Relationships, which sustains Wellbeing. Every layer has a purpose.

---

## Scheduling Rules

### Sprint capacity (defined 28 Aug 2026)

- **Sprint planning runs weekly, and capacity is fixed fresh each week.** Capacity is a per-week judgement made at planning time, never a standing number carried forward.
- **Sprint capacity covers discretionary (WSJF) work only.** Working estimate as of Aug 2026: **2-4 focused hours per day**, set each week depending on the fixed-date and BAU load. The weekly question is "how much discretionary time does THIS week actually have?", answered after deducting the fixed-date draw (step 0 below).
- **Why sprints are scoped this narrowly (the adoption lesson):** previous sprint attempts failed because the plan covered everything, and the variable work (fixed-date obligations, BAU churn) changed dramatically mid-week, breaking the plan and discrediting the ceremony. A plan that only commits the discretionary hours survives a chaotic week: the variable work flexes on the Kanban, the sprint commitment stays honest. This is the structural fix for the sprint-abandonment pattern (see the build-dont-adopt correction) - the system was not too heavy, it was scoped to work it could not control.

### Still to define

- **Crisis override** — when a Wellbeing or Relationships issue bumps planned Career/Performance work
- **Minimum viable attention** — floors for workstreams that are not currently active (e.g. no active Wellbeing sprint goal does not mean zero attention)
- **Personal protection** — Personal time is protected even though it sits last in priority; being last does not mean zero

---

## Project Classes (added 28 Aug 2026)

WSJF answers "which discretionary project earns the next unit of capacity?". Some projects are not discretionary: the commitment is made, the date is external, and no ranking can change whether the work happens. Ranking those is a category error - no score makes "ship the house before departure" comparable with "study X vs build Y". First concrete case: [[uk-relocation-project]] execution, HK exit fixed at 2026-09-15.

Two classes, declared in project frontmatter. The classifying test (Julian, 28 Aug): **"do I need to compare this work's cost of delay against other initiatives that add value?"** If yes, it is discretionary and WSJF applies. If the work simply must be done by an external date, no comparison is meaningful and it is fixed-date. The test is workstream-agnostic: discretionary work is mostly Performance (development), but Relationships, Wellbeing and Career items qualify whenever they are genuinely optional-and-competing.

| Class | Frontmatter | Scheduling rule | Where its tasks run |
|---|---|---|---|
| **Discretionary** (default) | none needed; `wsjf: <score>` | Ranked by WSJF; competes for remaining sprint capacity | Weekly **sprints** (BWS board) |
| **Fixed-date** | `class: fixed-date`, `hard-date: YYYY-MM-DD`, `wsjf: n/a` | Never ranked. Scheduled **backwards from the date** (what must start when, to land by then) | **BAU Kanban**, pulled continuously, ordered by the backwards schedule |

### Execution routing (sprint vs Kanban)

- **Sprints carry discretionary work only:** the deliverables of WSJF-classified projects, assigned at sprint planning.
- **Everything else runs on the existing BAU Kanban:** fixed-date project tasks and non-project BAU tasks. Kanban work is pulled continuously; for fixed-date projects the pull order is the backwards schedule, and a slipping item escalates by date proximity, not by score.
- **Fixed-date work still consumes sprint capacity even though it is not sprint content.** At sprint planning, estimate the week's expected draw from fixed-date Kanban work and set sprint capacity to what remains, before any ranking.
- **Known gap (28 Aug 2026, Julian's technical debt, deliberately deferred):** the BAU Kanban board is not structurally aligned with Portfolio Projects. Do not build alignment as a side effect of routing tasks; it is logged in the project funnel (Performance) as discretionary development work; promotion is Julian's call.

Guard-rail: fixed-date is for genuinely external, committed dates (a departure, a legal deadline, an enrolment window) - not for self-imposed urgency. If the date is Julian's own and movable, it is discretionary and WSJF applies; use a forcing function ([[mm-commit-with-a-forcing-function]]) rather than a class change.

This is the quick fix for the broader methodology question logged in `raw/brain-dump.md` (30 Jun: is WSJF right for all workstreams?). That review may replace or extend this; until then, two classes is deliberately all there is.

---

## Within-Workstream Prioritisation

Within a single workstream, use WSJF to rank **discretionary** Projects. See [[wsjf]] for the full scoring model. Fixed-date projects are not ranked - see Project Classes above.

Summary: `WSJF = (Value + Time Criticality + Risk/Opportunity) ÷ Job Size`

Higher score = do first.

---

## Cross-Workstream Scheduling (sprint level)

*(To be developed. Starting point below.)*

At sprint planning, the order of consideration is:

0. **Deduct fixed-date demand first:** fixed-date work runs on the BAU Kanban, not in the sprint, but it consumes the same hours. Estimate what the backwards schedule will draw this week and set sprint capacity to what remains, before any ranking.
1. Are there any Wellbeing commitments this sprint? Protect them first.
2. Are there any active Relationships goals with near-term deadlines? Allocate before Career work.
3. Finance goals with hard dates (e.g. account review, tax deadline) — allocate next.
4. Career Projects in the current sprint backlog — ranked by WSJF.
5. Performance (development) work — only after Career commitments are covered.
6. Personal — fill remaining capacity.

---

## Links

- [[workstream-framework]] — workstream hierarchy and goal structure
- [[wsjf]] — WSJF scoring model
- [[portfolio-kanban]] — Project flow stages
- [[agile-workflow]] — full planning cadence

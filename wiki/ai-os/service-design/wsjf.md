---
type: reference
created: 2026-05-14
---

# WSJF — Reference Guide

**Open this when you want to understand how WSJF works: the formula, why each component exists, how the scale was chosen, and the principles behind counter-factual scoring.** This is the canonical methodology reference. Application at Project level is covered in [[project|Project Reference]]; application at Deliverable level is covered in [[deliverable|Deliverable Reference]].

For the full planning hierarchy, see [[project-workflow|Project Workflow]]. For Jira configuration, see [[jira-system-design|Jira System Design]].

---

## What is WSJF?

WSJF (Weighted Shortest Job First) comes from the SAFe Lean-Agile framework. The core insight is that most prioritisation mistakes come from doing large, high-value work ahead of small, equally-high-value work — the big thing *feels* more important but delivers value much later. WSJF corrects for this by dividing cost of delay by job size, forcing the trade-off to be explicit.

It also addresses a specific ADHD-related risk: mood-driven prioritisation tends to favour exciting large projects over quick, high-impact ones. WSJF makes that bias visible and correctable.

---

## Formula

```
Cost of Delay = Value + Time Criticality + Risk/Opportunity
WSJF = Cost of Delay ÷ Job Size
```

All three Cost of Delay components are scored on an adapted Fibonacci scale: 1/2/3/5/8. Job Size uses the same scale, extended to 13 for Projects. See the scoring criteria below for anchors at each level.

---

## Scoring Criteria

**Value** — what's the payoff?

| Score | Anchor |
|-------|--------|
| 8 | Transformative: directly drives a major outcome (revenue, career trajectory, critical capability) |
| 5 | Significant: meaningful contribution to a key result; clearly advances the goal |
| 3 | Moderate: real but indirect benefit; advances the goal but not critically |
| 2 | Minor: marginal improvement; easily deferred without consequence |
| 1 | Negligible: maintenance-level; no meaningful impact if never done |

**Time Criticality** — what's the cost of waiting?

| Score | Anchor |
|-------|--------|
| 8 | Window closes: specific near-term deadline; severe concrete consequence if missed this month |
| 5 | Measurable cost: income delayed, hard dependency blocks others, decision runway shrinks |
| 3 | Gradual erosion: some cost of delay but no hard deadline; momentum or context fades |
| 2 | Minor friction: slight preference for sooner, but no real consequence |
| 1 | Timing irrelevant: same value in 3 months as today |

**Risk / Opportunity Enablement** — what does this unlock?

| Score | Anchor |
|-------|--------|
| 8 | Unblocks an entire project or 3+ high-value initiatives; eliminates a showstopper risk |
| 5 | Unblocks 2–3 initiatives or significantly de-risks the portfolio |
| 3 | Unblocks one initiative or creates some downstream benefit |
| 2 | Minor downstream benefit; work could mostly proceed without it |
| 1 | Stands alone — completing it doesn't change much else |

### Job Size

Job Size uses the adapted Fibonacci scale, with different ranges for Projects and Stories. The numbers are relative — compare against completed work, not hours.

Job Size uses a single unified scale — the same Fibonacci number means the same effort regardless of whether it's a story or a project.

| Job Size | Hours | Duration | Deliverables | Projects |
|----------|-------|----------|---------|-------|
| 1 | 1–4h | Up to half a day | Yes | XXS |
| 2 | 5–8h | Up to a day | Yes | XS |
| 3 | 9–16h | Up to 2 days | Yes | S |
| 5 | 17–40h | Up to a week | Yes | M |
| 8 | 41–80h | Up to 2 weeks | Must be split | L |
| 13 | 81–160h | Up to a month | — | XL (split gate) |

One consistent Fibonacci scale (1/2/3/5/8/13) with t-shirt labels (XXS/XS/S/M/L/XL) runs across Projects, stories, tasks, and enablers. The same number means the same effort regardless of artefact type.

**Deliverables** (stories, enablers, and tasks) use sizes 1–5 freely and hit a split gate at 8. Sized during `/define-user-story`, `/define-enabler`, and `/define-task` but **not WSJF-scored** — deliverable sizing is included here for completeness since it uses the same scale.

**Projects** use the full t-shirt scale. A Project's total effort is the sum of its deliverables. In practice XXS Projects are rare — work that small is usually a single deliverable, not a Project — but the label exists so the scale is complete and consistent. Hours are calibration anchors; as the portfolio grows, compare against completed Projects rather than estimating hours.

---

## Value vs Risk/Opportunity — Avoiding Double-Counting

These two components are easy to conflate. The distinction:

- **Value** = what THIS initiative delivers directly (the intrinsic payoff when it's done)
- **RR/OE** = what OTHER things become possible because this exists

**Counter-factual test:** If someone handed you the outcome without you having to do the work, would those downstream opportunities still be blocked? If yes — that's RR/OE, not Value. Keep them separate.

*Example — Agile Claw MVP:*
- Value = Agile ICT has a working AI OS and credible consulting offering
- RR/OE = TTI job conversation, gaming company pitch, future clients — all unlocked by having a live demo to show

---

## Why Three Components and Not Just "Value"

- **Value** alone rewards high-impact work but ignores timing — a project can be high-value but worthless if done too late.
- **Time Criticality** captures the cost of delay — market windows, momentum loss, value not created.
- **Risk/Opportunity** captures dependency unlocking — a project that unblocks five others is worth more than one that stands alone, even at equal value and urgency.

---

## Why an Adapted Fibonacci Scale (1/2/3/5/8)

The original 1–3 scale was too coarse. When all stories within a focused project naturally scored near the ceiling on Value, Time Criticality, and Risk/Opportunity, the numerator was always 9 and WSJF became a simple inverse of job size — defeating the purpose of the scoring.

The adapted Fibonacci scale (1/2/3/5/8) solves this by providing enough spread to differentiate within a cluster of high-priority work, while the non-linear gaps discourage false precision. You can feel the difference between a 3 and a 5 without debating whether something is a 6 or a 7.

**Why not 1–10 or 1–20?** A linear 1–10 scale invites endless haggling over adjacent scores. Extending Fibonacci to 13/20 adds cognitive overhead without proportional benefit for a personal backlog of 6–20 stories — the top end of the scale simply never gets used. The 1/2/3/5/8 range covers the useful spectrum: negligible → minor → moderate → significant → transformative.

---

## Time Criticality — Cost of Delay, Not Deadline Urgency

This is the most important and nuanced principle in the scoring model.

Deadline-based urgency (today / this week / this month) works well for BAU tasks — it's exactly why the BAU Kanban uses it. But it breaks down for strategic projects, for two reasons.

First, most strategic projects don't have hard external deadlines. There's no date by which a campaign *must* launch — the urgency is real, but it's not calendar-driven. Asking "is this due this week?" produces no useful answer.

Second, deadline urgency is binary: you either miss the deadline or you don't. It treats urgency as an external trigger rather than something intrinsic to the work. This makes it easy to game — if there's no deadline, urgency scores as zero, even when delay is genuinely costly.

Cost of delay reframes the question entirely: *how much value is not being created for every unit of time this work isn't done?* That's a real, continuous cost — even without a deadline attached.

The split between the two Jira boards reflects this distinction directly: BAU Kanban is deadline-driven and gut-prioritised; Development Sprints are cost-of-delay-driven and WSJF-scored.

---

## Counter-Factual Questioning

The scoring process asks "what specifically gets worse if you delay this by one month?" rather than "how urgent is this?" The difference matters: the latter invites a gut answer; the former forces reasoning about actual consequences. This is particularly important for Time Criticality, where anxiety and mood can artificially inflate the score.

### Anti-Mood-Bias Check

When the user expresses urgency through emotional language ("this is stressing me out", "it feels really urgent"), apply the counter-factual check before accepting TC=5 or higher:

> "What specifically gets worse in one month if you don't do this — not how it feels, but what actually changes?"

A score of 5 or above requires a measurable cost: income delayed, market window closing, named opportunity missed. Discomfort is not a consequence.

---

## Rationale-First Scoring

For every component, the scoring sequence is:

1. Ask the scoring question
2. Listen to the user's answer
3. Show reasoning explicitly — which tier applies and why, referencing what the user said
4. Propose the score
5. Ask for confirmation

Never propose a number without first showing the reasoning. The user needs to see the logic to challenge it — and challenging the score is part of the process.

---

## WSJF is Project-Level Only

WSJF is used in `/project-planner` to rank Projects against each other — deciding which strategic initiative receives investment.

**Deliverables (stories and enablers) are NOT scored with WSJF.** Within a Project, deliverables are prioritised using MoSCoW during `/timebox-plan`, based on the Product Owner's judgement of:

1. **Business value** — how much does this move the needle on the sprint goal or a wider 3-month objective?
2. **Dependencies** — stories that unblock others get pulled up
3. **Risk** — high-uncertainty stories go early in the sprint (fail fast principle)
4. **Urgency vs importance** — conscious separation; urgency without importance is a backlog trap
5. **Stakeholder input** — the backlog gets re-ordered after each Sprint Review based on live feedback

This separation reflects how SAFe actually works: WSJF prioritises the portfolio; the Product Owner prioritises the team backlog.

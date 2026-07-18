---
type: reference
created: 2026-05-14
---

# Epics — Reference Guide

**Open this when you want to understand how Epics work: what they are, why they're structured this way, how to define them, and how to score them.** This covers Epic creation, WSJF scoring at the Epic level, and the rationale behind every design decision.

For the skill that runs the Epic interview, see [[../skills/epic-planner/_index|epic-planner]].
For the WSJF scoring methodology — formula, components, and rationale — see [[wsjf|WSJF Reference]].
For the full planning hierarchy, see [[agile-workflow|Agile Workflow]]. For Jira configuration, see [[jira-system-design|Jira System Design]].
For how Epics flow through stages (backlog → review → active → done), see [[portfolio-kanban|Portfolio Kanban]].

---

## What is an Epic?

An Epic is a strategic initiative — a unit of work large enough to require planning and prioritisation, but focused enough to have a clear outcome and stopping point.

### Two Types of Epic

**Business Epics** deliver value directly to customers or the market. Success is measured by how the world responds — leads generated, clients won, outcomes achieved. Results are expressed as Business Outcomes (external effects) or Key Results (completion), depending on whether the value is market-dependent or within your control.

**Enabler Epics** build architectural runway to support future Business Epics. Success is measured by what gets built or proven — infrastructure live, capability demonstrated. Results are always Key Results. They must articulate what Business Epics they unlock; an Enabler Epic that doesn't unblock any named future work shouldn't be in the active queue.

In our system, every Epic has:

- **A type** — `business` or `enabler`
- **An Objective** — one sentence describing what will be different or better when done
- **Business Outcomes or Key Results** — 2–3 measurable results proving the Objective is achieved
- **A Hypothesis** — always for Enabler Epics (technical/architectural); for Business Epics only when at least one BO is defined
- **What This Unlocks** — Enabler Epics only: the Business Epics or capabilities this makes possible
- **Leading Indicators** — early signals that value is emerging (M+ Epics only)
- **A T-shirt size** — rough effort estimate (XS to XL)
- **A WSJF score** — cost of delay divided by job size, used to rank Epics against each other
- **A flow status** — current position in the Portfolio Kanban pipeline

Epics live in `wiki/epics/`. The master ranked list is `wiki/epics/_index.md`.

---

## Portfolio Kanban Flow Status

Every Epic carries a `flow` field in its frontmatter tracking its position in the Portfolio Kanban. The four stages are: Portfolio Backlog → Review → Active → Done.

For the full workflow definition — stage meanings, transition triggers, WIP limits, Jira sync, and SAFe mapping — see [[portfolio-kanban|Portfolio Kanban]].

---

## Lean Epic Model

In standard SAFe, Epics carry a Lean Business Case with business outcomes, leading indicators, an MVP, and cost/timing/risk analysis. Our system adapts this for a solo operator:

- **Business Outcomes or Key Results** replace the SAFe business outcomes section — the choice depends on whether success is measured by an external effect or by completion (see below)
- **Leading Indicators** are captured for M+ Epics only — XS/S Epics complete fast enough that the result is the indicator
- **MVP** is handled as a question during the interview, not a separate field — if an MVP makes sense, it becomes a story under the Epic
- **Lean Business Case** is the WSJF scoring with rationale — Value, Time Criticality, Risk/Opportunity, and Job Size cover the same dimensions (value, timing, cost, risk) without a separate narrative document

The commitment gate (Step 0 of `/epic-planner`) substitutes for the feasibility review step in SAFe's Portfolio Kanban. The Objective forces outcome thinking at the Epic level, which is where it matters most.

---

## The Commitment Gate

*Also documented in [[portfolio-kanban|Portfolio Kanban]] as the `backlog` → `review` transition.*

Before a full Epic interview begins, `/epic-planner` asks two questions:

> "In one sentence each: what's the concrete payoff if this Epic gets done, and what happens if you ignore it for 3 months?"

**What this tests:**
- Is the payoff specific enough to be real? Vague answers ("it would be good") signal the Epic isn't ready.
- Is the 3-month consequence a real cost, or just anxiety? Discomfort is not a consequence.

**If answers are compelling:** proceed with the full interview.

**If answers are vague or the case isn't clear:** park it in `wiki/ai-os/service-design/portfolio-backlog.md` with a structured row rather than forcing a definition that isn't ready. Running `/epic-planner` is a commitment to pursue the Epic — if it's not ready for that commitment, it stays in the ideas pile.

This gate exists because the default ADHD pattern is to plan everything rather than commit to anything. The gate forces the question "is this genuinely worth defining right now?" before investing 30–60 minutes in the interview.

---

## Defining the Objective

The Objective must be **outcome-focused**, not activity-focused. It describes what will be different or better when the Epic is done — not what you'll do.

| Activity-focused (wrong) | Outcome-focused (right) |
|--------------------------|------------------------|
| "Learn more about AI and build some tools" | "Be credibly positioned as an AI-native professional so I'm competitive for senior roles in the next 6 months" |
| "Improve my LinkedIn profile" | "Have a LinkedIn profile that generates inbound enquiries from target companies" |
| "Set up a finance system" | "Never miss a bill, know my net worth at any time, and be on track for savings goals" |

The test: can you imagine being done? Activity-framed objectives have no natural end. Outcome-framed objectives do.

---

## Business Outcomes and Key Results

Every Epic needs 2–3 measurable results that prove the Objective is achieved. The type depends on what the Epic delivers:

> **"Is success measured by an external effect, or by completion of the thing itself?"**

- **External effect** → write **Business Outcomes** — measurable changes in the world
  - "Inbound recruiter messages increase by 2x within 60 days"
  - "Pipeline generates 5 qualified leads per month"
  - "Consulting revenue reaches $X by end of quarter"
- **Completion** → write **Key Results** — binary proof the thing is built and working
  - "AI OS skills documented, mirrored, and passing evals"
  - "Sending domain configured with DKIM/SPF/DMARC passing"
  - "WSJF scoring framework operational and used for 3+ Epics"

An Epic may have a mix of both. Most career and outreach Epics will naturally have Business Outcomes. Most technical and infrastructure Epics will naturally have Key Results.

### Enforced constraints

- **Maximum 3.** More than 3 allows the Epic to expand indefinitely. If a fourth idea feels important, it's either a separate Epic or it's not in the top 3.
- **Binary or measurable.** You should be able to say definitively "done" or "not done" (Key Results), or point to a measurable change (Business Outcomes).
- **Time-boxed or effort-capped.** "Learn Python" fails. "One working Python project in production — by Q3" passes.
- **Outcome over activity.** Watch for verbs like attend, complete, read, take, watch — these describe what you'll do, not what changes. Push back: "What will you be able to do or demonstrate differently as a result?"

### Scope at Epic level

Business Outcomes and Key Results only need to be **specific enough to confirm scope and size the t-shirt**. Implementation detail belongs in stories, not here.

If a result requires significant thought to define, that's a signal the detail belongs in a story. The question to ask: "Will I be able to say 'done' or 'not done' when the time comes?" If yes, it's specific enough. If the answer requires designing the implementation, it's too detailed for Epic level.

This is a deliberate guardrail against perfectionism. At the Epic interview stage, you're making a go/no-go commitment and rough sizing — not specifying the deliverable.

---

## Leading Indicators

*M+ Epics only (a week or more of work). XS/S Epics skip this — they complete fast enough that the result is the indicator.*

Leading Indicators are early signals that value is emerging before the Epic is complete. They allow course-correction mid-flight rather than waiting until all outcomes are delivered to discover the approach was wrong.

The interview question:

> "This Epic will take at least a week. What's the earliest signal — within the first sprint — that your approach is working?"

Examples:
- Epic: "Cold outreach generates qualified leads" → "First 50 emails achieve >5% reply rate within week 1"
- Epic: "AI OS becomes a credible consulting demo" → "First client conversation references the demo unprompted"

Leading Indicators are written to the Epic file. They are not scored or tracked in Jira — they're a reference point for sprint reviews and retrospectives.

---

## T-shirt Sizing

T-shirt sizes are rough effort estimates at Epic level. They inform the WSJF denominator (Job Size) and set timeline expectations. For the full Job Size scoring criteria (including Story sizing), see [[wsjf|WSJF Reference]].

| T-shirt | Job Size | Hours | Duration | Gate |
|---------|----------|-------|----------|------|
| XS | 2 | 5–8h | Up to a day | |
| S | 3 | 9–16h | Up to 2 days | |
| M | 5 | 17–40h | Up to a week | |
| L | 8 | 41–80h | Up to 2 weeks | |
| XL | 13 | 81–160h | Up to a month | Must be split if scope unclear |

Epics start at Job Size 2 — anything under 5h of total effort is a story, not an Epic. These are the same Fibonacci numbers and hour anchors used for Story sizing (see [[wsjf|WSJF Reference]]); the t-shirt labels are an Epic-only convenience. As the portfolio grows, compare against completed Epics rather than estimating hours.

**XL gate:** An XL Epic (81–160h) is up to a month of work. Before committing, confirm: is this worth that commitment, or should it be split into two phased Epics?

### How to estimate Epic size

At Epic level, you are **not** enumerating all user stories. That would defeat the purpose of lightweight Epic planning. Instead:

1. **Analogy** — Compare to similar work you've done before. "This feels like the LinkedIn Enrichment build, which was M. This is bigger, so L."
2. **Major chunk counting** — Identify 3–6 high-level work areas (not stories). Gut-feel each one. Add up.
3. **Uncertainty as a signal** — Foggy scope is usually larger than it appears. If you can't picture the shape of the work, push the size up one band.
4. **Known unknowns** — Each significant unknown tends to add at least S worth of exploration or rework.

Estimation precision should match the planning horizon. At Epic level, ±50% accuracy is acceptable. The t-shirt serves to: catch XL Epics that need splitting, provide a meaningful WSJF denominator, and set rough timeline expectations. If you're spending more than 5 minutes on sizing, you're going too deep — that detail belongs in stories.

**Note:** Epic size = total effort across all stories in the Epic, not the size of any single story. A small Epic (XS) and a medium Story can occupy similar hour ranges — that's expected.

---

## WSJF Scoring at Epic Level

WSJF ranks Epics against each other to decide which initiative to pursue. Formula:

```
Cost of Delay = Value + Time Criticality + Risk/Opportunity
WSJF = Cost of Delay ÷ Job Size
```

All three Cost of Delay components are scored 1/2/3/5/8. Job Size uses the t-shirt number (XS=2, S=3, M=5, L=8, XL=13).

### Scoring criteria

```
Value (what's the payoff?)
  8 — Transformative: directly drives a major outcome (revenue, career trajectory, critical capability)
  5 — Significant: meaningful contribution to a key result; clearly advances the goal
  3 — Moderate: real but indirect benefit; advances the goal but not critically
  2 — Minor: marginal improvement; easily deferred without consequence
  1 — Negligible: maintenance-level; no meaningful impact if never done

Time Criticality (what's the cost of waiting?)
  8 — Window closes: specific near-term deadline; severe concrete consequence if missed this month
  5 — Measurable cost: income delayed, hard dependency blocks others, decision runway shrinks
  3 — Gradual erosion: some cost of delay but no hard deadline; momentum or context fades
  2 — Minor friction: slight preference for sooner, but no real consequence
  1 — Timing irrelevant: same value in 3 months as today

Risk / Opportunity Enablement (what does this unlock?)
  8 — Unblocks an entire epic or 3+ high-value initiatives; eliminates a showstopper risk
  5 — Unblocks 2–3 initiatives or significantly de-risks the portfolio
  3 — Unblocks one initiative or creates some downstream benefit
  2 — Minor downstream benefit; work could mostly proceed without it
  1 — Stands alone — completing it doesn't change much else
```

### Value vs Risk/Opportunity — avoid double-counting

These two components are easy to conflate. The distinction:

- **Value** = what THIS Epic delivers directly (the intrinsic payoff when it's done)
- **RR/OE** = what OTHER things become possible because this exists

**Counter-factual test:** If someone handed you the outcome of this Epic without you having to do the work, would those downstream opportunities still be blocked? If yes — that's RR/OE, not Value. Keep them separate.

*Example — Agile Claw MVP:*
- Value = Agile ICT has a working AI OS, credible consulting offering
- RR/OE = TTI job conversation, gaming company pitch, future clients — all unlocked by having a live demo to show

### Rationale-first scoring

For every component, the scoring sequence is:

1. Ask the scoring question
2. Listen to the user's answer
3. Show reasoning explicitly — which tier applies and why, referencing what the user said
4. Propose the score
5. Ask for confirmation

Never propose a number without first showing the reasoning. The user needs to see the logic to challenge it — and challenging the score is part of the process.

### Anti-mood-bias check (Time Criticality)

When the user expresses urgency through emotional language ("this is stressing me out", "it feels really urgent"), apply the counter-factual check before accepting TC=3:

> "What specifically gets worse in one month if you don't do this — not how it feels, but what actually changes?"

This catches the ADHD pattern of mood-driven prioritisation, where urgency is felt rather than real. A 3 requires a measurable cost: income delayed, market window closing, named opportunity missed.

---

## What Epic-Planner Does and Does Not Do

`/epic-planner` defines the Epic only — Objective, Business Outcomes or Key Results, T-shirt size, and WSJF score. It writes the Epic file to `wiki/epics/` and updates `wiki/epics/_index.md`.

A rough work breakdown is discussed during the interview to help sanity-check the t-shirt size, but this breakdown is informal and not written to the wiki as stories.

`/epic-planner` does **not** create user stories, enablers, or any files in `wiki/stories/`. Those are created by `/define-user-story` or `/define-enabler` when the user is ready to elaborate and execute.

The distinction:
- **User story** (user-facing deliverable) → `/define-user-story`
- **Enabler** (architectural, infrastructure, exploration, compliance) → `/define-enabler`

---

## Why Epics Use a Flat Folder Structure

Epic files live in `wiki/epics/` alongside each other rather than in workstream subfolders. The alternative — nesting project files inside epic subfolders — optimises for browsing the file explorer. The flat structure optimises for the WSJF queue in `wiki/epics/_index.md`, which is the primary planning file. The Epic file already cross-links to its workstream, so grouping is accessible without nesting.

---

## Why a Maximum of Three Business Outcomes / Key Results

Three BOs/KRs is a perfectionism guard. More KRs allow an Epic to expand indefinitely — each new KR becomes a reason to add more work. Three forces identification of the highest-signal outcomes. Any idea that doesn't make the top three is either a separate Epic or not worth the commitment.

KRs must be binary or measurable and time-boxed — vague KRs have no stopping condition and invite endless scope.

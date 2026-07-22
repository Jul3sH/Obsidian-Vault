---
type: reference
created: 2026-06-15
updated: 2026-06-15
---

# Estimation Baseline

> *Estimate vs actuals for every Project, so future sizing is grounded in real history rather than optimism. This is the outside-view check applied to effort. See [[prioritization-framework#Why This Pipeline Exists (the ADHD focus problem)|grounding rationale]].*

## Why this exists

Sizing is the easiest place for storytelling to creep back in: it is tempting to estimate the version of the work you wish were true. The antidote is data. By recording what each Project was estimated at and what it actually took, the estimates get calibrated against reality over time. The unifying test is the same one used everywhere else: a number you never check against the actual is a story, not an estimate.

## Three estimate points per Project

A Project is estimated at three moments in its lifecycle. The gaps between them are the calibration signal.

| Point | When | Captured by | What it tells you |
|-------|------|-------------|-------------------|
| **T-shirt (top-down)** | `review` stage | `/project-planner` Step 1.4 | Gut sizing before breakdown |
| **Scoped (bottom-up)** | as each deliverable is defined (`ready` → `implementing`) | `/define-user-story`, `/define-enabler`, `/define-task` | Running sum of deliverable sizes; grows as the pieces are created |
| **Actual** | `done` | `/retro` at Project close | What it really took |

Two variances matter:
- **Top-down vs Scoped** - was the gut t-shirt right once the work was broken down?
- **Scoped vs Actual** - was the execution estimate right?

## How to use it

- **When sizing a new Project** (`/project-planner` Step 1.4): scan this table for comparable past Projects before committing to a t-shirt size. "The last build-from-blueprint came in at X against an estimate of Y" beats a fresh guess.
- **When defining each deliverable** (`/define-user-story`, `/define-enabler`, `/define-task`): add its hour-equivalent to the parent Project's running **Scoped hrs**. Scope is created at definition time, so the bottom-up estimate accrues here rather than being summed late at sprint planning.
- **When a Project closes** (`/retro`): fill in the Actual column, compute variances, and capture one line of learning.

## Baseline

Hours columns: t-shirt band shows the size's hour range; record actuals as a single number. Variance is computed at close.

| Project | Workstream | T-shirt (est) | Top-down hrs | Scoped hrs | Actual hrs | Variance | Confidence | Notes / learning |
|---------|-----------|---------------|--------------|-----------|-----------|----------|------------|------------------|
| [[../../projects/tti-role\|TTI Role]] | Career | S | 9-16 | 20h | TBD | TBD | Medium | 6 queued tasks: Framework Content (5h) + Case Studies (6h) + NotebookLM Practice (4h) + Kari Scenario Prep (2h) + Formal Interview Prep (2h) + Stephan Follow-Up (1h). Scoped hrs (20h) exceeds S band - watch at close. |
| [[../../projects/automated-linkedin-networking\|Automated LinkedIn Networking]] | Career | M | 17-40 | TBD | TBD | TBD | High | Deliberate stretch: recommendation was L (41-80h). Sized M as a forcing function, MVP-first on contact's blueprint. Unknowns: rebuild effort, tooling specifics, personalisation complexity. |
| [[../../projects/genai-sa-market-validation\|GenAI SA: Go/No-Go Validation]] | Career | XS | 5-8 | 6-12 | TBD | TBD | High | Reframed 18 Jun as a go/no-go gate (Output-only, High confidence). Scoped (2 tasks: research size 2 + recruiter validation size 1) slightly exceeds XS top-down band; watch at close. Phase 2 parked in project funnel, activates on a "go" verdict. |
| [[../../projects/uk-relocation-decision\|UK Relocation Decision]] | Personal | S | 9-16 | TBD | TBD | TBD | N/A - Output | Deliberate stretch: recommendation was M (17-40h). Sized S as forcing function - AI (Perplexity) compresses research; judgment-heavy Phase 1 is the overflow risk. First personal/life-decision Project in the baseline. |
| [[../../projects/clsa-second-interview\|CLSA — Second Interview]] | Career | M | 17-40 | 4h | TBD | TBD | Medium | Deliberate 20h forcing-function cap (interview possibly this week); natural estimate was ~22-34h (mid-M). Overflow risk = the story-iteration loop. Scoped: 1h (scope doc) + 3h (ops-risk story) = 4h. **Process-benchmark: `/project-planner` definition run 30 min focused effort, 2026-06-30.** |

## Links

- [[prioritization-framework|Prioritization Framework]] - the grounding rationale and the three-stage pipeline
- [[wsjf|WSJF Reference]] - how Job Size (the t-shirt number) feeds the WSJF score
- [[portfolio-kanban|Portfolio Kanban]] - the stages where each estimate point is captured

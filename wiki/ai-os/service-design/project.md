---
type: reference
created: 2026-05-14
updated: 2026-06-09
---

# Projects — Reference Guide

**Open this when you want to understand how Projects work: what they are, why they're structured this way, how to define them, and how to score them.** This covers Project creation, WSJF scoring at the Project level, and the rationale behind every design decision.

For the skill that runs the Project interview, see [[../skills/project-planner/_index|project-planner]].
For the WSJF scoring methodology — formula, components, and rationale — see [[wsjf|WSJF Reference]].
For the full planning hierarchy, see [[project-workflow|Project Workflow]]. For Jira configuration, see [[jira-system-design|Jira System Design]].
For how Projects flow through stages (funnel → ready → implementing → done), see [[portfolio-kanban|Portfolio Kanban]].

> **Jira note:** Jira issue types are not renamed. wiki "Project" = Jira "Epic" issue type. The vocabulary is decoupled at the wiki boundary.

---

## What is a Project?

A Project is a strategic initiative — a unit of work large enough to require planning and prioritisation, but focused enough to have a clear outcome and stopping point. Every Project follows the same structure, whether it delivers value directly (to the market, clients, or income) or builds the runway that future Projects depend on. The distinction lives at the result level, not the Project level — see [[#Outcomes and Outputs]] below.

In our system, every Project has:

- **An Objective** — one sentence describing what will be different or better when done
- **2–3 Results proving the Objective is achieved** — each one individually typed as either an **Outcome** (external effect) or an **Output** (completion); see [[#Outcomes and Outputs]]
- **A Hypothesis** — present only if at least one Outcome is defined; omitted for Output-only Projects
- **What This Unlocks** — optional: any other Projects or capabilities this makes possible, where applicable
- **Leading Indicators** — early signals that value is emerging (M+ Projects only)
- **A Scope section** — the build-first/MVP slice, any explicit out-of-scope themes, and the informal work breakdown whose rows become deliverables. This is where scoping lives; deliverables are elaborated from it rather than re-scoped
- **A T-shirt size** — rough effort estimate (XS to XL)
- **A WSJF score** — cost of delay divided by job size, used to rank Projects against each other
- **A flow status** — current position in the Portfolio Kanban pipeline

Projects live in `wiki/projects/`. The master ranked list is `wiki/projects/_index.md`.

---

## Portfolio Kanban Flow Status

Every Project carries a `flow` field in its frontmatter tracking its position in the Portfolio Kanban. The four stages are: Funnel → Ready → Implementing → Done.

For the full workflow definition — stage meanings, transition triggers, WIP limits, Jira sync, and SAFe mapping — see [[portfolio-kanban|Portfolio Kanban]].

---

## Lean Project Model

In standard SAFe, the equivalent construct carries a Lean Business Case with business outcomes, leading indicators, an MVP, and cost/timing/risk analysis. Our system adapts this for a solo operator:

- **Outcomes or Outputs** replace the SAFe business outcomes section — the choice depends on whether success is measured by an external effect or by completion (see below)
- **Leading Indicators** are captured for M+ Projects only — XS/S Projects complete fast enough that the result is the indicator
- **MVP** is captured during the interview and recorded as the "Build first" line of the Project's `## Scope` section — if an MVP makes sense, that slice becomes the first deliverable under the Project
- **Lean Business Case** is the WSJF scoring with rationale — Value, Time Criticality, Risk/Opportunity, and Job Size cover the same dimensions (value, timing, cost, risk) without a separate narrative document

The commitment gate (Step 0 of `/project-planner`) substitutes for the feasibility review step in SAFe's Portfolio Kanban. The Objective forces outcome thinking at the Project level, which is where it matters most.

---

## The Commitment Gate

*Also documented in [[portfolio-kanban|Portfolio Kanban]] as the `funnel` → `ready` transition.*

Before a full Project interview begins, `/project-planner` asks two questions:

> "In one sentence each: what's the concrete payoff if this Project gets done, and what happens if you ignore it for 3 months?"

**What this tests:**
- Is the payoff specific enough to be real? Vague answers ("it would be good") signal the Project isn't ready.
- Is the 3-month consequence a real cost, or just anxiety? Discomfort is not a consequence.

**If answers are compelling:** proceed with the full interview.

**If answers are vague or the case isn't clear:** park it in `wiki/ai-os/service-design/portfolio-backlog.md` with a structured row rather than forcing a definition that isn't ready. Running `/project-planner` is a commitment to pursue the Project — if it's not ready for that commitment, it stays in the ideas pile.

This gate exists because the default ADHD pattern is to plan everything rather than commit to anything. The gate forces the question "is this genuinely worth defining right now?" before investing 30–60 minutes in the interview.

---

## Defining the Objective

The Objective must be **outcome-focused**, not activity-focused. It describes what will be different or better when the Project is done — not what you'll do.

| Activity-focused (wrong) | Outcome-focused (right) |
|--------------------------|------------------------|
| "Learn more about AI and build some tools" | "Be credibly positioned as an AI-native professional so I'm competitive for senior roles in the next 6 months" |
| "Improve my LinkedIn profile" | "Have a LinkedIn profile that generates inbound enquiries from target companies" |
| "Set up a finance system" | "Never miss a bill, know my net worth at any time, and be on track for savings goals" |

The test: can you imagine being done? Activity-framed objectives have no natural end. Outcome-framed objectives do.

---

## Outcomes and Outputs

Every Project needs 2–3 measurable results that prove the Objective is achieved. Each result is independently one of two flavours, decided result-by-result rather than for the Project as a whole:

> **"Is success measured by an external effect, or by completion of the thing itself?"**

- **External effect** → write an **Outcome** — a measurable change in the world
  - "Inbound recruiter messages increase by 2x within 60 days"
  - "Pipeline generates 5 qualified leads per month"
  - "Consulting revenue reaches $X by end of quarter"
- **Completion** → write an **Output** — binary proof the thing is built and working
  - "AI OS skills documented, mirrored, and passing evals"
  - "Sending domain configured with DKIM/SPF/DMARC passing"
  - "WSJF scoring framework operational and used for 3+ Projects"

A Project may have a mix of both. Most career and outreach Projects will naturally have Outcomes. Most technical and infrastructure Projects will naturally have Outputs.

### Why "Outcome / Output" rather than "Business Outcome / Key Result"

This split is not bespoke — it's the standard distinction used in benefits-realisation and OKR-coaching literature (e.g. the output → outcome → impact chain in the UK Treasury Green Book, and the output-based vs outcome-based Key Result distinction made by OKR coaches such as Felipe Castro). "Output" = something produced or completed; "Outcome" = the change in the world that output causes.

The labels were renamed from "Business Outcome" / "Key Result" to remove a naming collision with the [[workstream-framework|goals/OKR layer]]. There, "Key Result" is the name of the OKR item itself (an Objective has 2-3 Key Results), and each of *those* Key Results is independently typed using this same Outcome/Output test. Calling the Project-level completion-type result a "Key Result" made "KR" mean two different things depending on which layer you were reading — Outcome/Output is unambiguous at both.

### Enforced constraints

- **Maximum 3.** More than 3 allows the Project to expand indefinitely. If a fourth idea feels important, it's either a separate Project or it's not in the top 3.
- **Binary or measurable.** You should be able to say definitively "done" or "not done" (Outputs), or point to a measurable change (Outcomes).
- **Time-boxed or effort-capped.** "Learn Python" fails. "One working Python project in production — by Q3" passes.
- **Outcome over activity.** Watch for verbs like attend, complete, read, take, watch — these describe what you'll do, not what changes. Push back: "What will you be able to do or demonstrate differently as a result?"

### Scope at Project level

Outcomes and Outputs only need to be **specific enough to confirm scope and size the t-shirt**. Implementation detail belongs in deliverables, not here.

If a result requires significant thought to define, that's a signal the detail belongs in a deliverable. The question to ask: "Will I be able to say 'done' or 'not done' when the time comes?" If yes, it's specific enough. If the answer requires designing the implementation, it's too detailed for Project level.

This is a deliberate guardrail against perfectionism. At the Project interview stage, you're making a go/no-go commitment and rough sizing — not specifying the deliverable.

---

## Leading Indicators

*M+ Projects only (a week or more of work). XS/S Projects skip this — they complete fast enough that the result is the indicator.*

Leading Indicators are early signals that value is emerging before the Project is complete. They allow course-correction mid-flight rather than waiting until all outcomes are delivered to discover the approach was wrong.

The interview question:

> "This Project will take at least a week. What's the earliest signal — within the first timebox — that your approach is working?"

Examples:
- Project: "Cold outreach generates qualified leads" → "First 50 emails achieve >5% reply rate within week 1"
- Project: "AI OS becomes a credible consulting demo" → "First client conversation references the demo unprompted"

Leading Indicators are written to the Project file. They are not scored or tracked in Jira — they're a reference point for timebox reviews and retrospectives.

---

## T-shirt Sizing

T-shirt sizes are rough effort estimates at Project level. They inform the WSJF denominator (Job Size) and set timeline expectations. For the full Job Size scoring criteria (including Deliverable sizing), see [[wsjf|WSJF Reference]].

| T-shirt | Job Size | Hours | Duration | Gate |
|---------|----------|-------|----------|------|
| XXS | 1 | 1–4h | Up to half a day | |
| XS | 2 | 5–8h | Up to a day | |
| S | 3 | 9–16h | Up to 2 days | |
| M | 5 | 17–40h | Up to a week | |
| L | 8 | 41–80h | Up to 2 weeks | |
| XL | 13 | 81–160h | Up to a month | Must be split if scope unclear |

One consistent Fibonacci scale (1/2/3/5/8/13 → XXS/XS/S/M/L/XL) runs across Projects, stories, tasks, and enablers — the same number means the same effort regardless of artefact type. In practice XXS Projects are rare: work under ~5h of total effort is usually a single deliverable, not a Project. The label exists so the scale is complete and consistent. As the portfolio grows, compare against completed Projects rather than estimating hours.

**XL gate:** An XL Project (81–160h) is up to a month of work. Before committing, confirm: is this worth that commitment, or should it be split into two phased Projects?

### How to estimate Project size

At Project level, you are **not** enumerating all deliverables. That would defeat the purpose of lightweight Project planning. Instead:

1. **Analogy** — Compare to similar work you've done before. "This feels like the LinkedIn Enrichment build, which was M. This is bigger, so L."
2. **Major chunk counting** — Identify 3–6 high-level work areas (not deliverables). Gut-feel each one. Add up.
3. **Uncertainty as a signal** — Foggy scope is usually larger than it appears. If you can't picture the shape of the work, push the size up one band.
4. **Known unknowns** — Each significant unknown tends to add at least S worth of exploration or rework.

Estimation precision should match the planning horizon. At Project level, ±50% accuracy is acceptable. The t-shirt serves to: catch XL Projects that need splitting, provide a meaningful WSJF denominator, and set rough timeline expectations. If you're spending more than 5 minutes on sizing, you're going too deep — that detail belongs in deliverables.

**Note:** Project size = total effort across all deliverables in the Project, not the size of any single deliverable. A small Project (XS) and a medium Deliverable can occupy similar hour ranges — that's expected.

---

## WSJF Scoring at Project Level

WSJF ranks Projects against each other to decide which initiative to pursue. Formula:

```
Cost of Delay = Value + Time Criticality + Risk/Opportunity
WSJF = Cost of Delay ÷ Job Size
```

All three Cost of Delay components are scored 1/2/3/5/8. Job Size uses the t-shirt number (XS=2, S=3, M=5, L=8, XL=13).

### Scoring criteria

```
Value (what's the payoff?)
  8 — Transformative: directly drives a major outcome (revenue, career trajectory, critical capability)
  5 — Significant: meaningful contribution to one of the Project's results; clearly advances the goal
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
  8 — Unblocks an entire project or 3+ high-value initiatives; eliminates a showstopper risk
  5 — Unblocks 2–3 initiatives or significantly de-risks the portfolio
  3 — Unblocks one initiative or creates some downstream benefit
  2 — Minor downstream benefit; work could mostly proceed without it
  1 — Stands alone — completing it doesn't change much else
```

### Value vs Risk/Opportunity — avoid double-counting

These two components are easy to conflate. The distinction:

- **Value** = what THIS Project delivers directly (the intrinsic payoff when it's done)
- **RR/OE** = what OTHER things become possible because this exists

**Counter-factual test:** If someone handed you the outcome of this Project without you having to do the work, would those downstream opportunities still be blocked? If yes — that's RR/OE, not Value. Keep them separate.

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

## What Project-Planner Does and Does Not Do

`/project-planner` defines the Project only — Objective, Outcomes or Outputs, T-shirt size, and WSJF score. It writes the Project file to `wiki/projects/` and updates `wiki/projects/_index.md`.

A work breakdown is discussed during the interview to help sanity-check the t-shirt size, and it is written into the Project file's `## Scope` section (alongside the build-first/MVP slice and any explicit out-of-scope themes). It is informal and not individually scored — each row is a candidate deliverable, subject to change when elaborated. Scoping is a Project-level act: deliverables are elaborated from the Scope section, not re-scoped from scratch.

`/project-planner` does **not** create deliverable *files* in `wiki/deliverables/`. Those are created by `/define-user-story`, `/define-enabler`, or `/define-task` when the user is ready to elaborate and execute — each one elaborated from a row in the Project's Scope section.

The distinction:
- **User-facing deliverable** → `/define-user-story`
- **Enabler** (architectural, infrastructure, exploration, compliance) → `/define-enabler`

---

## Why Projects Use a Flat Folder Structure

Project files live in `wiki/projects/` alongside each other rather than in workstream subfolders. The alternative — nesting deliverable files inside project subfolders — optimises for browsing the file explorer. The flat structure optimises for the WSJF queue in `wiki/projects/_index.md`, which is the primary planning file. The Project file already cross-links to its workstream, so grouping is accessible without nesting.

---

## Why a Maximum of Three Outcomes / Outputs

Three results is a perfectionism guard. More results allow a Project to expand indefinitely — each new one becomes a reason to add more work. Three forces identification of the highest-signal results. Any idea that doesn't make the top three is either a separate Project or not worth the commitment.

Each Outcome or Output must be binary or measurable and time-boxed — vague results have no stopping condition and invite endless scope.

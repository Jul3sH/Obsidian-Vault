---
type: reference
created: 2026-05-21
updated: 2026-06-08
---

# Workstream Framework — Reference Guide

**Open this when you want to understand what workstreams are, how they are structured, and how vision, values, ambitions, directions, and goals connect to Projects.**

For how Projects flow through the system, see [[portfolio-kanban|Portfolio Kanban]].
For Project definition and WSJF scoring, see [[project|Project Reference]].
For the full planning hierarchy, see [[project-workflow|Project Workflow]].

---

## What is a Workstream?

A workstream is a persistent life domain — a standing area of focus that never completes, only evolves. Workstreams are the top-level organising principle of the entire planning hierarchy. Every goal, Project, deliverable, and timebox story belongs to exactly one workstream.

They exist so that:
- **Nothing gets lost.** Any idea or initiative has a natural home.
- **Balance is visible.** You can see at a glance which life areas are getting investment and which are being neglected.
- **Goals stay grounded.** Projects trace to workstream goals; goals don't float without context.

---

## The Six Workstreams

Six workstreams, ranked in descending priority. When goals or time compete, higher layers win.

| # | Workstream | Domain | Framework | Priority Rationale |
|---|-----------|--------|-----------|-------------------|
| 1 | **Wellbeing** | Sleep, energy, alcohol, physical and mental health, personal state management | SMART | The foundation. If health fails, nothing else can be delivered. Catastrophic to neglect — it sits first not because it is the most enjoyable to work on, but because it is the most consequential to ignore. |
| 2 | **Relationships** | Partner, family, social dynamics, and interpersonal patterns outside of work | SMART | Ultimate purpose. Sophia above all else, then Mum, then a life partner. Relationships are what actually produce happiness. Historically neglected; the priority placement is partly a deliberate correction. |
| 3 | **Finance** | Personal finances: budgeting, savings, investments, and financial planning | SMART | The means, not the end. Money exists to support Wellbeing and Relationships. Instrumentally important but not intrinsically as important as being well or connected. |
| 4 | **Career** | Professional progression, job search, workplace politics, personal brand, client relationships, and career strategy | OKR | Exists to fund Finance. Career choices should increasingly reflect what is needed, not just what maximises income. |
| 5 | **Performance** | Personal effectiveness, productivity, self-management, learning, and working with others | OKR | Your ability to perform well across all the layers above. Goals here should be laser-focused on improving capability where it serves the layers above. Not a hobby layer. |
| 6 | **Personal** | Hobbies, enjoyment, life goals, and things personally wanted from life | SMART | The foundation of a balanced life. Having things to enjoy makes you more likely to perform well in everything above it. Last in priority, not in importance. |

### The support structure

```
Wellbeing      ← sustained by Relationships
Relationships  ← enabled by Finance
Finance        ← produced by Career
Career         ← sharpened by Performance
Performance    ← balanced and sustained by Personal
```

Each layer feeds the one above it. Personal is the base: a life with hobbies, interests, and enjoyment produces the balance and resilience that Performance runs on. Career produces the income Finance needs. Finance enables the stability that Relationships depend on. Relationships sustain the mental and physical state that is Wellbeing.

**Scheduling rule:** when prioritising work across workstreams, a Wellbeing goal outranks a Career goal; a Relationships goal outranks a Finance goal; and so on. See [[prioritization-framework]] for how this hierarchy applies to sprint and weekly scheduling.

---

## Filing Rules

**One workstream per item.** If a deliverable or Project genuinely spans two workstreams, choose the primary one — the domain where the outcome lives, not where the work happens.

**Common edge cases:**

| Situation | Rule |
|-----------|------|
| Learning a skill (e.g. Python, Excel modelling) | **Performance** — capability development, regardless of which domain the skill applies to |
| A tool or system you're building for work | **Career** if it advances your professional position; **Performance** if it makes you more effective across all domains |
| A financial skill (e.g. reading investment reports) | **Performance** — learning belongs in Performance; the outcome (the investment) belongs in Finance |
| Health habit tied to work output (e.g. sleep for focus) | **Wellbeing** — the domain of the practice, not the downstream beneficiary |
| Consulting work or side income | **Career** — income generation is always Career, even if it's project-based |

---

## Workstream ↔ Wiki Index

Each workstream has its own wiki index and workstream file:

| Workstream | Wiki path | Workstream file |
|-----------|----------|----------------|
| Career | `wiki/career/` | [[career-workstream|Career Workstream]] |
| Finance | `wiki/finance/` | [[finance-workstream|Finance Workstream]] |
| Performance | `wiki/performance/` | [[performance-workstream|Performance Workstream]] |
| Personal | `wiki/personal/` | [[personal-workstream|Personal Workstream]] |
| Relationships | `wiki/relationships/` | [[relationships-workstream|Relationships Workstream]] |
| Wellbeing | `wiki/wellbeing/` | [[wellbeing-workstream|Wellbeing Workstream]] |

Skills and AI tooling are **not** filed in workstream indexes — they always live in `wiki/ai-os/skills/`. Workstream indexes cross-link to relevant skills but do not host them.

---

## Workstream Structure

Every workstream file follows the same cascade. Principles and Values form the foundation and apply at every level — they do not flow into the layers below so much as constrain and inform all of them.

```
Principles               (hard rules — must always adhere; override goals and decisions)
Values                   (directional guides — should always align; inform every layer)
Vision                   (aspirational future state — the life you want)
     ↓
10-year Ambitions        (directional, loosely measurable — where I want to be by 2036)
     ↓
5-year Directions        (more grounded — where I want to be by 2031; not strictly measured)
     ↓
Annual OKRs / SMART      (measurable, time-bound targets — current 12-month layer)
     ↓
Projects                 (initiative level — WSJF ranked)
     ↓
User Stories & Enablers
     ↓
Timebox
```

### The Layers

| Layer | What it is | Time horizon | How to use it |
|-------|-----------|-------------|--------------|
| **Principles** | Hard rules you will not break — override everything | Enduring | Go/no-go gate: does this action violate a principle? |
| **Values** | What you care about — directional guides that inform decisions | Enduring | Direction check: does this align with what matters to me? |
| **Vision** | Aspirational future state — the life you want | Enduring | Orientation: am I still heading in the right direction? |
| **10-year Ambitions** | High-level directional aspirations — loosely measurable | ~10 years | Sanity check: does this 5-year direction move me toward the ambition? |
| **5-year Directions** | More grounded directional goals — aligned to 10-year | ~5 years | Sanity check: does this annual goal advance a direction? |
| **Annual OKRs / SMART Goals** | Measurable, time-bound targets that prove progress | 12 months / quarterly KRs | Execution: what am I committing to this year? |

---

## Traceability Principle

**Every layer must trace to the layer above it. Values drive Ambitions. Ambitions drive Directions. Directions drive Goals. Goals drive Projects. And nothing — at any level — may violate a Principle.**

This is the single most important structural rule. If any item in the hierarchy cannot be traced back to a value, it should be questioned. If any action violates a principle, it is a hard stop.

### Alarm bell rule

Raise an alarm bell (flag explicitly, do not silently accept) if:
- Any action, goal, or decision violates a Principle — this is a hard stop, not a judgment call
- A 10-year Ambition cannot be connected to at least one Value
- A 5-year Direction cannot be connected to at least one 10-year Ambition
- An annual goal or KR cannot be connected to at least one 5-year Direction
- A Project cannot be connected to at least one annual goal or KR

If the gap is intentional (opportunistic work, time-sensitive exception), label it **"Opportunistic"** and document the justification. Misalignment is not automatically wrong — but it must be conscious and named, never invisible.

### Traceability in practice

When creating or reviewing any item, ask in order:
1. *Does this violate any Principle?* (If yes — stop.)
2. *What value does this serve?* (If none — question it.)
3. *Which ambition does this move me toward?*
4. *Which direction does this advance?*

If you cannot answer questions 3 and 4, the item either belongs somewhere else or should not exist.

---

## Workstreams in Practice

**In workstream files:** Each workstream has a dedicated file (e.g. `career-workstream.md`) containing its vision, values, ambitions, directions, and annual goals. The framework (SMART or OKR) is determined by the workstream.

**In Projects:** Every Project has a `workstream:` frontmatter field. The Project's WSJF scoring is done in the context of that workstream's goals — does this Project serve a current objective?

**In deliverables:** Every story and enabler inherits its workstream from its parent Project. Standalone deliverables (no Project) must explicitly declare a workstream.

**In planning:** Workstream is a label in Jira, allowing you to filter the sprint board by life domain if needed.

---

## The SMART / OKR Split

| Workstream | Framework | Rationale |
|-----------|-----------|-----------|
| Wellbeing | SMART Goals | Life management — clear, specific, measurable targets |
| Relationships | SMART Goals | Life management — clear, specific, measurable targets |
| Finance | SMART Goals | Life management — clear, specific, measurable targets |
| Personal | SMART Goals | Life management — clear, specific, measurable targets |
| Career | OKRs | Strategic and developmental — linked to portfolio management |
| Performance | OKRs | Strategic and developmental — linked to portfolio management |

**Why the split?**

SMART goals work best for domains where success is a specific, bounded outcome: save a target amount, maintain a habit, complete a defined milestone. These are the life management workstreams.

OKRs work best for domains where progress is strategic, developmental, and linked to larger initiatives. Career and Performance are professional growth workstreams where the objective provides aspirational direction and key results measure progress toward it. This also supports practising Lean Portfolio Management thinking — framing work around strategic outcomes rather than isolated tasks.

**The connection:** OKR Key Results and SMART goals are closely aligned — both are measurable and time-bound. The difference is that OKR Key Results sit under an Objective (which serves as the directional layer for Career and Performance), while SMART goals sit directly under the annual layer for life management workstreams. All workstreams share the same Vision, Values, and longer-horizon layers — the SMART/OKR split applies only at the 12-month measurement layer.

---

## Vision

Every workstream has a Vision statement — an aspirational future state describing the life you want. Visions are enduring; they only change when your fundamental direction changes.

**File format:** a blockquote at the top of each workstream file, below the heading.

---

## Principles (all workstreams)

Used for: **all six workstreams.**

Principles are hard rules you will not break under any circumstances. They override goals, decisions, and even other values. The test: if breaking this rule would cause lasting harm, regret, or would fundamentally compromise who you are — it is a principle.

**In practice:** when evaluating any decision or opportunity, run two checks in order:
- **Principles first — "Am I allowed to proceed?"** If an action violates a principle, stop. This is a hard gate, not a judgment call. Principles exist specifically to protect against emotional override — the moment when you want something badly enough to rationalise past your own rules.
- **Values second — "Do I want this?"** If the action passes the principles gate, check whether it aligns with what you care about. This is directional, not binary.

**Distinction from Values:**
- A Principle is binary — you either adhere to it or you don't. There is no "mostly" or "in context". Example: "Protect the Floor" — you will never drop below your current financial position, full stop.
- A Value is directional — it shapes your preferences and informs decisions but has some context-sensitivity. Example: "Enjoyment" — you value having fun, but may trade it temporarily for a higher goal.

**Guard rails:**
- Keep them genuinely non-negotiable — if you can imagine a circumstance where breaking it is acceptable, it is a value not a principle
- Fewer is better; a long list of "principles" signals they are not all truly hard constraints
- Principles almost never change

---

## Values (all workstreams)

Used for: **all six workstreams.**

Values are what you care about — directional guides that shape decisions and inform every layer of the hierarchy. They are not hard rules (those are Principles) and not time-bound targets (those are Goals). They define what matters to you and how you want to live.

**Distinction from Principles:**
- A Value guides direction — "I tend toward X because I care about Y"
- A Principle governs behaviour — "I will not do X, regardless of the circumstances"

**Guard rails:**
- Keep them genuinely about what you care about — if it has a date or a measure, it belongs in a goal layer
- 3–5 per workstream is typical; fewer is fine if they are strong
- If you are updating values frequently, they may be goals in disguise

---

## SMART Goals

Used for: **wellbeing, relationships, finance, personal.**

A SMART goal is a single statement that is inherently Specific, Measurable, Achievable, Relevant, and Time-bound. No need to break out S/M/A/R/T as separate fields — the goal statement itself embeds all five criteria.

**Example:** "Save $5,000 in emergency fund by September 30"

**File format:** a single Active Goals table with: Goal, Measure, Target Date, Status, Projects. Completed goals roll down into a Completed section for reference.

**Guard rails:**
- Max 3 active goals per workstream at any time
- Each goal must have a clear measure (binary or quantitative)
- Target date is embedded in the goal statement and shown in its own column
- Not every goal needs a Project — some goals are habits or targets without initiative-level work
- Goals are not restricted to a quarter — they are time-bound by the goal statement itself

---

## OKRs

Used for: **career, performance.**

Based on SAFe's OKR model. Each OKR has an Objective and 2–3 Key Results.

### Objectives

- **Inspirational** — a direction, not a deliverable
- **Clear and memorable** — one sentence you can recall without looking it up
- **Committed or Aspirational** — label which type it is
  - **Committed** — expect 100% achievement; failure means something went wrong
  - **Aspirational** — stretch targets; 70% achievement is a success
- **Horizon — Annual or Quarterly** — label which applies
  - **Annual** — the Objective is a persistent direction for the year; KRs are set each quarter as milestones toward it
  - **Quarterly** — the Objective is specific to this quarter; completing it closes it out

**Why Objectives often span a year:** An Objective is a direction, not a deliverable. If your Objective is something durable like "Build a profitable consulting business," it can remain in place across multiple quarters as long as it still reflects your strategic intent. What changes quarter to quarter are the Key Results — they capture the next measurable outcomes that matter *now*.

**When to change the Objective:** Change it when the *direction itself* changes — not just the measures. Moving from "be profitable" to "scale through productised services" or "build authority in Lean Portfolio Management consulting" justifies a new Objective.

**Practical pattern for a solo operator:** Keep 1–3 stable professional Objectives for a longer horizon (2–4 quarters), and update the KRs every quarter. This gives you continuity at the direction level and agility at the measurement level.

**Doing work vs improving work:** An Objective may be about executing a specific initiative ("doing work") or about improving capability or process ("improving work"). Both are valid.

### Key Results

- **Value-based** — measure value delivered, not activity performed
- **Measurable** — quantitative or binary
- **Gradable** — scored 0.0–1.0 at end of quarter (not just done/not done)
- **Always quarterly** — regardless of the Objective horizon, KRs are scoped to the current quarter
- **Outcome or Output** — each Key Result is labelled by what it measures, using the same test applied to Project results (see [[project#Outcomes and Outputs|Project Reference]]):
  - **Outcome** — measures an external effect; how the world responds. Success depends on others' behaviour (market, clients, employers). Example: "3 interviews reached", "Pipeline generates ≥1 lead per week"
  - **Output** — measures completion; within your control. Binary or quantitative proof something was built or done. Example: "AI OS MVP live and operational", "5 applications submitted"
- **Committed or Aspirational** — each Key Result is labelled individually:
  - **Com(mitted)** — expected 100% achievement this quarter; not hitting it means something went wrong
  - **Asp(irational)** — a stretch target; 70% is a success; valuable if achieved, not a failure if not

**Table column reference:**

| Column | Values | Meaning |
|--------|--------|---------|
| Outcome/Output | `Outcome` or `Output` | Is this Key Result measuring an external effect or a completion? |
| Type | `Com` or `Asp` | Is this Committed (100% expected) or Aspirational (70% is a success)? |
| Score | 0.0–1.0 | Graded at end of quarter |

**Example — stable Objective with rotating quarterly KRs:**

> **O:** Be a profitable AI-native solopreneur running multiple revenue streams *(Aspirational — Annual)*
>
> **Q2 2026 Key Results** *(foundation — identify and test)*
>
> | Key Result | Outcome/Output | Type | Measure | Score | Projects |
> |------------|-----------------|------|---------|-------|-------|
> | KR1: 3 revenue stream opportunities documented with hypothesis and rationale | Output | Com | 3 of 3 documented | 0.0 | — |
> | KR2: Feasibility and viability verdict reached on all 3 — go/no-go documented | Output | Com | 3 of 3 assessed | 0.0 | — |
> | KR3: MVP completed for ≥1 down-selected opportunity — results documented | Output | Asp | ≥1 MVP with outcome | 0.0 | — |
>
> **Q3 2026 Key Results** *(scale — defined at Q3 planning based on Q2 learnings)*

**File format:** Objective at top level; quarterly KR tables nested underneath. Type column in every KR table.

**Guard rails:**
- Max 3 Objectives per workstream active at any time
- Max 3 Key Results per Objective per quarter
- Score all Key Results at end of quarter during retrospective (Committed KRs below 1.0 warrant a retro discussion)
- Annual Objectives carry forward; Quarterly Objectives are closed when complete

**Candidate KRs:** Each workstream file has a **Candidate KRs — Unassigned** section at the bottom — a holding area for KR ideas not yet assigned to a quarter. No limit on entries. At each quarterly planning session, review the list and promote the best 3 per Objective to the relevant quarter's table. SMART workstream files use **Candidate Goals — Unassigned** for the same purpose.

---

## Goals ↔ Projects

Goals and Projects connect in both directions:

- **Goals → Projects:** each workstream file's table has a Projects column linking to the Projects that serve it
- **Projects → Goals:** Project files can reference which goal they contribute to (optional — the workstream file is the primary cross-reference)

Not every goal has Projects (some are habits or targets). Not every Project needs a goal (standalone Projects are valid for opportunistic work). But the default expectation is that active Projects serve a goal.

---

## Quarterly Cadence

- **KRs are always quarterly** — defined at the start of each quarter, scored at the end
- **Objectives may be annual or quarterly** — label the horizon when creating; annual Objectives persist across quarters
- At the start of each quarter: define new KRs under any active annual Objectives, and set any new Objectives
- At the end of each quarter: score all KRs (0.0–1.0 for OKRs; done/not done for SMART goals)
- Past KR tables stay in the file for reference and retro use — do not delete old quarters
- Quarterly review integrates with the retrospective cycle

---

## Links

- [[project-workflow|Project Workflow]] — full planning hierarchy
- [[project|Project Reference]] — how Projects are defined and scored
- [[portfolio-kanban|Portfolio Kanban]] — how Projects flow through stages
- [[wsjf|WSJF Reference]] — Project-level prioritisation methodology
- [[prioritization-framework|Prioritization Framework]] — cross-workstream scheduling rules

---
name: goal-planner
description: >
  Define quarterly goals and write them to the wiki. Use this skill whenever
  the user wants to set goals, define OKRs, or plan a quarter — including at
  the start of each quarter, when reviewing or updating goals, or when the user
  says "define a goal", "set OKRs", "plan my quarter", or "what should I be
  working toward?". Career and Performance workstreams use OKRs; Finance,
  Personal, Relationships, and Wellbeing use SMART Goals.
---

> **Mirror:** source file at `~/.claude/skills/goal-planner/SKILL.md`

You are helping the user define goals and write them to their wiki.
The output goes into `wiki/[workstream]/goals.md`.

OKRs (career and performance) are quarterly-scoped. SMART goals (finance, personal,
relationships, wellbeing) are time-bound by the goal statement itself — not restricted
to a quarter. A SMART goal can have any target date.

The user has ADHD traits and a tendency toward perfectionism and scope creep.
Keep goals focused and bounded. Enforce the max-3 constraint firmly. Push back
on activity-framed goals and vague objectives. Move through the interview
efficiently — the user should feel like they're making decisions, not answering
a questionnaire.

---

## Context

**Framework split:**

| Workstream | Framework | Rationale |
|-----------|-----------|-----------|
| Career | OKRs | Strategic/developmental — linked to portfolio management |
| Performance | OKRs | Strategic/developmental — linked to portfolio management |
| Finance | SMART Goals | Life management — specific, measurable, bounded targets |
| Personal | SMART Goals | Life management — specific, measurable, bounded targets |
| Relationships | SMART Goals | Life management — specific, measurable, bounded targets |
| Wellbeing | SMART Goals | Life management — specific, measurable, bounded targets |

**Planning hierarchy:**
```
SMART Goals / OKRs     (workstream level — quarterly)     ← THIS SKILL
     ↓
Projects                 (initiative level — WSJF ranked)   ← /project-planner
     ↓
User Stories & Enablers                                   ← /define-user-story, /define-enabler
     ↓
Timebox                                                   ← /timebox-plan
```

**Goals write to:** `wiki/[workstream]/goals.md`.

- OKRs: written under the relevant quarter section (KRs always quarterly).
- SMART goals: written to the Active Goals table — no quarter grouping.

**Quarter reference (OKRs only):**
- Q1 2026: Jan–Mar | Q2 2026: Apr–Jun | Q3 2026: Jul–Sep | Q4 2026: Oct–Dec

---

## Step 0 — Setup

### 0.1 — Which workstream?
Ask: "Which workstream is this goal for — career, finance, personal, performance,
relationships, or wellbeing?"

Based on the answer, branch to the correct path:
- **career or performance** → OKR Path (Steps 1A onwards)
- **finance, personal, relationships, or wellbeing** → SMART Path (Steps 1B onwards)

### 0.2 — Which quarter? (OKR workstreams only)
For career or performance: ask "Are we setting goals for Q2 2026 (current) or
Q3 2026 (next quarter)?"

Default: Q2 2026 (Apr–Jun) if mid-quarter. Skip this step for SMART workstreams.

### 0.3 — Check existing goals
Read `wiki/[workstream]/goals.md`.

- **OKR workstreams:** count existing Objectives for the target quarter. If 3
  already exist, say: "You already have 3 Objectives for [quarter] — that's the
  maximum. Should we update one instead?" and show them.
- **SMART workstreams:** count rows in the Active Goals table. If 3 already
  exist, say: "You already have 3 active goals — that's the maximum. Should we
  complete or remove one first?"

If under the limit, continue silently.

---

## OKR PATH (Career, Performance)

### Step 1A — Define the Objective

#### 1A.1 — Objective Statement
Ask: "In one sentence, what's the Objective? It should be inspirational and
memorable — a direction, not a deliverable."

A good Objective is:
- **Inspirational** — motivating, not administrative
- **Clear and memorable** — you can recall it without looking it up
- **Directional** — where you're heading, not what you'll produce

Push back if:
- **Activity-framed:** "Complete the AI course" → that's a Key Result, not an
  Objective. Reframe: "Be a credible AI practitioner that clients trust"
- **Too vague:** "Get better at my job" → at what? In what way?
- **Deliverable-shaped:** "Launch the cold outreach system" → more like a KR.
  Ask: "What does launching that make possible? What's the bigger outcome?"

#### 1A.2 — Committed or Aspirational?
Ask: "Is this Committed or Aspirational?"
- **Committed** — you expect 100% achievement. Failure means something went wrong.
- **Aspirational** — a stretch target. 70% achievement is a success.

If unsure: "Aspirational objectives feel ambitious enough that you're not certain
you'll fully achieve them. Committed objectives feel firmly within your control.
Which feels right for this one?"

#### 1A.3 — Objective Horizon: Annual or Quarterly?
Ask: "Is this Objective specific to this quarter, or is it a longer-term direction
you'll pursue across multiple quarters?"

- **Annual** — a persistent direction for the year. The Objective stays in the file;
  KRs are defined each quarter as milestones toward it. Most aspirational Objectives
  are annual.
- **Quarterly** — specific to this quarter. When the KRs are achieved (or the quarter
  ends), the Objective is closed out.

Note the horizon — it affects how the file is written and how the Objective is labelled.

#### 1A.4 — Doing or Improving?
Note the type internally (no need to ask explicitly unless unclear):
- **Doing work** — executing a specific initiative
- **Improving work** — building capability or changing how you operate

---

### Step 2A — Define Key Results (2–3)

Work through Key Results one at a time. After each one, ask if there are more
(up to 3). Never allow more than 3.

For each Key Result, ask three things in sequence:

**First:** "What's a Key Result that would prove this Objective is being achieved?
It should measure value delivered, not activity performed."

**Then:** Confirm whether it's a BO or KR — the user may name it, or you classify it:
- **BO (Business Outcome)** — measures an external effect; how the world responds.
  Success depends on others' behaviour (market, clients, employers).
  Example: "Pipeline generates ≥1 qualified lead per week"
- **KR (Key Result)** — measures completion; within your control.
  Binary or quantitative proof something was built or done.
  Example: "AI OS MVP platform live and operational"

Tell the user which it sounds like and ask them to confirm: "That sounds like a [BO/KR]
— it's measuring [an external effect / something within your control]. Does that feel right?"

**Then:** "Is this Committed or Aspirational?"
- **Com(mitted)** — expected 100% this quarter; not hitting it means something went wrong
- **Asp(irational)** — a stretch; 70% is a success; valuable if achieved, not a failure if not

An Objective can have a mix — some KRs are non-negotiable, others are stretch goals.

**Enforce:**
- **Value-based, not activity-based.** Watch for these activity signals:
  - ❌ "Complete [course]" → ✅ "Can demonstrate [capability] in client context"
  - ❌ "Attend [event]" → ✅ "Generate [X] qualified leads from event connections"
  - ❌ "Build [tool]" → ✅ "[Tool] is live and [measurable outcome]"
  - Exception: passing a certification exam or completing a specific programme
    is valid as a KR if the completion itself is the meaningful milestone.
- **Measurable.** Quantitative (number, percentage, frequency) or binary
  (exists/doesn't exist, happens/doesn't happen).
- **Gradable 0.0–1.0.** The user should be able to say "we achieved 0.7 of
  this" at end of quarter, not just yes/no.
  - Quantitative KRs are naturally gradable (achieved 3 of 5 target = 0.6)
  - Binary KRs grade as 0.0 or 1.0 — these are fine if the distinction is
    genuinely binary, but flag them: "This will score 0.0 or 1.0 — is there
    a way to make it more gradable, or is it genuinely all-or-nothing?"
- **Max 3.** At 3, stop: "That's the maximum for one Objective. Any more would
  dilute focus. Are these the right 3?"

**After all KRs are defined:**
Ask: "Do any of these Key Results map to existing Projects in your queue?"
Read `wiki/projects/_index.md` and suggest matches if obvious. The user may say
"none yet" — that's fine. Leave the Projects column blank.

---

### Step 3A — Confirm and Write (OKR)

Summarise the full OKR before writing:

```
Workstream: [career/performance]
Quarter: [Q2/Q3 2026] (KRs scoped to this quarter)
Type: OKR

Objective: [statement] (Committed / Aspirational — Annual / Quarterly)

Key Results:
  KR1: [statement] | Measure: [how it's measured]
  KR2: [statement] | Measure: [how it's measured]
  KR3: [statement] | Measure: [if applicable]

Project links: [slugs or "none yet"]
```

Ask: "Does this look right before I write it?"

**Write to `wiki/[workstream]/goals.md`:**

**Annual Objectives** — the Objective sits at the top level; KRs are nested under
the relevant quarter. If the Objective is new, append it after any existing Objectives.
If it already exists (from a prior quarter), find it and add the new quarter's KR
table under it.

```markdown
## Objective [N]: [Short title] *(Aspirational / Committed — Annual)*

> *[Objective statement]*

### [Q2 2026] Key Results

| Key Result | BO/KR | Type | Measure | Score | Projects |
|------------|-------|------|---------|-------|-------|
| KR1: [statement] | KR | Com | [how measured] | 0.0 | [project links or —] |
| KR2: [statement] | BO | Com | [how measured] | 0.0 | [project links or —] |
| KR3: [statement] | KR | Asp | [how measured] | 0.0 | [project links or —] |
```

**Quarterly Objectives** — the Objective sits under the quarter heading, same as before:

```markdown
## [Q2 2026]

### Objective [N]: [Short title] *(Aspirational / Committed — Q2 2026)*

> *[Objective statement]*

| Key Result | BO/KR | Type | Measure | Score | Projects |
|------------|-------|------|---------|-------|-------|
| KR1: [statement] | KR | Com | [how measured] | 0.0 | [project links or —] |
```

Remove any placeholder text (e.g. "*To be defined at quarterly planning.*") for the
quarter being written. Do NOT overwrite previously defined Objectives or KR tables.

---

## SMART PATH (Finance, Personal, Relationships, Wellbeing)

### Step 1B — Define the Goal

Ask: "In one sentence, what's the goal? It should be specific, measurable,
achievable, relevant, and time-bound — all in the statement itself."

**Examples of good SMART goals:**
- "Save $5,000 in emergency fund by 30 June"
- "Run 3x per week, every week until end of year"
- "Call mum at least 5 days per week throughout 2026"
- "Complete DB 10K in under 45 minutes on 26 November"

SMART goals are not restricted to a quarter — they are time-bound by the
goal statement itself. The target date can be any date.

Push back if:
- **Vague:** "Get fitter" → fitter how? By when? What's the measure?
- **Open-ended:** "Save more money" → how much? By when?
- **No time bound:** "Learn to cook" → what does 'done' look like, and by when?
- **Not achievable:** "Run a marathon next month" starting from scratch →
  is this realistic?

If the user's statement is close but missing one SMART element, help them
sharpen it rather than rejecting it outright: "Almost — you've got the what
and why, but what's the measure or deadline?"

### Step 2B — Confirm the Measure
Ask: "How will you know this goal is done? What's the specific measure?"

This is often already embedded in the goal statement. If it is, just confirm
it rather than asking again. Only ask explicitly if the measure is unclear.

- **Quantitative measure:** a number, frequency, amount, or percentage
- **Binary measure:** a clear yes/no state (e.g., "account exists and is funded")

### Step 3B — Link to Projects (optional)
Ask: "Does this goal connect to any active Projects, or is it a habit/target
without initiative-level work?"

Read `wiki/projects/_index.md` if they want to link. Leave blank if standalone.

---

### Step 4B — Confirm and Write (SMART)

Confirm before writing:

```
Workstream: [workstream]
Type: SMART Goal

Goal: [statement]
Measure: [how measured]
Target Date: [date]
Project links: [slugs or "none"]
```

Ask: "Does this look right?"

**Write to `wiki/[workstream]/goals.md`:**

Add a row to the Active Goals table:

```markdown
| [N] | [Goal statement] | [Measure] | [Target Date] | in progress | [Project links or —] |
```

---

## Step 5 — Next Steps (both paths)

After writing, tell the user:

**OKR workstreams:**
"OKR added to [workstream] goals for [quarter]. Next steps:"
- **Define another Objective:** run `/goal-planner` again (max 3 per quarter)
- **Create supporting Projects:** run `/project-planner` to define the Projects that
  will drive these Key Results
- **Score at quarter end:** during the retro, update the Score column (0.0–1.0)

**SMART workstreams:**
"Goal added to [workstream]. Next steps:"
- **Define more goals:** run `/goal-planner` again (max 3 active at a time)
- **Create supporting Projects:** if this goal needs initiative-level work, run
  `/project-planner`
- **Mark done when complete:** update Status column to `done` and move row to
  Completed Goals section

---

## Log the operation

Append one row to `wiki/ai-os/logs/log-2026-Q2.md`:

For OKR:
`| [date] | Setup | Defined OKR — [workstream] [quarter]: "[Objective]" ([N] KRs); written to wiki/[workstream]/goals.md. |`

For SMART:
`| [date] | Setup | Defined SMART goal — [workstream]: "[Goal]" (target: [date]); written to wiki/[workstream]/goals.md. |`

---

## Edge Cases

**User wants to update an existing goal mid-quarter:**
- Read the current entry, confirm what's changing, edit in place.
- For OKRs: you may update the Objective statement or Key Results, or update
  the Score column if it's end-of-quarter.
- For SMART: you may update Status or the goal statement if the target has changed.

**User wants to define goals for multiple workstreams at once:**
- Handle one workstream at a time. Complete each one fully before moving to
  the next. Don't batch-estimate or batch-write.

**User proposes a goal that belongs in a different workstream:**
- Redirect: "That sounds like it belongs under [other workstream] rather than
  [this workstream]. Want to file it there?"

**User wants to score OKRs (end of quarter):**
- Read the current goals.md, walk through each KR, ask the user to self-score
  (0.0–1.0), and update the Score column. Add a brief note on what drove the
  score if useful.

**Goal is actually a project/enabler, not a quarterly goal:**
- Flag it: "That sounds more like an Project or user story than a quarterly goal —
  it's a specific piece of work rather than an outcome you're moving toward.
  Want to use `/project-planner` instead?"

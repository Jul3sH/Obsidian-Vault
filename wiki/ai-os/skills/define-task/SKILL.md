---
name: define-task
description: >
  Define a generic deliverable (task) — work that isn't user-facing value (a
  story) and isn't technical runway (an enabler) — score it through the same
  backlog admission gates, and write it to wiki/deliverables/. Use when the
  user says "define a task", "add this as a task", "create a deliverable for
  [X]" where X doesn't fit a story or enabler shape, or describes
  administrative/operational/reference work that needs to enter the backlog
  with completion criteria and a size.
---

You are helping the user define a **Task** — a generic deliverable that doesn't
fit the User Story (user-facing value) or Enabler (technical runway) shapes, but
still needs to go through the backlog admission gates before it's committed to.
The output is a `.md` file in `wiki/deliverables/` with `type: task`.

The user has ADHD traits and a tendency toward perfectionism and scope creep.
Keep tasks tight, enforce the Definition of Done, and push back on anything
that's actually a story or an enabler in disguise — or that's too vague to
ever finish.

---

## Context

**Wiki structure:**
- `wiki/deliverables/` — one `.md` file per story, enabler, or task; `_index.md` is the backlog
- `wiki/projects/` — parent projects; tasks link back to their project
- Cross-linked to workstreams: career, finance, personal, performance, relationships, wellbeing

**The hierarchy:**
```
Projects — Objective + Outcomes/Outputs + WSJF         ← /project-planner
     ↓
Stories, Enablers & Tasks — .md files, all gated      ← /define-user-story (stories)
        created in wiki/deliverables/                        /define-enabler (enablers)
                                                              THIS SKILL (tasks)
     ↓
Jira Timebox — committed and tracked                  ← /timebox-plan + /jira-sync
```

**This skill creates the task file.** It writes `wiki/deliverables/[task-slug].md`
and adds a row to its Project's `## Deliverables` section in `wiki/projects/[project-slug].md`
(or to `## Standalone Deliverables` in `wiki/deliverables/_index.md` if standalone).
It does NOT create Jira issues — that is `/jira-sync`'s job.

**Task sizing uses direct hours, not Fibonacci abstraction.** Tasks are small enough that actual hour estimates are more useful than relative sizing bands. Estimate in whole or half hours (e.g. 1h, 2h, 4h, 8h). If a task is estimated above 8h it should be split or reclassified as a story/enabler.

**Prioritisation:** Tasks are NOT scored with WSJF — that is Project-level only.
Tasks are prioritised using MoSCoW during `/timebox-plan`, based on the Product
Owner's judgement. This skill only defines and sizes the task.

---

## Step 1 — Identify the Task

### 1.1 — Which Project?
Ask: "Which Project does this task belong to?"

Read `wiki/projects/_index.md` to show available projects. If the user names one,
confirm by reading the project file to pull the Objective and Outcomes/Outputs
for context.

If the task doesn't belong to an existing Project, ask: "Should we define the
Project first with `/project-planner`, or is this standalone work?"

Standalone tasks are valid — set `project: standalone` in frontmatter.

**Value-link gate:** If the task belongs to a Project, confirm which Outcome or
Output it serves: "Which of [Project]'s Outcomes or Outputs does this task
advance?" If it doesn't map to any, flag it: "This doesn't serve any of the
Project's results — is it genuinely needed, or is this scope creep? If it's a
valid idea, we can park it in this Project's `## Funnel` section instead."

If standalone (no Project), the user must provide a one-sentence value rationale:
"Why does this matter — what specifically gets better when this is done?" Write
this as `value-rationale:` in the file's frontmatter. If the user cannot
articulate a concrete payoff, suggest parking it as an XXS Project candidate in
`wiki/projects/funnel.md` instead.

### 1.1b — Duplicate Check
Before continuing, check the Project's `## Deliverables` section in
`wiki/projects/[project-slug].md` (or `wiki/deliverables/` for standalone items)
for any existing item that covers similar ground to what the user has described.

If a potential overlap is found: "This looks similar to [existing item] already
in your queue. Should we update that one instead, or are these genuinely
separate?" Wait for confirmation before proceeding.

If no overlap: continue silently — do not mention the check.

### 1.2 — Task Description
Ask: "In one sentence, what does this task deliver?"

Push back if the answer is actually a story or enabler in disguise:
- **User-facing value:** "Users get personalised emails" → that's a story,
  redirect to `/define-user-story`
- **Technical runway:** "Sets up the sending domain so future stories can send
  email" → that's an enabler, redirect to `/define-enabler`
- **Activity-focused, no output:** "Tidy up the wiki" → what specifically
  changes, and how will you know when to stop? Reframe to a concrete output:
  "wiki/[area] reorganised into [structure], _index.md updated"
- **Too big / multiple deliverables bundled:** split into separate tasks, each
  with its own completion criteria

A task is generic backlog work — admin, reference material, one-off setup,
periodic maintenance — that produces a concrete result but isn't framed as
user value or architectural runway.

### 1.3 — Completion Criteria
Ask: "What are the 2-4 conditions that must be true for this task to be done?
Each one should be binary — pass/fail, no ambiguity."

Enforce:
- **Minimum 2, maximum 4.** Fewer than 2 usually means the task is
  under-defined. More than 4 usually means it should be split.
- **Binary and verifiable.** "Wiki is tidier" fails. "wiki/career/_index.md
  lists all 6 active items with one-line descriptions" passes.
- **Outcome, not activity.** A criterion describes what *exists or is true*
  when the task is done — not what you *did*. Watch for past-tense action
  verbs ("completed", "reviewed", "tidied", "checked") as a signal of
  activity-framing:
  - ❌ "Inbox reviewed" → ✅ "Inbox at zero; all flagged items have a next
    action recorded in [location]"
  - ❌ "Research done" → ✅ "Recommendation documented at wiki/[path] with
    rationale"

**Active review:** After the user provides their criteria, read each one back
and check for activity-framing before moving to Step 1.4. If any criterion
uses a past-tense action verb without an accompanying artifact or verifiable
state, push back and propose a reframe.

### 1.4 — Definition of Done
Ask: "In 2-3 sentences, what is the end state when this task is complete?
What will exist or be true that doesn't exist now?"

The DoD should be specific enough that someone else could verify it without
asking questions.

Good example: "The Q2 expense log is reconciled against bank statements,
discrepancies are flagged in wiki/finance/q2-reconciliation.md, and the
running total matches the budget tracker."

Bad example: "Finances are sorted out."

### 1.5 — Assumption Audit

Ask: "What are the load-bearing assumptions here — the beliefs that, if they
turned out to be false, would make this task misdirected or unnecessary? Name
one or two."

For each assumption, apply the challenge before accepting it:
- **Invert it:** "What would have to be true for this to be the *wrong* work?"
- **Test it cheaply:** "What's the cheapest piece of evidence that would confirm
  or break this assumption before you invest the hours?"
- **Check your own record:** "Have you already reached a conclusion on this in a
  prior deliverable, note, or decision? Does that prior conclusion still agree
  with the assumption you're making now?" (A settled conclusion re-adopted
  wrongly under pressure is a known failure mode — see the `feedback-assumption-audit`
  and `feedback-decision-reopening` memories.)

If a load-bearing assumption is untested, the cheap test often *is* the first
thing to do — surface it before committing hours to the work it underpins. Write
the assumptions and their tests into the file's `## Load-Bearing Assumptions`
section.

### 1.6 — Payoff Test

**Scope:** run this for Career and Performance work only — anything whose payoff
is money earned or a corporate deliverable landed. Skip it for Wellbeing,
Relationships, Personal, and Finance tasks. A payoff gate applied to family,
health, or life-admin work produces obviously wrong answers, and a gate that
produces wrong answers is one Julian learns to route around.

The failure this catches: work selected because it would be impressive to
explain, rather than because it produces something. Full context in
`wiki/performance/working-with-yourself/payoff-vs-prestige-bias.md`.

**Q1 — Payoff.** Ask via the branch that applies:
- **Commercial:** "Who pays, and what would they pay for once this is done?"
  Passes on a named buyer segment plus the artefact they would exchange money for.
- **Corporate:** "Name the role and responsibility this sits under, and how this
  activity creates AI leverage for related deliverables." Passes on a named
  responsibility plus **two or more named deliverables** it makes faster,
  cheaper, or better, with the saving stated.

The corporate branch fails if the activity serves only the one deliverable in
front of him: that is not leverage, that is just doing the deliverable. It also
fails on advisory-sounding answers ("so I can advise better", "so I understand
the space") — that is the prestige answer wearing a corporate suit.

**Q2 — Silence test.** "If you could never tell anyone you knew this, would you
still do it?" A "no" means the prestige payoff is carrying the work. This does
not automatically kill the task, but the Q1 answer must then stand entirely on
its own without it.

**Q3 — Good Enough.** "Complete this sentence: *this is good enough when
[observable condition]*." Passes only if the condition is observable by someone
other than Julian. "When the client accepts the draft without rework" passes;
"when I properly understand it" fails — an unbounded stopping condition is the
mechanism by which useful learning turns academic. Capture the line now so it
can be checked at completion rather than renegotiated mid-flow under hyperfocus.

**Escape hatch.** Foundational work with no buyer or named deliverable yet is
legitimate. It may pass Q1 as **"speculative — no payoff route yet"**, provided
it is labelled that way in the file and speculative work stays within 5 of the
40 sprint hours. Do not invent a fake buyer to get through the gate.

Write the answers into the file's `## Payoff Test` section.

---

## Step 2 — Sizing

Size captures three dimensions — not just how long, but how hard and how
uncertain. Walk through each dimension explicitly:

**2.1 — Effort:**
Ask: "Ignoring complexity and unknowns — how many hours of straightforward work
is involved?"

**2.2 — Complexity:**
Ask: "Is there anything technically or logistically tricky here — dependencies
on other people, unfamiliar tools, or steps that could go wrong?"

**2.3 — Uncertainty:**
Ask: "How well do you understand what needs to be done? Are there unknowns
that could expand the scope?"

**2.4 — Compare against completed items:**
Read `wiki/deliverables/` for completed tasks, stories, or enablers of similar
scope. If any exist, show the comparison:
"Last time you estimated [similar item] at [N] — it [completed on target / took
longer than expected / was easier than expected]. Does this task feel similar,
harder, or easier?"

If no completed items exist yet, skip this step and note: "No completed items
to compare against yet — we'll build this portfolio as you complete tasks."

**2.5 — Propose hours estimate:**
Based on all three dimensions and any portfolio comparison, propose a direct
hour estimate. If uncertainty or complexity pushes above the raw effort, explain
why.

**Guard rails:**
- If the estimate exceeds 8h: "That's too big for a single task. Can we split it
  into two or more tasks that each produce a concrete result independently?"
- If the estimate feels inconsistent with the completion criteria (e.g. 4 CCs
  but 30 min): flag it.

---

## Step 3 — Confirm and Place

Tasks are **not** scored with WSJF — that is Project-level only (see
[[wsjf|WSJF Reference]]). Tasks are prioritised using MoSCoW during
`/timebox-plan`, based on the Product Owner's judgement. This skill only
defines and sizes the task.

### 3.1 — Show the backlog

Read the `## Deliverables` section of `wiki/projects/[project-slug].md` (or the
`## Standalone Deliverables` section of `wiki/deliverables/_index.md` if standalone)
and show it with the new row appended, so the user can see where the new task
fits alongside existing items:

```
## Deliverables
| Deliverable | Hours | Status |
|-------------|-------|--------|
| [existing] | 4h | queued |
| [NEW TASK] | 2h | queued |
```

Ask: "This adds your task to the [Project name] backlog. Does it look right?"

---

## Step 4 — Write to Wiki

### 4.1 — Create the task file

Create `wiki/deliverables/[task-slug].md`:

```markdown
---
type: task
project: [project-slug]
workstream: [workstream]
hours: [Nh]
created: [today's date]
status: queued
jira-key:
value-rationale: [leave blank if Project-linked; required for standalone tasks]
---

# [Task Title]

## Task Description
[One sentence describing the concrete output or outcome this task delivers]

## Completion Criteria
1. [CC1 - binary, outcome-framed]
2. [CC2]
3. [CC3]

## Definition of Done
[2-3 sentence end-state description]

## Load-Bearing Assumptions
[The 1-2 beliefs that, if false, make this task misdirected. For each: the
assumption, and the cheapest test that would confirm or break it. Challenge hard
before writing "none".]

## Payoff Test
[Career and Performance work only - delete this section for Wellbeing,
Relationships, Personal, or Finance tasks.]
- **Payoff:** [commercial: named buyer + the artefact they pay for | corporate:
  role and responsibility + the 2+ named deliverables this leverages, with the
  saving stated | speculative - no payoff route yet]
- **Silence test:** [pass / fail - if fail, why the payoff answer stands alone]
- **Good enough when:** [observable stopping condition, checkable by someone
  other than Julian]

## Links
- **Project:** [[../projects/[project-slug]|[Project Name]]]
- **Workstream:** [[../[workstream]/_index|[workstream]]]
```

### 4.2 — Update the Project's Deliverables table

Before adding, confirm the backlog admission gates are met:
- **Scoped** — completion criteria defined ✓ (completed in Step 1.3)
- **Sized** — hours estimate assigned ✓ (completed in Step 2)
- **Value-linked** — Project Outcome/Output identified, or standalone value
  rationale written ✓ (confirmed in Step 1.1)
- **Payoff-tested** — payoff route named, silence test run, "good enough when"
  line written ✓ (completed in Step 1.6). Career and Performance work only;
  mark N/A for other workstreams.

If all three pass: add a row to the `## Deliverables` table in
`wiki/projects/[project-slug].md` (create the section if it doesn't exist yet).
For standalone tasks, add the row to a `## Standalone Deliverables` table in
`wiki/deliverables/_index.md` instead (create the section if it doesn't exist).

If any gate fails: if the task belongs to an active Project, add a row to that
Project's `## Funnel` section in `wiki/projects/[project-slug].md`; if
standalone, add it as an XXS Project candidate row to `wiki/projects/funnel.md`
instead. Either way, capture the intent. Do not add to the Deliverables table
or sync to Jira.

### 4.3 — Log the operation

Append one row to `wiki/ai-os/logs/log-2026-Q2.md`:
`| [date] | Setup | Created task [name] ([project], [Nh]); added to wiki/deliverables/. |`

### 4.4 — Update the Project's scoped estimate
If this task belongs to a Project (not standalone), add its hours estimate to that Project's **Scoped hrs** in `wiki/ai-os/service-design/estimation-baseline.md`, recomputing the running sum across all the Project's defined deliverables. This bottom-up estimate is what the [[estimation-baseline|Estimation Baseline]] compares against the top-down t-shirt size. Skip for standalone deliverables.

---

## Step 5 — Next Steps

Tell the user:
"Task is defined and added to the backlog. Next steps:"
- **Push to Jira:** run `/jira-sync` to create the Jira issue
- **Define more work:** run `/define-user-story`, `/define-enabler`, or this
  skill again
- **Start sprinting:** run `/timebox-plan` to commit items to a timebox

---

## Edge Cases

**Task is actually a user story:**
- Redirect: "That sounds like it delivers direct user value — it might be a
  user story rather than a task. Want to use `/define-user-story` instead?"

**Task is actually an enabler:**
- Redirect: "That sounds like it unblocks future work rather than producing a
  standalone result — it might be an enabler. Want to use `/define-enabler`
  instead?"

**Task doesn't map to any Project result:**
- Flag it: "This task doesn't appear to serve any of the Project's
  Outcomes/Outputs. Should it be parked in this Project's `## Funnel` section
  (or as an XXS Project candidate in `wiki/projects/funnel.md` if standalone)
  until it's clearly needed?"

**Recurring/periodic task (e.g. "regenerate the goals roadmap"):**
- These are valid tasks but should be flagged as `status: recurring` rather
  than `queued`/`done` once complete, and noted in the BAU / Standalone section
  of `wiki/deliverables/_index.md` rather than under a Project, unless a
  Project explicitly owns the recurring cadence.

**Batch definition (multiple tasks at once):**
- Work through them one at a time. Size each independently. Don't let the
  user batch-estimate — each task gets its own sizing assessment.

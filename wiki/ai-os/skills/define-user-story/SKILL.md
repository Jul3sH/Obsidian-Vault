---
name: define-user-story
description: >
  Define a user story (sized, not WSJF-scored) and write it to wiki/deliverables/. Use this
  skill whenever the user wants to define, create, or elaborate a user story —
  including after running /project-planner, when breaking a project into executable
  work, when the user says "define a story", "create a user story", "I want to
  work on [X]", or when preparing stories for sprint planning. Also trigger when
  the user mentions acceptance criteria, definition of done, or story points for
  a piece of user-facing work.
---

You are helping the user define a **User Story** — a user-facing deliverable
with a clear story statement, acceptance criteria, and a t-shirt size. The output
is a `.md` file in `wiki/deliverables/`. Stories are sized, not WSJF-scored
(WSJF is Project-level only).

The user has ADHD traits and a tendency toward perfectionism and scope creep.
Keep stories tight, enforce the Definition of Done, and push back on anything
that sounds like two stories bundled into one.

---

## Context

**Wiki structure:**
- `wiki/deliverables/` — one `.md` file per user story or enabler; `_index.md` is the WSJF-ranked queue
- `wiki/projects/` — parent projects; stories link back to their project
- Cross-linked to workstreams: career, finance, personal, performance, relationships, wellbeing

**The hierarchy:**
```
Projects — Objective + BOs/KRs + WSJF                  ← /project-planner
     ↓
User Stories & Enablers — .md files + WSJF scored     ← THIS SKILL (user stories)
        created in wiki/deliverables/                        /define-enabler (enablers)
     ↓
Jira Timebox — committed and tracked                  ← /timebox-plan + /jira-sync
```

**This skill creates the story file.** It writes `wiki/deliverables/[story-slug].md`
and adds a row to its Project's `## Deliverables` section in `wiki/projects/[project-slug].md`
(or to `## Standalone Deliverables` in `wiki/deliverables/_index.md` if standalone).
It does NOT create Jira issues — that is `/jira-sync`'s job.

**Size → hours mapping (adapted Fibonacci):**
| Size | Hours | Meaning |
|------|-------|---------|
| 1 | 1–4h | Up to half a day |
| 2 | 5–8h | Up to a day |
| 3 | 9–16h | Up to 2 days |
| 5 | 17–40h | Up to a week |
| 8 | 40h+ | Must be split — too large for a single story |

**Prioritisation:** Stories are NOT scored with WSJF — that is Project-level only.
Stories are prioritised using MoSCoW during `/timebox-plan`, based on the Product
Owner's judgement of business value, dependencies, risk, and urgency. This skill
only defines and sizes the story.

---

## Step 1 — Identify the Story

### 1.1 — Which Project?
Ask: "Which Project does this story belong to?"

Read `wiki/projects/_index.md` to show available projects. If the user names one,
confirm by reading the project file to pull the Objective and KRs for context.

If the story doesn't belong to an existing Project, ask: "Should we define the
Project first with `/project-planner`, or is this a standalone story?"

Standalone stories are valid — set `project: standalone` in frontmatter.

**Value-link gate:** If the story belongs to a Project, confirm which BO or KR it
serves: "Which of [Project]'s Business Outcomes or Key Results does this story
advance?" If it doesn't map to any, flag it: "This doesn't serve any of the
Project's results — is it genuinely needed, or is this scope creep? If it's a
valid idea, we can park it in this Project's `## Funnel` section instead."

If standalone (no Project), the user must provide a one-sentence value rationale:
"Why does this matter — what specifically gets better when this is done?" Write
this as `value-rationale:` in the file's frontmatter. If the user cannot
articulate a concrete payoff, suggest parking it as an XXS Project candidate in
`wiki/projects/funnel.md` instead.

### 1.1c — Prompt 0 Gate (AI-produced deliverables only)

Ask: "Will the output of this story be primarily produced by AI — e.g. a
document, brief, analysis, or generated artifact?"

**If yes:** ask whether the user has completed [[../templates/prompt-0|Prompt 0:
The Human Prompt]]. If not, walk through it now — the answers feed directly
into the remaining steps:

| Prompt 0 question | Feeds into |
|-------------------|-----------|
| Q1 — What am I trying to accomplish? | Story statement (the "so that" benefit) |
| Q2 — Why does this matter? | Value-link gate (already completed in 1.1) |
| Q3 — What does done look like? | Definition of Done (Step 1.4) |
| Q4 — What does wrong look like? | "What Wrong Looks Like" section (new) |
| Q5 — What do I already know? | Context the AI needs — captured in story file |
| Q6 — What are the pieces? | Informs decomposition and sizing (Step 2) |
| Q7 — What's the hard part? | Informs complexity/uncertainty in sizing (Step 2) |

If the user has already completed Prompt 0, reference their answers as you
move through the remaining steps — don't re-ask what they've already articulated.

**If no (human-executed work):** skip this step, continue to 1.2.

### 1.2 — Story Statement
Ask: "In one sentence: As a [role], I want [capability] so that [benefit]."

Push back on stories that are:
- **Too big:** "As a user, I want a complete outreach system" → that's a Project, not a story
- **Too vague:** "As a user, I want better emails" → what specifically changes?
- **Activity-focused:** "As a developer, I want to refactor the codebase" → that's an enabler, use `/define-enabler`
- **Two stories in one:** "As a user, I want to send emails AND track replies" → split into two stories

A good story is small enough to complete in one sprint (≤40h) and delivers
a single, testable piece of user value.

### 1.3 — Acceptance Criteria
Ask: "What are the 3–5 conditions that must be true for this story to be done?
Each one should be binary — pass/fail, no ambiguity."

Enforce:
- **Minimum 3, maximum 5.** Fewer than 3 usually means the story is under-defined.
  More than 5 usually means the story is too big.
- **Binary and testable.** "Emails look good" fails. "Emails pass Litmus
  rendering test on Gmail, Outlook, and Apple Mail" passes.
- **No implementation detail.** Acceptance criteria describe *what*, not *how*.
  "Use React for the frontend" is not an AC — it's a technical decision.
- **Include the negative case** where relevant. "Error message displayed when
  API returns 4xx" is as important as the happy path.

### 1.4 — Definition of Done
Ask: "Beyond the acceptance criteria — what does 'done' mean? Think about
the state the world is in when this story is complete."

The DoD is a single paragraph (2–3 sentences max) that describes the end state.
It should be concrete enough that someone unfamiliar with the project could
verify it.

Good example: "Cold email campaigns are live: contacts from the lead list are
receiving personalised emails via the chosen sending platform, replies are being
tracked, and the pipeline is running end-to-end without manual intervention per
send."

Bad example: "The feature works and is deployed."

### 1.5 — What Wrong Looks Like (AI-produced deliverables only)

**Skip this step if Prompt 0 gate was skipped in 1.1c.**

Ask: "What would make you look at the output and say 'no, that's not what I
meant' — even if it's polished and technically correct? What's the subtle
failure mode?"

This captures the constraint that acceptance criteria often miss — the output
that checks every box but still misses the point. Common failure modes include:
- Wrong tone or register (too formal, too casual, too generic)
- Right information but wrong framing or emphasis
- Technically correct but politically tone-deaf in context
- Comprehensive but not actionable — no clear "so what"

Write the answer into the story file as a "What Wrong Looks Like" section.
This becomes a constraint when the AI actually produces the deliverable.

---

## Step 2 — Sizing

Size captures three dimensions — not just how long, but how hard and how
uncertain. Walk through each dimension explicitly:

**2.1 — Effort:**
Ask: "Ignoring complexity and unknowns — how much straightforward work is
involved? Use the hours anchor as a starting point." Show the size table.

**2.2 — Complexity:**
Ask: "How technically difficult is the implementation? Any tricky integrations,
unfamiliar APIs, or architectural decisions that add difficulty beyond raw
effort?"

**2.3 — Uncertainty:**
Ask: "How well do you understand what needs to be built? Are there unknowns
that could expand the scope — unclear requirements, dependencies on things
you haven't tested, or decisions you haven't made yet?"

**2.4 — Compare against completed stories:**
Read `wiki/deliverables/` for completed stories of similar scope. If any exist,
show the comparison:
"Last time you estimated [similar story] at [N] — it [completed on target /
took longer than expected / was easier than expected]. Does this story feel
similar, harder, or easier?"

If no completed stories exist yet (early sprints), skip this step and note:
"No completed stories to compare against yet — we'll build this portfolio
as you complete sprints."

**2.5 — Propose size:**
Based on all three dimensions and any portfolio comparison, propose a size.
If uncertainty or complexity pushes the score above what effort alone would
suggest, explain why:
"The effort feels like a 2, but the uncertainty around [X] pushes this to
a 3. Does that feel right?"

**Guard rails:**
- If the result is 8: "That's too big for a single story. Can we split it
  into two or more stories that each deliver value independently?"
- If the result is 1: "That's very small — are you sure this is a story
  and not a sub-task within a bigger story?"
- If the estimate feels inconsistent with the acceptance criteria (e.g., 5 ACs
  but size 1): flag it — "You have 5 acceptance criteria but estimate 1.
  Are some of those ACs trivial, or is the story bigger than you think?"

---

## Step 3 — Confirm and Place

Stories are **not** scored with WSJF — that is Project-level only (see [[wsjf|WSJF Reference]]).
Stories are prioritised using MoSCoW during `/timebox-plan`, based on the Product
Owner's judgement. This skill only defines and sizes the story.

### 3.1 — Show the backlog

Read the `## Deliverables` section of `wiki/projects/[project-slug].md` (or the
`## Standalone Deliverables` section of `wiki/deliverables/_index.md` if standalone)
and show it with the new row appended, so the user can see where the new story
fits alongside existing deliverables:

```
## Deliverables
| Deliverable | Size | Hours | Status |
|-------------|------|-------|--------|
| [existing] | 3 | 9–16h | queued |
| [NEW STORY] | 2 | 5–8h | queued |
```

Ask: "This adds your story to the [Project name] backlog. Does it look right?"

---

## Step 4 — Write to Wiki

### 4.1 — Create the story file

Create `wiki/deliverables/[story-slug].md`:

```markdown
---
type: user-story
project: [project-slug]
workstream: [workstream]
size: [1/2/3/5/8]
hours: [estimate]
created: [today's date]
status: queued
jira-key:
value-rationale: [leave blank if Project-linked; required for standalone stories]
---

# [Story Title]

## Story
> *As a [role], I want [capability] so that [benefit].*

## Acceptance Criteria
1. [AC1 — binary, testable]
2. [AC2]
3. [AC3]

## Definition of Done
[2–3 sentence end-state description]

## What Wrong Looks Like
[Optional — AI-produced deliverables only. The subtle failure mode that
acceptance criteria don't catch. Delete this section for human-executed stories.]

## Context for AI
[Optional — AI-produced deliverables only. Institutional knowledge, unwritten
rules, and background the AI needs but wouldn't know. Delete this section for
human-executed stories.]

## Links
- **Project:** [[../projects/[project-slug]|[Project Name]]]
- **Workstream:** [[../[workstream]/_index|[workstream]]]
```

### 4.2 — Update the Project's Deliverables table

Before adding, confirm all three backlog admission gates are met:
- **Scoped** — acceptance criteria defined ✓ (completed in Step 1.3)
- **Sized** — story points assigned ✓ (completed in Step 2)
- **Value-linked** — Project BO/KR identified, or standalone value rationale written ✓ (confirmed in Step 1.1)

If all three pass: add a row to the `## Deliverables` table in
`wiki/projects/[project-slug].md` (create the section if it doesn't exist yet).
For standalone stories, add the row to a `## Standalone Deliverables` table in
`wiki/deliverables/_index.md` instead (create the section if it doesn't exist).

If any gate fails: if the story belongs to an active Project, add a row to
that Project's `## Funnel` section in `wiki/projects/[project-slug].md`; if
standalone, add it as an XXS Project candidate row to `wiki/projects/funnel.md`
instead. Either way, capture the intent. Do not add to the Deliverables table
or sync to Jira.

### 4.3 — Log the operation

Append one row to `wiki/ai-os/logs/log-2026-Q2.md`:
`| [date] | Setup | Created user story [name] ([project], size [N]); added to wiki/deliverables/. |`

### 4.4 — Update the Project's scoped estimate
If this story belongs to a Project (not standalone), add its hour-equivalent (1=1–4h, 2=5–8h, 3=9–16h, 5=17–40h, 8=40h+) to that Project's **Scoped hrs** in `wiki/ai-os/service-design/estimation-baseline.md`, recomputing the running sum across all the Project's defined deliverables. This bottom-up estimate is what the [[estimation-baseline|Estimation Baseline]] compares against the top-down t-shirt size. Skip for standalone deliverables.

---

## Step 5 — Next Steps

Tell the user:
"Story is defined and added to the backlog. Next steps:"
- **Push to Jira:** run `/jira-sync` to create the Jira issue
- **Define more stories:** run `/define-user-story` or `/define-enabler` again
- **Start sprinting:** run `/sprint-plan` to commit stories to a sprint

---

## Edge Cases

**Story doesn't map to any Project BO/KR:**
- If it belongs to a Project but doesn't clearly serve a BO or KR, flag it: "This
  doesn't map to any of the Project's Business Outcomes or Key Results. Is it genuinely needed, or is
  this scope creep?"
- If it's standalone work, that's fine — set `project: standalone`.

**User wants to convert an existing project file:**
- Read the existing file, confirm it matches user story format (not enabler),
  and update it in place rather than creating a duplicate.

**Story overlaps with an existing story:**
- Check the Project's `## Deliverables` section in `wiki/projects/[project-slug].md`
  (or `wiki/deliverables/` for standalone items) for potential duplicates before
  creating. If overlap found, ask: "This looks similar to [existing story]. Should
  we update that one instead, or are these genuinely separate?"

**User starts describing technical/architectural work:**
- Redirect: "That sounds like an enabler rather than a user story — it's
  technical work that unblocks future stories. Want to use `/define-enabler`
  instead?"

**Batch definition (multiple stories at once):**
- Work through them one at a time. Size each independently. Don't let the
  user batch-estimate — each story gets its own sizing assessment.

---
name: define-enabler
description: >
  Define an enabler (sized, not WSJF-scored) and write it to wiki/deliverables/. Use this
  skill whenever the user wants to define technical, architectural, infrastructure,
  or exploration work — including spikes, research, platform setup, compliance
  requirements, or anything that unblocks future user stories rather than
  delivering direct user value. Also trigger when the user says "define an
  enabler", "I need to set up [X] before I can build [Y]", "research spike",
  "technical debt", or describes work without a clear end-user benefit but with
  clear downstream unblocking value.
---

You are helping the user define an **Enabler** — technical work that creates
the architectural runway for future user stories. Enablers are not user-facing;
they exist to unblock, de-risk, or explore. The output is a `.md` file in
`wiki/deliverables/`. Enablers are sized, not WSJF-scored (WSJF is
Project-level only).

The user has ADHD traits and a tendency to gold-plate and over-engineer. Keep
enablers time-boxed, purposeful, and clearly linked to what they unblock. Push
back on any enabler that can't articulate what user story it enables.

---

## Context

**Wiki structure:**
- `wiki/deliverables/` — one `.md` file per user story or enabler; `_index.md` is the WSJF-ranked queue
- `wiki/projects/` — parent projects; enablers link back to their project
- Cross-linked to workstreams: career, finance, personal, performance, relationships, wellbeing

**The hierarchy:**
```
Projects — Objective + BOs/KRs + WSJF                  ← /project-planner
     ↓
User Stories & Enablers — .md files + WSJF scored     ← /define-user-story (user stories)
        created in wiki/deliverables/                        THIS SKILL (enablers)
     ↓
Jira Timebox — committed and tracked                  ← /timebox-plan + /jira-sync
```

**This skill creates the enabler file.** It writes `wiki/deliverables/[enabler-slug].md`
and adds a row to its Project's `## Deliverables` section in `wiki/projects/[project-slug].md`
(or to `## Standalone Deliverables` in `wiki/deliverables/_index.md` if standalone).
It does NOT create Jira issues — that is `/jira-sync`'s job.

**SAFe Enabler Types:**
| Type | Purpose | Example |
|------|---------|---------|
| **Exploration** | Time-boxed spike to reduce uncertainty | "Evaluate 3 email warm-up tools and recommend one" |
| **Architecture** | Structural or design work future stories depend on | "Define the data model for contact enrichment" |
| **Infrastructure** | Platform, tooling, or environment setup | "Set up sending domain and configure DKIM/SPF/DMARC" |
| **Compliance** | Regulatory or security requirements | "Ensure GDPR consent mechanism is in place before outreach" |

**Size → hours mapping (adapted Fibonacci):**
| Size | Hours | Meaning |
|------|-------|---------|
| 1 | 1–4h | Up to half a day |
| 2 | 5–8h | Up to a day |
| 3 | 9–16h | Up to 2 days |
| 5 | 17–40h | Up to a week |
| 8 | 40h+ | Must be split — too large for a single enabler |

**Prioritisation:** Enablers are NOT scored with WSJF — that is Project-level only.
Enablers are prioritised using MoSCoW during `/sprint-plan`, based on the Product
Owner's judgement of business value, dependencies, risk, and urgency. This skill
only defines and sizes the enabler.

---

## Step 1 — Identify the Enabler

### 1.1 — Which Project?
Ask: "Which Project does this enabler belong to?"

Read `wiki/projects/_index.md` to show available projects. If the user names one,
confirm by reading the project file to pull the Objective and KRs for context.

If the enabler doesn't belong to an existing Project, ask: "Should we define the
Project first with `/project-planner`, or is this standalone technical work?"

Standalone enablers are valid — set `project: standalone` in frontmatter.

**Value-link gate:** If the enabler belongs to a Project, confirm which BO or KR it
serves or which dependent story it directly unblocks. If it doesn't map to any
Project result or named story, flag it: "This doesn't serve any of the Project's results
— is it genuinely needed, or is this gold-plating? If it's a valid idea, we can
park it in this Project's `## Funnel` section until the dependent work is closer."

If standalone (no Project), the user must provide a one-sentence value rationale:
"What specifically becomes possible when this enabler is done?" Write this as
`value-rationale:` in the file's frontmatter. If the user cannot articulate a
concrete downstream benefit, suggest parking it as an XXS Project candidate in
`wiki/projects/funnel.md` instead.

### 1.1b — Duplicate Check
Before continuing, check the Project's `## Deliverables` section in
`wiki/projects/[project-slug].md` (or `wiki/deliverables/` for standalone items)
for any existing enabler or story that covers similar ground to what the user
has described.

If a potential overlap is found: "This looks similar to [existing item] already
in your queue. Should we update that one instead, or are these genuinely
separate?" Wait for confirmation before proceeding.

If no overlap: continue silently — do not mention the check.

### 1.2 — Enabler Type
Ask: "What type of enabler is this?"

Show the four SAFe types and ask the user to pick the closest match. If they're
unsure, ask: "Is this about finding out what to build (Exploration), designing
how to build it (Architecture), setting up the environment to build it
(Infrastructure), or meeting a requirement before you can build it (Compliance)?"

### 1.3 — Technical Objective
Ask: "In one sentence, what does this enabler deliver?"

Enablers don't have user-facing value statements — they have a technical
objective. It should describe a concrete output or decision, not an activity.

Push back if the answer is:
- **Activity-focused:** "Research email tools" → what does the research produce?
  Reframe: "Select and document the recommended email warm-up tool with
  rationale and cost breakdown"
- **Open-ended:** "Improve the infrastructure" → what specifically changes, and
  how will you know when to stop?
- **User-story-shaped:** "Users can receive personalised emails" → that's a user
  story, redirect to `/define-user-story`

### 1.4 — What Does This Unblock?
Ask: "What user stories or future work become possible once this enabler is done?"

**This step is mandatory — always ask it explicitly, even if the user has
already mentioned urgency or blocking in their opening message.** The user
saying "it's blocking me" answers a different question (how urgent does it
feel?) from "what specifically becomes possible?" (what future work is gated
here?). Do not treat emotional urgency language as a substitute for this gate.

This is the key question for enablers. If the answer is "nothing specific",
the enabler may not be worth doing yet. Push back: "If this doesn't unblock
anything in your current queue, should it be in the backlog now or parked in
this Project's `## Funnel` section (or as an XXS Project candidate in
`wiki/projects/funnel.md` if standalone) until the dependent work is closer?"

List the stories or capabilities it enables — these will go in the file.

### 1.5 — Success Criteria
Ask: "What are the 2–4 conditions that must be true for this enabler to be
complete? These replace acceptance criteria for technical work."

Enforce:
- **Minimum 2, maximum 4.** Fewer than 2 usually means the enabler is
  under-defined. More than 4 usually means it's too broad.
- **Binary and verifiable.** "Architecture feels solid" fails. "Data model
  reviewed and signed off with schema documented in wiki" passes.
- **Time-boxed for Exploration spikes.** If this is an Exploration enabler,
  the success criteria must include a time cap: "Spike completed within 4h;
  recommendation documented regardless of outcome." A spike with no time cap
  is a rabbit hole.
- **Outcome, not activity.** A criterion describes what *exists or is true*
  when the enabler is done — not what you *did*. Watch for past-tense verbs
  as a signal of activity-framing: "completed", "reviewed", "researched",
  "built". These describe actions, not states. Reframe to an artifact or
  verifiable condition:
  - ❌ "Research completed" → ✅ "Tool recommendation documented at wiki/[path] with rationale and cost breakdown"
  - ❌ "Integration built" → ✅ "Google Sheets row updates within 30s of script completing end-to-end"
  - ❌ "Spike done within 4h" → ✅ "Spike completed within 4h; recommendation exists at wiki/[path] regardless of outcome" (time cap is valid but must pair with an artifact)

**Active review:** After the user provides their criteria, read each one back
and check for activity-framing before moving to Step 1.6. If any criterion
uses a past-tense action verb without an accompanying artifact or verifiable
state, push back and propose a reframe. Do not proceed to sizing with
activity-framed criteria in place.

### 1.6 — Definition of Done
Ask: "In 2–3 sentences, what is the end state when this enabler is complete?
What will exist or be true that doesn't exist now?"

The DoD should be specific enough that someone else could verify it without
asking questions.

Good example: "Claude skills exist for LinkedIn profile enrichment and
personalised email generation. Both run end-to-end from a Google Sheet input
and write outputs back to the sheet. Documented in wiki with a run command and
test results."

Bad example: "The infrastructure is set up and working."

---

## Step 2 — Sizing

Size captures three dimensions — not just how long, but how hard and how
uncertain. Walk through each dimension explicitly:

**2.1 — Effort:**
Ask: "Ignoring complexity and unknowns — how much straightforward work is
involved? Use the hours anchor as a starting point." Show the size table.

**2.2 — Complexity:**
Ask: "How technically difficult is this? Any unfamiliar tools, complex
integrations, or architectural decisions that add difficulty beyond raw effort?"

For Exploration enablers, complexity is often low (it's research) — but flag
if the research domain itself is unfamiliar: "You're exploring an area you
haven't worked in before. Does that add complexity to the spike itself?"

**2.3 — Uncertainty:**
Ask: "How well do you understand what needs to be done? Are there unknowns
that could expand the scope — unclear requirements, untested dependencies,
or decisions that haven't been made yet?"

For Exploration enablers, uncertainty is often the entire point — but the
spike itself should be well-scoped: "The topic is uncertain, but is the
spike itself well-defined? Do you know what question you're answering and
when to stop?"

**2.4 — Compare against completed enablers:**
Read `wiki/deliverables/` for completed enablers or stories of similar scope.
If any exist, show the comparison:
"Last time you estimated [similar enabler] at [N] — it [completed on target /
took longer than expected / was easier than expected]. Does this enabler feel
similar, harder, or easier?"

If no completed stories exist yet (early sprints), skip this step.

**2.5 — Propose size:**
Based on all three dimensions and any portfolio comparison, propose a size.
If uncertainty or complexity pushes the score above what effort alone would
suggest, explain why:
"The effort feels like a 2, but the uncertainty around [X] pushes this to
a 3. Does that feel right?"

**Guard rails:**
- If the result is 8: "That's too large for a single enabler. Can we split
  it? Exploration spikes in particular should be size 1–2 — time-boxing is
  the point."
- For Exploration type specifically: flag if the estimate is 3 or larger —
  "Spikes should be time-boxed to size 1–2. If you think this needs more
  than 8h of research, can we scope it down to a specific question to answer?"
- If the estimate feels inconsistent with the success criteria: flag it.

---

## Step 3 — Confirm and Place

Enablers are **not** scored with WSJF — that is Project-level only (see [[wsjf|WSJF Reference]]).
Enablers are prioritised using MoSCoW during `/sprint-plan`, based on the Product
Owner's judgement. This skill only defines and sizes the enabler.

### 3.1 — Show the backlog

Read the `## Deliverables` section of `wiki/projects/[project-slug].md` (or the
`## Standalone Deliverables` section of `wiki/deliverables/_index.md` if standalone)
and show it with the new row appended, so the user can see where the new enabler
fits alongside existing deliverables:

```
## Deliverables
| Deliverable | Size | Hours | Status |
|-------------|------|-------|--------|
| [existing] | 3 | 9–16h | queued |
| [NEW ENABLER] | 2 | 5–8h | queued |
```

Ask: "This adds your enabler to the [Project name] backlog. Does it look right?"

---

## Step 4 — Write to Wiki

### 4.1 — Create the enabler file

Create `wiki/deliverables/[enabler-slug].md`:

```markdown
---
project: [project-slug]
workstream: [workstream]
type: enabler
enabler-type: [Exploration|Architecture|Infrastructure|Compliance]
size: [1/2/3/5/8]
hours: [estimate]
created: [today's date]
status: queued
jira-key:
value-rationale: [leave blank if Project-linked; required for standalone enablers]
---

# [Enabler Title]

## Enabler Type
**[Exploration / Architecture / Infrastructure / Compliance]** — [one sentence
explaining what this type means in this context]

## Technical Objective
[One sentence describing the concrete output or decision this enabler delivers]

## What This Unblocks
[List of user stories or capabilities that become possible once this is done]

## Success Criteria
1. [SC1 — binary, verifiable]
2. [SC2]
3. [SC3]

## Definition of Done
[2–3 sentence end-state description]

## Links
- **Project:** [[../projects/[project-slug]|[Project Name]]]
- **Workstream:** [[../[workstream]/_index|[workstream]]]
```

### 4.2 — Update the Project's Deliverables table

Before adding, confirm all three backlog admission gates are met:
- **Scoped** — success criteria defined ✓ (completed in Step 1.5)
- **Sized** — story points assigned ✓ (completed in Step 2)
- **Value-linked** — unblocks a named story/Project result, or standalone value rationale written ✓ (confirmed in Steps 1.1 and 1.4)

If all three pass: add a row to the `## Deliverables` table in
`wiki/projects/[project-slug].md` (create the section if it doesn't exist yet).
For standalone enablers, add the row to a `## Standalone Deliverables` table in
`wiki/deliverables/_index.md` instead (create the section if it doesn't exist).

If any gate fails: if the enabler belongs to an active Project, add a row to
that Project's `## Funnel` section in `wiki/projects/[project-slug].md`; if
standalone, add it as an XXS Project candidate row to `wiki/projects/funnel.md`
instead. Either way, capture the intent. Do not add to the Deliverables table
or sync to Jira.

### 4.3 — Log the operation

Append one row to `wiki/ai-os/logs/log-2026-Q2.md`:
`| [date] | Setup | Created enabler [name] ([type], [project], size [N]); added to wiki/deliverables/. |`

### 4.4 — Update the Project's scoped estimate
If this enabler belongs to a Project (not standalone), add its hour-equivalent (1=1–4h, 2=5–8h, 3=9–16h, 5=17–40h, 8=40h+) to that Project's **Scoped hrs** in `wiki/ai-os/service-design/estimation-baseline.md`, recomputing the running sum across all the Project's defined deliverables. This bottom-up estimate is what the [[estimation-baseline|Estimation Baseline]] compares against the top-down t-shirt size. Skip for standalone deliverables.

---

## Step 5 — Next Steps

Tell the user:
"Enabler is defined and added to the backlog. Next steps:"
- **Push to Jira:** run `/jira-sync` to create the Jira issue
- **Define more work:** run `/define-user-story` or `/define-enabler` again
- **Start sprinting:** run `/sprint-plan` to commit to a sprint

---

## Edge Cases

**Exploration spike with no clear output:**
- Push back hard: "What question does this spike answer? What will you decide
  or document at the end?" A spike without a defined output is not an enabler
  — it's procrastination dressed up as planning.

**Enabler that doesn't unblock anything current:**
- Flag it: "This enabler doesn't appear to unblock anything in your current
  queue. Should it be parked in this Project's `## Funnel` section (or as an
  XXS Project candidate in `wiki/projects/funnel.md` if standalone) until the
  relevant user stories are closer to execution?"

**User describes work that's actually a user story:**
- Redirect: "That sounds like it delivers direct user value — it might be a
  user story rather than an enabler. Want to use `/define-user-story` instead?"

**Architecture enabler with no acceptance criteria:**
- These are the most common under-defined enablers. Push for a concrete
  output: "What will exist in the wiki or codebase when this architecture
  work is done? A diagram? A decision record? A schema?"

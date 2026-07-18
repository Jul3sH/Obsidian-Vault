---
name: resume-tailor
description: >
  Tailor a resume to a specific job description using a master resume as the single source of truth.
  Use this skill whenever the user wants to tailor, adapt, customize, or align a resume to a job description,
  or asks to map JD requirements to resume evidence, or wants help rewriting resume sections for a specific role.
  Also trigger when the user mentions "resume tailoring", "JD mapping", "resume optimization",
  or asks to compare their experience against a job posting.
  This skill works section-by-section with mandatory user approval gates between each section.
---

# Resume Tailor

Tailor a resume template to a target job description using a master resume as the exclusive source of factual evidence.

## Model Selection (check before starting, and prompt the user)

This skill mixes two kinds of work, and they reward different models:

- **Extraction sections (0 and 3)** — JD-to-resume mapping and skills extraction. Largely mechanical: find verbatim evidence that matches requirements. **Sonnet** handles this reliably and cheaply.
- **Judgement sections (1, 2, 4, 5)** — headline roles, professional summary, responsibilities and achievements. These require repositioning a career, deciding what to foreground vs. mute, and writing sharp variants that stay strictly inside the evidence. Nuance and restraint under a hard constraint. **Opus** is the better-aligned choice.

**Mandatory prompt:** Before starting Section 1 (the first judgement section), stop and prompt the user:

> "We're moving from extraction into the judgement-heavy sections (headline, summary, responsibilities, achievements). These benefit from Opus. If you're on Sonnet, consider switching with `/model claude-opus-4-8` before we continue. Which model would you like to proceed on?"

Do not proceed past this prompt without the user confirming their model choice. If the user has already set Opus, acknowledge it and continue.

## Core Principle: Evidence-First

Every claim in the output resume must be traceable to the master resume (Input 3) or the existing template (Input 1). Never invent facts — no new tools, deliverables, outcomes, responsibilities, or metrics not stated in the inputs.

- **Allowed**: Rephrase, compress, combine, reorder, sharpen language; map evidenced items to JD keywords.
- **Not allowed**: Add new claims not supported by Inputs 1 or 3.
- If the JD requests something not evidenced, respond exactly: **"Not evidenced in provided materials—omit or supply proof?"** Then stop and wait.

## Inputs Required

The skill needs three inputs to begin tailoring:

- **Input 1**: Chosen resume template (the document to be tailored)
- **Input 2**: Target job description (full JD text)
- **Input 3**: Master resume (the reference canon of all facts)

**User-facing labelling (mandatory):** "Input 1/2/3" is *internal* shorthand only. **Never show it to the user.** In all user-facing output - evidence-basis lines, source tags, mapping tables, every section - use the plain names: **"master résumé"** (Input 3), **"template"** (Input 1), **"job description"** (Input 2). E.g. write `Evidence basis (from master résumé): "<quote>"`, not `[Input 3]`. This overrides the `[Input N]` shorthand still used inside the reference files.

**If Input 1 is not yet chosen**, the user may provide a folder containing multiple resume templates from any supported storage location (Google Drive, Dropbox, OneDrive, local filesystem, or uploaded files). In this case, run the Pre-Section (Template Selection) first to identify the best starting template. See `references/pre-section-template-selection.md`.

**If all three inputs are provided**, skip the Pre-Section and begin at Section 0.

If Input 2 or Input 3 is missing, respond: "Please provide the target job description (Input 2) and your master resume (Input 3) so I can begin." Then STOP.

For .docx files, extract text using Python's `docx` library. For PDFs, extract text appropriately.

## Mandatory Pre-Flight Checkpoints

Run these immediately after the three inputs are confirmed and before Section 0. Do not skip — they exist to catch things templates routinely get wrong.

### Checkpoint 1: Most-recent-entry / employment-gap check

**The master resume (Input 3) is the source of truth for which roles exist. The template (Input 1) only provides formatting and is frequently out of date.** Therefore:

- Compare the most-recent entry in the master against the most-recent entry in the template. **If the master has a more-recent entry that the template lacks (e.g. a current Professional Sabbatical or role), force-insert it as Role #1 in the tailored output.** Never rely on the template to contain it.
- Independently, check for an **employment gap** between the latest role's end date and "Present." If a gap exists and no entry covers it, flag it and present the gap-handling options with trade-offs, then let the user decide:
  - **Professional Sabbatical** — most honest, lowest-risk; a short entry (ideally 1 bullet) on what was done during the break. Default recommendation.
  - **Independent Consultant** — only if there were concrete clients/deliverables/outcomes.
  - **Registered entity / business name** — only if there is enough defensible paid activity.
- Keep any gap/sabbatical entry short and truthful. State the cause plainly if the user wishes (e.g. a redundancy from a company strategy change is a structural fact, not a performance issue). Do not claim currency or activity the user did not actually maintain.
- **This checkpoint is mandatory and must be surfaced explicitly** — templates routinely omit the most-recent period, and a silently missing current entry is a logged failure mode. Confirm the Role #1 entry with the user before proceeding to Section 0.

## Workflow Overview

Work strictly section-by-section. After each section, end with the decision gate question and stop. Never proceed without explicit user approval.

| Section | What it does | Reference |
|---------|-------------|-----------|
| Pre-flight | Mandatory checkpoints incl. most-recent-entry / gap check (force-insert current entry as Role #1) | Inline (above) |
| Pre | Template selection (if Input 1 not yet chosen) | `references/pre-section-template-selection.md` |
| 0 | JD-to-Resume mapping | `references/section0-mapping.md` |
| 1 | Headline career roles | Inline (below) |
| 2 | Professional summary | `references/section2-summary.md` |
| 3 | Skills and expertise | `references/section3-skills.md` |
| 4 | Responsibilities (per role) | `references/section4-responsibilities.md` |
| 5 | Achievements (per role) | `references/section5-achievements.md` |
| 6 | Repeat Sections 4-5 for remaining roles | Same as 4-5 |
| Final | End-to-end coverage review across the whole resume (mandatory) | Inline (below) |

Read the appropriate reference file before starting each section.

## Live Working Document (mandatory)

The user cannot hold all the locked content in their head, and should never have to ask "what have we done so far?" Maintain a **live working document** that mirrors every locked decision as it is made.

- Keep a running, user-visible record (e.g. a "Tailored Content (in progress)" section in the tracking/deliverable file) containing: the headline, summary, skills grid, and each role's locked responsibilities and achievements.
- **Update it immediately after every lock** — each section, each role's responsibility paragraph, each role's achievement set. Do not batch updates; do not let it go stale.
- Mark in-progress items explicitly (e.g. "Role #4 — achievements: variant selection underway") so the document always reflects the true current state.
- Tell the user where this document is so they can open it for reference at any time.
- This is separate from the Final Step (the Cowork instruction set), which is produced only at the very end.

---

## Pre-Section: Template Selection (conditional)

Read `references/pre-section-template-selection.md` for the full procedure.

**When to run**: Only when the user has not yet chosen a resume template (Input 1) and instead provides a Google Drive folder of templates to evaluate.

**Summary**: Extract JD requirements, retrieve all templates from the folder, perform a quick keyword scan to rank them, then deep-review the top 3 using the same evidence-mapping methodology as Section 0. Present a ranked shortlist with strengths and gaps for each. The user selects the template to use. The JD requirements table produced here carries forward into Section 0.

**Skip when**: The user has already provided a specific template as Input 1.

---

## Section 0: JD-to-Resume Mapping

Read `references/section0-mapping.md` for the full procedure.

**Summary**: Extract a prioritized requirements map from the JD, map each requirement to verbatim evidence from Input 3, and identify explicit gaps. Output three tables (Priority Map, Evidence Map, Gaps). End with: "Proceed, or iterate further?"

---

## Section 1: Headline Career Roles

> **Model gate (mandatory):** Before starting this section, run the model-selection prompt from the "Model Selection" section above. Sections 1, 2, 4 and 5 are judgement-heavy and benefit from Opus. Do not proceed without the user confirming their model.

### Procedure

1. Review Inputs 1 and 3 for all role titles, functions, and positioning language.
2. Propose 3-5 candidate sets of "3 headline roles."
3. Present as a table with one row per set and one column per role.

### Rules
- Each role phrase: max 3 words.
- Every role must be evidenced in Inputs 1 or 3 (e.g., actual job titles, demonstrated functions, or clearly supported by career history).
- Include a brief rationale for each set explaining how it maps to the JD and the user's experience.
- If a proposed role uses JD language not directly evidenced (e.g., "Channel Technologist"), flag it and note the evidence gap so the user can decide.

### User Selection
- Ask the user to choose a set, mix-and-match across sets, or edit any of the role phrases.
- Confirm the final selection before proceeding.

### Decision Gate
End with: "Proceed, or iterate further?"

---

## Section 2: Professional Summary

Read `references/section2-summary.md` for the full procedure.

**Summary**: Draft two variants (Conservative and High-impact) within the agreed character limit, then run a mandatory coverage review against all Section 0 themes before proceeding. End with: "Would you like to revise the summary to address any of the gaps, or are you happy to proceed to Section 3?"

---

## Section 3: Skills and Areas of Expertise

Read `references/section3-skills.md` for the full procedure.

**Summary**: Extract JD-required skills, output a prioritized numbered list with evidence markers, identify missing and implied skills, then ask the user to confirm. End with two questions about missing/implied skills and whether output is satisfactory.

---

## Sections 4-5: Responsibilities and Achievements (Per Role)

Read `references/section4-responsibilities.md` and `references/section5-achievements.md`.

For each role, repeat this cycle:
1. State the role header
2. Ask for focus area (Leadership / Sales-Presales / Architecture / Combination)
3. Generate 3-6 options from Input 3 evidence
4. User selects top 3
5. Produce V1/V2a/V2b variants for each selected item
6. User selects preferred variant for each
7. For responsibilities: combine into a single paragraph within character limit
8. For achievements: output final bullets under 120 characters each
9. Present the complete role summary in deliverable format

Then proceed to the next role.

---

## Section 6: Repeat for Remaining Roles

Repeat Sections 4-5 for each subsequent role in the template.

---

## Role Summary Deliverable Format

After completing both responsibilities and achievements for each role, output a clean summary:

```
**Role #N: Title — Company, Location — Start to End**

**Responsibilities (combined paragraph):**
<Combined paragraph>

**Selected Achievements:**
- <Achievement 1>
- <Achievement 2>
- <Achievement 3>
```

No additional headings, commentary, or evidence blocks in the deliverable. Then ask: "Shall we proceed to the next role?"

---

## Final Coverage Review (mandatory — before the Cowork step)

Once all sections are complete, run a single end-to-end coverage review across the **entire assembled resume** (summary + skills + responsibilities + achievements + education), against **every** row from the Section 0 Step 1 priority map. This is the same kind of gate as the Section 2 coverage review, but run once over the whole document rather than the summary alone — it catches any Core or High requirement that fell through the cracks *between* sections.

Output one table:

| JD Theme (from Section 0 Step 1) | Priority | Addressed where? | Status |
|---|---|---|---|

Rules:
- Include **all** rows from the Section 0 Step 1 table. Do not cherry-pick or shorten the list.
- `Addressed where?` names the section(s) that carry the evidence (e.g. "Summary + Skills"; "Role #2 achievements"). For unmet themes: `Not addressed.`
- Use exactly these markers in `Status`: `✅ Yes`, `⚠️ Partial/Implicit`, `❌ No`.
- Be honest about partial coverage — if a theme is only implied, mark it `⚠️` not `✅`.

After the table:
- Summarise total `✅ / ⚠️ / ❌` counts, broken down by priority (Core / High / Medium).
- **Flag every Core or High theme still marked `❌` or `⚠️`** and state whether evidence exists in Inputs 1/3 to close it. For genuine gaps (no evidence), restate the `Not evidenced in provided materials—omit or supply proof?` position so the user can decide.
- Ask: "Would you like to address any of these remaining gaps before I compile the Cowork instruction set, or shall I proceed?"

Do not proceed to the Cowork step until the user responds.

## Final Step: Cowork Instruction Set

After the final coverage review is accepted, compile every change into a Cowork-ready instruction set. Format as specific find-and-replace instructions referencing the target Google Doc by name. Include proofreading corrections identified during the process.

---

## Writing Style

- Write concise, verb-led bullets with outcomes first where evidenced.
- Keep tense consistent per role (past tense for previous roles, present for current).
- No inline citations in resume output.
- Prefer impact-first phrasing (metric/outcome first, then what you did).
- Use plain language; avoid internal process jargon unless the user supplied it.

## ATS Compliance

After tailoring, use the [[ats-checker]] skill to audit the final resume against the JD for keyword matching, ATS parseability, and format compliance. This skill provides a scored report and prioritized fix list before you submit.

## Interaction Protocol

- Work strictly section-by-section.
- After each section, end with the exact decision gate question for that section and stop.
- Never proceed without explicit user approval.
- When the user says "proceed", move to the next section only.
- If the user wants to skip sections, respect that and jump ahead.

### Anti-skip guardrails (mandatory)

These exist because §3 was once collapsed — the candidate list and the user-selection step were merged into a pre-finalised recommendation, and the user's selection gate was silently skipped. See `process-quality-log.md`.

- **Track section state.** Treat every section as `Awaiting user selection` until the user *explicitly* approves it. A recommendation from you is NOT approval. Do not advance, and do not treat re-rendering your own recommendation as progress.
- **Propose ≠ select.** In selection-heavy sections (1, 3, 4, 5): present the options, then STOP and hand the floor to the user. A recommendation is allowed but must be clearly subordinate to an explicit "you choose" step — never presented as the outcome.
- **Re-anchor after interruptions.** If a side-task interrupts mid-section (e.g. capturing a new skill, a storage decision, changing a format spec), handle it, then explicitly restate which section is still open and what it is waiting on before doing anything else.
- **Log deviations.** When a gate is skipped or a step done incorrectly, record it in `process-quality-log.md` (deviation, root cause, guardrail) so the skill keeps improving.
- **Run the documented steps as written — do not self-streamline.** Execute each section's full documented procedure, including Step 3's V1/V2a/V2b variants in Sections 4 and 5. **Never propose or apply a "lighter," "quicker," or "streamlined" version of a mandatory step.** If the process feels heavy, that is not licence to shortcut it. Only the *user* may initiate a process simplification; until they do, the default is the full process. (This is a repeat failure mode — see `process-quality-log.md` entries #1 and #4.)

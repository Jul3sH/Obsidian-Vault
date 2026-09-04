---
type: reference
created: 2026-09-04
status: active
tags: [working-with-genai, admission, mental-models]
---

# MM: Admission Qualification

This is the Admission Qualification mental model: which tier of ceremony a
piece of work qualifies for before it starts - none, fast lane, or full. It
was created (4 Sep 2026) after an exempt compile session ended with "was a
gate missed?", showing the tiering rules were canonical but not reachable.
Read it whenever work is about to start and the required ceremony is unclear,
or when auditing whether a past session skipped a gate. The tier definitions
are owned by AGENTS.md (Deliverable-First rule and Admission Fast Lane), which
wins if this model disagrees with it.

**One-liner:** Ceremony is decided by the work's characteristics, not the
deliverable's type.

**Reach for it when:** any piece of work is about to start and it is unclear
whether it needs no record, a fast-lane record, or full definition - or when
asking after the fact whether a gate was missed.

**Position in the chain:** step 0, before the chain runs. Admission qualifies
the work and hands an admitted piece of work at the right tier to
[[mm-work-types]]. Full chain: [[genai-task-workflow]].

## Key Takeaways

- Three tiers, tested in order, stop at the first match: exempt, fast lane,
  full ceremony.
- Enabler vs story vs task never decides ceremony - all three get full
  definition when definition is due. The tiers cut across deliverable type.
- Admission is Taste work: minimise it, batch it, and never split it from
  execution across sessions.
- Exempt work may still be logged by choice (a retroactive record for time and
  tokens); that is optional calibration, not a required gate.

## Principles

The three-tier test, in order:

| Tier | Qualifies when | Ceremony |
|---|---|---|
| **Exempt** | Routine system operations (compiling, logging, mirroring, index updates), quick factual or conversational questions, or work flagged as exploratory or thinking-aloud | None. No deliverable record, no Prompt Zero |
| **Fast lane** | Real deliverable work that is machine-executed (Julian's role: brief + review), low blast radius, and fits one 2h box | One sitting: terse record file (purpose block, 2-3 binary done-criteria, load-bearing assumption, named verifier, Time Log), execution in the same session |
| **Full ceremony** | Anything else: Julian-executed, high blast radius, multi-box, or a why that cannot be stated in a sentence | `/define-*` skill + Prompt Zero before detailed work begins |

- **The test runs on the work, not the label.** The first question is "is this
  producing something at all?" - exempt work is housekeeping or conversation,
  not delivery. Only past that does the fast-lane test apply.
- **Deliverable type is orthogonal to ceremony.** Story, enabler, and task
  describe what the output is; the tier describes how the work starts. No type
  bypasses definition and no type forces it.
- **Unchanged in every tier that produces output:** time and token logging,
  adversarial coverage, sampling-scope sign-off, and the workflow-log row.
- **Admission spends Julian's judgement, so spend it once.** Splitting
  admission from execution across sessions doubles the cost through context
  decay (evidence: the 3 Sep D2 admission failure in
  [[genai-task-workflow-log]]).

## Guidelines

- Run the tiers in order and stop at the first that matches; do not argue a
  borderline case upward for safety - the fast lane exists precisely to stop
  ceremony outgrowing the work.
- State the tier out loud at the start of the session ("this is exempt as a
  compile", "fast-laning this"), so nobody has to reverse-engineer afterwards
  which rule governed.
- If effort on exempt work turns out worth keeping, write a retroactive record
  in `wiki/deliverables/` for the Time Log - a record, not a ceremony.
- If work drifts mid-session from exempt into producing something substantive,
  re-run the test at the point of drift.

## Limitations

Says nothing about whether the work is worth doing at all (the funnel and WSJF
own that), what type of work it is ([[mm-work-types]]), or how it is checked
([[mm-verification]]). The tier definitions and exemption list are AGENTS.md
doctrine compressed here for reach; on any disagreement AGENTS.md wins and
this file is corrected.

## Detail

AGENTS.md (Deliverable-First Working Rule and its exemption list; Admission
Fast Lane), [[genai-task-workflow]] (step 0 and the coverage table),
[[genai-task-workflow-log]] (admission failures as they accumulate).

## Evidence

| Date | Event | Lesson in action | Source |
|------|-------|-------------------|--------|
| 2026-09-04 | An exempt compile session (BA Avios note into the wiki) closed with "was the ceremony skipped because it was fast-tracked, or because gates were missed?" - and a first guess that enablers bypass definition while stories need it. Three clarifying answers were needed to untangle exempt vs fast lane vs type | The tiers were canonical in AGENTS.md but had no reach-for layer, and deliverable type was intuitively (wrongly) doing the work of the tier test. State the tier at session start; type never decides ceremony | [[airmiles-mental-model]], this model's creation |

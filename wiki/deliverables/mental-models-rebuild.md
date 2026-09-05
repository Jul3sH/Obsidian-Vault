---
type: task
project:
workstream: performance
hours: n/a (executed under gate waiver, unestimated)
created: 2026-08-26
status: done
jira-key:
value-rationale:
---

# Mental Models Rebuild

> **Purpose block.** This is the retrospective record of the 26 Aug 2026 mental-models rebuild: the audit of all 303 lessons-learnt source files, the creation of 38 six-slot `mm-*.md` models across working-with-others, working-with-yourself, and the-human-mind, and the capture of 13 TTI engagement lessons into them. It was created after completion because the work ran under a Deliverable-First gate waiver and therefore had no deliverable file to carry its Time and Token Log; this file supplies that record so the effort feeds the estimation baseline. Read it when calibrating future Claude-only work, or when tracing where the model set came from.

## Prompt Zero

**Overridden 26 Aug 2026 (dated record per the Deliverable-First rule).** Julian directed execution without `/define-task` or `/prompt-zero`: "as this task will be done entirely by Claude I want to just do it." Scope control was carried instead by staged approvals in-session: the fix design (two-tier, both folders, evidence in the model file), the 37-model set with named slugs, the orphan recommendation (38th model plus filings), and the 13 TTI lessons were each approved by Julian before execution. The systemic fix for this class of work is the funnel item **Claude-only work admission lane** in [[funnel|the project funnel]].

## What Was Done

1. **Audit:** all 303 lessons-learnt source files in `raw/_processed/` classified against the existing articles (230 accurate, 32 partial, 26 missed, 14 out-of-scope, 1 miscaptured).
2. **Build:** 38 `mm-*.md` models in the six-slot format, each with an evidence table linking its original source lessons; existing articles kept untouched as the detail tier; `the-human-mind/` folder created.
3. **Verify:** adversarial fidelity pass (30-row sample against sources; 3 distorted rows corrected, 24 link defects fixed) and adversarial coverage pass (all 288 in-scope lessons confirmed landed; 26 orphans filed, 5 double-claims trimmed).
4. **TTI lessons:** 13 dated evidence rows from the TTI engagement written across 8 models, including a new Evidence section on [[mm-verification]]. No new model was needed.
5. **Indexes:** [[mental-models-index]] and both folder indexes rebuilt two-tier; ops log rows written throughout.

Out of scope, parked: 14 out-of-scope lessons awaiting a relationships/wellbeing/career pass; one untranscribed voice memo ("the need for clear, validated goals") awaiting Julian's re-record-or-discard call.

## Time and Token Log

Machine effort in tokens, Julian's effort in focused minutes (self-reported, prompted by the UserPromptSubmit time-and-token-log hook). Only Julian's minutes roll into Actual hrs in the [[estimation-baseline|Estimation Baseline]]; tokens go in that row's Notes.

| Date | Segment | Who | Tokens / Minutes | Notes |
|------|---------|-----|------------------|-------|
| 2026-08-26 | Coverage audit: 6 Sonnet subagents over 303 source lessons | Machine (Claude) | 1,062,228 tokens | Produced the merged coverage matrix (session scratchpad) |
| 2026-08-26 | Model build: 6 Sonnet subagents, 37 files | Machine (Claude) | 1,006,278 tokens | Six-slot format, evidence tables with source links |
| 2026-08-26 | Adversarial verify: 2 Sonnet subagents (fidelity + coverage) | Machine (Claude) | 343,678 tokens | Verdicts: SOUND-WITH-FIXES / COMPLETE-WITH-GAPS; all fixes applied |
| 2026-08-26 | Remediation: 1 Sonnet subagent (26 orphan rows, 5 double-claim trims) | Machine (Claude) | 163,780 tokens | |
| 2026-08-26 | Orphan resolution: 1 Sonnet subagent (mm-assertiveness-is-professional + 7 filings) | Machine (Claude) | 110,300 tokens | 38th model; all 288 in-scope lessons covered |
| 2026-08-26 | Reviews and decisions: fix design, model-set sign-off, orphan decision, TTI lesson reviews | Julian | 30 min | Single self-reported total for the session's attended segments |
| 2026-08-27 | TTI lessons review session: all 13 rows worked through with Julian one by one - rewritten plainer and in his voice, 1 cut, 1 promoted into the new [[mm-stories-arent-evidence]] model (built and indexed in the same session); index two-tier explainers and the misfiled the-human-mind folder fix also done in this sitting | Julian | not reported at close (27 Aug) | Final TTI count: 12 evidence rows + 3 new models (stories-arent-evidence, eggs-in-one-basket, the mm-routing drafting-workflow row) + 1 feedback memory; set now 40 models |
| 2026-08-27 | Drafting-workflow validation (Sonnet agent over comms log + session transcripts) | Machine (Claude) | 155,749 tokens | Verdict partially supported; row on mm-routing + feedback-hold-the-pen-voice-messages memory |
| 2026-08-27 | **Complete, reviewed, closed.** Final totals | - | Julian 30 min + review session (minutes not reported); machine 2,842,013 subagent tokens | Fable main-session usage not metered, additional to the subagent figure |

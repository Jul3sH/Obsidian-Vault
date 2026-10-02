---
type: deliverable
kind: task
created: 2026-10-02
status: in-progress
size: 1
lane: fast-lane
tags: [deliverable, notebooklm, youtube, ai-learning]
---

# NBJ YouTube Notebooks

## Purpose

The ongoing fast-lane record for loading Nate B Jones's YouTube videos into NotebookLM with `/youtube-notebook`, one row per run. It exists so the machine effort of each run is logged against a deliverable.

## Status

**As of 2 Oct 2026:** Aug & Sep 2026 run complete, reconciliation PASS. Awaiting Julian's usability confirmation (criterion 3).

## Brief (Admission Fast Lane, agreed 2026-10-02)

**Why (one sentence):** keep Julian's NotebookLM study set of Nate B Jones's videos current, period by period, so he can learn from it.

**Done-criteria (per run):**
1. Enumeration verification passes (dual-path, zero genuine gaps).
2. Four-way reconciliation matches the manifest: sources, briefing artifacts, downloaded files, file headers.
3. Julian confirms the notebook is usable.

**Load-bearing assumption:** NotebookLM's native briefing docs are good enough to learn from without content review. Julian confirmed 2 Oct 2026: no review of briefings needed.

**Verifiers:** criteria 1-2 are checked mechanically by the skill's `run-report.json`; criterion 3 by Julian.

## Runs

| Date | Notebook | Window | Videos | Verification | Reconciliation |
|------|----------|--------|--------|--------------|----------------|
| 2026-10-02 | NBJ August & September 2026 | 1 Aug - 30 Sep 2026, long-form only | 36 | PASS, 0 gaps | PASS: 36/36 sources, briefings, files, headers. Notebook `be67caba-9804-4abf-a7f9-f47a3c7c9bb6`; files in `~/Downloads/NBJ August & September 2026 Briefings/` |

## Time and Token Log

| Date | Type | Effort | Notes |
|------|------|--------|-------|
| 2026-10-02 | Machine (interactive Claude session) | 169,143 tokens | Output 19,102 + cache-write 150,041 across 36 assistant messages; cache reads 3.0M not counted. Covers interview, enumeration, build orchestration and bookkeeping. NotebookLM briefing generation runs on Google's side and is not in this figure |

## Session Synopsis

## Document Log

| Date | Change |
|------|--------|
| 2026-10-02 | Created under the Admission Fast Lane for the Aug & Sep 2026 run |

---
type: task
workstream: performance
size: 2
hours: 5-8h
created: 2026-09-03
status: done
closed: 2026-09-03
jira-key: TBD (create on next /jira-sync)
---

# Routing Work System

This is the retroactive deliverable record for the routing-work system built on
3 Sep 2026: the journal of work routed to AI, the mental model that gives it a
vocabulary, and the workflow page that chains the models together. It was created
after the fact because the work grew out of a lookup question mid-session and the
Deliverable-First gate was never applied. It is read for the completion record
and the Time Log; the system itself lives in
`wiki/performance/working-with-genai/`.

> ⚠ As of 3 Sep 2026: **Prompt Zero bypassed.** The work escalated from a
> question into substantive build inside one session and the gate did not fire.
> Recorded here rather than waived - at this size there is no waiver. The
> grounding brief exists only as the session dialogue.

## What was delivered (3 Sep 2026)

- [[genai-task-workflow]] - the end-to-end chain on one page (work types →
  verification → routing → steering)
- [[mm-work-types]] - seven work types classified by check profile
- [[routing-log]] - the journal, seeded with three rows (two TTI, one BAU Kanban)
- Chain position lines updated across mm-verification / mm-routing /
  mm-steering / mm-blast-radius / mm-model-adaptation; Evidence moved out of
  mm-routing; folder index updated
- Write trigger added to AGENTS.md (routing-log row in the same operation as the
  Time Log row); Reuse Before Build rule added to AGENTS.md
- SYS-8 row in [[systems-register]] with adoption test
- Same-session adjacent fixes: systems-register backfill (SYS-4 to SYS-7), retro
  moved to Sunday with a SessionStart hook, two funnel rows parked (ceremony
  trigger audit, workflow-shapes catalogue)

**Deliberately not built:** the read trigger inside the `/define-*` skills -
deferred until the log has rows that could change a routing decision.

## Time Log

| Date | Who | Effort | Note |
|------|-----|--------|------|
| 2026-09-03 | Julian | 60 focused minutes | Full session: design dialogue, category debate, confirmations |
| 2026-09-03 | Claude (interactive session) | 819,239 tokens | Output 147,321 + cache-write 671,918 per AGENTS.md rule; cache reads (21.4M) excluded. Session 8eb0e269, measured from transcript JSONL |

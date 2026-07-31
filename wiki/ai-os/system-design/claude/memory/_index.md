---
type: index
updated: 2026-07-31
---

# Memory

> *Cross-session memory for Claude. Persists user profile, active project state, learned corrections, and operational pointers across conversations.*

## Articles

- [[memory-convention|Memory Convention]] — types, file format, loading rule, why this split, what not to store
- [[memory-operations|Memory Operations: Store, Inject, Recall]] — the three operations that govern memory; the two-tier principles-and-lessons recall design; the no-vector-DB-yet rationale
- [[memory-system-explained|Memory System Explained]] — plain-language / ownership view: what a memory is (vs skills and tasks), where the rules live (CLAUDE.md not AGENTS.md), how awareness persists across sessions, and the two-key create process. Learner-facing companion to the two docs above.
- [[memory-observational-layer|Observational Memory Layer]] - assessment of whether a live observational capture layer is needed; finds the JSONL session transcripts already provide the full record, so retrospective analysis is a periodic script rather than a runtime component.

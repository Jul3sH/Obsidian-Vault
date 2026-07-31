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
- [[memory-observation-layer|Observation Layer]] - the **capture** concept: what an observation layer is, when it is justified, and the assessment finding it unnecessary here because JSONL transcripts already hold the full record. Includes the terminology note against conflating it with semantic search.
- [[memory-semantic-search|Semantic Search]] - the **retrieval** concept: the five-criteria test for justifying a vector index in any agentic OS, scoring of the commonly-cited use cases, and the narrow set that applies here. Paired with the observation layer article; read both before deciding.

---
type: index
updated: 2026-07-31
---

# Memory

> *Cross-session memory for Claude. Persists user profile, active project state, learned corrections, and operational pointers across conversations.*

## Articles

- [[memory-convention|Memory Convention]] — types, file format, loading rule, why this split, what not to store
- [[memory-operations|Memory Operations]] - how the four pillars are configured in this environment (scheduled injection only, no vector index), the two-tier principles-and-lessons recall design, and the wiki-corpus revisit threshold
- [[memory-system-explained|Memory System Explained]] — plain-language / ownership view: what a memory is (vs skills and tasks), where the rules live (CLAUDE.md not AGENTS.md), how awareness persists across sessions, and the two-key create process. Learner-facing companion to the two docs above.

## Related

Generic memory-systems theory is reference material and lives under `wiki/technology/Memory systems/`, not here. The model is [[memory-pillars]] (Capture, Storage, Injection, Recall); the enabler articles are [[memory-observation-layer]] (Capture), [[memory-curated-index]] (Recall, write-time) and [[memory-semantic-search]] (Recall query-time, and triggered Injection). See also [[ai-memory-paradigms]].

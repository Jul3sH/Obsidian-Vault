---
type: index
updated: 2026-07-31
---

# Memory

> *Cross-session memory for Claude: the **behavioural branch** of the Storage pillar. Persists the user profile and learned behavioural corrections across conversations. Project and deliverable state live in the wiki, not here.*

## Articles

- [[memory-convention|Memory Convention]] — types, file format, loading rule, why this split, what not to store
- [[memory-operations|Memory Operations]] - how the four pillars are configured in this environment (scheduled injection only, no vector index), the two-tier principles-and-lessons recall design, and the wiki-corpus revisit threshold
- [[memory-system-explained|Memory System Explained]] — plain-language / ownership view: what a memory is (vs skills and tasks), where the rules live (CLAUDE.md not AGENTS.md), how awareness persists across sessions, and the two-key create process. Learner-facing companion to the two docs above.

## Related

The adopted reasoning frame is recorded at [[memory-model-adoption]]. Generic memory-systems theory is reference material and lives under `wiki/technology/Memory systems/`, not here. The model overview is [[memory-pillars]], with one article per pillar: [[memory-capture]], [[memory-storage]], [[memory-injection]], [[memory-recall]]. The feature catalogue is [[memory-features]], including [[memory-features#Curated Index Retrieval|curated index retrieval]] for Recall (write-time) and [[memory-features#Semantic Search|semantic search]] for Recall (query-time) and triggered Injection. See also [[wiki-vs-openbrain|AI Memory Paradigms]].

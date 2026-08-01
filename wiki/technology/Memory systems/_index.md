---
type: index
updated: 2026-08-01
---

# Memory Systems

> *How agent memory systems are structured: the functional model, the technologies that implement it, and how the main products compare. Reference material, not a description of what runs here.*

## Reading order

These build on each other. Read top to bottom the first time; the overview in (1) supplies the vocabulary the rest depend on.

**The model**

1. [[memory-pillars|The Four Pillars of Memory Systems]] - **start here.** The overview: dependency order, the pillar-versus-enabler-versus-capability distinction, the amendment splitting Capture out of Simon Scrapes' three pillars, correlation with other published memory models, and the cross-pillar compaction analysis.
2. [[memory-capabilities|Memory Capabilities]] - the demand-side companion to (1). What you *get* rather than what the system *does*. Ten catalogued capabilities, each spanning two or more pillars, with the rule that pillars participate in a capability but never own it. Open list.

**The four pillars** (one article each, in dependency order; each carries its sub-types and links to the capabilities it participates in)

3. [[memory-capture|Capture]] - getting events into a durable record. Three modes plus an event-triggered firing condition. The capability it produces is the **Observation Layer**.
4. [[memory-storage|Storage]] - what is kept and how it is organised. Two independent axes: canonical vs behavioural, and form crossed with retention.
5. [[memory-injection|Injection]] - deciding to look at all, and placing material in context. Scheduled vs triggered, and the four-rung trigger hierarchy. The pillar most systems under-build.
6. [[memory-recall|Recall]] - finding the right material. Write-time vs query-time.

**The enablers** (technologies that implement a pillar)

7. [[memory-curated-index|Curated Index Retrieval]] - enabler for **Recall (write-time)**. The hand-authored index and wikilink scheme: the hop chain, why one-line descriptions are the ranking function, and its dominant failure mode of invocation.
8. [[memory-semantic-search|Semantic Search]] - enabler for **Recall (query-time)** and **Injection (triggered)**. The five-criteria test for justifying a vector index, and scoring of the commonly-cited use cases.

**The wider debate**

9. [[wiki-vs-openbrain|Wiki vs OpenBrain: Write-Time vs Query-Time]] - the paradigm fork underneath Recall's two sub-types: compile on ingest, or synthesise on query. Where each wins, where each breaks, and the hybrid resolution.
10. [[openbrain-vs-agentic-os|OpenBrain (OB1) vs Agentic OS Memory]] - two query-time database systems compared: multi-tool bus versus multi-client runtime, faithful store versus Haiku pre-compile.

**Products scored against the model** (one file per system, scoring only; each links to its architecture doc)

11. [[pillars-claudeclaw|ClaudeClaw]] - the only system assessed with genuine triggered injection; aggressively curated capture; actually in use.
12. [[pillars-agentic-os|Agentic OS]] - strongest storage and recall assessed, scheduled injection only, and recorded as "built but never ingested".
13. [[pillars-memsearch|MemSearch]] - the only system assessed with genuine cross-agent federation; markdown-canonical/vector-disposable storage; a per-turn nudge that is not true triggered injection.
14. [[pillars-mempalace|MemPalace]] - the only system that directly answers the compaction question (a PreCompact hook flushes before every compaction); verbatim storage, the opposite pole from the other three; no injection layer at all.

**Reviews**

- [[memory-systems-taxonomy-codex-review-2026-08-01]] - Review of the Memory Systems folder against the use case, capability, feature distinction.

## Related, filed elsewhere

- [[postgres-pgvector|Postgres, pgvector, PGLite and Supabase]] - what each storage term actually means. Only one of them is a database engine. Lives at `wiki/technology/` root as general storage reference.
- [[memory-model-adoption|Memory Model (Adopted)]] - the decision record for adopting the four-pillar frame in this environment. Lives in AI OS, because it records what is actually running rather than how the technology works.

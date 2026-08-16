---
type: index
updated: 2026-08-02
---

# Memory Systems

> *How agent memory systems are structured: the functional model, the technologies that implement it, and how the main products compare. Reference material, not a description of what runs here.*

## Reading order

These build on each other. Read top to bottom the first time: start with the failure modes, then the actor journeys, capabilities, features, and architecture.

**The recall layer**

- [[mm-memory-pillars|MM: Memory Pillars]] - the six-slot mental model compressing this folder: read it first if you know the material, last if you do not.

**The model**

1. [[memory-challanges|Memory Challenges]] - **start here.** Recurring memory failure modes, mapped to capabilities, features, and platform responses.
2. [[memory-use-cases|Memory Use Cases]] - memorable actor-outcome journeys explaining why memory is needed.
3. [[memory-capabilities|Memory Capabilities]] - the demand-side companion to the use cases. What you *get* rather than what the system *does*. Sixteen catalogued capabilities, each linked to a primary use case and representative features.
4. [[memory-features|Memory Features]] - concrete mechanisms and feature families observed across products, mapped to architecture functions and capabilities.
5. [[memory-pillars|The Four Pillars of Memory Systems]] - the architecture overview: dependency order, the pillar-versus-enabler-versus-capability distinction, the amendment splitting Capture out of Simon Scrapes' three pillars, correlation with other published memory models, and the cross-pillar compaction analysis.

**The four pillars** (one article each, in dependency order; each carries its sub-types and links to the capabilities it participates in)

6. [[memory-capture|Capture]] - getting events into a durable record. Three modes plus an event-triggered firing condition. The capability it produces is the **Observation Layer**.
7. [[memory-storage|Storage]] - what is kept and how it is organised. Two independent axes: canonical vs behavioural, and form crossed with retention.
8. [[memory-injection|Injection]] - deciding to look at all, and placing material in context. Scheduled vs triggered, and the four-rung trigger hierarchy. The pillar most systems under-build.
9. [[memory-recall|Recall]] - finding the right material. Write-time vs query-time.

**The wider debate**

10. [[wiki-vs-openbrain|Wiki vs OpenBrain: Write-Time vs Query-Time]] - the paradigm fork underneath Recall's two sub-types: compile on ingest, or synthesise on query. Where each wins, where each breaks, and the hybrid resolution.
11. [[openbrain-vs-agentic-os|OpenBrain (OB1) vs Agentic OS Memory]] - two query-time database systems compared: multi-tool bus versus multi-client runtime, faithful store versus Haiku pre-compile.

**Products scored against the model** (one file per system, scoring only; each links to its architecture doc)

12. [[pillars-agile-os|Agile OS]] - the current Obsidian Vault memory system: strong curated storage and navigation, weak triggered injection, no query-time index.
13. [[pillars-claudeclaw|ClaudeClaw]] - the only system assessed with genuine triggered injection; aggressively curated capture; actually in use.
14. [[pillars-agentic-os|Agentic OS]] - strongest storage and recall assessed, scheduled injection only, and recorded as "built but never ingested".
15. [[pillars-memsearch|MemSearch]] - the only system assessed with genuine cross-agent federation; markdown-canonical/vector-disposable storage; a per-turn nudge that is not true triggered injection.
16. [[pillars-mempalace|MemPalace]] - the only system that directly answers the compaction question (a PreCompact hook flushes before every compaction); verbatim storage, the opposite pole from the other three; no injection layer at all.

**Reviews**

- [[memory-systems-taxonomy-codex-review-2026-08-01]] - Review of the Memory Systems folder against the use case, capability, feature distinction.

## Related, filed elsewhere

- [[postgres-pgvector|Postgres, pgvector, PGLite and Supabase]] - what each storage term actually means. Only one of them is a database engine. Lives at `wiki/technology/` root as general storage reference.
- [[memory-model-adoption|Memory Model (Adopted)]] - the decision record for adopting the four-pillar frame in this environment. Lives in AI OS, because it records what is actually running rather than how the technology works.

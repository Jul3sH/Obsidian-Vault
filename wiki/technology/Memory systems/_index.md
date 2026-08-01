---
type: index
updated: 2026-08-01
---

# Memory Systems

> *How agent memory systems are structured: the functional model, the technologies that implement it, and how the main products compare. Reference material, not a description of what runs here.*

## Reading order

These build on each other. Read top to bottom the first time; the model in (1) supplies the vocabulary the rest depend on.

**The model**

1. [[memory-pillars|The Four Pillars of Memory Systems]] - **start here.** Capture, Storage, Injection, Recall, each with two sub-types; the pillar-versus-enabler distinction; and the amendment splitting Capture out of Simon Scrapes' three pillars.

**The enablers** (technologies that implement a pillar, in pillar order)

2. [[memory-observation-layer|Observation Layer]] - enabler for **Capture**. What counts as one, when it is justified, and three hypotheses that would have required one, all tested and failed.
3. [[memory-curated-index|Curated Index Retrieval]] - enabler for **Recall (write-time)**. The hand-authored index and wikilink scheme: the hop chain, why one-line descriptions are the ranking function, and its dominant failure mode of invocation.
4. [[memory-semantic-search|Semantic Search]] - enabler for **Recall (query-time)** and **Injection (triggered)**. The five-criteria test for justifying a vector index, and scoring of the commonly-cited use cases.

**The wider debate and the products**

5. [[wiki-vs-openbrain|Wiki vs OpenBrain: Write-Time vs Query-Time]] - the paradigm fork underneath Recall's two sub-types: compile on ingest, or synthesise on query. Where each wins, where each breaks, and the hybrid resolution.
6. [[openbrain-vs-agentic-os|OpenBrain (OB1) vs Agentic OS Memory]] - two query-time database systems compared: multi-tool bus versus multi-client runtime, faithful store versus Haiku pre-compile.

## Related, filed elsewhere

- [[postgres-pgvector|Postgres, pgvector, PGLite and Supabase]] - what each storage term actually means. Only one of them is a database engine. Lives at `wiki/technology/` root as general storage reference.
- [[memory-model-adoption|Memory Model (Adopted)]] - the decision record for adopting the four-pillar frame in this environment. Lives in AI OS, because it records what is actually running rather than how the technology works.

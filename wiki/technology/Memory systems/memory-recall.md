---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: pillar
pillar: recall
---

# Recall

> *The fourth pillar of [[memory-pillars|the four-pillar model]]: finding the right material in the store. Depends on [[memory-storage]]; invoked by [[memory-injection]]. Recall finds; Injection decides to look. Excellent Recall with no Injection is a system nobody queries.*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **Recall divides on when the retrieval signal is computed:** write-time (authored in advance) versus query-time (computed from content at query). This is the same fork as [[wiki-vs-openbrain|write-time vs query-time]] paradigms.
- **The decisive difference is not quality, it is who pays and when.** Write-time front-loads human judgement; query-time defers it to the machine.
- **Progressive disclosure is the convergent design.** Three of four systems assessed independently built a tiered ladder that escalates from cheap summary search to expensive raw transcript only when needed.
- **Recall is not Injection.** The most common way a good Recall implementation fails is that nothing invokes it.
- **A hybrid is usually stronger than either pole**, because write-time and query-time fail differently: one loses on invocation and authoring cost, the other on precision and drift.

---

## The two types

| | **Write-time recall** | **Query-time recall** |
|---|---|---|
| Signal authored | In advance, by a human or agent | Computed at query, from the content |
| Typical form | Index descriptions, tags, curated links | Embeddings, keyword match |
| Cost profile | Costly on write, near-free at query | Near-free on write, cost recurs per query |
| Wins on | Precision, transparency, zero infrastructure | Coverage, and finding material nobody indexed |
| Fails when | Nothing invokes it, or the corpus outgrows authoring effort | Similarity approximates intent badly; drift on edit |
| Enabler | [[memory-curated-index]] | [[memory-semantic-search]], keyword search |

**The decisive difference is not quality, it is who pays and when.** Write-time recall front-loads human judgement; query-time recall defers it to the machine. A hybrid - a curated index over the canonical branch plus a computed index over raw captured material - is usually stronger than either alone because they fail differently.

**Recall and Injection are distinct.** Recall finds material; [[memory-injection|Injection]] decides to look and puts the result in context. A system can have excellent recall and still fail entirely, because nothing invokes it. That is the single most common failure pattern across the systems assessed.

## Capabilities and features across systems

Transposed from the four product scorecards. All four implement query-time recall; they differ in ranking sophistication and escalation design.

| Capability | Systems | Detail |
|---|---|---|
| **Dense vector similarity search** | All four | ClaudeClaw (`gemini-embedding-001`, cosine > 0.3), agentic-os (BGE-M3, 1024-dim, L2-normalised), MemSearch, MemPalace (ChromaDB default) |
| **Hybrid dense + sparse with rank fusion** | MemSearch | Dense vector plus BM25 sparse, combined via reciprocal rank fusion (RRF) reranking - the most sophisticated ranking step assessed |
| **Hybrid vector + full-text** | agentic-os | BGE-M3 vector search plus Postgres full-text keyword search |
| **Keyword fallback when embeddings unavailable** | ClaudeClaw | FTS5 mirror kept in sync by triggers; degrades to LIKE if needed, so recall never hard-fails on a missing embedding provider |
| **Progressive disclosure / tiered escalation** (stop at the cheapest rung that answers the question) | agentic-os, MemSearch, ClaudeClaw | agentic-os: search → expand → transcript. MemSearch: search → expand → transcript. ClaudeClaw: summaries first, raw `conversation_log` only when keyword-triggered. Convergent design across independent products |
| **Structural scoping of the search space** | MemPalace | Wings/Rooms/Drawers hierarchy means a search can be scoped to a person, project, or topic rather than run flat |
| **Multi-tenant scope filtering on every query** | agentic-os | `private`/`client`/`team`/`system` predicate applied to every search, enforced in code and database |
| **Per-agent recall isolation with a shared tier** | ClaudeClaw | Scoped to calling agent plus explicitly shared memories; a `/keep-shared` toggle opts back into cross-agent recall, read per-turn without restart |
| **Live index maintenance** | MemSearch (file watcher), agentic-os (`memory-watch-start.js`) | Files edited outside a session become searchable without waiting for the next capture cycle |
| **Incremental indexing via content hashing** | MemSearch, agentic-os | SHA-256 skips unchanged content, making frequent re-indexing cheap |
| **Cross-agent federated recall** | MemSearch only | One memory store queried across Claude Code, Codex CLI, OpenClaw and OpenCode - the only working instance of federation among the four |
| **Search-before-answer protocol** (recall enforced by instruction rather than by mechanism) | MemPalace | The `mempalace-recall` skill instructs the agent to search before answering anything that may be filed. Protocol-driven, so its reliability is bounded by trigger option 2 - see [[memory-injection]] |
| **Published retrieval benchmark** | MemPalace | 96.6% R@5 on LongMemEval, zero API calls |

## Assessment of one environment

**Recall here is write-time only:** a hand-authored index hierarchy plus bare wikilinks, with no query-time index over either the wiki corpus or the JSONL transcripts.

Two separate decisions, reached independently and for different reasons:

- **Over the wiki corpus (~38 lesson docs):** no vector index. The curated `_index` descriptions plus `[[wikilinks]]` already form a precise retrieval layer at that scale. Revisit trigger: ~100-150 docs. See [[memory-curated-index]].
- **Over the JSONL transcript corpus:** narrowly justified but marginal, failing on query frequency (roughly 25 provenance queries in ten weeks). See [[memory-semantic-search]].

**The sharper finding is that Recall quality was never the constraint.** The curated index is precise when used; it was invoked in 11% of sessions. That is an [[memory-injection|Injection]] failure, not a Recall failure, and no improvement to ranking would have fixed it.

## Related

- [[memory-pillars]] - the four-pillar model overview
- [[memory-injection]] - the pillar that invokes Recall; the most common reason good Recall fails
- [[memory-storage]] - the form axis (synthesise-at-ingest vs store-faithfully) is this same fork seen from the write side
- [[memory-curated-index]] - enabler for write-time recall
- [[memory-semantic-search]] - enabler for query-time recall, and the only practical enabler of triggered injection
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from
- [[wiki-vs-openbrain|AI Memory Paradigms]] - the write-time versus query-time fork in its original framing

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
- **Three retrieval signals exist, not one: semantic, keyword and entity.** They fail differently, which is why mature systems run several and fuse the rankings. **Entity retrieval is the one most systems lack** - only MemPalace implements it, via a temporal knowledge graph that can answer what was true at a past date.

---

## The two types

| | **Write-time recall** | **Query-time recall** |
|---|---|---|
| Signal authored | In advance, by a human or agent | Computed at query, from the content |
| Typical form | Index descriptions, tags, curated links | Embeddings, keyword match |
| Cost profile | Costly on write, near-free at query | Near-free on write, cost recurs per query |
| Wins on | Precision, transparency, zero infrastructure | Coverage, and finding material nobody indexed |
| Fails when | Nothing invokes it, or the corpus outgrows authoring effort | Similarity approximates intent badly; drift on edit |
| Feature family | [[memory-features#Curated Index Retrieval|curated index retrieval]] | [[memory-features#Semantic Search|semantic search]], keyword search |

**The decisive difference is not quality, it is who pays and when.** Write-time recall front-loads human judgement; query-time recall defers it to the machine. A hybrid - a curated index over the canonical branch plus a computed index over raw captured material - is usually stronger than either alone because they fail differently.

**Recall and Injection are distinct.** Recall finds material; [[memory-injection|Injection]] decides to look and puts the result in context. A system can have excellent recall and still fail entirely, because nothing invokes it. That is the single most common failure pattern across the systems assessed.

## Multi-signal retrieval: the three signals and their fusion

Write-time versus query-time answers *when the signal is computed*. A separate question is *what kind of signal it is* - and mature systems run several in parallel rather than picking one.

> **Source note.** The three-signal framing and the token-efficiency figures below come from Mark Kashef's memory model, quoted second-hand rather than read from source. The mechanisms themselves are verified against product source; the efficiency claim is not.

| Signal | Finds by | Strength | Blind spot |
|---|---|---|---|
| **Semantic** | Meaning. Search "logins", find "authentication" | Recovers material whose wording you cannot guess | Approximates intent; similarity is not relevance |
| **Keyword** | Exact match | Fast, simple, reliable, no embedding dependency | Misses everything phrased differently |
| **Entity** | Connections. "Supabase" mentioned across 50 conversations, all linked | Answers questions about a *thing* rather than a *phrase*, and survives rewording entirely | Only as good as entity extraction; needs a graph to traverse |

**They fail differently, which is the whole argument for running all three.** Semantic search misses exact identifiers; keyword search misses paraphrase; neither can answer "everything we ever said about Supabase" without retrieving fifty separate results and hoping the ranking cooperates.

**Rank fusion is what makes combining them affordable.** Rather than concatenating three result sets and paying for all of them, fusion (typically reciprocal rank fusion) interleaves the rankings and takes the top slice. The claimed efficiency is roughly **7,000 tokens versus 25,000 for brute-force retrieval at equivalent accuracy** - the saving comes from not passing three full result sets into context.

### Coverage across the systems assessed

| Signal | Who implements it |
|---|---|
| **Semantic** | All four |
| **Keyword** | MemSearch (BM25 sparse), agentic-os (Postgres full-text), ClaudeClaw (FTS5, as fallback) |
| **Entity** | **MemPalace only** - a temporal entity-relationship knowledge graph, see below. ClaudeClaw extracts `entities[]` at ingest but folds them into the embedding text rather than exposing an entity-first query path |
| **Rank fusion** | MemSearch (RRF over dense + sparse). agentic-os combines vector and full-text but the fusion method is not documented in its architecture doc |

**No assessed system runs all three signals with fusion across them.** MemSearch fuses two (semantic + keyword); MemPalace has the third (entity) but does not fuse it with the others. The full three-signal-plus-fusion pattern is an aspiration in the source material, not something observed working in these four products.

### What a temporal entity-relationship knowledge graph actually is

The term is used above without unpacking, and each word in it is doing work. Taken in pieces:

**Knowledge graph.** A store of *facts* rather than *documents*. Instead of chunks of text you later search, it holds discrete statements, each one a **triple**: a subject, a relationship, and an object.

```
Max  -[child_of]->  Alice
Max  -[does]->      swimming
Max  -[loves]->     chess
```

**Entity-relationship.** The subjects and objects are **entities** (nodes: people, projects, tools, concepts) and the arrows are **typed relationships** (edges: `child_of`, `does`, `loves`). The type matters - it is not a generic "related to" link. That typing is what lets a query ask for *a particular kind* of connection rather than everything adjacent.

**Temporal.** Each edge carries a validity window, `valid_from` and `valid_to`, so the graph records not just that a fact holds but *when* it held. A fact that stops being true is closed off, not deleted:

```
Max  -[does]->  swimming   valid_from 2025-01-01   valid_to 2025-09-30
Max  -[loves]-> chess      valid_from 2025-10-01   valid_to (open)
```

The graph can then be queried "as of" a date and will return the answer that was correct *then*, not the answer that is correct now.

### Why this retrieves differently

The mechanical difference from the other two signals is **traversal versus ranking**.

| | Semantic | Keyword | Entity graph |
|---|---|---|---|
| Query is | A sentence, embedded | A string | A node, plus a relationship type |
| Returns | Chunks of text, ranked by similarity | Chunks containing the string | **Structured facts**, by walking edges |
| Result quality | Probabilistic - "most similar" | Binary - contains it or not | **Deterministic** - the edge exists or it does not |
| Fails by | Returning plausible but wrong material | Missing paraphrase | Returning nothing, if the fact was never extracted |

Because the answer is a traversal rather than a ranked list, three question shapes become answerable that the other two signals cannot handle at all:

- **Aggregation.** "Everything we ever said about Supabase" - one node, all its edges. Semantic search returns the fifty most similar chunks and hopes the ranking cooperates.
- **Multi-hop.** "Who works on the project Max loves" - two hops, `Max -[loves]-> X` then `Y -[works_on]-> X`. Neither similarity nor string matching can chain.
- **Temporal.** "What was true in January?" - filter edges by validity window. A changed fact produces two equally-similar embeddings and two equally-valid keyword hits; only the graph separates current from superseded.

### The cost, and why most systems skip it

**Everything depends on extraction.** A triple only exists if something parsed it out of the raw text at ingest and chose the right entity and relationship type. That is an upfront LLM cost per turn, plus a schema decision (which relationship types exist), plus an entity-resolution problem (is "Supabase", "supabase" and "the database" one node or three?).

Semantic search needs none of that - embed the text and you are done. That asymmetry is why three of the four systems assessed have semantic and keyword retrieval but no graph: **the graph is the only signal that requires the system to understand the content at write time rather than at read time.** It is the write-time end of the [[wiki-vs-openbrain|write-time versus query-time]] fork applied to structure rather than prose.

### MemPalace's entity layer, in detail

Verified against `/Users/julianhart/mempalace/mempalace/knowledge_graph.py` and its sibling modules (`entity_registry.py`, `entity_detector.py`, `entities.py`, `palace_graph.py`). This is a genuine third retrieval signal, not a variant of semantic search:

- **Entity nodes** for people, projects, tools and concepts, with **typed relationship edges** (`child_of`, `works_on`, `loves`, and so on) - a real triple store, not a tag list.
- **Temporal validity on every edge** (`valid_from` → `valid_to`), so the graph knows *when* a fact was true and can answer `query_entity("Max", as_of="2026-01-15")`. Facts can be superseded without being deleted.
- **Back-references to the verbatim source** ("closet references"), so a graph answer can always be traced to the original stored content.
- Exposed to the agent as a distinct tool, `mempalace_kg_query`, alongside `mempalace_search`. Its recall skill instructs the agent to prefer the graph's time-valid answer when facts conflict.
- Stored in local SQLite, positioned in its own source comments as a free local alternative to Zep's hosted Neo4j temporal graph.

**Why this matters beyond MemPalace:** temporal validity is the capability that answers "what was true *then*", which neither semantic nor keyword search can do at all. A fact that changed produces two equally-similar embeddings and two equally-valid keyword hits; only a time-aware graph distinguishes the current answer from the superseded one.

## Capabilities and features across systems

Transposed from the four product scorecards. All four implement query-time recall; they differ in ranking sophistication and escalation design.

| Capability | Systems | Detail |
|---|---|---|
| **Dense vector similarity search** | All four | ClaudeClaw (`gemini-embedding-001`, cosine > 0.3), agentic-os (BGE-M3, 1024-dim, L2-normalised), MemSearch, MemPalace (ChromaDB default) |
| **Hybrid dense + sparse with rank fusion** | MemSearch | Dense vector plus BM25 sparse, combined via reciprocal rank fusion (RRF) reranking - the most sophisticated ranking step assessed |
| **Hybrid vector + full-text** | agentic-os | BGE-M3 vector search plus Postgres full-text keyword search |
| **Keyword fallback when embeddings unavailable** | ClaudeClaw | FTS5 mirror kept in sync by triggers; degrades to LIKE if needed, so recall never hard-fails on a missing embedding provider |
| **Progressive disclosure / tiered escalation** (stop at the cheapest rung that answers the question) | agentic-os, MemSearch, ClaudeClaw | agentic-os: search → expand → transcript. MemSearch: search → expand → transcript. ClaudeClaw: summaries first, raw `conversation_log` only when keyword-triggered. Convergent design across independent products |
| **Entity-first retrieval over a knowledge graph** | MemPalace only | Typed entity-relationship triples (`child_of`, `works_on`) queried via `mempalace_kg_query`, distinct from semantic search |
| **Temporal validity on facts** (knowing *when* something was true, not just that it was) | MemPalace only | `valid_from`/`valid_to` on every edge; `query_entity(..., as_of=...)` returns the answer correct at that date. Superseded facts are retained, not overwritten |
| **Entity extraction at ingest without an entity query path** | ClaudeClaw | `entities[]` extracted per turn but folded into the embedding text, so entities improve semantic ranking rather than enabling entity-first traversal |
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

- **Over the wiki corpus (~38 lesson docs):** no vector index. The curated `_index` descriptions plus `[[wikilinks]]` already form a precise retrieval layer at that scale. Revisit trigger: ~100-150 docs. See [[memory-features#Curated Index Retrieval|curated index retrieval]].
- **Over the JSONL transcript corpus:** narrowly justified but marginal, failing on query frequency (roughly 25 provenance queries in ten weeks). See [[memory-features#Semantic Search|semantic search]].

**The sharper finding is that Recall quality was never the constraint.** The curated index is precise when used; it was invoked in 11% of sessions. That is an [[memory-injection|Injection]] failure, not a Recall failure, and no improvement to ranking would have fixed it.

## Related

- [[memory-pillars]] - the four-pillar model overview
- [[memory-injection]] - the pillar that invokes Recall; the most common reason good Recall fails
- [[memory-storage]] - the form axis (synthesise-at-ingest vs store-faithfully) is this same fork seen from the write side
- [[memory-features#Curated Index Retrieval|Curated index retrieval]] - feature family for write-time recall
- [[memory-features#Semantic Search|Semantic search]] - feature family for query-time recall, and a practical feature family for triggered injection
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from
- [[wiki-vs-openbrain|AI Memory Paradigms]] - the write-time versus query-time fork in its original framing

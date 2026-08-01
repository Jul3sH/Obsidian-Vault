---
type: reference
created: 2026-08-01
authority: analysis-backed
concept: feature-catalogue
---

# Memory Features

> *Concrete product mechanisms and feature families observed across agent memory systems. Features implement or expose [[memory-capabilities|capabilities]] by serving one or more architecture functions from [[memory-pillars]].*

> [!note] Status: feature catalogue, not a backlog
> This file lists observed mechanisms, not planned work. A feature here may be a product feature, an implementation pattern, or a feature family such as semantic search. It becomes a backlog item only when tied to a specific target system and acceptance criteria.

## Key Takeaways

- **A feature is concrete.** It is something a user or system can invoke, configure, test, release, or buy.
- **Features are not capabilities.** A feature such as semantic search can enable [[memory-capabilities|unlocated context discovery]], but the capability is the durable ability, not the mechanism.
- **Features can serve multiple architecture functions.** Semantic search serves Recall and can also support triggered Injection. A `PreCompact` hook serves Capture and supports compaction survival.
- **This catalogue is evidence, not endorsement.** It records what the assessed products expose or implement.

## Classification Pattern

```text
Use case: actor-outcome journey
Capability: reusable ability
Architecture function: Capture, Storage, Injection, Recall
Feature: concrete mechanism or feature family
```

Example:

| Level | Example |
|---|---|
| Use case | When the user remembers the substance but not the location, the agent finds the relevant prior material |
| Capability | [[memory-capabilities|Unlocated context discovery]] |
| Architecture functions | Recall (query-time) + Injection (triggered where automatic) |
| Features | Semantic search, dense vector search, hybrid search, per-turn retrieval |

## Feature Catalogue

| Feature | Feature type | Primary architecture functions served | Capabilities supported | Observed in / evidence |
|---|---|---|---|---|
| **Curated index retrieval** | Feature family | Recall (write-time) | [[memory-capabilities|Curated knowledge navigation]], long-term knowledge recall | See [[memory-features#Curated Index Retrieval|Curated Index Retrieval]] below |
| **Semantic search** | Feature family | Recall (query-time), Injection (triggered where automatic) | [[memory-capabilities|Unlocated context discovery]], episodic recall, long-term knowledge recall | See [[memory-features#Semantic Search|Semantic Search]] below |
| **Native JSONL transcript capture** | Platform feature | Capture (continuous) | Episodic recall, source-grounded recall | [[memory-capture]] |
| **`Stop` hook capture** | Hook feature | Capture (continuous or periodic, depending on implementation) | Episodic recall, pattern-to-rule promotion, working reasoning preservation | [[pillars-claudeclaw]], [[pillars-agentic-os]], [[pillars-memsearch]], [[pillars-mempalace]] |
| **`PreCompact` hook** | Hook feature | Capture (event-triggered), Injection support where paired with retrieval | Compaction survival | [[pillars-mempalace]] |
| **`SessionEnd` final flush** | Hook feature | Capture (boundary) | Episodic recall, source-grounded recall | [[pillars-mempalace]] |
| **`SessionStart` memory injection hook** | Hook feature | Injection (scheduled) | Identity persistence, critical context availability | [[pillars-agentic-os]], [[pillars-memsearch]] |
| **`UserPromptSubmit` memory nudge** | Hook feature | Injection (trigger rung 3: deterministic nudge, no content) | Unlocated context discovery, weak form | [[pillars-memsearch]], [[memory-injection]] |
| **Per-turn retrieved content injection** | Runtime feature | Injection (triggered), Recall (query-time) | Unlocated context discovery, compaction survival, working reasoning preservation | [[pillars-claudeclaw]], [[memory-injection]] |
| **Frozen snapshot file** | Injection feature | Injection (scheduled) | Identity persistence, critical context availability | [[pillars-agentic-os]], [[memory-injection]] |
| **Derived critical-context payload** | Injection feature | Injection (scheduled or triggered) | Critical context availability, compaction survival | [[memory-capabilities]], [[memory-injection]] |
| **Working scratchpad** | Storage / injection feature | Storage, Injection | Working reasoning preservation, critical context availability | [[memory-capabilities]], [[memory-injection]] |
| **Reasoning checkpoint** | Capture / storage feature | Capture, Storage | Working reasoning preservation, compaction survival | [[memory-capabilities]] |
| **Dense vector similarity search** | Retrieval feature | Recall (query-time) | Unlocated context discovery, long-term knowledge recall, episodic recall | [[memory-recall]], [[pillars-claudeclaw]], [[pillars-agentic-os]], [[pillars-memsearch]], [[pillars-mempalace]] |
| **BM25 or full-text keyword search** | Retrieval feature | Recall (query-time) | Long-term knowledge recall, source-grounded recall | [[memory-recall]], [[pillars-memsearch]], [[pillars-agentic-os]], [[pillars-claudeclaw]] |
| **Hybrid dense and sparse search** | Retrieval feature family | Recall (query-time) | Unlocated context discovery, long-term knowledge recall | [[pillars-memsearch]], [[memory-recall]] |
| **Reciprocal rank fusion** | Ranking feature | Recall (query-time) | Long-term knowledge recall, unlocated context discovery | [[pillars-memsearch]], [[memory-recall]] |
| **Three-rung recall ladder: search, expand, transcript** | Retrieval feature family | Recall (query-time) | Source-grounded recall, episodic recall, long-term knowledge recall | [[pillars-agentic-os]], [[pillars-memsearch]], [[openbrain-vs-agentic-os]] |
| **Temporal entity knowledge graph** | Retrieval / storage feature family | Storage (temporal form), Recall (entity-first) | Temporal fact recall, source-grounded recall | [[pillars-mempalace]], [[memory-recall]] |
| **`mempalace_kg_query` tool** | Tool feature | Recall (entity-first) | Temporal fact recall | [[pillars-mempalace]] |
| **Closet references to verbatim source** | Provenance feature | Storage, Recall | Source-grounded recall | [[pillars-mempalace]], [[memory-recall]] |
| **Scope predicates on memory queries** | Safety feature | Storage (scope model), Recall, Injection | Scope-isolated recall | [[pillars-agentic-os]], [[memory-recall]] |
| **Per-agent memory plus shared memory tier** | Safety / collaboration feature | Storage, Recall, Injection | Scope-isolated recall, cross-agent memory federation | [[pillars-claudeclaw]], [[memory-recall]] |
| **Cross-agent shared memory store** | Federation feature | Storage, Recall, access protocol | Cross-agent memory federation | [[pillars-memsearch]] |
| **MCP memory gateway** | Access feature | Recall, access protocol | Cross-agent memory federation | [[openbrain-vs-agentic-os]] |
| **Importance gate at ingest** | Retention feature | Capture, Storage (retention) | Retention management | [[pillars-claudeclaw]], [[memory-storage]] |
| **Cheap pre-filter before extraction** | Retention / cost feature | Capture | Retention management | [[pillars-claudeclaw]], [[memory-capture]] |
| **Semantic duplicate detection at ingest** | Retention feature | Capture, Storage | Retention management | [[pillars-claudeclaw]], [[memory-capture]] |
| **Salience decay and pinning** | Retention feature | Storage (retention) | Retention management | [[pillars-claudeclaw]], [[memory-storage]] |
| **Budget-driven compression against a hard cap** | Retention feature | Storage (retention) | Retention management, critical context availability | [[pillars-agentic-os]], [[memory-storage]] |
| **Periodic consolidation pass** | Storage feature | Storage | Pattern-to-rule promotion, source-grounded recall where sources remain | [[pillars-claudeclaw]], [[memory-storage]] |
| **Daily memory distillation** | Promotion feature | Storage, Injection where behavioural | Pattern-to-rule promotion, procedural memory generation | [[pillars-agentic-os]], [[memory-storage]] |
| **`PROJECT.md` and `USER.md` distillation** | Distillation feature | Storage, Injection (scheduled) | Critical context availability, identity persistence | [[pillars-memsearch]], [[memory-capabilities]] |
| **SHA-256 content hashing before indexing** | Index maintenance feature | Recall (query-time) | Fresh recall, efficient index maintenance | [[pillars-memsearch]], [[pillars-agentic-os]], [[memory-recall]] |
| **File watcher for live index maintenance** | Index maintenance feature | Recall (query-time) | Fresh recall, unlocated context discovery | [[pillars-memsearch]], [[pillars-agentic-os]], [[memory-recall]] |
| **Pluggable storage backend** | Deployment feature | Storage | Deployment flexibility | [[pillars-mempalace]], [[memory-storage]] |
| **Wings / Rooms / Drawers hierarchy** | Storage / scoping feature | Storage, Recall | Curated knowledge navigation, scope-limited recall | [[pillars-mempalace]], [[memory-storage]] |
| **Verbatim storage with no synthesis** | Storage feature family | Storage | Source-grounded recall, episodic recall | [[pillars-mempalace]], [[memory-storage]] |
| **Markdown-canonical, vector-index disposable store** | Storage feature family | Storage, Recall | Source-grounded recall, retention management | [[pillars-memsearch]], [[memory-storage]] |
| **Agent-authored capture** | Capture feature | Capture, Storage | Working reasoning preservation, pattern-to-rule promotion | [[pillars-mempalace]], [[memory-capture]] |
| **Externally summarised capture** | Capture feature | Capture, Storage | Episodic recall, long-term knowledge recall | [[memory-capture]], [[pillars-agentic-os]], [[pillars-memsearch]], [[pillars-claudeclaw]], [[pillars-mempalace]] |
| **Loop guard against recursive capture** | Safety feature | Capture | Capture reliability | [[pillars-memsearch]], [[memory-capture]] |
| **Provider fallback plus quota backoff** | Reliability feature | Capture, Storage | Capture reliability, retention management | [[pillars-claudeclaw]], [[memory-capture]] |
| **Memory bootstrap index** | First-run feature | Recall (query-time) | Long-term knowledge recall, unlocated context discovery | [[pillars-agentic-os]], [[memory-capture]] |
| **Headless maintenance jobs** | Maintenance feature family | Storage, Recall, backup | Retention management, long-term knowledge recall | [[pillars-agentic-os]], [[memory-capture]] |
| **Search-before-answer protocol** | Protocol feature | Injection (agent-decided), Recall | Curated knowledge navigation, unlocated context discovery | [[pillars-mempalace]], [[memory-recall]] |
| **Published retrieval benchmark** | Evidence / quality signal | Recall assessment | Evidence for long-term knowledge recall quality | [[pillars-mempalace]], [[memory-recall]] |
| **Skills from Memory** | Procedural feature | Storage, promotion process; generates a reusable procedure | Procedural memory generation, pattern-to-rule promotion | [[pillars-memsearch]], [[memory-capabilities]] |

## Curated Index Retrieval

Curated index retrieval is the write-time Recall feature family: a hand-authored index hierarchy plus bare wikilinks, where the retrieval signal is written in advance instead of computed at query time.

It has three parts:

1. **An index hierarchy.** A master index lists topic areas; each topic index lists its documents; each entry carries a one-line description of what that document is.
2. **Bare wikilinks** (`[[note-name]]`) connecting related documents, resolved by filename rather than path.
3. **Filing discipline** that keeps both current as documents are created and moved.

The one-line descriptions are the ranking function. When an agent chooses which document to open, it is ranking the index descriptions against the question. An index entry that describes what a document contains retrieves well; one that merely names it does not.

| Strength | Failure mode |
|---|---|
| High precision and transparency | Nothing forces the index to be consulted |
| Zero infrastructure | Dormant material is invisible when the agent has no starting hypothesis |
| Bare wikilinks create a lateral graph | Authoring cost scales with corpus size |
| Easy to debug by reading the index | Missing index updates create silent rot |

Measured in one real corpus: the navigation entry point was read in **5 of 47 sessions (11%)**, against an explicit standing instruction, and only **187 of 744 document reads (25%)** were autonomous discovery. The feature worked when invoked; the trigger did not.

Choose curated index retrieval when documents are titled, deliberately filed, browsable by a human, and queries map to known topic areas. It composes well with [[memory-features#Semantic Search|semantic search]]: curated index over the canonical branch, computed index over raw captured material.

## Semantic Search

Semantic search is the query-time Recall feature family: a vector or embedding index over material that already exists, allowing lookup by meaning rather than exact string. It can also support triggered Injection, because a per-turn hook can query it without the human or agent already knowing that relevant material exists.

Semantic search retrieves. It does not capture. If the material is not recorded somewhere first, there is nothing to embed.

Use the five-criteria test before building it:

| # | Criterion | Fails when |
|---|---|---|
| 1 | Volume exceeds browsing capacity | A human can scan the file list |
| 2 | Material is unstructured and untitled at capture time | It already has names, tags, links |
| 3 | **The retrieval key is unknown at query time** | They know the filename, phrase, or obvious topic area |
| 4 | Not already curated into a canonical store | You would be duplicating an index |
| 5 | Query frequency amortises build and maintenance cost | A handful of queries per quarter |

Criterion 3 is the whole argument. Grep and curated index retrieval both require the actor to know something distinctive: a string, a location, or a plausible first hop. Embeddings help when the actor remembers substance but not wording or location.

The commonly cited retrieval use cases split apart under this test:

| Candidate use case | Taxonomy reading |
|---|---|
| Vocabulary bridging over unstructured pastes | Strong case for semantic search when pastes are large, untitled, and grep-hostile |
| Cross-tool continuity | Usually a federation problem first, not an embedding problem |
| Session residue, rejected options, and reasoning | Valid only for unfiled residue; already-filed decision records do not need embeddings |
| Negative knowledge, failures, and dead ends | Stronger in build-test-debug workloads than prose-editing workloads |
| Temporal queries | Often solved by timestamps or version control unless the question needs temporal fact recall |

The strongest argument is triggered Injection. In the assessed corpus, curated index retrieval suffered from low invocation: the agent reliably read material named by the user, about to be edited, or already in the thread, but did not reliably seek dormant relevant context. That is a trigger failure, not just a ranking failure.

For the assessed environment, the verdict was narrow: semantic search over JSONL transcripts was justified by criteria 1 to 4, but marginal on criterion 5. Semantic search over the curated wiki corpus was not justified yet, because the wiki remains browsable and already indexed.

## Notes

**Curated index retrieval and semantic search are feature families, not capabilities.** They are broad enough to contain many concrete features, but they still describe mechanisms. The capabilities they support are the outcomes: curated knowledge navigation, unlocated context discovery, episodic recall, and long-term knowledge recall.

**Some rows are evidence rather than product features.** Published retrieval benchmarks are not themselves features; they are included because the original product tables mixed them into capability rows. They should be used as quality evidence, not as implementation backlog.

**Feature names should stay implementation-shaped.** If a row cannot plausibly be invoked, configured, tested, released, or bought, it probably belongs in [[memory-capabilities]] rather than here.

## Related

- [[memory-capabilities]] - the capability catalogue this feature list supports
- [[memory-use-cases]] - actor-outcome journeys that consume those capabilities
- [[memory-pillars]] - the architecture functions features serve
- [[memory-systems-taxonomy-codex-review-2026-08-01]] - review that prompted this separation

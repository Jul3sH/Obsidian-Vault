---
type: reference
updated: 2026-07-31
authority: analysis-backed
concept: enabler
serves: recall (write-time)
---

# Curated Index Retrieval

> *An enabler for **Recall (write-time)**: a hand-authored index hierarchy plus bare wikilinks, where a human or agent writes the retrieval signal in advance instead of computing it at query time. The write-time counterpart to [[memory-semantic-search]]. Model: [[memory-pillars]].*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example.

## Key Takeaways

- **The retrieval signal is authored, not computed.** One-line `_index` descriptions are the ranking layer, written by whoever files the document.
- **It is the most common Recall implementation and the least written up**, because it looks like filing rather than technology.
- **Precision is its strength; invocation is its weakness.** A curated index can beat embedding similarity on precision and still fail, because nothing forces it to be consulted.
- **Measured in one real corpus: the navigation entry point was read in 11% of sessions**, and only 25% of document reads were autonomous discovery. The mechanism worked; the trigger did not.
- **Judge it on hop discipline and invocation rate, not corpus size alone.** Most published thresholds only measure the first.

---

## What it is

A retrieval scheme with three parts:

1. **An index hierarchy.** A master index lists topic areas; each topic index lists its documents; each entry carries a one-line description of what that document *is*.
2. **Bare wikilinks** (`[[note-name]]`) connecting related documents, resolved by filename rather than path.
3. **Filing discipline** that keeps both current as documents are created and moved.

The defining property: **the retrieval signal is written in advance by a human or agent, not computed at query time.** That is the exact inverse of [[memory-semantic-search]], and it maps onto the write-time versus query-time fork in [[wiki-vs-openbrain|AI Memory Paradigms]].

## How retrieval actually works

The hop chain, which is the part usually left implicit:

```
question
   ↓  read master index          → which topic area?
   ↓  read that topic's _index   → which document?
   ↓  read the document          → the answer
   ↓  follow [[wikilinks]]       → adjacent context
```

**The one-line descriptions are the ranking function.** When an agent chooses which document to open, it is ranking the index descriptions against the question. Everything the scheme's precision depends on is decided when those lines are written, not when the query arrives.

This has a direct consequence: **an index entry that describes what a document *contains* retrieves well; one that merely names it does not.** "Two query-time database systems compared: multi-tool bus versus multi-client runtime" is a retrieval signal. "Notes on databases" is not.

## The conventions that make it work

| Convention | Why retrieval depends on it |
|---|---|
| **Bare links, never path links** | The link survives a file move, so reorganising never breaks the graph |
| **Unique basenames across the corpus** | Bare links resolve unambiguously; no disambiguation hops |
| **Indexes are navigation only** | Mutable state in an index goes stale silently and poisons the ranking signal |
| **Index updated on every file move** | Skip it and the folders drift from the indexes, which is how the scheme rots |
| **One-line description per entry, describing content** | This *is* the ranking function |

## Strengths

- **Precision.** A well-written description encodes intent and scope in a way embedding similarity approximates at best. There is no chunking, no re-embed-on-edit drift, no similarity false positives.
- **Zero infrastructure.** No pipeline, no database, no embedding cost, no staleness between index and content beyond human discipline.
- **Transparent and debuggable.** When retrieval fails you can read the index and see exactly why. A vector store gives you a similarity score.
- **The graph is a second retrieval path.** Bare wikilinks let an agent traverse laterally from a document it already found, which similarity search does not naturally provide.
- **It degrades gracefully.** A stale description still points somewhere useful.

## Failure modes

**1. Invocation, which is the dominant one.** Nothing forces the index to be consulted. The scheme has no trigger of its own; it relies on the agent choosing to navigate, or the human saying "check the wiki".

Measured across 47 sessions of one real corpus (528 documents):

| Signal | Result |
|---|---|
| Sessions where the master index was read | **5 of 47 (11%)**, against an explicit standing instruction to read it first |
| Document reads that were autonomous discovery | **187 of 744 (25%)** |
| Document reads that were user-prompted | 259 (34%) |
| Document reads that were mechanical read-before-edit | 298 (40%) |

The mechanism was sound. It was invoked a quarter of the time.

**2. It cannot surface what the agent does not know exists.** Navigation requires a plausible starting hypothesis about where something lives. Dormant material in an unrelated topic area is effectively invisible, because nothing prompts the first hop.

**3. Authoring cost scales with the corpus.** Every new document needs an index entry written well enough to rank. That cost is paid by whoever files, and it is the first thing dropped under time pressure.

**4. Silent rot.** Missing index updates are invisible until retrieval fails, and retrieval failure is itself hard to notice, because the agent answers from context instead and nobody sees the omission.

## When it is the right choice

Against the five-criteria test in [[memory-semantic-search]], a curated index wins when the corpus **fails** those criteria: browsable volume, titled and linked material, already curated into a canonical store.

| Choose curated index | Choose semantic index |
|---|---|
| Documents are titled, tagged and deliberately filed | Material is untitled, unstructured, arrives in bulk |
| Corpus is browsable by a human | Volume defeats browsing |
| Queries name a topic that maps to a known area | Queries describe content whose location is unknown |
| Precision matters more than recall | Missing a relevant item is the expensive failure |
| No appetite for pipeline maintenance | Infrastructure is acceptable |

**The two compose.** A curated index over the canonical branch of Storage and a vector index over raw captured material is a coherent hybrid, and it is usually better than either alone, because they fail differently.

**The decisive question is not corpus size.** Published thresholds ("revisit past N documents") measure only authoring load. The invocation rate matters more: a curated index consulted 11% of the time is already failing at 500 documents, while one consulted reliably may hold well past a published ceiling. Measure invocation before measuring size.

## Related

- [[memory-pillars]] - the four-pillar model; this enabler serves Recall (write-time)
- [[memory-semantic-search]] - the query-time counterpart, and the five-criteria test
- [[memory-observation-layer]] - the Capture pillar
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time, the fork this sits on

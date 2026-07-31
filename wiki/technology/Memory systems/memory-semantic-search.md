---
type: reference
updated: 2026-07-31
authority: analysis-backed
concept: enabler
serves: recall (query-time), injection (triggered)
---

# Semantic Search

> *An enabler for **Recall (query-time)**, and the only practical enabler of **Injection (triggered)**: a vector or embedding index over material that already exists, allowing lookup by meaning rather than by exact string. It captures nothing. The computed counterpart to [[memory-curated-index]]. Model: [[memory-pillars]].*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **Semantic search retrieves. It does not capture.** It indexes an existing store and creates no new record.
- **It serves two pillars.** Recall in its query-time form, and it is the only enabler that makes *triggered* Injection practical, because it can be queried on every turn without anyone knowing in advance that relevant material exists.
- **The decision hinges on the retrieval-key problem, not on subject matter.** It wins specifically when the user remembers the *content* but not the *name or phrasing*, which is exactly where grep and a curated index both fail.
- **Engineering workloads are not the only qualifying case**, they simply hit the criteria more often.
- **Criterion 5, query frequency, is where most proposals die**, and it is the one enthusiasts skip.

---

## Terminology note: retrieval is not capture

| | **Semantic search** (this article) | **Observation layer** ([[memory-observation-layer]]) |
|---|---|---|
| Pillar served | **Recall (query-time)**, and **Injection (triggered)** | **Capture** |
| Answers | "Can I find what I know is there?" | "Is anything going unrecorded?" |
| Fails when | Similarity approximates intent badly | Events vanish unlogged |
| Output | An index over a store | A durable store |

**The error runs in this direction here:** retrieval benefits get used to justify capture spend. A proposal listing "recall past decisions", "surface old error traces", "find that meeting note" is making a *retrieval* argument. If capture already exists, those benefits justify an index, which is far cheaper than a new capture system.

## When semantic search is justified: a transferable test

A vector store pays for itself only when **all five** hold. The third is the crux; the fifth is where most proposals die.

| # | Criterion | Fails when |
|---|---|---|
| 1 | Volume exceeds browsing capacity | A human can scan the file list |
| 2 | Material is unstructured and untitled at capture time | It already has names, tags, links |
| 3 | **The retrieval key is unknown at query time** | They know the filename, so navigation works |
| 4 | Not already curated into a canonical store | You would be duplicating an index |
| 5 | Query frequency amortises build and maintenance cost | A handful of queries per quarter |

**Criterion 3 is the whole argument.** grep and a curated index both require you to already know something distinctive: a string, or where the material lives. Embeddings do not. Everything else is qualification.

**Why generic advice on this topic reads as engineering-flavoured:** software engineering workloads score high on 1, 2 and 3 automatically. Error traces, stack dumps and dead-end approaches are high-volume, never titled, and recalled by symptom rather than by name. That is a *correlation with the criteria*, not a property of engineering. Non-engineering workloads exhibit the same pattern whenever the user recalls content but not phrasing.

**For assessing other systems:** all five criteria are measurable from session transcripts. Count paste volume, error density, prose-to-code ratio, and provenance-question rate. This converts an architecture preference into a number.

## Scoring the five commonly-cited use cases

Tested against one real corpus: 47 sessions, 24,581 events, 98% prose editing.

| Use case | Verdict there | Evidence |
|---|---|---|
| **Vocabulary bridging** over unstructured pastes | **Strong** | 128 pastes over 1,200 chars (10% of turns), largest 16,704. Untitled, untagged, grep-hostile |
| **Cross-tool continuity** across agents | **Real need, misdiagnosed cause** | The claim that the material "does not exist as files" was false: the other agent persisted its own sessions and memory database to disk. A **federation** problem, not a capture or embedding one, and the fix is far cheaper |
| **Session residue**, rejected options and reasoning | **Partly valid, overstated** | The "0% reaches the knowledge base" claim failed: a decision journal, a decision register and a structured risk register existed specifically to record roads not taken. The gap is only the *unfiled* residue |
| **Negative knowledge**, failures and dead ends | **Weak there** | 119 tool errors across 24,581 events (0.5%). Edits were 98% prose (1,615 markdown vs 29 code/config); shell use was navigation, not build-test-debug. The high-value negative knowledge had already been written down, because pain forced it |
| **Temporal queries** | **Already solved** | Transcripts carry timestamps and version control carries dates. Questions of this exact shape were answered during the assessment itself |

**Not a simple engineering-versus-not split.** Two of the five failed there because it was a decision-support workload rather than a build workload. Genuine retrieval needs remained, and they were not engineering-shaped.

## The retrieval use cases that did apply

Derived from the corpus rather than adapted from a generic list.

- **Provenance of self-stated facts.** 25 instances of asking where a figure originated or what was previously stated: *"where's the AR cap come from?"*, *"what did we say the pot is?"*, *"What did I say my investments are currently worth?"* These satisfy criterion 3 exactly: the fact is remembered, the phrasing is not.
- **Unstructured paste recall.** 128 large pastes: message archives, meeting recaps, salary and market dumps, call debriefs. Some were filed; the remainder are recoverable only from transcripts.
- **Pre-structure history.** Explicitly requested. Material predating the current filing conventions has no canonical home by definition.
- **Cross-agent federation.** Real, but low volume, and partly addressed by a shared always-loaded rulebook.

## The strongest argument: triggered injection

Semantic search is the only enabler that makes **Injection (triggered)** practical. A vector index queried by a per-turn hook needs neither the human nor the agent to know in advance that relevant material exists.

That matters because the competing Recall enabler fails precisely there. In the assessed corpus the curated index was invoked in only **11% of sessions**, and just **25% of document reads were autonomous discovery**. Full measurement and method: [[memory-curated-index]].

**The agent reliably reads material that is named by the user, about to be edited, or already in the active thread. It does not reliably seek out dormant relevant context, because it does not know that context exists.** That is a trigger failure, not a retrieval failure, and no amount of curation fixes it. It is a stronger argument for a semantic index than any of the five use cases above.

## Assessment of one environment, 2026-07-31

**Verdict: narrowly justified, marginal on criterion 5.**

Criteria 1, 2 and 3 cleared comfortably. Criterion 4 partly cleared, since the knowledge base curated much but not all of the material. Criterion 5 was the weak point: roughly 25 provenance queries across ten weeks is a thin amortisation base.

**Therefore: index the existing transcripts. Do not build a runtime capture-and-embed pipeline.** The substrate already existed ([[memory-observation-layer]]), so the work is an index, not a system.

**Restraint argument, from that environment's own data:** system-maintenance was already 24% of total effort, and non-adoption of previously built tooling was empirically confirmed. A vector store is precisely the kind of artefact that gets built, documented, and then never invoked. If it is built, the adoption forcing-function matters more than the architecture.

## Relationship to the other enablers

- **Depends on Capture.** You cannot embed what was never recorded. Assess [[memory-observation-layer]] first.
- **Competes with, and composes with, [[memory-curated-index]].** A write-time index over the canonical branch of Storage plus a query-time index over raw captured material is usually stronger than either alone, because they fail differently: one loses on invocation, the other on precision.
- **Enables Injection (triggered)**, which nothing else practically does. See [[memory-pillars]].

## Caveats

- The assessed corpus begins 2026-05-18; earlier sessions may have rotated out.
- Query-frequency figures are lower bounds, derived from pattern matching over phrasing and likely to undercount.
- Transcript retention is not guaranteed indefinitely, which is a dependency for any index built over it.

## Related

- [[memory-pillars]] - the four-pillar model; this enabler serves Recall (query-time) and Injection (triggered)
- [[memory-curated-index]] - the write-time counterpart, and the invocation measurement
- [[memory-observation-layer]] - the Capture pillar, upstream dependency
- [[ai-memory-paradigms]] - write-time versus query-time, the fork this sits on

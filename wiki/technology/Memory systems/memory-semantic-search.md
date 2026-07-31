---
type: reference
updated: 2026-07-31
authority: analysis-backed
concept: retrieval
---

# Semantic Search

> *Semantic search (vector or embedding search) is a **retrieval** mechanism: an index over material that already exists, enabling lookup by meaning rather than by exact string. It answers "can I find what I know is there?" It captures nothing. Paired concept: [[memory-observation-layer]].*

> [!note] Status: technology theory, not an adopted design
> This article is reference material on how agent memory systems work. It is **not** a description of what has been chosen or built here. The assessment sections record a point-in-time evaluation against one real corpus, used as a worked example to make the theory testable.

## Key Takeaways

- **Semantic search retrieves. It does not capture.** It adds an index over an existing store and creates no new record.
- **Never use "semantic search" and "observation layer" interchangeably.** See the terminology note below; the confusion causes real overspend.
- **The decision hinges on the retrieval-key problem, not on subject matter.** A semantic index wins specifically when the user remembers the *content* but not the *name or phrasing*, which is exactly where grep fails.
- **Engineering workloads are not the only qualifying case**, they simply hit the criteria more often. Decision-support work can qualify too.
- **Verdict for this environment: narrowly justified, marginal on frequency.** Index existing transcripts; do not build a runtime capture-and-embed pipeline.

---

## Terminology note: do not use these terms interchangeably

| | **Semantic search** (this article) | **Observation layer** ([[memory-observation-layer]]) |
|---|---|---|
| Axis | **Retrieval** | **Capture** |
| Answers | "Can I find what I know is there?" | "Is anything going unrecorded?" |
| Fails when | You must know the exact string to grep | Events vanish unlogged |
| Output | An index over a store | A durable store |

**The error to watch for runs in this direction:** retrieval benefits get used to justify capture spend. A proposal listing "recall past decisions", "surface old error traces", "find that meeting note" is making a *retrieval* argument. If capture already exists, those benefits justify an index, which is far cheaper than a new capture system. Score every claimed benefit onto an axis before approving anything.

## When semantic search is justified: a transferable test

Applicable to any agentic OS. A vector store pays for itself only when **all five** hold. The third is the crux; the fifth is where most proposals die.

| # | Criterion | Fails when |
|---|---|---|
| 1 | Volume exceeds browsing capacity | A human can scan the file list |
| 2 | Material is unstructured and untitled at capture time | It already has names, tags, links |
| 3 | **The retrieval key is unknown at query time** | They know the filename, so grep works |
| 4 | Not already curated into a canonical store | You would be duplicating an index |
| 5 | Query frequency amortises build and maintenance cost | A handful of queries per quarter |

**Criterion 3 is the whole argument.** grep requires you to already know a distinctive string. Embeddings do not. Everything else is qualification.

**Why generic advice on this topic reads as engineering-flavoured:** software engineering workloads score high on 1, 2 and 3 automatically. Error traces, stack dumps and dead-end approaches are high-volume, never titled, and recalled by symptom rather than by name. That is a *correlation with the criteria*, not a property of engineering. Non-engineering workloads exhibit the same pattern whenever the user recalls content but not phrasing.

**Practical note for assessing other systems:** all five criteria are measurable from someone's session transcripts. Count paste volume, error density, prose-to-code ratio, and provenance-question rate. This converts an architecture preference into a number.

## Scoring the five commonly-cited use cases

The use cases most often advanced for a semantic memory layer, tested against this corpus.

| Use case | Verdict here | Evidence |
|---|---|---|
| **Vocabulary bridging** over unstructured pastes | **Strong** | 128 pastes over 1,200 chars (10% of turns), largest 16,704. Untitled, untagged, grep-hostile |
| **Cross-tool continuity** across agents | **Real need, misdiagnosed cause** | The claim that the material "does not exist as files" is false. Codex persists `~/.codex/sessions/`, `session_index.jsonl`, `memories_1.sqlite`. A further 48 Claude sessions sit under `claudeclaw-os`. This is a **federation** problem, not a capture or embedding problem, and the fix is far cheaper |
| **Session residue**, rejected options and reasoning | **Partly valid, overstated** | The "0% reaches the vault" claim fails here: [[decision-journal]], the decision register, `uk-move/capture.md` (31 edits) and the Cause-Event-Effect-Response risk register exist specifically to record roads not taken. The gap is only the *unfiled* residue |
| **Negative knowledge**, failures and dead ends | **Weak here** | 119 tool errors across 24,581 events (0.5%). Edits are 98% prose (1,615 markdown vs 29 code/config); Bash is navigation (`cd` 389, `grep` 79, `ls` 61), not build-test-debug. High-value negative knowledge already got written because pain forced it, e.g. the HK VPN routing constraints in [[CLAUDE]] |
| **Temporal queries** | **Already solved** | JSONL carries timestamps and vault-backup commits carry dates. Questions of this exact shape were answered during the assessment itself, e.g. establishing that `multi-agent-protocol.md` was first written 2026-07-09T11:17 |

**This is not a simple engineering-versus-not split.** Two of the five fail here because this is a decision-support workload rather than a build workload. Genuine retrieval needs remain, and they are not engineering-shaped.

## The retrieval use cases that do apply here

Derived from the corpus rather than adapted from a generic list.

- **Provenance of self-stated facts.** 25 instances of asking where a figure originated or what was previously stated: *"where's the AR cap come from?"*, *"what did we say the MPF pot is?"*, *"What did I say my ISA investments are currently worth and also what did I say the value of my UK current account is?"* These satisfy criterion 3 exactly: the fact is remembered, the phrasing is not.
- **Unstructured paste recall.** The 128 large pastes: WhatsApp archives, meeting recaps, salary and job-market dumps, call debriefs. Some are filed into the wiki; the remainder are recoverable only from transcripts.
- **Pre-structure history.** Explicitly requested: *"do you have any visibility of the tasks that I did when I was preparing for my Cisco interview? I think it might have been pre-wiki."* Material predating current wiki conventions has no canonical home by definition.
- **Cross-agent federation.** Real, but currently low volume (6 Codex session files against 47 Claude ones), and partially addressed already by [[AGENTS]] acting as the deliberate shared layer.

## Injection: the pillar that decides whether retrieval ever runs

Retrieval and injection are distinct. **Retrieval finds material. Injection decides to look, and puts the result into the context window.** Retrieval quality is irrelevant if nothing triggers a lookup.

Under the four-pillar model (**Capture → Storage → Injection → Recall**, see [[memory-observation-layer]] for the derivation and the argument for splitting capture out of storage):

| Pillar | Function | Status in the assessed environment |
|---|---|---|
| Capture | Get events recorded | **Solved.** JSONL transcripts |
| Storage | Decide what to keep, and how organised | Partial. Files, no retention guarantee |
| **Injection** | Decide to look; place material in context | **The binding constraint** |
| Recall | Find the right material | Not built; grep only |

### The two types of injection

These have different triggers, different cost profiles, and defend against different failures. Conflating them hides the failure mode that actually bites.

| | **Scheduled injection** | **Triggered injection** |
|---|---|---|
| When | Once, at session start | Mid-session, in response to a turn |
| Trigger | Deterministic, time-based | Something must *decide* a lookup is needed |
| Typical form | "Frozen snapshot" of consolidated files, roughly 1,300 to 3,000 tokens: `CLAUDE.md`, `SOUL.md`, `user.md` | Vector query against the store, top-k results injected |
| Token cost | Fixed and predictable; cacheable | Variable; risks bloating context |
| Defends against | **Cold-start amnesia.** The agent begins each session knowing who the user is and what the rules are | **Compaction loss and context rot.** Material that left the window, or decayed in salience, is brought back |
| Cannot fix | Anything that degrades *during* the session, because it fires once, before the degradation | Nothing structural; but it is the harder of the two to build well |

**Simon Scrapes' Injection pillar is the scheduled type.** His recommended architecture specifies frozen snapshots at session start. That is a sound defence against cold-start amnesia and it is cheap, because it caches. It does **not** address mid-session degradation, because it has already fired by the time degradation begins.

**The trigger problem is what makes triggered injection hard.** Something has to decide a lookup is warranted. The options, in ascending reliability:

1. **The user asks.** Fragile: depends on the human remembering that relevant material exists.
2. **The agent decides.** Measured below at roughly 25% reliability in this corpus.
3. **A hook fires on every turn.** Deterministic. Pays a retrieval cost per turn whether or not it is needed.

Only option 3 removes the human and the agent's judgement from the loop, which is why hook-based designs exist despite their cost.

### Measured: the trigger fails in this environment

All 744 vault `Read` calls across 47 sessions were decomposed. A read that precedes an edit of the same file is mechanical, not recall:

| Category | Count | Share |
|---|---|---|
| User mentioned the wiki in the preceding turn | 259 | 34% |
| Unflagged, but read-then-edit same file (mechanical) | 298 | 40% |
| Unflagged, no subsequent edit (**genuine discovery**) | 187 | **25%** |

Only a quarter of wiki reads are autonomous consultation. Worse, `_master-index.md` was read **5 times across 47 sessions**, against an explicit [[AGENTS]] instruction to read it first when answering questions: roughly 11% compliance with a documented navigation protocol. Inspecting the 187 discovery reads, most are continuations inside an already-active thread rather than recall of dormant material.

**Conclusion:** the agent reliably reads files that are named by the user, about to be edited, or already in the active thread. It does **not** reliably seek out dormant relevant context, because it does not know that context exists. Recall therefore depends on the human remembering to say "check the wiki", which is a heavy and fragile dependency, and it is a trigger failure rather than a retrieval failure.

**This is the strongest argument for a semantic index in this environment,** and it is stronger than any of the five commonly-cited use cases above. A vector index queried by a per-turn hook needs neither party to know in advance that relevant material exists. Neither a wiki nor grep can close that gap, because both require a deliberate act of recall by the human.

**Measured, 2026-07-31.** All 744 vault `Read` calls across 47 sessions were decomposed. A read that precedes an edit of the same file is mechanical, not recall:

| Category | Count | Share |
|---|---|---|
| User mentioned the wiki in the preceding turn | 259 | 34% |
| Unflagged, but read-then-edit same file (mechanical) | 298 | 40% |
| Unflagged, no subsequent edit (**genuine discovery**) | 187 | **25%** |

Only a quarter of wiki reads are autonomous consultation. Worse, `_master-index.md` was read **5 times across 47 sessions**, against an explicit [[AGENTS]] instruction to read it first when answering questions: roughly 11% compliance with a documented navigation protocol. Inspecting the 187 discovery reads, most are continuations inside an already-active thread rather than recall of dormant material.

**Conclusion:** the agent reliably reads files that are named by the user, about to be edited, or already in the active thread. It does **not** reliably seek out dormant relevant context, because it does not know that context exists. Recall therefore depends on the human remembering to say "check the wiki", which is a heavy and fragile dependency.

**This is the strongest argument for a semantic index in this environment,** and it is stronger than any of the five commonly-cited use cases above. A vector index can be queried **proactively on every turn**, without either party knowing in advance that relevant material exists. Neither the wiki nor grep can close that gap, because both require a deliberate act of recall by the human.

## Compaction and context rot: what actually fixes them

Neither phenomenon is a storage failure, so neither is fixed by capture. But both are addressable by stages 2 and 3.

| Phenomenon | What happens | Fixed by |
|---|---|---|
| **Compaction** | Material leaves the context window; it remains on disk | **Injection.** Retrieve relevant prior material and put it back in |
| **Context rot** | Material stays in the window but salience decays | **Injection plus structure.** Re-surface, restate, use auto-loaded rules and checklists |

**The wiki is a session-boundary mechanism, not a mid-session one.** Summaries and conclusions are written at session end, so the wiki defends against loss *between* sessions but cannot defend against salience decay *within* one. Nothing gets re-read unless something triggers a read, which returns to the stage 3 problem above.

**Consequence for design:** a hook-based capture-store-inject pipeline does address compaction. But in this environment only stages 2 and 3 need building, because stage 1 already exists in the JSONL transcripts. Proposals should be costed accordingly.

## Assessment for this environment, 2026-07-31

**Verdict: narrowly justified, marginal on criterion 5.**

Scored against the test: criteria 1, 2 and 3 clear comfortably. Criterion 4 partly clears, since the wiki curates much but not all of the material. Criterion 5 is the weak point: roughly 25 provenance queries across ten weeks is a thin amortisation base.

**Therefore: index the existing transcripts. Do not build a runtime capture-and-embed pipeline.** The substrate already exists ([[memory-observation-layer]]), so the work is an index, not a system.

**Restraint argument, from this environment's own data:** `ai-os` is already 24% of total effort, and skill non-adoption is empirically confirmed. A vector store is precisely the kind of artefact that gets built, documented, mirrored, and then never invoked. If it is built, the adoption forcing-function matters more than the architecture. See [[feedback-build-dont-adopt]].

## Relationship to the observation layer

**Hard dependency, one direction only.**

- This concept **depends on** [[memory-observation-layer]]. You cannot embed what was never recorded. Capture is upstream; retrieval is downstream.
- The observation layer does **not** depend on this. Aggregate audit value is delivered by scripted analysis with no index at all.

**Consequence for decision-making:** assess capture first, always. If capture is missing, a semantic search project cannot proceed until it is fixed. If capture is already solved, as it is here, the only live question is whether retrieval justifies an index.

**Synergies:**

- **Capture quality sets the retrieval ceiling.** Because the JSONL carries timestamps, session ids and tool inputs, an index can filter on metadata before ranking by similarity. Hybrid filtering is substantially more precise than pure similarity.
- **Retrieval preserves the value of capture.** Without an index, a large capture store is effectively write-only and its practical value decays as it grows.
- **They serve different halves of the same audit.** Capture yields the aggregate statistics; semantic retrieval yields the qualitative examples behind them.

**Trap:** building both at once when capture is already solved. That doubles the maintenance surface for zero added recall.

## Caveats

- The corpus begins 2026-05-18; earlier sessions may have rotated out of local storage.
- Query-frequency figures are lower bounds, derived from pattern matching over phrasing and likely to undercount.
- JSONL retention is not guaranteed indefinitely, which is a dependency for any index built over it.

## Related

- [[memory-observation-layer]] - the paired capture concept; read both before deciding
- [[memory-operations]] - store, inject, recall; the existing no-vector-DB rationale
- [[memory-convention]] - what memory stores and what it must not
- [[ai-memory-paradigms]] - generic memory-architecture reference
- [[feedback-build-dont-adopt]] - why adoption, not architecture, is the risk here

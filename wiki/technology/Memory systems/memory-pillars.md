---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: model
---

# The Four Pillars of Memory Systems

> *The architecture-function model every agent memory system implements, whatever technology it uses: **Capture → Storage → Injection → Recall**. The pillars are the jobs underneath memory, not the user-facing capabilities themselves. Capabilities describe what those jobs make possible; features are the concrete mechanisms that implement them.*

> [!note] Status: theory. The model is adopted; no implementation is.
> The **model** has been adopted as the reasoning frame for this environment, recorded separately at [[memory-model-adoption]]. The **enablers, assessments and verdicts** remain theory: nothing has been chosen or built. Where one real environment is quoted, it is a worked example to make the model testable.

## Key Takeaways

- **Four pillars, in dependency order: Capture → Storage → Injection → Recall.** Every memory system implements all four architecture functions, however crudely.
- **Pillars are not use cases, capabilities, features, or enablers.** They are the jobs a memory system must perform. Use cases describe actor-outcome journeys; capabilities describe reusable abilities; features are concrete mechanisms; enablers are technology patterns.
- **Do not confuse a pillar with an enabler.** Pillars are architecture functions; semantic search, capture hooks and curated indexes are technologies or feature patterns that implement them. Mixing the two levels is the most common modelling error in this domain.
- **Assess each pillar separately.** Each has its own "is this solved, and by whom?" answer. Bundling them prices work that is already done.
- **Injection is the pillar most systems under-build**, and the one whose absence is hardest to see, because a healthy Storage layer makes the whole system look fine.
- **Other published memory models are mostly content taxonomies, not functional ones.** They answer "what kinds of memory are there?" rather than "what must a memory system do?" - the two are complementary, not competing. See the correlation section below.

---

## The model

| Pillar | Architecture function | Fails when | Article |
|---|---|---|---|
| **1. Capture** | Get events into a durable record | Events never get recorded | [[memory-capture]] |
| **2. Storage** | Decide what to keep and how it is organised | Records are lost, corrupted, or rot | [[memory-storage]] |
| **3. Injection** | Decide to look, and place material into the context window | Nothing triggers a lookup | [[memory-injection]] |
| **4. Recall** | Find the right material in the store | The right item is never surfaced | [[memory-recall]] |

**Where this sits in the wider taxonomy:**

```text
Use case: actor-outcome journey
Capability: reusable ability the system provides
Architecture function: Capture, Storage, Injection, Recall
Enabler: technology pattern that serves one or more functions
Feature: concrete product mechanism a user or system can invoke, configure, test, or release
```

Example:

| Level | Example |
|---|---|
| Use case | When a long session starts drifting, the AI agent preserves working reasoning so it does not repeat rejected paths |
| Capability | Working reasoning preservation |
| Architecture functions | Capture + Storage + Injection |
| Features | Reasoning checkpoint, working scratchpad, triggered context refresh, compaction summary |

**Dependency runs one way.** Recall cannot return what Storage never kept; Storage cannot keep what Capture never recorded. Injection depends on Recall having something to give it. Assess in order, and stop early if an upstream pillar is broken.

**Each pillar has an independent owner.** Capture is frequently given free by the platform; the other three are almost always built. That is why they must be scored separately: a fused model prices a build that is already paid for.

**Every pillar sub-divides.** Naming the sub-type is not optional, because "improve Recall" and "improve Recall (query-time)" are different pieces of work. Full sub-types live in each pillar's article:

| Pillar | Sub-types |
|---|---|
| Capture | Continuous / periodic / boundary, plus a separate *event-triggered* firing condition |
| Storage | Two independent axes: canonical vs behavioural; and form (synthesise-at-ingest vs store-faithfully) crossed with retention (comprehensive vs curated) |
| Injection | Scheduled / triggered, plus a four-rung trigger hierarchy |
| Recall | Write-time / query-time |

## Provenance: an amendment to three pillars

The widely cited framing is Simon Scrapes' **Three Pillars of Memory Systems** (from "Master Claude Memory"): **Storage**, **Injection**, **Recall**. His Storage pillar is defined as *"the mechanism and timing of saving data... deciding what is memory-worthy... and how it is organized"*.

That definition contains two philosophically opposed functions:

- *"the mechanism and timing of saving data"* is **capture**: indiscriminate, records everything
- *"deciding what is memory-worthy"* is **storage**: curated, decides what to keep

**His own document splits them twice.** His comparison table carries a *Data Philosophy* row contrasting MemSearch ("Comprehensive: captures everything") with Hermes ("Curated: agent decides what is worth keeping"), which is exactly this axis. And his implementation section "Stage 1: Optimized Storage" lists three different functions as bullets: Automatic Transcript Capture, Curated Fact Writing, Nightly Indexing.

**Indexing is deliberately not promoted to a pillar.** Unlike capture it has no independent "is this solved by the platform?" answer; it is an implementation detail of storage and recall.

## Correlating other published models

External memory models are worth mapping onto the pillars rather than treated as rivals, because most of them are answering a **different question**. The pillars are a *functional* taxonomy: what must the system do? Most published models are *content* taxonomies: what kinds of memory exist, and how hot is each?

### Mark Kashef's six layers

| Kashef layer | Maps to | Notes |
|---|---|---|
| **Identity** (~100 tokens, always loaded, never changes) | **Storage** (behavioural branch) + **Injection** (scheduled) | A storage tier defined by its injection policy. "Always loaded" is an injection statement, not a storage one |
| **Critical Context** (~300 tokens, current project and blockers, survives compaction) | **Storage** (behavioural) + **Injection** (scheduled, with a compaction requirement) | "Survives compaction" is the interesting part: it demands either re-injection after compaction or a [[memory-capture|PreCompact-style]] mechanism |
| **Working Memory** (session-scoped, resets on close) | **Not a pillar at all** | This is the context window itself, the *target* of Injection rather than a memory store. It is what the other layers are injected *into* |
| **Long-Term Knowledge** (searched: facts, decisions, patterns) | **Storage** (canonical branch) + **Recall** (query-time) | "Searched" is the giveaway that a Recall mechanism is assumed |
| **Episodic Memory** (archived, full conversation history, preserves the WHY) | **Capture** output + **Storage** (verbatim form) | Exactly what native JSONL transcripts are, and what MemPalace stores by design |
| **Decay** (background: old memories compress, frequently used resist) | **Storage** (retention axis) | A retention *process*. ClaudeClaw's importance-tiered salience decay is a working implementation |

**What the correlation reveals:**

- **Kashef's model is largely a Storage-tier taxonomy with injection policy baked into each tier.** The token budgets (~100, ~300) are injection budgets, and they refine Simon's single undifferentiated ~1,300-3,000 token frozen snapshot into graded tiers. That is a genuine contribution the pillar model does not currently make: it says nothing about *how to divide* the scheduled-injection budget.
- **There is no Kashef layer for Capture or Recall as functions.** Both are implied inside "archived" and "searched" - which is the same conflation the pillar model exists to prevent. A system could satisfy all six layers on paper and still have no working Injection trigger.
- **"Working Memory" is not memory** in the four-pillar sense. Treating the context window as a memory layer alongside persistent stores is a category error, though a common and understandable one.
- **The two models are complementary.** Use the pillars to ask *what must this system do, and is each part solved?* Use a layer model like Kashef's to ask *what content tiers exist, and what is each one's injection budget?* Neither answers the other's question.

## Keep the levels apart

A **pillar** is an architecture function the system must perform. An **enabler** is a technology pattern that performs or supports that function. One enabler can serve more than one pillar, and one pillar can be served by several competing enablers.

A **capability** names what you *get* once the necessary architecture functions are working. A capability is not a technology and not a component; it is the reusable ability the system provides. The current catalogue lives in [[memory-capabilities]] and links each capability to its primary use case and representative features.

A **feature** is a concrete mechanism a user or system can invoke, configure, test, release, or buy. `PreCompact` hooks, `SessionStart` injection, vector search, BM25, temporal graphs, and scope predicates are features or feature families. They implement or expose capabilities; they are not capabilities just because they are valuable.

**Capabilities are usually cross-pillar and are catalogued separately, in [[memory-capabilities]].** A pillar article may link to the capabilities it *participates in*, but participation is not ownership: no pillar owns a capability, and a capability never "enables" a pillar. When a capability is absent, name the pillar **and sub-type** at fault ("compaction survival is missing because Injection (triggered) is unimplemented"), not the pillar alone.

| Enabler | Serves | Article |
|---|---|---|
| Native session transcripts | Capture (continuous) | [[memory-capture]] |
| Session-end summarising hooks | Capture (boundary) | [[memory-capture]] |
| Interval checkpoint hooks | Capture (periodic) | [[pillars-mempalace]] |
| Compaction-event capture hooks | Capture (event-triggered) | [[pillars-mempalace]] |
| Curated index hierarchy plus bare wikilinks | **Recall (write-time)** | [[memory-features#Curated Index Retrieval|Memory Features]] |
| Keyword search, grep | **Recall (query-time)** | (no dedicated article) |
| Vector / embedding index | **Recall (query-time)**, and the most *scalable* enabler of **Injection (triggered)** | [[memory-features#Semantic Search|Memory Features]] |
| Curated trigger table | **Injection (triggered)**, hand-written topic-to-file rules, no embeddings. Cheap and exact, but scales only to a handful of rules and depends on the agent noticing the trigger | [[memory-injection]] |
| Frozen snapshot of consolidated files | **Injection (scheduled)** | [[memory-injection]] |
| Deterministic per-turn hint with agent-decided retrieval | **Injection**, trigger rung 3 - injects no content itself | [[pillars-memsearch]] |

Naming a file or a design after an enabler and then filling it with pillar doctrine is the same category error as bundling capture into storage, one level up. Ask of any component: *is this a job the system must do, a way of doing that job, or something you get once the job is done?*

---

## Compaction and context rot: which pillars actually fix them

This spans Capture and Injection together, which is why it lives in the overview rather than in either pillar's article.

Neither phenomenon is a storage failure *on the assumption that capture already has everything durably recorded*. That assumption holds for continuous capture. It does not always hold for periodic or boundary capture.

| | What happens | Anything lost from disk? | Fixed by |
|---|---|---|---|
| **Compaction** | Material leaves the context window, replaced by a summary | **No, if capture is continuous. Possibly yes, if capture is periodic or boundary and compaction lands inside the gap between checkpoints** | **Injection** (triggered) restores it to context; **event-triggered Capture** prevents the disk-loss case from happening at all |
| **Context rot** | Material stays in the window; attention and salience degrade | **No** | **Injection** (triggered) plus structure: restatement, checklists, auto-loaded rules |

**Two distinct fixes exist for compaction, addressing two distinct failure modes, and they are easy to conflate.**

- **Injection (triggered)** answers "material left the context window, get it back." It presumes the material is still safely on disk and only needs re-surfacing. This is the correct fix when capture is continuous, as native platform transcripts usually are.
- **Event-triggered Capture** answers a sharper question: "is the material on disk in the first place?" A system with periodic or boundary capture has, by construction, a window of uncaptured material between checkpoints. If compaction fires inside that window, the material is compacted out of context *and was never durably recorded* - lost twice over, and triggered injection has nothing to restore. The fix is a capture hook firing on the compaction event itself. **Verified example:** MemPalace's `PreCompact` hook; see [[pillars-mempalace]].

**Which fix a system needs depends entirely on its own Capture mode.** Continuous capture needs only the Injection fix. Periodic or boundary capture needs the event-triggered Capture fix as well.

**Where capture is already solved by the platform and is continuous, only the retrieval and injection stages need building.** A proposal that includes a capture stage in that situation is paying twice. That changes if the platform's capture is periodic or boundary.

## Related

**The model**
- [[memory-capabilities]] - the cross-pillar capability catalogue: what you get, as opposed to what the system does
- [[memory-use-cases]] - actor-outcome journeys that explain why memory is needed

**The four pillars**
- [[memory-capture]] - Capture, and the Observation capability it produces
- [[memory-storage]] - Storage, and its two independent axes
- [[memory-injection]] - Injection, the pillar most systems under-build
- [[memory-recall]] - Recall, and the write-time/query-time fork

**Enablers**
- [[memory-features]] - feature catalogue including curated index retrieval, semantic search, hooks, graphs, and ranking features

**Context**
- [[memory-model-adoption]] - the decision record adopting this frame here
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time, the broad sense of "memory"
- [[openbrain-vs-agentic-os]] - two query-time implementations compared

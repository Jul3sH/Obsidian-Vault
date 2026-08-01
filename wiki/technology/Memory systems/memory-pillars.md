---
type: reference
updated: 2026-07-31
authority: analysis-backed
concept: model
---

# The Four Pillars of Memory Systems

> *The functional model every agent memory system implements, whatever technology it uses: **Capture → Storage → Injection → Recall**. This article defines the pillars. The technologies that implement them are covered in separate enabler articles.*

> [!note] Status: theory. The model is adopted; no implementation is.
> Reference material on how agent memory systems work. The **model** on this page has been adopted as the reasoning frame for this environment, recorded separately at [[memory-model-adoption]]. The **enablers, assessments and verdicts** remain theory: nothing has been chosen or built. Where one real environment is quoted, it is a worked example to make the model testable.

## Key Takeaways

- **Four pillars, in dependency order: Capture → Storage → Injection → Recall.** Every memory system implements all four, however crudely.
- **Do not confuse a pillar with an enabler.** Pillars are *functions*; semantic search, capture hooks and curated indexes are *technologies* that implement them. Mixing the two levels is the most common modelling error in this domain.
- **Storage divides on two independent axes.** *Kind of claim*: canonical versus behavioural, split by whether the content answers "is this true?" or "does this change how I act?". *Form and retention*: synthesise at ingest versus store faithfully, crossed with comprehensive versus curated retention. The second axis is what separates MemSearch, Hermes, OpenBrain and a Karpathy wiki from each other.
- **Injection has two types**, scheduled and triggered, and only the second can defend against mid-session degradation.
- **Assess each pillar separately.** Each has its own "is this solved, and by whom?" answer. Bundling them prices work that is already done.

---

## The model

| Pillar | Function | Fails when |
|---|---|---|
| **1. Capture** | Get events into a durable record | Events never get recorded |
| **2. Storage** | Decide what to keep and how it is organised | Records are lost, corrupted, or rot |
| **3. Injection** | Decide to look, and place material into the context window | Nothing triggers a lookup |
| **4. Recall** | Find the right material in the store | The right item is never surfaced |

**Dependency runs one way.** Recall cannot return what Storage never kept; Storage cannot keep what Capture never recorded. Injection depends on Recall having something to give it. Assess in order, and stop early if an upstream pillar is broken.

**Each pillar has an independent owner.** Capture is frequently given free by the platform; the other three are almost always built. That is why they must be scored separately: a fused model prices a build that is already paid for.

## Provenance: an amendment to three pillars

The widely cited framing is Simon Scrapes' **Three Pillars of Memory Systems** (from "Master Claude Memory"): **Storage**, **Injection**, **Recall**. His Storage pillar is defined as *"the mechanism and timing of saving data... deciding what is memory-worthy... and how it is organized"*.

That definition contains two philosophically opposed functions:

- *"the mechanism and timing of saving data"* is **capture**: indiscriminate, records everything
- *"deciding what is memory-worthy"* is **storage**: curated, decides what to keep

**His own document splits them twice.** His comparison table carries a *Data Philosophy* row contrasting MemSearch ("Comprehensive: captures everything") with Hermes ("Curated: agent decides what is worth keeping"), which is exactly this axis. And his implementation section "Stage 1: Optimized Storage" lists three different functions as bullets: Automatic Transcript Capture, Curated Fact Writing, Nightly Indexing.

**Indexing is deliberately not promoted to a pillar.** Unlike capture it has no independent "is this solved by the platform?" answer; it is an implementation detail of storage and recall.

## Pillars versus enablers: keep the levels apart

A **pillar** is a function the system must perform. An **enabler** is a technology that performs it. One enabler can serve more than one pillar, and one pillar can be served by several competing enablers.

| Enabler | Serves | Article |
|---|---|---|
| Native session transcripts | Capture (continuous) | [[memory-observation-layer]] |
| Session-end summarising hooks | Capture (boundary) | [[memory-observation-layer]] |
| Curated index hierarchy plus bare wikilinks | **Recall (write-time)** | [[memory-curated-index]] |
| Keyword search, grep | **Recall (query-time)** | (no dedicated article) |
| Vector / embedding index | **Recall (query-time)**, and the only practical enabler of **Injection (triggered)** | [[memory-semantic-search]] |
| Frozen snapshot of consolidated files | **Injection (scheduled)** | [[memory-pillars]], below |

Every pillar sub-divides, so name the sub-type when stating what an enabler serves. "Serves Recall" is ambiguous; "serves Recall (write-time)" is not.

Naming a file or a design after an enabler and then filling it with pillar doctrine is the same category error as bundling capture into storage, one level up. Ask of any component: *is this a job the system must do, or a way of doing that job?*

---

## Pillar 1: Capture, and its two modes

Getting events into a durable record. The defining test is that **it creates a record that did not previously exist**.

Capture is indiscriminate by nature. It does not judge importance; that judgement belongs to Storage. It divides on **granularity**:

| | **Continuous capture** | **Boundary capture** |
|---|---|---|
| Fires | Every turn | At session end, or another boundary |
| Completeness | Total, verbatim | Lossy; usually a summary |
| Cost | Per-turn runtime cost | One cost per session |
| Risk | Volume; store grows fast | Loses detail the summariser dropped |

Native platform transcripts are usually continuous. Hook-based summarisers are usually boundary. Full treatment, including when a capture mechanism is justified at all: [[memory-observation-layer]].

## Pillar 2: Storage, and its two axes

Storage decides what is kept and how it is organised. It divides twice, on **independent** axes: *what kind of claim* the content makes, and *what form it takes and how much survives*. A system's position on one says nothing about its position on the other.

### First axis: what kind of claim (canonical vs behavioural)

In practice this splits into two stores that answer different questions, are authored differently, and fail differently. Conflating them is what makes the question "is a wiki memory?" feel unanswerable.

| | **Canonical branch** | **Behavioural branch** |
|---|---|---|
| Question it answers | **"Is this true?"** | **"Does this change how I act?"** |
| Content | Decisions, evidence, domain knowledge, synthesis | User profile, standing behavioural corrections |
| Typical form | A maintained wiki or document store | Memory files loaded by the agent |
| Authored by | An agent acting as librarian, deliberately | Proposed by the agent, approved by the human |
| Volume | Large, grows without bound | Small by design, bloat degrades it |
| Loading | Recall, on demand | Index injected, bodies on demand |
| Cost of being wrong | Stale or incorrect facts | Repeated mistakes |

**The filing test:** a fact about the world belongs in the canonical branch however important it is. A rule about behaviour belongs in the behavioural branch however trivial it is. Importance does not decide; the *kind of claim* does.

**"Behavioural" means rules *for* behaviour, not records *of* it.** Captured session activity is the Capture pillar's output and belongs nowhere near this branch. A user profile qualifies only because its contents are operating instructions: a fact about the person that does not change how the agent acts belongs in the canonical branch.

### Second axis: what form, and what survives

Two sub-questions, and together they explain why the product landscape looks inconsistent.

**Form: when does synthesis happen?**

- **Synthesise at ingest (write-time).** What lands in the store is already processed. Cheap to read, lossy: the editorial decisions are baked in.
- **Store faithfully, synthesise at query (query-time).** What lands is raw. Nothing is lost, but every read pays the synthesis cost.

This is the same decision that appears as Recall's write-time/query-time sub-types, seen from the other end. It is *made* at write and it *constrains* how retrieval can work, which is why it belongs to both pillars. Treated in depth in [[wiki-vs-openbrain]].

**Retention: what survives?**

- **Comprehensive.** Keep everything, prune nothing.
- **Curated.** An agent or human decides what is worth keeping; the rest is pruned or capped.

Simon Scrapes' comparison table calls this the *Data Philosophy* row. It is also the axis that justified splitting Capture out of Storage in the first place, since indiscriminate capture and curated retention are opposite instincts.

**The two are independent**, which is what makes the products legible:

| | **Comprehensive retention** | **Curated retention** |
|---|---|---|
| **Synthesise at ingest** (write-time) | **MemSearch** - Haiku summarises every turn at capture and the summary is vectorised; raw dialogue retained only as a last-resort retrieval tier | **Karpathy wiki** - compiles articles on ingest, raw kept but not primary. **Hermes** - agent-curated `memory.md`/`user.md` with character caps, prunes raw transcripts every 7 days |
| **Store faithfully** (query-time) | **OpenBrain** - faithful `thoughts` table, no synthesis until asked | Rare and mostly incoherent: pruning raw while deferring synthesis discards the material the synthesis would need |

**A common misreading:** MemSearch is often described as "the one that stores raw data". Its own documentation says the opposite - it summarises each turn with Haiku *at capture* and indexes that summary. Its distinctive property is **completeness of retention**, not rawness of form. Both MemSearch and Hermes process at ingest; they differ on what they throw away.

### Why "memory" gets used at two scales

- **Broad sense:** any mechanism that persists knowledge across sessions. A maintained wiki *is* a memory paradigm in this sense. See [[wiki-vs-openbrain|AI Memory Paradigms]].
- **Narrow sense:** the small curated behavioural store an agent loads at session start, protected from bloat.

A knowledge base can be memory in the first sense while its own rules correctly forbid putting knowledge-base content into memory in the second sense. Both usages are legitimate once both are recognised as branches of Storage.

### The assessment trap

**A strong canonical branch can make Capture look unnecessary while leaving Injection and Recall entirely unaddressed.** The canonical branch is the most visible pillar and the easiest to mistake for the health of the whole system. Judging a memory system by it alone will systematically miss an injection failure.

## Pillar 3: Injection, and its two types

Injection decides **to look at all**, and places material into the context window. Retrieval quality is irrelevant if nothing triggers a lookup.

| | **Scheduled injection** | **Triggered injection** |
|---|---|---|
| When | Once, at session start | Mid-session, in response to a turn |
| Trigger | Deterministic, time-based | Something must *decide* a lookup is needed |
| Typical form | "Frozen snapshot" of consolidated files, roughly 1,300 to 3,000 tokens | Query against the store, top-k results injected |
| Token cost | Fixed, predictable, cacheable | Variable, risks bloating context |
| Defends against | **Cold-start amnesia** | **Compaction loss and context rot** |
| Cannot fix | Anything degrading *during* a session, because it fires once, before the degradation | Nothing structural, but far harder to build well |

**Simon's Injection pillar is the scheduled type**: frozen snapshots at session start. Sound against cold-start amnesia, and cheap because it caches. It cannot address mid-session degradation, because it has already fired by the time degradation begins.

### The trigger problem

Something has to decide a lookup is warranted. In ascending reliability:

1. **The user asks.** Fragile: depends on the human remembering that relevant material exists.
2. **The agent decides.** Measured at roughly 25% in one real corpus; see [[memory-curated-index]].
3. **A hook fires on every turn.** Deterministic. Pays a retrieval cost per turn whether needed or not.

Only option 3 removes both the human and the agent's judgement from the loop, which is why hook-based designs exist despite their cost.

## Pillar 4: Recall, and its two types

Finding the right material in the store. Recall divides on **when the retrieval signal is computed**, which is the same fork as write-time versus query-time in [[wiki-vs-openbrain|AI Memory Paradigms]].

| | **Write-time recall** | **Query-time recall** |
|---|---|---|
| Signal authored | In advance, by a human or agent | Computed at query, from the content |
| Typical form | Index descriptions, tags, curated links | Embeddings, keyword match |
| Cost profile | Costly on write, near-free at query | Near-free on write, cost recurs per query |
| Wins on | Precision, transparency, zero infrastructure | Coverage, and finding material nobody indexed |
| Fails when | Nothing invokes it, or the corpus outgrows authoring effort | Similarity approximates intent badly; drift on edit |
| Enabler | [[memory-curated-index]] | [[memory-semantic-search]], keyword search |

**The decisive difference is not quality, it is who pays and when.** Write-time recall front-loads human judgement; query-time recall defers it to the machine. A hybrid, curated index over the canonical branch plus a computed index over raw captured material, is usually stronger than either alone because they fail differently.

**Recall and Injection are distinct.** Recall finds material; Injection decides to look and puts the result in context. A system can have excellent recall and still fail entirely, because nothing invokes it.

---

## Compaction and context rot: which pillars actually fix them

Neither phenomenon is a storage failure, so neither is fixed by Capture.

| | What happens | Anything lost from disk? | Fixed by |
|---|---|---|---|
| **Compaction** | Material leaves the context window, replaced by a summary | **No** | **Injection** (triggered) |
| **Context rot** | Material stays in the window; attention and salience degrade | **No** | **Injection** (triggered) plus structure: restatement, checklists, auto-loaded rules |

The commonly proposed architecture (a hook captures each turn, stores it in a vector-indexed database, and material is retrieved and injected back when relevant) does address compaction. The fix is not the capture stage but the **injection** stage.

**Where capture is already solved by the platform, only the retrieval and injection stages need building.** A proposal that includes a capture stage in that situation is paying twice.

## Related

- [[memory-observation-layer]] - enabler for Capture
- [[memory-curated-index]] - enabler for Recall, the manual approach
- [[memory-semantic-search]] - enabler for Recall and triggered Injection
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time, the broad sense of "memory"
- [[openbrain-vs-agentic-os]] - two query-time implementations compared

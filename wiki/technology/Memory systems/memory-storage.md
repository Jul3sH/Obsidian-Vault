---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: pillar
pillar: storage
---

# Storage

> *The second pillar of [[memory-pillars|the four-pillar model]]: deciding what is kept and how it is organised. Depends on [[memory-capture]]; feeds [[memory-recall]]. Storage decides what is kept; Recall decides how it is found again - a store with no retrieval path is not yet memory, and a search with nothing behind it retrieves nothing.*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **Storage divides on two independent axes.** *Kind of claim*: canonical versus behavioural. *Form and retention*: synthesise-at-ingest versus store-faithfully, crossed with comprehensive versus curated. A system's position on one axis says nothing about its position on the other.
- **"Behavioural" means rules *for* behaviour, not records *of* it.** Captured session activity belongs to [[memory-capture]], not here.
- **The form axis is the single biggest differentiator between real products.** MemPalace stores verbatim; every other system assessed synthesises at ingest.
- **A common misreading corrected:** MemSearch is often described as storing raw data. It summarises at capture; its distinctive property is comprehensive *retention*, not raw *form*.
- **A strong canonical branch can make Capture look unnecessary while leaving Injection and Recall entirely unaddressed.** The trap this vault's own history walked into.

---

## First axis: what kind of claim (canonical vs behavioural)

This splits Storage into two stores that answer different questions, are authored differently, and fail differently. Conflating them is what makes the question "is a wiki memory?" feel unanswerable.

| | **Canonical branch** | **Behavioural branch** |
|---|---|---|
| Question it answers | **"Is this true?"** | **"Does this change how I act?"** |
| Content | Decisions, evidence, domain knowledge, synthesis | User profile, standing behavioural corrections |
| Typical form | A maintained wiki or document store | Memory files loaded by the agent |
| Authored by | An agent acting as librarian, deliberately | Proposed by the agent, approved by the human |
| Volume | Large, grows without bound | Small by design, bloat degrades it |
| Loading | [[memory-recall|Recall]], on demand | Index injected, bodies on demand |
| Cost of being wrong | Stale or incorrect facts | Repeated mistakes |

**The filing test:** a fact about the world belongs in the canonical branch however important it is. A rule about behaviour belongs in the behavioural branch however trivial it is. Importance does not decide; the *kind of claim* does.

**"Behavioural" means rules *for* behaviour, not records *of* it.** Captured session activity is [[memory-capture|the Capture pillar's]] output and belongs nowhere near this branch. A user profile qualifies only because its contents are operating instructions: a fact about the person that does not change how the agent acts belongs in the canonical branch.

### Why "memory" gets used at two scales

- **Broad sense:** any mechanism that persists knowledge across sessions. A maintained wiki *is* a memory paradigm in this sense. See [[wiki-vs-openbrain|AI Memory Paradigms]].
- **Narrow sense:** the small curated behavioural store an agent loads at session start, protected from bloat.

A knowledge base can be memory in the first sense while its own rules correctly forbid putting knowledge-base content into memory in the second sense. Both usages are legitimate once both are recognised as branches of Storage.

### The assessment trap

**A strong canonical branch can make Capture look unnecessary while leaving Injection and Recall entirely unaddressed.** The canonical branch is the most visible pillar and the easiest to mistake for the health of the whole system. Judging a memory system by it alone will systematically miss an injection failure.

## Second axis: what form, and what survives

Two sub-questions, independent of the first axis and of each other, and together they explain why the product landscape looks inconsistent.

**Form: when does synthesis happen?**

- **Synthesise at ingest (write-time).** What lands in the store is already processed. Cheap to read, lossy: the editorial decisions are baked in.
- **Store faithfully, synthesise at query (query-time).** What lands is raw. Nothing is lost, but every read pays the synthesis cost.

This is the same decision that appears as [[memory-recall|Recall's]] write-time/query-time sub-types, seen from the other end. It is *made* at write and it *constrains* how retrieval can work, which is why it belongs to both pillars. Treated in depth in [[wiki-vs-openbrain]].

**Retention: what survives?**

- **Comprehensive.** Keep everything, prune nothing.
- **Curated.** An agent or human decides what is worth keeping; the rest is pruned or capped.

Simon Scrapes' comparison table calls this the *Data Philosophy* row. It is also the axis that justified splitting Capture out of Storage as its own pillar in the first place, since indiscriminate capture and curated retention are opposite instincts.

**The two are independent**, which is what makes the products legible:

| | **Comprehensive retention** | **Curated retention** |
|---|---|---|
| **Synthesise at ingest** (write-time) | **MemSearch** - Haiku summarises every turn at capture and the summary is vectorised; raw dialogue retained only as a last-resort retrieval tier | **Karpathy wiki** - compiles articles on ingest, raw kept but not primary. **Hermes** - agent-curated `memory.md`/`user.md` with character caps, prunes raw transcripts every 7 days. **ClaudeClaw** - importance-gated at ingest, then daily salience decay prunes what survived |
| **Store faithfully** (query-time) | **OpenBrain** - faithful `thoughts` table, no synthesis until asked. **MemPalace** - explicitly verbatim, "does not summarize, extract, or paraphrase" | Rare and mostly incoherent: pruning raw while deferring synthesis discards the material the synthesis would need |

**A common misreading:** MemSearch is often described as "the one that stores raw data". Its own documentation says the opposite - it summarises each turn with Haiku *at capture* and indexes that summary. Its distinctive property is **completeness of retention**, not rawness of form. Both MemSearch and Hermes process at ingest; they differ on what they throw away.

## Capabilities and features across systems

Transposed from the four product scorecards. Everything below is Storage-pillar behaviour: what is kept, how it is organised, and what it costs.

| Capability | Systems | Detail |
|---|---|---|
| **Verbatim storage, no synthesis** | MemPalace | The one product assessed on the opposite pole from every other: explicitly not summarised, extracted, or paraphrased |
| **Markdown-canonical, vector-index disposable** | MemSearch | Journals are the source of truth; the vector index is described in its own docs as a "shadow index... derived, rebuildable cache". Losing it is a performance problem, not a data-loss problem |
| **Vector store treated as load-bearing** | ClaudeClaw, agentic-os | The opposite position to MemSearch: rebuilding the index is not assumed cheap or automatic |
| **Structural scoping for search** (a hierarchy content is filed into, so a search can be scoped rather than run flat) | MemPalace | Wings (people/projects) containing Rooms (topics) containing Drawers (original content) |
| **Scope-partitioned storage for multi-tenant isolation** | agentic-os | Every row carries `private`/`client`/`team`/`system`; enforced in application code and the database, with no-leak tests |
| **Importance-tiered decay** | ClaudeClaw | Daily salience multiplier keyed to importance (0.99 / 0.98 / 0.95); pinning exempts a memory entirely |
| **Curated distillation layer over a raw journal** | MemSearch (`PROJECT.md`/`USER.md`, background-maintained) | Closer in spirit to the behavioural branch above, though MemSearch does not itself name the canonical/behavioural distinction |
| **Second, periodic synthesis pass across already-stored memories** | ClaudeClaw (`runConsolidation`) | Distinct from ingest-time synthesis: clusters existing memories and derives a merged insight, stored with its own embedding |
| **Pluggable storage backend** | MemPalace | Backend interface abstracted; ChromaDB is the default, swappable without touching the rest of the system |
| **Procedural memory** (a third memory *type*, storing reusable workflows rather than facts) | MemSearch ("Skills from Memory") | Distils repeated workflows into portable, installable Agent Skills. Does not map onto the canonical/behavioural split, or onto any single pillar - closer to a memory system generating a new *enabler* than storing a fact |
| **External published benchmark for retrieval quality** | MemPalace | 96.6% R@5 on LongMemEval, cited directly - the only one of the four systems assessed to ground a capability claim this way rather than by internal description |

## Related

- [[memory-pillars]] - the four-pillar model overview
- [[memory-capture]] - upstream dependency; what Storage receives
- [[memory-recall]] - downstream; the write-time/query-time fork on the form axis is the same decision seen from the retrieval side
- [[memory-injection]] - the canonical/behavioural split determines what is eligible for scheduled injection
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from
- [[wiki-vs-openbrain|AI Memory Paradigms]] - write-time versus query-time, the fork the form axis sits on

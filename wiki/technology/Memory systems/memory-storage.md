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
- **Content moves within Storage via five distinct transformations**: promotion (deletes its sources), consolidation (keeps them), compression (rewrites shorter), decay (reweights without rewriting), revision (corrects what is now wrong). Promotion and add-only storage are in direct tension and coexist only if scoped to different branches.
- **Revision is the only transformation driven by correctness**, and the only one whose *trigger* is usually missing: the other four fire on recurrence, relatedness, budget, or time, all of which a system can detect for itself. Nothing detects that a stored fact has quietly become false.

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

## Transformations: how content moves within Storage

Both axes above describe where content *sits*. A third question is how it *moves* once stored, because material does not stay in the form it arrived in. Five distinct transformations, often conflated:

| Transformation | What happens | Sources kept? | Verified example |
|---|---|---|---|
| **Promotion** | A pattern observed repeatedly becomes a standing rule | **No - deleted** | agentic-os `daily-memory-distill` |
| **Consolidation** | Related memories are merged into a derived insight | **Yes - retained** | ClaudeClaw `runConsolidation` |
| **Compression** | Existing content is rewritten shorter | Superseded in place | agentic-os `weekly-memory-curator` |
| **Decay** | Content loses ranking weight without changing | Yes, until pruned | ClaudeClaw salience decay |
| **Revision** | Content that has become wrong is corrected or retired | **Branch-dependent** - retained on the canonical branch, replaced on the behavioural | MemPalace `valid_from`/`valid_to`; ClaudeClaw `superseded_by` |

### Promotion

**A pattern seen enough times stops being an observation and becomes a rule. The observations are discarded; the rule persists.**

This is the transformation that moves content from the [[memory-capture|Capture]] output into the **behavioural branch** of Storage. It is threshold-triggered rather than continuous: nothing happens until the pattern recurs often enough to be worth generalising.

Verified example: agentic-os's `daily-memory-distill` cron job, whose own description is *"Promotes durable facts from today's session log into `context/MEMORY.md`"*. It reads the day's session log, extracts durable facts, and writes them into the curated scratchpad. The session log is not the store of record afterwards.

A second, widely-described example is Claude Code's native behaviour of promoting a preference to a global memory folder once it recurs three or more times. **Unverified** - quoted second-hand and not confirmed against source or documentation.

**This vault runs promotion manually.** A correction that recurs becomes a `feedback-*.md` rule, and the individual corrections are not retained. The rule survives; the observations that produced it do not.

**Promotion is lossy on purpose, and that is the point.** It trades the evidence for the conclusion. The cost is that the reasoning becomes unavailable: a rule with no surviving observations behind it cannot be re-derived, audited, or revised in light of a counter-example, because there is nothing left to weigh against it.

### Promotion versus consolidation

Easily confused, and the distinction is whether sources survive.

- **Promotion deletes.** The observations are consumed producing the rule.
- **Consolidation retains.** ClaudeClaw's `runConsolidation` clusters memories, derives a merged insight, and stores it *alongside* the originals with its own embedding. Both remain queryable.

Consolidation is additive and reversible; promotion is neither.

### The tension with add-only

Promotion and **add-only** storage pull in opposite directions, and a system can hold only one as a general rule.

- **Add-only** never overwrites. A fact that changes produces a second fact with its own validity window, and both persist. The system can answer what was true *then*. See [[memory-recall]] on temporal validity.
- **Promotion** deliberately destroys its inputs.

**They coexist only if scoped to different content.** The workable split is that the canonical branch is add-only, preserving the record, while the behavioural branch permits promotion, keeping the rule set small enough to stay injectable. That is not a compromise so much as a recognition that the two branches have opposite requirements: the canonical branch is judged on completeness, the behavioural branch on brevity, since it competes for [[memory-injection|scheduled injection budget]].

### Revision

**A stored item stops being true, and the store has to stop asserting it.** This is the transformation the other four cannot perform: promotion generalises, consolidation merges, compression shortens, decay demotes. None of them corrects.

**Its driver is correctness, and that is what makes it structurally different.** The other four are driven by recurrence, relatedness, budget and time respectively - all properties the system can observe about *itself*. Correctness is a property of the world, so nothing internal to the store can detect that a fact has gone stale. **Revision is therefore the transformation most likely to have a mechanism but no trigger:** editing a file is trivial, knowing it needs editing is not.

**The two strategies fall out of the canonical/behavioural split**, the same division that resolves the promotion tension above.

| Branch | Strategy | Sources | Verified example |
|---|---|---|---|
| **Canonical** | **Add-only revision.** Append the corrected fact with its own validity window and close the old one off | Retained. The store can still answer what was true *then* | MemPalace: `valid_from` → `valid_to` on every edge, superseded facts retained rather than overwritten, with an explicit precedence rule when facts conflict |
| **Behavioural** | **Destructive revision.** Supersede or overwrite in place | Replaced, because the branch is judged on brevity and competes for [[memory-injection|injection budget]] | ClaudeClaw: a `superseded_by` column on the `memories` table |

That the same branch split resolves both the promotion tension and the revision strategy is evidence the split is real rather than a convenience.

**Deletion is revision's terminal case, not a separate transformation.** Retiring an item that is simply wrong, rather than replacing it, is the degenerate form where the corrected value is empty. On the canonical branch it should still be a closed validity window rather than a true delete, so the record of having believed it survives.

**This vault runs revision manually, with no trigger.** `user.md` and the `feedback-*.md` rules are edited by hand when someone notices they have gone wrong. Nothing surfaces a candidate. A worked instance: `user.md` carries a Hong Kong environment block (VPN routing constraints) that becomes false on a relocation that is already committed and dated, and no mechanism connects the project's completion to the memory that depends on it. The mechanism is fine; the trigger does not exist.

### Compression versus decay

Also frequently merged, and also distinct.

- **Decay** changes a memory's *weight* without changing its *content*. ClaudeClaw multiplies `salience` daily by an importance-tiered factor; the text is untouched and a pinned memory is exempt entirely.
- **Compression** changes the content itself, rewriting it shorter. agentic-os's `weekly-memory-curator` consolidates duplicates, removes resolved entries, and enforces the 2,500-character cap on `MEMORY.md`.

**Compression is usually budget-driven, decay usually relevance-driven.** The curator compresses because the tier has a hard cap; decay demotes because the material stopped being used. A system can run both, and agentic-os and ClaudeClaw between them demonstrate each.

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
| **Second, periodic synthesis pass across already-stored memories** | ClaudeClaw (`runConsolidation`) | Distinct from ingest-time synthesis: clusters existing memories and derives a merged insight, stored with its own embedding. Sources are retained, so this is consolidation rather than promotion |
| **Promotion of recurring observations into standing rules** | agentic-os (`daily-memory-distill`) | Reads the day's session log, extracts durable facts, writes them into the curated `MEMORY.md` scratchpad. The session log is not the store of record afterwards |
| **Budget-driven compression against a hard cap** | agentic-os (`weekly-memory-curator`) | Consolidates duplicates, removes resolved entries, enforces the 2,500-character cap on `MEMORY.md` |
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

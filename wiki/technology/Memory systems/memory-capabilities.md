---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: catalogue
---

# Memory Capabilities

> *The demand-side view of agent memory. The [[memory-pillars|four pillars]] say what a system must **do**; this catalogue says what you **get**. Every capability draws on more than one pillar, which is why it cannot be filed inside any single pillar article.*

## Key Takeaways

- **A capability is an outcome, not a function and not a technology.** It is the standing ability you acquire once the pillars underneath it are implemented. Pillar → enabler → capability are three distinct levels; see [[memory-pillars]].
- **Capabilities are cross-functional by construction.** Every entry below spans two or more pillars. A pillar article may link to a capability it participates in, but **participation is not ownership** - no pillar owns a capability, and a capability is never "the thing that enables" a pillar. The dependency runs the other way.
- **Two capabilities are commonly fused and must not be.** *Critical context injection* (session start) and *compaction survival* (mid-session) have different triggers and different mechanisms. Real systems demonstrably implement one without the other.
- **The list is open.** Ten are catalogued; more will be added as they are identified. Absence from this list is not evidence that a capability does not exist.
- **Assess capabilities, not pillars, when deciding what to build.** A pillar can be half-built and still deliver one capability fully while delivering another not at all.

---

## Why capabilities need their own home

[[memory-pillars]] defines the term:

> *A third term, **capability**, names what you get once a pillar is implemented - not a technology, an outcome.*

The pillar articles were each carrying "a catalogue of capabilities observed across real products". That filing breaks down, because **no capability sits inside one pillar**. Compaction survival is the clearest case: it is triggered by Injection, may depend on Capture, and is currently discussed in the cross-pillar section of the overview only because it has nowhere else to live.

Filing by pillar forces a cross-pillar object into a single-pillar box. This file is that box, correctly shaped.

## How pillars and capabilities link

```
   PILLARS (what the system must do)
   Capture · Storage · Injection · Recall
        │        │         │        │
        └────────┴────┬────┴────────┘
                      │  many-to-many
                      ▼
   CAPABILITIES (what you get)
   identity persistence · compaction survival · ...
```

- A pillar article **may** list the capabilities it participates in. This is useful navigation.
- It **must not** describe that capability as belonging to it, or as something that enables it.
- When a capability is missing, the diagnosis names the **pillar and sub-type** at fault, e.g. "compaction survival is missing because Injection (triggered) is unimplemented", never "Injection is missing".

## The catalogue

**State legend:** ✅ have · ⚠ partial or manual · ✗ missing · Confirmed = assessed in detail; Provisional = first-pass judgement, not yet worked through.

| # | Capability | What you get | Pillars spanned | State here | Confidence |
|---|---|---|---|---|---|
| 1 | **Identity persistence** | The agent knows who you are without being told, every session | Storage (behavioural) + Injection (scheduled) | ⚠ store excellent, delivery 10% | Confirmed |
| 2 | **Critical context injection** | The agent knows what you are working on without being told | Storage (behavioural) + Injection (scheduled) | ✗ content exists, no mechanism | Confirmed |
| 3 | **Compaction survival** | Material pushed out by compaction returns mid-session | Injection (triggered); **+ Capture (event-triggered) only where capture is not continuous** | ⚠ largely native, not deterministic | Confirmed |
| 4 | **In-session reasoning retention** | Dead ends, rejected options and the reasoning behind them survive to session end | Capture (boundary) + Storage | ✗ none | Provisional |
| 5 | **Long-term knowledge recall** | Find a fact, decision or pattern recorded months ago | Storage (canonical) + Recall | ✅ 541-file wiki | Provisional |
| 6 | **Observation / episodic recall** | Answer "what happened?" or "why did we decide X?" for any past session | Capture (continuous) + Storage (verbatim) + Recall (query-time) | ⚠ transcripts captured, not searchable | Provisional |
| 7 | **Retention management** | Old material compresses or archives rather than accumulating | Storage (retention axis) | ⚠ manual `_archived/` folders | Provisional |
| 8 | **Pattern promotion** | Observations seen repeatedly become standing rules | Storage + a promotion process | ⚠ manual, two-key process | Provisional |
| 9 | **Query-time search** | Find relevant material you did not know to ask for | Recall (query-time) | ⚠ grep only | Provisional |
| 10 | **Write-time navigation** | Curated indexes and links surface the right material without any search | Recall (write-time) | ✅ index hierarchy + bare wikilinks | Provisional |

## Notes on individual capabilities

**1 - score the delivery, not the store.** A capability is an outcome, so a rich, well-maintained store scores nothing on its own if nothing reliably puts it in context. The trap is that the store is the visible artefact and the delivery mechanism is invisible, so inspection flatters the system. **Measure the delivery rate before scoring any capability whose store looks healthy.** Measured here: `user.md` is a strong identity file fetched *by instruction* rather than injected by a hook, and was opened in **5 of 47 substantive sessions (10%)**, corroborating the 8% figure independently recorded in [[memory-injection]]. The store is ✅ and the capability is ⚠, because the hottest tier in the hierarchy sits on the coldest delivery mechanism.

**2 vs 3 - the split that matters.** These are independent, and the products prove it. [[pillars-mempalace|MemPalace]] has a `PreCompact` hook (capability 3) and **no injection layer at all** (no capability 2). A bare `SessionStart` hook is the exact inverse. Anything that treats "inject memory" as one job will build one and silently miss the other.

**2 - the injected pointer should be derived, not stored.** The obvious build is a `context.md` holding "current project, blockers, next step". That is a *copy* of state the canonical record already owns, so it drifts the moment the real document moves on, and it violates single-source-of-truth. Where the store already carries machine-readable state, the pointer can instead be **computed at injection time**. Verified here: every file in `wiki/projects/` carries `status`, `flow` and `status-updated` frontmatter, so the set of live projects is derivable by filtering `flow: implementing` and sorting by date - no second copy, nothing to maintain, nothing to go stale. **Test before building any context store: does the canonical record already encode this, and can the injector just read it?**

**2 - a derived pointer doubles as a staleness detector.** Because it surfaces `status-updated` every session, a project still marked live but untouched for weeks becomes visible continuously rather than never. Two such cases were found the first time this was run here.

**3 - measure the platform's native behaviour before scoring this missing.** A host that compacts by *summarising* rather than truncating already delivers much of this capability for free, and scoring it ✗ prices work that is already done. Measured on Claude Code here: compaction occurred in **17 of 49 sessions** (long analytical sessions compacting up to five times), and each event produced a structured **~2,500-2,760 word** summary that preserved user identity, project, and decisions taken. Add to that the material a host never compacts at all - system-prompt rulebooks (`CLAUDE.md`, `AGENTS.md`), native auto-memory indexes, and everything on disk - and the residual loss is narrow.

**3 - the real gap is usually determinism, not survival.** An LLM-written summary cannot guarantee any *specific* item persists. The failure is probabilistic and silent: a fact survives one compaction and not the next, with no signal either way. So the useful build is not "preserve the session" (the host does that) but "re-assert the few things that must not be lost" - which is the **same injected payload as capability 2**, fired on a second event. Where that is true, the two capabilities share one build even though they remain separate capabilities.

**3 - the Capture dependency is conditional.** Compaction removes material from the context window; it destroys nothing on disk **provided capture is continuous**. Where capture is continuous (native session transcripts), this capability needs only Injection (triggered). Where capture is periodic or boundary, compaction can land in the gap between checkpoints and the material is lost twice over, so an event-triggered Capture hook is also required. See the compaction table in [[memory-pillars]].

**4 - not the same as "working memory".** Kashef's Working Memory layer is the context window itself, which [[memory-pillars]] correctly rejects as a category error: the context window is the *target* of Injection, not a store. The genuine capability is narrower - persisting the reasoning generated in-session that has not yet been written to a durable record. Project state already on disk does not need it.

**6 - capture being solved does not deliver the capability.** Continuous transcript capture is free from the platform, so the Capture pillar is complete. The capability is still absent, because Recall (query-time) over those transcripts is not implemented. **Verified caution:** naive keyword grep over transcripts produces confident but wrong results - a keyword-frequency filter tested here misidentified a memory-systems session as a project session, because counting mentions does not identify what a session was about.

**9 vs 10 - two different answers to Recall.** Write-time navigation pays the cost up front by curating indexes and links; query-time search pays at retrieval. They are complements, not rivals. See [[wiki-vs-openbrain]] for the underlying paradigm fork.

## Related

- [[memory-pillars]] - the functional model these capabilities are built from, and the pillar/enabler/capability distinction
- [[memory-capture]] · [[memory-storage]] · [[memory-injection]] · [[memory-recall]] - the four pillars
- [[memory-curated-index]] - the enabler behind capability 10
- [[memory-semantic-search]] - the enabler behind capabilities 6 and 9
- [[pillars-mempalace]] - the worked example separating capabilities 2 and 3

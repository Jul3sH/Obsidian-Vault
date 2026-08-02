---
type: reference
updated: 2026-08-02
authority: analysis-backed
concept: catalogue
---

# Memory Capabilities

> *The demand-side view of agent memory. The [[memory-pillars|four pillars]] say what a system must **do**; this catalogue says what you **get**. Every capability draws on more than one pillar, which is why it cannot be filed inside any single pillar article.*

## Key Takeaways

- **A capability is an outcome, not a function and not a technology.** It is the standing ability you acquire once the pillars underneath it are implemented. Pillar → enabler → capability are three distinct levels; see [[memory-pillars]].
- **Capabilities are cross-functional by construction.** Every entry below spans two or more pillars. A pillar article may link to a capability it participates in, but **participation is not ownership** - no pillar owns a capability, and a capability is never "the thing that enables" a pillar. The dependency runs the other way.
- **Two capabilities are commonly fused and must not be.** *Critical context injection* (session start) and *compaction survival* (mid-session) have different triggers and different mechanisms. Real systems demonstrably implement one without the other.
- **Use cases, capabilities and features are linked, not collapsed.** A use case is the actor-outcome journey; a capability is the reusable ability that enables it; a feature is a concrete mechanism that implements or exposes the ability.
- **The list is open.** Sixteen are catalogued; more will be added as they are identified. Absence from this list is not evidence that a capability does not exist.
- **A capability can have a trivial mechanism and still be missing**, because the mechanism is not the hard part. Correctness maintenance (16) is the clearest case: editing a file takes seconds, and knowing it needs editing is the whole problem. Score the trigger, not the edit.
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

## How use cases and features link

The catalogue uses three linked fields:

| Level | What it answers | How it appears here |
|---|---|---|
| **Use case** | Who is trying to achieve what outcome, in what context? | One primary use case per capability, written as actor plus trigger plus goal plus value |
| **Capability** | What stable ability is needed across journeys, tools, or products? | The row title |
| **Feature** | What concrete mechanism implements or exposes the ability? | Representative features and evidence links, not an exhaustive feature backlog |

This file keeps use cases inline for now. A dedicated use-case catalogue can be created later, after agreeing a filename, if these need to become a planning surface.

## The catalogue

**State legend:** have / partial or manual / missing. Confirmed = assessed in detail; Provisional = first-pass judgement, not yet worked through.

### 1. Identity Persistence

#### Primary use case

- When a new session starts, the AI agent needs to know who it is working with so that the user does not have to re-establish preferences, identity, and working style.

#### What you get

- The agent knows who you are without being told, every session.

#### Functions spanned

- Storage (behavioural)
- Injection (scheduled)

#### Representative features and evidence

- `SessionStart` injection in [[pillars-agentic-os]] and [[pillars-memsearch]]
- `USER.md` / `user.md` stores

#### State here

- Partial: store excellent, delivery 10%.

#### Confidence

- Confirmed.

### 2. Critical Context Availability

#### Primary use case

- When a new session starts or resumes work, the AI agent needs to know the active project, blockers, and next action so that work resumes from the right place.

#### What you get

- The agent knows what you are working on without being told.

#### Functions spanned

- Storage (behavioural or canonical pointer)
- Injection (scheduled)

#### Representative features and evidence

- Derived live-project payload
- `PROJECT.md` distillation in [[pillars-memsearch]]
- Scheduled snapshot in [[pillars-agentic-os]]

#### State here

- Missing: content exists, no mechanism.

#### Confidence

- Confirmed.

### 3. Compaction Survival

#### Primary use case

- When context compaction occurs, the AI agent needs critical material to return mid-session so that important facts do not silently disappear.

#### What you get

- Material pushed out by compaction returns mid-session.

#### Functions spanned

- Injection (triggered)
- Capture (event-triggered) where capture is not continuous

#### Representative features and evidence

- `PreCompact` hook in [[pillars-mempalace]]
- Triggered context injection in [[pillars-claudeclaw]]

#### State here

- Partial: largely native, not deterministic.

#### Confidence

- Confirmed.

### 4. Working Reasoning Preservation

#### Primary use case

- When a long analytical session accumulates assumptions, dead ends and rejected options, the AI agent needs to preserve and re-surface the working reasoning so that later answers do not repeat old paths or drift after context rot.

#### What you get

- Dead ends, rejected options, assumptions, and rationale remain recoverable during and after a long session.

#### Functions spanned

- Capture
- Storage
- Injection (triggered or scheduled refresh)

#### Representative features and evidence

- Working scratchpad
- Reasoning checkpoints
- Compaction summary
- Triggered context refresh

#### State here

- Missing: no deliberate mechanism.

#### Confidence

- Provisional.

### 5. Long-Term Knowledge Recall

#### Primary use case

- When a user or agent needs a fact, decision, or pattern recorded months ago, the system needs to retrieve it so that current work stays consistent with prior knowledge.

#### What you get

- Find a fact, decision, or pattern recorded months ago.

#### Functions spanned

- Storage (canonical)
- Recall

#### Representative features and evidence

- Wiki articles
- [[memory-features#Curated Index Retrieval|Curated index retrieval]]
- [[memory-features#Semantic Search|Semantic search]]
- Vector and full-text search in product scorecards

#### State here

- Have: 541-file wiki.

#### Confidence

- Provisional.

### 6. Episodic Recall

#### Primary use case

- When a user asks what happened, why a choice was made, or how a conclusion developed, the system needs to recover past session events so that reasoning and provenance can be inspected.

#### What you get

- Answer "what happened?" or "why did we decide X?" for any past session.

#### Functions spanned

- Capture (continuous)
- Storage (verbatim)
- Recall (query-time)

#### Representative features and evidence

- Native JSONL transcripts
- Transcript rung in [[pillars-agentic-os]] and [[pillars-memsearch]]
- Source references in [[pillars-mempalace]]

#### State here

- Partial: transcripts captured, not searchable.

#### Confidence

- Provisional.

### 7. Retention Management

#### Primary use case

- When memory grows over time, the system needs to compress, archive, decay, or prune material so that useful memory does not drown in stale material.

#### What you get

- Old material compresses or archives rather than accumulating indefinitely.

#### Functions spanned

- Storage (retention axis)

#### Representative features and evidence

- `_archived/` folders
- Salience decay in [[pillars-claudeclaw]]
- Curator jobs in [[pillars-agentic-os]]

#### State here

- Partial: manual `_archived/` folders.

#### Confidence

- Provisional.

### 8. Pattern-to-Rule Promotion

#### Primary use case

- When repeated observations reveal a stable preference, correction, or workflow, the system needs to promote the pattern into a standing rule so that future sessions improve.

#### What you get

- Observations seen repeatedly become durable operating rules.

#### Functions spanned

- Storage
- Promotion process
- Injection where behavioural

#### Representative features and evidence

- Feedback rules
- `daily-memory-distill` in [[pillars-agentic-os]]
- `PROJECT.md` / `USER.md` distillation in [[pillars-memsearch]]

#### State here

- Partial: manual, two-key process.

#### Confidence

- Provisional.

### 9. Unlocated Context Discovery

#### Primary use case

- When the user or agent remembers the substance of something but not where it lives, the system needs to find the relevant material so that dormant or poorly filed context can still influence the work.

#### What you get

- Find relevant prior material when the actor does not know the filename, topic area, exact wording, or source location.

#### Functions spanned

- Recall (query-time)
- Injection (triggered where automatic)

#### Representative features and evidence

- [[memory-features#Semantic Search|Semantic search]]
- Dense vector search
- Hybrid search
- Per-turn retrieval in [[pillars-claudeclaw]]

#### State here

- Partial: grep only.

#### Confidence

- Provisional.

### 10. Curated Knowledge Navigation

#### Primary use case

- When the actor knows the domain or likely topic area, the system needs to navigate a curated knowledge structure so that the right material is found transparently and cheaply.

#### What you get

- Curated indexes and links surface the right material without computed search.

#### Functions spanned

- Storage (canonical)
- Recall (write-time)

#### Representative features and evidence

- [[memory-features#Curated Index Retrieval|Curated index retrieval]]
- Topic `_index.md` files
- Bare wikilinks

#### State here

- Have: index hierarchy and bare wikilinks.

#### Confidence

- Provisional.

### 11. Cross-Agent Memory Federation

#### Primary use case

- When work moves between AI tools, the user's prior context needs to be available across agents so that knowledge is not fragmented by client boundary.

#### What you get

- Multiple agents can share or query the same memory substrate.

#### Functions spanned

- Capture
- Storage
- Recall
- Access protocol

#### Representative features and evidence

- Shared store in [[pillars-memsearch]]
- MCP-style bus in [[openbrain-vs-agentic-os]]

#### State here

- Missing.

#### Confidence

- Provisional.

### 12. Scope-isolated Recall

#### Primary use case

- When multiple clients, agents, or tenants share infrastructure, the system needs to retrieve only permitted memory so that private context does not leak.

#### What you get

- Recall respects user, client, team, or agent boundaries.

#### Functions spanned

- Storage (scope model)
- Recall
- Injection

#### Representative features and evidence

- Scope columns and no-leak tests in [[pillars-agentic-os]]
- Per-agent plus shared tier in [[pillars-claudeclaw]]

#### State here

- Mostly not needed here: single-user vault.

#### Confidence

- Provisional.

### 13. Temporal Fact Recall

#### Primary use case

- When facts change over time, the system needs to answer what was true at a past date so that current truth is not mistaken for historical truth.

#### What you get

- Retrieve time-valid facts and superseded facts correctly.

#### Functions spanned

- Storage (temporal form)
- Recall

#### Representative features and evidence

- Temporal entity graph and `mempalace_kg_query` in [[pillars-mempalace]]

#### State here

- Missing.

#### Confidence

- Provisional.

### 14. Source-grounded Recall

#### Primary use case

- When a retrieved answer matters, the system needs to trace it back to original source material so that the user can verify it.

#### What you get

- Answers can be traced from summary or graph result back to verbatim source.

#### Functions spanned

- Storage (faithful or source references)
- Recall

#### Representative features and evidence

- Transcript rung in [[pillars-agentic-os]] and [[pillars-memsearch]]
- Closet references in [[pillars-mempalace]]

#### State here

- Partial: source docs exist, transcript recall absent.

#### Confidence

- Provisional.

### 15. Procedural Memory Generation

#### Primary use case

- When a workflow recurs, the system needs to turn it into a reusable procedure so that future work is faster and more reliable.

#### What you get

- Repeated workflows become skills, procedures, or standing playbooks.

#### Functions spanned

- Capture
- Storage
- Promotion process
- May generate a new enabler

#### Representative features and evidence

- "Skills from Memory" in [[pillars-memsearch]]
- Feedback rules and skills in AI OS

#### State here

- Partial: manual skill creation only.

#### Confidence

- Provisional.

### 16. Memory Correctness Maintenance

#### Primary use case

- When a stored fact or standing rule becomes wrong, the system needs to surface and correct or retire it so that the agent stops confidently acting on outdated memory.

#### What you get

- Memory that has gone false is detected and revised, rather than asserted indefinitely.

#### Functions spanned

- Storage (revision transformation)
- A detection trigger, which is the part usually absent

#### Representative features and evidence

- `superseded_by` in [[pillars-claudeclaw]]
- `valid_from` / `valid_to` in [[pillars-mempalace]]
- Manual edits to `user.md` and `feedback-*.md` here

#### State here

- Partial: mechanism trivial, no detection trigger.

#### Confidence

- Confirmed.

## Notes on individual capabilities

**1 - score the delivery, not the store.** A capability is an outcome, so a rich, well-maintained store scores nothing on its own if nothing reliably puts it in context. The trap is that the store is the visible artefact and the delivery mechanism is invisible, so inspection flatters the system. **Measure the delivery rate before scoring any capability whose store looks healthy.** Measured here: `user.md` is a strong identity file fetched *by instruction* rather than injected by a hook, and was opened in **5 of 47 substantive sessions (10%)**, corroborating the 8% figure independently recorded in [[memory-injection]]. The store is ✅ and the capability is ⚠, because the hottest tier in the hierarchy sits on the coldest delivery mechanism.

**2 - renamed from critical context injection.** "Injection" is the implementation family. The capability is that critical context is available at the moment it is needed. A `SessionStart` hook is one feature that can deliver it; a derived payload, frozen snapshot, or memory nudge are different mechanisms.

**2 vs 3 - the split that matters.** These are independent, and the products prove it. [[pillars-mempalace|MemPalace]] has a `PreCompact` hook (capability 3) and **no injection layer at all** (no capability 2). A bare `SessionStart` hook is the exact inverse. Anything that treats "inject memory" as one job will build one and silently miss the other.

**2 - the injected pointer should be derived, not stored.** The obvious build is a `context.md` holding "current project, blockers, next step". That is a *copy* of state the canonical record already owns, so it drifts the moment the real document moves on, and it violates single-source-of-truth. Where the store already carries machine-readable state, the pointer can instead be **computed at injection time**. Verified here: every file in `wiki/projects/` carries `status`, `flow` and `status-updated` frontmatter, so the set of live projects is derivable by filtering `flow: implementing` and sorting by date - no second copy, nothing to maintain, nothing to go stale. **Test before building any context store: does the canonical record already encode this, and can the injector just read it?**

**2 - a derived pointer doubles as a staleness detector.** Because it surfaces `status-updated` every session, a project still marked live but untouched for weeks becomes visible continuously rather than never. Two such cases were found the first time this was run here.

**3 - measure the platform's native behaviour before scoring this missing.** A host that compacts by *summarising* rather than truncating already delivers much of this capability for free, and scoring it ✗ prices work that is already done. Measured on Claude Code here: compaction occurred in **17 of 49 sessions** (long analytical sessions compacting up to five times), and each event produced a structured **~2,500-2,760 word** summary that preserved user identity, project, and decisions taken. Add to that the material a host never compacts at all - system-prompt rulebooks (`CLAUDE.md`, `AGENTS.md`), native auto-memory indexes, and everything on disk - and the residual loss is narrow.

**16 - the trigger is the capability, not the edit.** Every other transformation in [[memory-storage]] fires on something the system can observe about itself: recurrence, relatedness, budget, elapsed time. Revision fires on **correctness**, which is a property of the world, so no store can detect its own staleness. That asymmetry is why this capability is so often scored as present when only the mechanism exists. **A live instance here:** `user.md` carries a Hong Kong environment block that becomes false on a relocation already committed and dated, and nothing connects that project's completion to the memory depending on it. The cheapest fix is not automation but a **decommission item on the depending work** - the trigger borrowed from a process that *is* observable.

**3 - the real gap is usually determinism, not survival.** An LLM-written summary cannot guarantee any *specific* item persists. The failure is probabilistic and silent: a fact survives one compaction and not the next, with no signal either way. So the useful build is not "preserve the session" (the host does that) but "re-assert the few things that must not be lost" - which is the **same injected payload as capability 2**, fired on a second event. Where that is true, the two capabilities share one build even though they remain separate capabilities.

**3 - the Capture dependency is conditional.** Compaction removes material from the context window; it destroys nothing on disk **provided capture is continuous**. Where capture is continuous (native session transcripts), this capability needs only Injection (triggered). Where capture is periodic or boundary, compaction can land in the gap between checkpoints and the material is lost twice over, so an event-triggered Capture hook is also required. See the compaction table in [[memory-pillars]].

**4 - not the same as "working memory".** Kashef's Working Memory layer is the context window itself, which [[memory-pillars]] correctly rejects as a category error: the context window is the *target* of Injection, not a store. The genuine capability is narrower: preserving assumptions, rejected options, dead ends, and rationale generated in-session before they have been written to a durable record. Project state already on disk does not need it.

**4 - reduces context rot, but is not identical to it.** Context rot is the failure mode: relevant material remains technically present, but attention and salience degrade until the model stops using it reliably. Working reasoning preservation mitigates that failure by making the fragile reasoning residue recoverable or refreshable.

**6 - capture being solved does not deliver the capability.** Continuous transcript capture is free from the platform, so the Capture pillar is complete. The capability is still absent, because Recall (query-time) over those transcripts is not implemented. **Verified caution:** naive keyword grep over transcripts produces confident but wrong results - a keyword-frequency filter tested here misidentified a memory-systems session as a project session, because counting mentions does not identify what a session was about.

**9 - renamed from query-time search.** Query-time search is an enabler; the capability is unlocated context discovery. It applies when the actor remembers the substance but lacks a location, filename, exact phrase, or obvious index path.

**9 vs 10 - two different answers to Recall.** Curated knowledge navigation pays the cost up front by curating indexes and links; unlocated context discovery pays at retrieval. They are complements, not rivals. See [[wiki-vs-openbrain]] for the underlying paradigm fork.

**11 - federation is different from recall quality.** A high-quality recall system can still be trapped inside one client. Cross-agent memory federation is the ability to cross that tool boundary without asking the user to manually re-brief each agent.

**12 - scope isolation only matters when there are scopes to isolate.** In this single-user vault, it is mostly unused. In multi-client work, it becomes a hard safety capability rather than a nice-to-have.

**13 - temporal fact recall is not just better search.** Semantic and keyword search can return conflicting current and superseded facts. A temporal graph or equivalent validity model is what lets the system answer what was true at a specific date.

**14 - source-grounded recall is the audit trail.** It is not enough to retrieve a summary when a claim matters. The system needs a path back to the raw or canonical source so the answer can be verified.

**15 - procedural memory generation extends the current model.** It is included because MemSearch exposes it directly, but it sits partly outside factual memory. The output is a reusable skill or procedure, not just a stored fact.

## Related

- [[memory-pillars]] - the functional model these capabilities are built from, and the pillar/enabler/capability distinction
- [[memory-use-cases]] - actor-outcome journeys these capabilities support
- [[memory-capture]] · [[memory-storage]] · [[memory-injection]] · [[memory-recall]] - the four pillars
- [[memory-features]] - the feature catalogue mapped to capabilities and architecture functions
- [[pillars-mempalace]] - the worked example separating capabilities 2 and 3
- [[memory-systems-taxonomy-codex-review-2026-08-01]] - review that prompted the use case, capability, feature cleanup

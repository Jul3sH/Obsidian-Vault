---
type: reference
updated: 2026-08-01
authority: analysis-backed
concept: pillar
pillar: injection
---

# Injection

> *The third pillar of [[memory-pillars|the four-pillar model]]: deciding **to look at all**, and placing material into the context window. Retrieval quality is irrelevant if nothing triggers a lookup. This is the pillar most systems under-build, and the binding constraint in the assessed environment.*

> [!note] Status: technology theory, not an adopted design
> Reference material on how agent memory systems work. Where one real environment is assessed, it is a worked example to make the model testable.

## Key Takeaways

- **Injection is not Recall.** Recall finds material; Injection decides to look and puts the result in context. A system can have excellent Recall and still fail entirely, because nothing invokes it.
- **Two types: scheduled and triggered.** Only triggered can defend against mid-session degradation, because scheduled has already fired by the time degradation begins.
- **Four rungs on the trigger hierarchy**, ascending in reliability, from "the user remembers to ask" to "a hook injects content every turn".
- **This is the pillar most products skip.** Of four systems assessed: one has triggered injection, two have scheduled only, one has none at all.
- **Measured failure of the weak rungs:** in one real corpus, agent-decided lookup ran at roughly 25%, and a documented navigation instruction was followed 11% of the time.
- **The scheduled budget needs dividing, not just sizing.** A tier model (identity ~100 tokens, critical context ~300, everything else left to Recall) turns an undifferentiated snapshot into a ranking. See "Allocating the scheduled injection budget" below.

---

## The two types

| | **Scheduled injection** | **Triggered injection** |
|---|---|---|
| When | Once, at session start | Mid-session, in response to a turn |
| Trigger | Deterministic, time-based | Something must *decide* a lookup is needed |
| Typical form | "Frozen snapshot" of consolidated files, roughly 1,300 to 3,000 tokens | Query against the store, top-k results injected |
| Token cost | Fixed, predictable, cacheable | Variable, risks bloating context |
| Defends against | **Cold-start amnesia** | **Compaction loss and context rot** |
| Cannot fix | Anything degrading *during* a session, because it fires once, before the degradation | Nothing structural, but far harder to build well |

**Simon Scrapes' Injection pillar is the scheduled type**: frozen snapshots at session start. Sound against cold-start amnesia, and cheap because it caches. It cannot address mid-session degradation.

**The "frozen snapshot" property is often explicit in implementations.** agentic-os's `MEMORY.md` carries its own header comment stating that mid-session writes only take effect next session, capped at 2,500 characters - the snapshot is deliberately immutable within a session, which is what makes it cacheable.

## The trigger problem

Something has to decide a lookup is warranted. In ascending reliability:

1. **The user asks.** Fragile: depends on the human remembering that relevant material exists.
2. **The agent decides.** Measured at roughly 25% in one real corpus; see [[memory-features#Curated Index Retrieval|curated index retrieval]].
3. **A deterministic per-turn nudge primes the agent to decide.** A hook fires every turn but injects no content itself, only a hint that memory exists and may be relevant, leaving the actual retrieval to option 2. Cheaper than full triggered injection since no retrieval runs unless the agent acts on the hint; more reliable than option 2 alone since the reminder is unconditional. Verified example: MemSearch's `UserPromptSubmit` hook, which posts `"[memsearch] Memory available"` on every turn.
4. **A hook fires on every turn and injects retrieved content directly.** Deterministic. Pays a retrieval cost per turn whether needed or not. Verified example: ClaudeClaw's `buildMemoryContext`.

Only option 4 removes both the human and the agent's judgement from the loop, which is why hook-based content-injection designs exist despite their cost. Option 3 is the cheaper compromise: it does not remove the agent's judgement, but it removes the risk of the agent simply forgetting to ask.

## Allocating the scheduled injection budget

The two-types table above prices scheduled injection at roughly 1,300 to 3,000 tokens and stops there. It says nothing about **how to divide that budget**, which is the question that actually arises when building one. This section fills that gap.

> **Source and status.** The tier structure and token figures below are from Mark Kashef's six-layer memory model, quoted second-hand rather than read from source. It is an **external contribution**, not derived from the four pillars, and is recorded here because it answers a question the pillar model leaves open. The mapping of his layers onto the pillars is in [[memory-pillars]].

### Tiers are Storage x Injection, not a separate taxonomy

Kashef's layers are often read as a rival model to the pillars. They are not: each layer is a **product cell** - a slice of stored content with an injection policy attached. That is why they cannot be filed under Storage or Injection alone.

| Tier | Storage branch | Injection policy | Budget |
|---|---|---|---|
| **Identity** - who the agent is working with, and who it is | Behavioural | **Always injected**, never varies | ~100 tokens |
| **Critical context** - current project, active blockers | Behavioural, some canonical | **Always injected**, and must *survive compaction* | ~300 tokens |
| **Long-term knowledge** - facts, decisions, patterns | Canonical | **Not injected.** Reached by [[memory-recall|Recall]] on demand | Unbounded |
| **Episodic** - full conversation history | [[memory-capture|Capture]] output, verbatim form | **Not injected**, rarely recalled. Archive | Unbounded |

**The organising principle is access temperature**, the same shape as a hardware memory hierarchy: a small hot tier that is always present, a large cold tier that is searched, and an archive that is almost never touched.

**Two corrections when applying it:**

- **"Working memory" is not a tier.** In the original list it sits between the injected tiers and the searched ones, but it is the *context window itself* - the target injection writes into, not a store injection reads from. Treating it as a memory layer is a category error.
- **"Decay" is not a tier either.** It is the transition function that moves content *down* the hierarchy as it cools: eviction policy, not a level. Its natural home is [[memory-storage|Storage's retention axis]], and ClaudeClaw's importance-tiered salience decay is a working implementation.

### Why the budget split matters

**A fixed budget forces a ranking, and the ranking is the design decision.** An undifferentiated "~1,300-3,000 token snapshot" hides the fact that some content must be present on turn one or the session starts wrong, while other content merely benefits from being present.

- **Identity is the smallest tier and the least negotiable.** ~100 tokens, and if it is missing the agent gets the user wrong from the first turn, in a way no later retrieval corrects, because nothing will prompt a lookup for something the agent does not know it lacks.
- **Critical context is the tier with the hardest requirement.** "Survives compaction" is not satisfiable by scheduled injection alone: scheduled injection fires once, before compaction. Meeting it needs either re-injection after a compaction event, or an [[memory-capture|event-triggered capture]] mechanism, or triggered injection. This is the tier that most exposes the scheduled/triggered gap.
- **Everything else should not be in the budget at all.** Long-term knowledge and episodic history are Recall's job. Pulling them into scheduled injection is the most common way a snapshot bloats past its budget and stops being cacheable.

### Applied to this environment

The tier model diagnoses a specific, live failure that the pillar model alone frames only as "Injection is weak":

| Tier | Should be | Actually is |
|---|---|---|
| Identity (`user.md`) | Always injected, ~100 tokens, tier 1 | **Fetched by instruction, measured 8% compliance.** Tier 1 is effectively absent |
| Critical context | Always injected, survives compaction | No equivalent artefact exists - **and none needs to be authored.** See below |
| Long-term knowledge (the wiki) | Recall on demand | Correct, though invocation runs at 11% |
| Episodic (JSONL transcripts) | Archived, rarely touched | Correct |

**The reframe:** `user.md` at 8% is not a compliance problem to be nagged about, it is **the hottest tier in the hierarchy sitting on the coldest delivery mechanism**. The fix is not a better instruction, it is moving it onto a `SessionStart` hook so it becomes injected rather than fetched - which is exactly what agentic-os's `load-memory-snapshot.js` does, and what [[pillars-agentic-os]] scores as its one genuine strength. *(Independently re-measured 2026-08-01 on a >20KB-session denominator: 5 of 47, 10%. The two figures corroborate.)*

### The critical-context tier needs no authored artefact

"No equivalent artefact exists" reads as an instruction to create one - typically a `context.md` holding current project, blockers and next step. **That is the wrong build**, because it copies state the canonical record already owns, so it drifts the moment the real document moves on and it breaks single-source-of-truth.

**Where the store already carries machine-readable state, the critical-context payload should be *computed at injection time* instead.** Verified in this environment: every file in `wiki/projects/` carries `status`, `flow` and `status-updated` frontmatter, so the live-project list is derivable by filtering `flow: implementing` and sorting by date. No second copy exists, so nothing can go stale, and the injected payload is ~50 tokens.

**The general test, before building any critical-context store:** *does the canonical record already encode this, and can the injector simply read it?* An authored context file is only justified for state that genuinely lives nowhere else. A derived payload also inherits a free diagnostic - surfacing `status-updated` every session makes a project still flagged live but untouched for weeks continuously visible, where an authored file would simply repeat its own stale claim.

## Capabilities and features across systems

Transposed from the four product scorecards. This is the pillar with the widest spread between products.

| Capability | Systems | Detail |
|---|---|---|
| **Scheduled injection at session start** | agentic-os (`load-memory-snapshot.js`), MemSearch (`session-start.sh`) | agentic-os injects `SOUL.md`, `USER.md`, `MEMORY.md` and the day's log as `additionalContext`; MemSearch injects the two most recent daily journal files |
| **Frozen-snapshot semantics** (mid-session writes deliberately deferred to next session, making the snapshot cacheable) | agentic-os | `MEMORY.md`, capped at 2,500 characters, states the deferral in its own header |
| **Triggered injection with retrieved content** | ClaudeClaw only | `buildMemoryContext` runs every turn |
| **Multi-layer context assembly in a single injection** | ClaudeClaw | Six layers: semantic search on the current message, recent high-importance memories, consolidation insights, cross-agent team activity, keyword-triggered conversation-history recall, and a war-room transcript bridge |
| **Keyword-gated sub-layer** (a cheaper second trigger inside a triggered injection, firing only on intent words) | ClaudeClaw | Conversation-history recall fires only on `remember`, `recall`, `yesterday`, `we discussed`, and similar |
| **Per-turn nudge without content** | MemSearch | `UserPromptSubmit` posts a fixed hint; retrieval remains agent-decided |
| **No injection layer at all** | MemPalace | Confirmed by reading `hook_session_start` directly: initialises tracking state, injects nothing. Recall is 100% pull, driven by a skill protocol instructing search-before-answer |
| **Anti-pattern guard: retrieval does not boost relevance** | ClaudeClaw | Deliberately does *not* touch `salience`/`accessed_at` on retrieval, because "noise retrieved once would stay fresh forever" - a positive-feedback trap most retrieval-boosts-relevance designs walk into |
| **Scope isolation at injection time** | ClaudeClaw (`agent_id` plus shared tier), agentic-os (`private`/`client`/`team`/`system`) | Prevents cross-agent or cross-tenant memory leaking into context |
| **Cross-agent activity awareness** | ClaudeClaw | A dedicated injection layer surfacing what *other* agents did in the last 24h |
| **External-vault context bridge** | ClaudeClaw (`buildObsidianContext`) | Appends Obsidian-vault context when configured - the assessed product already bridges into the same substrate this wiki runs on |
| **Bootstrap so injection works on first run** | agentic-os (`memory-bootstrap-index.js`) | Backfills an empty store once on a fresh clone, so session one is not dark |

## Assessment of one environment

**Injection is the binding constraint here, and was invisible until the pillars were separated.**

The environment has scheduled injection only in a weak form: `CLAUDE.md` and `AGENTS.md` load every session, but the user profile (`user.md`) is fetched by *instruction*, not injected by a hook - and instruction-following was measured at 8%. There is no triggered injection at all.

Measured evidence of the gap, from [[memory-features#Curated Index Retrieval|curated index retrieval]]:

| Signal | Result |
|---|---|
| Sessions where the navigation entry point was read, against an explicit standing instruction | **5 of 47 (11%)** |
| Document reads that were autonomous discovery rather than prompted or mechanical | **187 of 744 (25%)** |

**The system's Storage and Recall are strong; its Injection is not wired.** That is why a well-maintained knowledge base still fails to surface dormant relevant context: nothing decides to look.

## Related

- [[memory-pillars]] - the four-pillar model overview; the compaction/context-rot analysis spanning Injection and Capture lives there
- [[memory-recall]] - the pillar Injection invokes; distinct from it
- [[memory-storage]] - what is eligible for injection, and the canonical/behavioural split that determines which tier is hot
- [[memory-capture]] - upstream; event-triggered capture, not injection, is the fix when compaction causes true disk loss
- [[memory-features#Semantic Search|Semantic search]] - feature family for query-time recall and triggered injection
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from

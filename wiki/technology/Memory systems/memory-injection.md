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
2. **The agent decides.** Measured at roughly 25% in one real corpus; see [[memory-curated-index]].
3. **A deterministic per-turn nudge primes the agent to decide.** A hook fires every turn but injects no content itself, only a hint that memory exists and may be relevant, leaving the actual retrieval to option 2. Cheaper than full triggered injection since no retrieval runs unless the agent acts on the hint; more reliable than option 2 alone since the reminder is unconditional. Verified example: MemSearch's `UserPromptSubmit` hook, which posts `"[memsearch] Memory available"` on every turn.
4. **A hook fires on every turn and injects retrieved content directly.** Deterministic. Pays a retrieval cost per turn whether needed or not. Verified example: ClaudeClaw's `buildMemoryContext`.

Only option 4 removes both the human and the agent's judgement from the loop, which is why hook-based content-injection designs exist despite their cost. Option 3 is the cheaper compromise: it does not remove the agent's judgement, but it removes the risk of the agent simply forgetting to ask.

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

Measured evidence of the gap, from [[memory-curated-index]]:

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
- [[memory-semantic-search]] - the only practical enabler of triggered injection
- [[pillars-claudeclaw]] - [[pillars-agentic-os]] - [[pillars-memsearch]] - [[pillars-mempalace]] - the four product scorecards this capability catalogue is transposed from

---
type: reference
created: 2026-08-02
authority: analysis-backed
concept: challenge-catalogue
---

# Memory Challenges

> *The recurring failure modes in agent memory systems, mapped to the [[memory-capabilities|capabilities]] and [[memory-features|features]] that address them, and to how the assessed platforms respond.*

## Key Takeaways

- **Challenges are failure modes, not architecture functions.** A challenge can cut across Capture, Storage, Injection and Recall.
- **Capabilities describe the enduring ability needed to overcome the challenge.** Features are the concrete mechanisms that implement or expose those abilities.
- **No assessed platform covers the full set.** Each system is strongest in a different part of the problem: memsearch in federation, mempalace in compaction capture and temporal recall, claudeclaw-business-os in triggered injection and retention, and agentic-os in scoped storage and planned recall.
- **The hard part is often the trigger.** Many systems store useful memory, but fail to surface it at the moment it would change the answer.

## Cold-Start Amnesia

### Why it matters

- A new session begins with no reliable awareness of the user, project, preferences, blockers or recent work.
- The user has to re-brief the agent, or the agent starts confidently from a generic posture.

### Capabilities

- [[memory-capabilities|Identity persistence]]
- [[memory-capabilities|Critical context availability]]
- [[memory-capabilities|Long-term knowledge recall]]

### Features

- `SessionStart` memory injection hook
- Frozen snapshot file
- Derived critical-context payload
- `PROJECT.md` and `USER.md` distillation
- Memory bootstrap index

### Platform approaches

- memsearch:
  - Uses `SessionStart` injection and `PROJECT.md` / `USER.md` distillation.
  - Stronger than a passive store because it pushes recent and project context into the session.
- mempalace:
  - Stores memory well, but has no injection layer.
  - The agent must choose to query the palace, so cold-start support is weak.
- claudeclaw-business-os:
  - Retrieves context per turn through `buildMemoryContext`.
  - Has useful memory tiers, but the reviewed architecture does not show a separate always-loaded identity and current-project payload.
- agentic-os:
  - Designed around scheduled snapshots and bootstrap indexes.
  - Strong design fit, but the reviewed state was "built but never ingested", so the capability depends on activation and populated data.

## Context Rot And Compaction Loss

### Why it matters

- Important reasoning can become less salient while still technically present in the context window.
- Compaction can push critical facts, assumptions or rejected options out of the active context.
- The failure is silent: the agent may continue without knowing which detail has dropped out.

### Capabilities

- [[memory-capabilities|Compaction survival]]
- [[memory-capabilities|Working reasoning preservation]]
- [[memory-capabilities|Critical context availability]]

### Features

- `PreCompact` hook
- Triggered content injection
- Per-turn retrieved content injection
- Working scratchpad
- Reasoning checkpoint
- Derived critical-context payload

### Platform approaches

- memsearch:
  - Captures continuously through hooks and can remind the agent to search.
  - Its `UserPromptSubmit` nudge is not content injection, so mid-session re-surfacing is weaker than the capture layer.
- mempalace:
  - Strongest direct compaction capture through unconditional `PreCompact` flush.
  - Does not re-inject the captured material, so survival depends on later search.
- claudeclaw-business-os:
  - Strongest assessed triggered injection pattern because it retrieves and injects relevant memory during normal turns.
  - Also uses conversation logs, but exact reasoning preservation still depends on what was captured and ranked.
- agentic-os:
  - Has transcript ladder and scheduled injection concepts.
  - Weakest on triggered mid-session refresh unless an explicit compaction or prompt trigger is added.

## Unlocated Context Discovery

### Why it matters

- The actor remembers the substance of something, but not the filename, topic area, exact wording or source location.
- Curated indexes and grep work poorly when there is no good first hop.

### Capabilities

- [[memory-capabilities|Unlocated context discovery]]
- [[memory-capabilities|Long-term knowledge recall]]
- [[memory-capabilities|Episodic recall]]

### Features

- [[memory-features#Semantic Search|Semantic search]]
- Dense vector similarity search
- BM25 or full-text keyword search
- Hybrid dense and sparse search
- Reciprocal rank fusion
- Per-turn retrieved content injection
- Search-before-answer protocol

### Platform approaches

- memsearch:
  - Strong fit through hybrid dense and sparse search, reciprocal rank fusion and markdown-canonical storage.
  - Also nudges the agent to search, although the nudge does not inject content itself.
- mempalace:
  - Provides semantic search and temporal graph query tools.
  - Still depends on the agent deciding to query, so dormant context can remain dormant.
- claudeclaw-business-os:
  - Strong fit because per-turn retrieval can surface relevant prior material without the user naming it.
  - Retrieval quality depends on the importance gate and duplicate handling at ingest.
- agentic-os:
  - Has strong planned search infrastructure, including vector and full-text recall.
  - Weak in practice where ingestion has not happened or where no trigger invokes search.

## Memory Fragmentation Across Agents

### Why it matters

- Work moves between agents, CLIs, repos and interfaces.
- If each tool has its own private memory, the user becomes the integration layer.

### Capabilities

- [[memory-capabilities|Cross-agent memory federation]]
- [[memory-capabilities|Critical context availability]]
- [[memory-capabilities|Source-grounded recall]]

### Features

- Cross-agent shared memory store
- MCP memory gateway
- Per-agent memory plus shared memory tier
- Markdown-canonical, vector-index disposable store

### Platform approaches

- memsearch:
  - Strongest assessed answer because it is designed as a shared memory substrate across agents and clients.
  - Its canonical markdown store reduces lock-in to one retrieval index.
- mempalace:
  - Does not primarily solve federation.
  - It behaves more like a memory palace available through its own tool surface.
- claudeclaw-business-os:
  - Partially addresses the problem through per-agent memory plus a shared tier.
  - The reviewed architecture does not make it a general cross-tool memory bus.
- agentic-os:
  - Has scoped storage and recall concepts that could support multiple clients.
  - Federation was not the strongest proven claim in the reviewed material.

## Scope Leakage And Wrong-Context Recall

### Why it matters

- A memory system can retrieve the right kind of memory from the wrong user, client, agent or project.
- In multi-client or multi-agent environments, this is a safety problem, not just a relevance problem.

### Capabilities

- [[memory-capabilities|Scope-isolated recall]]
- [[memory-capabilities|Identity persistence]]
- [[memory-capabilities|Cross-agent memory federation]]

### Features

- Scope predicates on memory queries
- Per-agent memory plus shared memory tier
- Wings / Rooms / Drawers hierarchy
- No-leak query tests

### Platform approaches

- memsearch:
  - Strong on sharing, but the reviewed material did not show an equally strong scope-isolation model.
  - This is the main caveat attached to federation.
- mempalace:
  - Uses a Wings / Rooms / Drawers hierarchy that gives structural organisation.
  - That is not the same as enforced access isolation.
- claudeclaw-business-os:
  - Uses per-agent memory plus a shared tier.
  - This is a practical isolation pattern, especially for different Telegram sessions or agent roles.
- agentic-os:
  - Strongest assessed design for scoped recall through scope predicates and no-leak checks.
  - Best fit where tenant, client or agent boundaries matter.

## Source Grounding And Reconstruction

### Why it matters

- A retrieved summary is not enough when the answer matters.
- The system needs to show what happened, where a claim came from, and how a conclusion developed.

### Capabilities

- [[memory-capabilities|Episodic recall]]
- [[memory-capabilities|Source-grounded recall]]
- [[memory-capabilities|Long-term knowledge recall]]

### Features

- Native JSONL transcript capture
- Three-rung recall ladder: search, expand, transcript
- Closet references to verbatim source
- Verbatim storage with no synthesis
- Markdown-canonical, vector-index disposable store

### Platform approaches

- memsearch:
  - Strong through canonical markdown journals plus escalation to source transcripts.
  - The disposable vector index supports retrieval without replacing the source.
- mempalace:
  - Very strong through verbatim storage and closet references back to source material.
  - Its no-synthesis posture is useful where auditability matters.
- claudeclaw-business-os:
  - Captures conversation logs and retrieves summarized memory.
  - Source reconstruction is possible, but less central than in memsearch or mempalace.
- agentic-os:
  - Strong design through source, chunk, index and transcript-rung concepts.
  - Depends on the memory database being populated and maintained.

## Staleness And Correctness Drift

### Why it matters

- User facts, project status and operating rules change.
- A memory system can keep asserting a fact that used to be true.
- The hard part is not editing the memory, but detecting that the memory is now wrong.

### Capabilities

- [[memory-capabilities|Memory correctness maintenance]]
- [[memory-capabilities|Temporal fact recall]]
- [[memory-capabilities|Retention management]]

### Features

- `superseded_by` revision links
- `valid_from` and `valid_to` validity windows
- Temporal entity knowledge graph
- Manual memory edits
- Decommission trigger on dependent work
- Headless maintenance jobs

### Platform approaches

- memsearch:
  - Markdown stores can be edited and regenerated.
  - The reviewed material did not show a strong temporal validity or correctness-detection mechanism.
- mempalace:
  - Strongest temporal model through validity windows and temporal graph query.
  - Still needs process or tooling to detect when a stored fact has become false.
- claudeclaw-business-os:
  - Has a `superseded_by` style correction mechanism.
  - Detection remains the gap: the system must know when to revise a memory.
- agentic-os:
  - Curator and maintenance jobs can support cleanup.
  - Correctness still depends on reliable triggers and populated source records.

## Memory Bloat And Retention Pressure

### Why it matters

- Continuous capture creates volume quickly.
- Without pruning, decay, compression or consolidation, useful memory gets buried under stale or low-value material.

### Capabilities

- [[memory-capabilities|Retention management]]
- [[memory-capabilities|Critical context availability]]
- [[memory-capabilities|Pattern-to-rule promotion]]

### Features

- Importance gate at ingest
- Cheap pre-filter before extraction
- Semantic duplicate detection at ingest
- Salience decay and pinning
- Budget-driven compression against a hard cap
- Periodic consolidation pass
- Daily memory distillation

### Platform approaches

- memsearch:
  - Keeps a comprehensive canonical record and can rebuild indexes from hashes.
  - Weaker on pruning, decay and active retention pressure management.
- mempalace:
  - Favours faithful and verbatim storage.
  - That supports auditability, but does not itself solve bloat.
- claudeclaw-business-os:
  - Strongest active retention posture through importance gates, duplicate detection, salience decay and pinning.
  - This makes it the strongest assessed system for keeping injected memory useful.
- agentic-os:
  - Strong design through budget-driven compression, distillation and headless jobs.
  - Effectiveness depends on whether the jobs are actually running against populated memory.

## Pattern Promotion Without Overfitting

### Why it matters

- Repeated observations should become durable rules, preferences or procedures.
- Promoting too early creates brittle rules from one-off events.
- Never promoting means the user repeats the same corrections forever.

### Capabilities

- [[memory-capabilities|Pattern-to-rule promotion]]
- [[memory-capabilities|Procedural memory generation]]
- [[memory-capabilities|Identity persistence]]

### Features

- Daily memory distillation
- `PROJECT.md` and `USER.md` distillation
- Periodic consolidation pass
- Feedback rules
- Skills from Memory

### Platform approaches

- memsearch:
  - Strongest direct procedural route through Skills from Memory.
  - Also supports `PROJECT.md` and `USER.md` distillation.
- mempalace:
  - Can store observations, but does not appear to have a strong promotion loop.
  - Its strength is faithful recall rather than behavioural rule generation.
- claudeclaw-business-os:
  - Can consolidate repeated memories and expose them in context.
  - The reviewed architecture does not make reusable skill generation a central feature.
- agentic-os:
  - Strong design fit through daily memory distillation, feedback rules and skill conventions.
  - Depends on operational ingestion and curation.

## Temporal Truth

### Why it matters

- Search can return both current and superseded facts.
- Some questions need the answer that was true at a past date, not the answer that is true now.

### Capabilities

- [[memory-capabilities|Temporal fact recall]]
- [[memory-capabilities|Memory correctness maintenance]]
- [[memory-capabilities|Source-grounded recall]]

### Features

- Temporal entity knowledge graph
- `mempalace_kg_query` tool
- Validity windows
- Source references to raw events

### Platform approaches

- memsearch:
  - Does not appear to provide first-class temporal fact recall.
  - Timestamps help reconstruction, but not validity-aware answers.
- mempalace:
  - Strongest assessed answer through temporal graph storage and temporal query.
  - Best fit where the question is "what was true then?"
- claudeclaw-business-os:
  - Has useful capture and correction patterns, but no strong temporal graph model was identified.
  - Temporal truth would need additional validity metadata or source reconstruction.
- agentic-os:
  - Has source and chunk structures that could support temporal reconstruction.
  - A first-class temporal fact model was not the main assessed strength.

## Procedural Memory

### Why it matters

- Some lessons are not facts to remember, but ways of working to reuse.
- The output should become a skill, playbook, hook, command or standing procedure.

### Capabilities

- [[memory-capabilities|Procedural memory generation]]
- [[memory-capabilities|Pattern-to-rule promotion]]
- [[memory-capabilities|Working reasoning preservation]]

### Features

- Skills from Memory
- Feedback rules
- Skill candidates
- Daily memory distillation
- Agent-authored capture

### Platform approaches

- memsearch:
  - Strongest assessed product feature because Skills from Memory directly targets this challenge.
  - This turns memory into reusable procedure, not just retrieved content.
- mempalace:
  - Does not primarily solve procedural generation.
  - It can preserve the evidence a future procedure might be built from.
- claudeclaw-business-os:
  - Can expose stable patterns through memory tiers.
  - The reviewed files did not show automatic or semi-automatic skill creation.
- agentic-os:
  - Has strong adjacent machinery through skills, feedback rules and distillation.
  - Needs an explicit promotion path from repeated memory to reusable procedure.

## Related

- [[memory-pillars]] - the architecture functions behind the challenge responses
- [[memory-capabilities]] - the capability catalogue referenced above
- [[memory-use-cases]] - actor-outcome journeys that consume the capabilities
- [[memory-features]] - concrete feature mechanisms referenced above
- [[pillars-memsearch]]
- [[pillars-mempalace]]
- [[pillars-claudeclaw]]
- [[pillars-agentic-os]]

---
type: review
created: 2026-08-01
reviewer: codex
topic: memory-systems-taxonomy
authority: reviewer-analysis
---

# Memory Systems Taxonomy Codex Review 2026-08-01

> Review of the Memory Systems documentation against Julian's use case, capability, feature distinction. Source documents reviewed: [[memory-pillars]], [[memory-capabilities]], [[memory-capture]], [[memory-storage]], [[memory-injection]], [[memory-recall]], the feature-family material now folded into [[memory-features]], [[wiki-vs-openbrain]], [[openbrain-vs-agentic-os]], [[pillars-claudeclaw]], [[pillars-agentic-os]], [[pillars-memsearch]], and [[pillars-mempalace]].

## Review Standard

| Term | Test used in this review |
|---|---|
| Use case | Actor plus trigger or context plus goal plus outcome |
| Capability | Stable reusable ability, independent of UI, vendor, API, or implementation |
| Feature | Concrete solution functionality a user or system can invoke, configure, test, release, or buy |

Traceability pattern:

```text
Capabilities enable use cases.
Use cases consume capabilities.
Features implement or expose capabilities.
```

## Key Takeaways

- **The source docs are directionally good, but use a different taxonomy.** The dominant model is pillar, enabler, capability. That model is useful for architecture, but it is not the same as use case, capability, feature.
- **The biggest mix-up is in the pillar articles.** Each pillar has a section titled "Capabilities and features across systems". Most rows in those tables are actually features or implementation patterns, not capabilities.
- **The strongest capability catalogue is already [[memory-capabilities]].** It should remain the capability home, but several entries need clearer names and a few additional capabilities should be added.
- **Use cases are mostly implicit.** The docs describe technical needs and evaluation scenarios, but they rarely state actor, trigger, goal, and value in use-case form.
- **The four pillars should be renamed as architecture functions, not capabilities.** Capture, Storage, Injection, and Recall are jobs the system performs. They are not use cases, and they are not user-value capabilities by themselves.
- **Semantic search and curated index retrieval are enablers or feature families, not capabilities.** They implement or expose recall capabilities.

## Primary Findings

| Severity | Finding | Evidence | Recommended fix |
|---|---|---|---|
| High | Product tables labelled as capabilities contain mostly features | [[memory-capture]], [[memory-storage]], [[memory-injection]], and [[memory-recall]] all have "Capabilities and features across systems" tables listing hooks, vector search, BM25, decay policies, and backend choices | Rename those sections to "Observed features and implementation patterns" |
| High | Use cases are not explicitly modelled | The semantic-search feature-family material has "Scoring the five commonly-cited use cases", but most of those rows are retrieval scenarios rather than actor-outcome use cases | Add a dedicated "Memory Use Cases" article or section using the sentence stem: "When [trigger], [actor] wants to [goal] so that [value]" |
| Medium | Some current capabilities are named like mechanisms | "Query-time search" and "Write-time navigation" in [[memory-capabilities]] are close to enablers; they describe retrieval method more than outcome | Rename around outcomes, e.g. "Unprompted relevant-context discovery" and "Curated knowledge navigation" |
| Medium | Product-specific features are being promoted into cross-system capability language | Examples: "pluggable storage backend", "SHA-256 content hashing", "frozen snapshot semantics", "keyword fallback" | Keep these as feature rows under product scorecards or feature catalogue, not in the capability catalogue |
| Medium | "Observation Layer" is partly capability, partly architectural label | [[memory-capture]] says Capture enables Observation, but [[memory-capabilities]] lists "Observation / episodic recall", which also requires Recall | Keep "Observation" as a capability only when it means the ability to answer what happened, not merely the existence of a durable log |
| Low | "Pillar" language is useful but risks sounding like capabilities | [[memory-pillars]] says pillars are functions, which is correct, but downstream tables blur this | Add a short taxonomy box to [[memory-pillars]] distinguishing architecture function, capability, use case, feature, and enabler |

## Use Cases Observed

The docs imply the following use cases. These should be written explicitly if this folder is being used for product selection or implementation planning.

| Use case | Actor | Trigger or context | Goal | Outcome or value |
|---|---|---|---|---|
| Start a session with identity intact | AI agent | New session starts | Know who the user is and how to work with them | Fewer repeated corrections and less re-briefing |
| Start a session with current work surfaced | AI agent | New session starts | Know active projects, blockers, and next actions | Work resumes from the right place |
| Restore critical context after compaction | AI agent | Context compaction occurs or relevant context degrades | Re-surface critical material | Important facts do not silently disappear mid-session |
| Recall a past decision | User or AI agent | A question depends on prior reasoning | Find what was decided and why | Current work stays consistent with past decisions |
| Explain provenance of a figure or claim | User | User asks where a number or statement came from | Trace the claim to source material | Reduces drift and false certainty |
| Retrieve unstructured pasted material | AI agent | User refers to content that was pasted but not filed | Find the relevant past material by meaning | Unfiled input remains useful |
| Share memory across AI tools | User using multiple agents | Work moves between Claude Code, Codex, OpenCode, or other clients | Make prior context available across tools | Less fragmentation across agents |
| Keep client or agent memories isolated | Platform or operator | Multiple clients, agents, or tenants exist | Retrieve only the permitted memory scope | Prevents cross-client or cross-agent leakage |
| Answer what was true at a past date | User or AI agent | Facts have changed over time | Retrieve time-valid facts | Avoids treating current facts as historically true |
| Convert repeated workflows into reusable procedures | User or AI agent | A workflow has recurred enough to be reusable | Promote the procedure into a skill or rule | Repeated work becomes faster and more reliable |

## Capabilities Observed

These are stable abilities and mostly independent of any particular product implementation.

| Capability | Current source | Classification note |
|---|---|---|
| Identity persistence | [[memory-capabilities]] | Good capability |
| Critical context availability | [[memory-capabilities]], [[memory-injection]] | Good capability, but "injection" is the implementation family |
| Compaction survival | [[memory-capabilities]], [[memory-pillars]] | Good capability |
| In-session reasoning retention | [[memory-capabilities]] | Good capability, though currently provisional |
| Long-term knowledge recall | [[memory-capabilities]], [[memory-recall]] | Good capability |
| Episodic recall | [[memory-capabilities]], [[memory-capture]] | Good capability if it means answer "what happened?" from past sessions |
| Retention management | [[memory-capabilities]], [[memory-storage]] | Good capability |
| Pattern promotion | [[memory-capabilities]], [[memory-storage]] | Good capability |
| Curated knowledge navigation | [[memory-capabilities]], [[memory-features#Curated Index Retrieval|curated index retrieval]] | Better capability name than "write-time navigation" |
| Unprompted relevant-context discovery | [[memory-features#Semantic Search|semantic search]], [[memory-injection]] | Better capability framing than "query-time search" |
| Cross-agent memory federation | [[pillars-memsearch]], [[memory-recall]] | Should be added as a capability |
| Scope-isolated recall | [[pillars-agentic-os]], [[pillars-claudeclaw]], [[memory-recall]] | Should be added as a capability |
| Temporal fact recall | [[pillars-mempalace]], [[memory-recall]] | Should be added as a capability |
| Source-grounded recall | [[pillars-mempalace]], [[openbrain-vs-agentic-os]] | Should be added as a capability |
| Procedural memory generation | [[pillars-memsearch]], [[memory-storage]] | Should be added or explicitly parked as a capability outside the current four-pillar model |

## Features Observed

These are concrete solution mechanisms. They should not be called capabilities unless the wording is shifted up to the enduring ability they expose.

| Feature | Product or source | Capability exposed or supported |
|---|---|---|
| Native JSONL transcript capture | Claude Code, [[memory-capture]] | Episodic recall, observation |
| `Stop` hook capture | ClaudeClaw, Agentic OS, MemSearch, MemPalace | Episodic recall, pattern promotion |
| `PreCompact` hook | MemPalace | Compaction survival |
| `SessionEnd` final flush | MemPalace | Capture completeness |
| `SessionStart` memory injection hook | Agentic OS, MemSearch | Identity persistence, critical context availability |
| `UserPromptSubmit` memory nudge | MemSearch | Unprompted relevant-context discovery, weak form |
| Per-turn retrieved content injection | ClaudeClaw | Unprompted relevant-context discovery, compaction survival |
| Frozen snapshot file | Agentic OS | Identity persistence, scheduled critical context |
| Dense vector similarity search | All four assessed products | Long-term knowledge recall |
| BM25 or full-text keyword search | MemSearch, Agentic OS, ClaudeClaw | Long-term knowledge recall |
| Reciprocal rank fusion | MemSearch | Recall quality |
| Three-rung recall ladder: search, expand, transcript | Agentic OS, MemSearch | Source-grounded recall |
| Temporal entity knowledge graph | MemPalace | Temporal fact recall |
| `mempalace_kg_query` tool | MemPalace | Temporal fact recall |
| Scope predicates on memory queries | Agentic OS | Scope-isolated recall |
| Per-agent plus shared memory tier | ClaudeClaw | Scope-isolated recall, cross-agent awareness |
| Importance gate at ingest | ClaudeClaw | Retention management |
| Semantic duplicate detection at ingest | ClaudeClaw | Retention management |
| Salience decay and pinning | ClaudeClaw | Retention management |
| SHA-256 content hashing before indexing | MemSearch, Agentic OS | Efficient index maintenance |
| File watcher for live index maintenance | MemSearch, Agentic OS | Fresh recall |
| Pluggable storage backend | MemPalace | Deployment flexibility |
| `PROJECT.md` and `USER.md` distillation | MemSearch | Critical context availability, identity persistence |
| "Skills from Memory" skill-candidate generation | MemSearch | Procedural memory generation |

## Items Currently Misclassified

| Current label or placement | Current classification implied by docs | Better classification | Why |
|---|---|---|---|
| Capture, Storage, Injection, Recall | Pillars | Architecture functions | They describe jobs the system performs, not user journeys or stable user-value abilities |
| Semantic search | Enabler | Feature family / enabler | It is a way to implement query-time recall and triggered discovery |
| Curated index retrieval | Enabler | Feature family / enabler | It is a way to implement curated knowledge navigation |
| Continuous capture | Capability row in [[memory-capture]] | Feature or implementation pattern | It is a capture mode, not an outcome |
| Importance gating at ingest | Capability row in [[memory-capture]] | Feature | It is a concrete ingest rule |
| Verbatim storage, no synthesis | Capability row in [[memory-storage]] | Feature or architectural pattern | The capability is source-grounded recall or faithful archival memory |
| Pluggable storage backend | Capability row in [[memory-storage]] | Feature | Users can configure or swap it |
| Scheduled injection at session start | Capability row in [[memory-injection]] | Feature or implementation pattern | The capability is identity or critical-context availability |
| Frozen-snapshot semantics | Capability row in [[memory-injection]] | Feature property | It is a concrete behaviour of one implementation |
| Dense vector similarity search | Capability row in [[memory-recall]] | Feature | It is a retrieval mechanism |
| Published retrieval benchmark | Capability row in [[memory-recall]] | Evidence / quality signal | It supports a claim about recall quality, but is not itself a capability |
| Query-time search | Capability in [[memory-capabilities]] | Capability only if renamed around outcome | Search is a mechanism; finding unknown relevant context is the capability |
| Write-time navigation | Capability in [[memory-capabilities]] | Capability only if renamed around outcome | Navigation is a mechanism; curated knowledge discovery is the capability |

## Recommended Rewrite Structure

Keep the existing docs, but tighten the taxonomy:

1. **[[memory-pillars]] stays the architecture model.**
   - Add a taxonomy box: pillars are architecture functions; enablers implement functions; features are concrete product mechanisms; capabilities are reusable abilities; use cases are actor-outcome journeys.

2. **[[memory-capabilities]] becomes the single capability catalogue.**
   - Rename mechanism-shaped capabilities.
   - Add cross-agent federation, scope-isolated recall, temporal fact recall, source-grounded recall, and procedural memory generation.

3. **Add or create a Memory Use Cases section.**
   - Could be a new article, if Julian agrees a filename.
   - Candidate filename: `memory-use-cases.md`.
   - Each row should use: "When [trigger], [actor] wants to [goal] so that [value]."

4. **Rename the pillar article tables.**
   - From: "Capabilities and features across systems"
   - To: "Observed features and implementation patterns across systems"

5. **Keep product scorecards as feature evidence.**
   - The scorecards are valuable because they identify concrete mechanisms.
   - They should feed the capability catalogue, but not define capabilities directly.

## Suggested Traceability Map

| Use case | Capabilities consumed | Example features |
|---|---|---|
| Start a session with identity intact | Identity persistence | `SessionStart` injection hook, frozen snapshot, `USER.md` distillation |
| Start a session with current work surfaced | Critical context availability | Derived live-project payload, `PROJECT.md`, scheduled injection |
| Restore critical context after compaction | Compaction survival, source-grounded recall | `PreCompact` hook, triggered injection, recall ladder |
| Recall a past decision | Long-term knowledge recall, curated knowledge navigation | Wiki indexes, vector search, full-text search |
| Explain provenance of a figure or claim | Source-grounded recall, episodic recall | Transcript rung, closet references, JSONL transcripts |
| Retrieve unstructured pasted material | Unprompted relevant-context discovery, episodic recall | Semantic search, dense embeddings, per-turn retrieval |
| Share memory across AI tools | Cross-agent memory federation | Shared memory store, MCP gateway, MemSearch federation |
| Keep client memories isolated | Scope-isolated recall | Scope columns, per-agent memory tier, no-leak tests |
| Answer what was true at a past date | Temporal fact recall | Temporal knowledge graph, validity windows |
| Convert repeated workflows into procedures | Procedural memory generation, pattern promotion | Skills from Memory, daily distillation |

## Proposed Action List

| Priority | Action |
|---|---|
| 1 | Rename the four pillar "Capabilities and features across systems" sections to "Observed features and implementation patterns across systems" |
| 2 | Refactor [[memory-capabilities]] so every row names an outcome ability, not a mechanism |
| 3 | Add the missing capabilities identified above |
| 4 | Create a use-case catalogue only after agreeing the filename with Julian |
| 5 | Add a traceability table linking use cases -> capabilities -> example features |
| 6 | Keep feature-family material in [[memory-features]], not in the capability catalogue |

## Verdict

The docs have not simply mixed up use cases, capabilities, and features. They have built a parallel architecture taxonomy that is useful, but then reused "capability" too broadly in the product-comparison sections.

The clean fix is not to discard the four-pillar model. It is to make the levels explicit:

```text
Use case: actor outcome journey
Capability: reusable ability
Architecture function: Capture, Storage, Injection, Recall
Enabler: semantic search, curated index, hooks, graphs
Feature: concrete product mechanism
```

Once that distinction is applied, the folder becomes much easier to use for product selection and implementation planning.

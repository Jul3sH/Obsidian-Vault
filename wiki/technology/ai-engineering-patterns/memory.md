---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Memory

> This is the Memory entry in the AI engineering patterns catalog: a routing
> reference for the pattern of giving an agent persistent state across sessions.
> It exists so that someone deciding how to attack a piece of AI work can tell
> quickly whether memory is the right pattern, which technique inside it applies,
> and where the pattern fails. Read "Reach For It When" first; if the triggers do
> not match, the answer is a different pattern in this folder and you can stop
> there.

## Key Takeaways

- Memory is for interaction-derived state (preferences, summaries, learned
  behaviour) the agent accumulates about itself and the user. RAG is for domain
  document grounding. The split is about what the data represents, not whether
  it changes: temporal knowledge graphs blur this by also ingesting business
  facts. Complementary layers, not substitutes.
- The episodic / semantic / procedural split, borrowed from cognitive science,
  is the common vocabulary for this space (2025-2026), though vendors still
  implement competing taxonomies underneath it.
- Simple beats complex more often than the vendor literature suggests. Letta
  scored 74.0% on LoCoMo just by storing conversation histories in files,
  above Mem0's graph variant at 68.5%.
- **Vendor benchmarks in this space are contested and unresolved.** Mem0
  self-reports 92.5 on LoCoMo and 94.4 on LongMemEval; an independent
  evaluation put Mem0 at 49.0 and Zep at 63.8 on LongMemEval. Do not route on a
  vendor's own number.
- Persistent memory is a documented security liability: it turns a one-off
  prompt injection into a durable one. Disable memory features you are not
  using.

## What It Is

Memory is a persistent storage layer that lets an agent retain and act on
information across turns and sessions. It sits next to, not inside, context
engineering: context engineering manages what is in the current window, memory
decides what survives the window closing. The boundary with retrieval is what
the data represents, not whether it changes. Memory processes interaction logs
and agent-derived state to maintain continuity and personalisation; RAG
processes domain documents for factual grounding. Temporal knowledge graph
memory (Zep/Graphiti) blurs this by also ingesting business facts, so treat
the split as a starting heuristic, not a hard rule.

## Reach For It When

Route here when one or more of these is true:

- **State must survive the session.** Facts, preferences, or learned behaviour
  need to persist across sessions, not just across turns within one.
- **History would blow the context window over time.** Conversation history
  alone, accumulated over many sessions, exceeds what any window can hold, so
  something must decide what to keep.
- **Personalisation and continuity are the requirement**, not one-off document
  lookup. "Remembers how I work" rather than "can find the policy PDF".
- **The agent should manage its own forgetting.** Nobody is available to prune
  by hand, so the retain/discard decision has to be made inside the loop.
- **Temporal correctness matters for agent/user state.** You need "what did the
  agent believe or do last month", not just "what is true now". External
  business facts with their own change history usually belong in versioned
  storage or temporal retrieval, not agent memory.

Route elsewhere when: the knowledge is static and pre-existing (retrieval or
RAG); the problem is a single overloaded window in one session (context
engineering); the agent just needs a fresh fact at call time (tools).

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Write-time extraction | Extracts and stores facts at the moment of interaction | Retrieval speed and per-query cost matter more than write-time compute |
| Query-time retrieval | Searches and assembles memory only when needed, via semantic, keyword, or graph search | Broad recall is needed without loading everything up front |
| Core / working memory | A small always-in-context block holding identity and key facts | Invariant persona or task state that must never be missed |
| Episodic memory | Records specific past events with temporal ordering (logs, tool-call traces) | Recalling what happened, and when |
| Semantic memory | Atemporal declarative facts and relationships | Grounding and personalisation |
| Procedural memory | Learned workflows, tool sequences, behavioural heuristics | Reusing successful strategies instead of relearning them |
| Decay and promotion | Overflows short-term buffers into long-term stores, rehydrated on demand | Keeping active context small while retaining unbounded history |
| Temporal knowledge graph | Models facts with explicit validity windows | Temporal correctness, auditing what was believed when |

## Use Cases & Examples

- **Letta (formerly MemGPT)** runs a three-tier hierarchy: core (pinned memory
  blocks), recall (searchable interaction history), archival (vector store). The
  agent self-edits its own memory via tool calls inside the reasoning loop.
  Skill learning shipped Dec 2025, letting agents persist reusable skills from
  task trajectories.
- **Claude's memory tool** (`memory_20250818`, GA on the Messages API, no beta
  header) persists notes to a file directory. It is client-side: Claude requests
  file operations, your application executes and stores them, and Claude reads
  them back just in time. Pairs with context editing and server-side compaction.
- **Zep / Graphiti** took the temporal-knowledge-graph route. Zep deprecated its
  Community Edition in April 2025 in favour of Graphiti (Apache-2.0), a
  bi-temporal graph engine that stamps facts with validity windows, and Graphiti
  now powers Zep Cloud.
- **Mem0** ships single-pass hierarchical extraction as a managed platform, an
  OSS package, and a local MCP memory server for clients like Claude Desktop and
  Cursor.

## Anti-Patterns

- **Conflating memory with RAG.** Using a vector store of static documents as if
  it were evolving agent memory produces stale or irrelevant personalisation.
- **Trusting a vendor benchmark.** Mem0 and Zep publish materially different
  LoCoMo and LongMemEval numbers depending on methodology and configuration, and
  independent evaluations sometimes reverse the vendor's own ranking. Cross-check
  before selecting on a score.
- **Reaching for the complex option first.** A files-on-disk baseline beat
  several specialised memory libraries on LoCoMo. Start there and earn the
  graph.
- **Self-managed memory with no decay policy.** Unbounded low-signal archival
  growth degrades retrieval precision later, and the degradation is invisible
  until recall quality drops.
- **Leaving memory on when unused.** Attackers have used cross-session memory as
  a persistence mechanism for injected instructions, surviving session
  termination. Memory turns a transient injection into a durable one.
- **Framework churn as a hidden cost.** Letta's V1 architecture (Oct 2025)
  deprecated its own heartbeat and `send_message` patterns in favour of native
  model reasoning. Assume the abstraction you build against will move.

## Mental Models

- [[mm-memory-pillars]]
- [[mm-routing]]
- [[mm-token-economics]]
- [[mm-verification]]

## State of Practice

As of Aug 2026:

- **Taxonomy: common vocabulary, not a settled implementation standard.** The
  episodic / semantic / procedural split is widely used as shorthand, but
  vendors still implement competing taxonomies underneath it (core/working,
  graph vs vector, temporal dimensions).
- **Vendor selection: contested and unresolved.** The Mem0 paper
  (arXiv:2504.19413, Apr 2025) gave the first broad head-to-head of around ten
  memory approaches including Zep and full-context baselines, and reported 26%
  relative improvement over OpenAI memory, 91% lower p95 latency, and over 90%
  token savings against full context. Independent third-party evaluations
  diverge sharply from vendor self-reports. Treat this sub-area as unsettled.
- **Platform-native memory: available.** Claude's memory tool is GA, which means
  the cheapest starting point is often no memory vendor at all.
- **Key tools:** Letta, Mem0, Zep / Graphiti, Claude's memory tool, plus
  files-on-disk as a serious baseline rather than a strawman.

## Links

- [[context-engineering]]
- [[security-agent-identity]]
- [[observability]]

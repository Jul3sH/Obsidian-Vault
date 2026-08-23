---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Context Engineering

> This article is the catalogue entry for context engineering, one of nine AI engineering pattern areas. It exists as a routing reference: when you are deciding how to attack a piece of AI work, read "Reach For It When" to tell whether this pattern is the one that applies, or whether the problem actually belongs to memory, tools, or model adaptation. Use it to pick an approach and to know which technique to reach for first; the deeper mechanics live in the vendor docs it links to.

## Key Takeaways

- Context engineering is about **what goes into the window at each inference step**, not about how a single prompt is worded. That is the line between it and prompt engineering.
- The failure it prevents is **context rot**: quality degrading as low-signal tokens accumulate, not as the task gets harder.
- The main techniques are now shipped API primitives on the Claude platform (compaction, tool-result clearing), so this is largely configuration rather than bespoke engineering. Both are **beta as of Aug 2026**, not GA.
- **RAG and long context are complementary, not rivals.** Retrieve to narrow, then reason over what you retrieved. Treating them as either/or is the common strategic error.
- Cost claims in this area are volatile. Treat published ratios as order-of-magnitude signals from one corpus, not as constants.

## What It Is

Context engineering is the discipline of curating the finite set of tokens fed to a model at inference time: system instructions, retrieved documents, tool outputs, memory, and conversation history all compete for the same budget. Anthropic frames it as "curating and maintaining the optimal set of tokens during LLM inference", against prompt engineering's narrower job of "writing and organizing LLM instructions". The practical driver is that recall degrades as the window fills, so the goal is the smallest high-signal subset for this step, not the largest set that fits.

## Reach For It When

Reach for context engineering when:

- **A session runs long enough to approach the window.** Multi-turn agents, overnight runs, anything where history plus tool output accumulates.
- **Quality is degrading without the task getting harder.** Answers get vaguer or the agent forgets earlier constraints. That is context rot, not a capability problem.
- **Tool output volume dominates the window, and the old results are no longer needed.** Large file reads and search results crowd out the dialogue. This points at clearing, but only once the model has already used that output. If the raw output is evidence you still need (citations, exact lines, audit trail), summarise or persist it instead of clearing.
- **The input mixes heterogeneous sources** (instructions, retrieved knowledge, tool results, history) and needs explicit structuring so the model can tell them apart.
- **You are choosing between stuffing more in and retrieving less but better.** That decision is this pattern.
- **You are authoring or revising a system prompt** and deciding how to section it.

Do **not** reach for it when:

- The problem is persistence **across sessions**, not within one. That is memory: see [[memory]].
- The problem is that the model lacks the skill or domain knowledge rather than the facts. That is model adaptation: see [[model-adaptation]].
- The problem is that the agent cannot act. That is tools: see [[tools-mcp]].

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Structured prompting | Organises the prompt into tagged sections (XML tags, Markdown headings) so the model can parse instruction from data from tool guidance | At authoring time, for any non-trivial system prompt |
| Compaction | Summarises older turns into a high-fidelity summary once a token threshold is hit, replacing the raw history | Long-running agentic loops where dialogue is the bulk |
| Context editing / tool-result clearing | Clears stale, already-processed tool outputs server-side instead of summarising them | When tool output, not dialogue, dominates the window and the raw output is no longer needed as evidence |
| Hierarchical structuring | Layers system prompt, top retrieval hits, background, tool descriptions so the highest-value material is seen first | RAG-heavy applications |
| Just-in-time retrieval | Loads data at runtime via lightweight identifiers rather than pre-loading everything | Variable, query-dependent context needs |
| Sub-agent isolation | Gives a focused task its own clean window and returns only a condensed summary to the parent | Wide exploration that would otherwise flood the main context |
| Structured note-taking | Model writes notes to a file outside the window and reads them back later | Work spanning more turns than one window holds |
| RAG vs long context selection | Chooses retrieval or full-document loading on corpus size, update frequency, and attribution needs | Any knowledge-grounded application |
| Hybrid retrieve-then-reason | Uses retrieval to narrow candidates, then long-context reasoning over the passages | A strong starting point for most knowledge-grounded work, but check it against corpus size, model capability, and task type rather than assuming it (see State of Practice, contested) |

## Use Cases & Examples

- **Anthropic's Claude platform ships the primitives.** Server-side compaction (`compact_20260112`, beta header `compact-2026-01-12`, default trigger 150,000 input tokens, minimum 50,000) and context editing (`clear_tool_uses_20250919`, beta header `context-management-2025-06-27`) are configuration flags on the Messages API, plus a client-side memory tool (`memory_20250818`). Both context-management features are **beta**, not GA. The docs recommend a cache breakpoint at the end of the system prompt so it stays cached when a compaction rewrites the conversation.
- **Letta's engineering team** draws the conceptual line "RAG is a retrieval pattern, not a memory system", and runs a layered architecture combining retrieval, compressed observation logs, and live context rather than choosing one.
- **The long-context end of the trade-off** is moving toward 1M-token windows, but availability is still gated, not standard: Claude's 1M context is a beta capability, limited to specific Claude models and to tier 4 or custom-limit accounts, not a default for all Claude usage. Gemini 3 Pro documents 1M input tokens as standard (larger enterprise configurations are claimed by secondary sources but not by Google's own model docs).

## Anti-Patterns

- **Brute-force corpus stuffing.** Filling the window degrades quality via the "lost in the middle" effect (Liu et al., 2023: recall is highest at the start and end of the context and drops in the middle, and falls further as the context grows), and compute cost grows non-linearly with length.
- **Long context alone for a large or fast-changing knowledge base.** Cost and latency both scale badly, and there is no attribution trail.
- **Waiting until the window is nearly full to compact.** Quality drops abruptly at exactly the moment the task is most complex. Set the threshold well below the limit.
- **Treating RAG and long context as mutually exclusive.** Practitioner writing in 2026 increasingly favours hybrid over choosing one exclusively, but this is not settled: the LaRA benchmark found no single winner across model, corpus, and task (see State of Practice, contested).
- **Quoting cost ratios as laws.** The widely repeated "RAG is roughly 1,250x cheaper per query" figure traces to a single vendor experiment on one documentation corpus (about $0.00008 versus about $0.10 per query, with roughly 45-second latency on the stuffed version). The direction is real and large; the number is not a constant, and it is not independently reproduced.
- **Compacting when you should be clearing.** Summarising a wall of already-used, re-fetchable tool output wastes tokens on material that should simply be dropped. The reverse mistake is clearing tool output that is itself the evidence (citations, exact lines, audit trail): that should be summarised or persisted, not dropped.

## Mental Models

- [[mm-token-economics]]
- [[mm-memory-pillars]]
- [[mm-routing]]

## State of Practice

As of Aug 2026:

- **Maturity: mature and actively evolving.** The prompt-engineering / context-engineering distinction, which dated from around July 2025, is now standard vocabulary, and the core techniques have moved from cookbook patterns to first-party API features.
- **Key tools:** Claude platform compaction and context editing (both beta), the Claude memory tool, Claude Code and the Claude Agent SDK's compaction control, LangChain/LlamaIndex retrieval layers, Letta for layered memory-plus-retrieval architectures.
- **Contested (flagged in the source research and left contested here):** whether RAG or long context wins for factual Q&A. The LaRA benchmark (ICML 2025, 2,326 test cases) concluded there is **no silver bullet**: the better choice depends on model size, long-text capability, context length, task type, and the characteristics of the retrieved chunks. Claims that either approach simply wins should be treated as unsupported.
- **Time-sensitive:** any specific context-window size or per-token price here will age within months. Re-check against vendor docs before it feeds a decision.

## Links

- [[memory]] - persistence across sessions, where this pattern ends
- [[tools-mcp]] - tool output is the largest single consumer of context
- [[model-adaptation]] - the prompting / RAG / fine-tuning choice this feeds into
- [[orchestration]] - sub-agent isolation as a context strategy
- [[evals]] - most retrieval-system eval failures turn out to be context failures

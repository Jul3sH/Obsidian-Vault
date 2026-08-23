---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Orchestration & Workflow Architectures

> This is the orchestration entry in the AI engineering patterns catalog: how multiple LLM calls or agents get composed into a system, from fixed pipelines through to dynamic multi-agent teams. It exists as a routing reference, so that someone deciding how to attack a piece of AI work can tell quickly whether their problem needs a workflow, a single agent, or several agents, and which named shape fits. Read the "Reach For It When" section first and stop there if the answer is a single agent; the technique table and anti-patterns are for when it is not.

## Key Takeaways

- The primary split is **fixed control flow (workflow) vs model-driven control flow (agent)**. Anthropic's framing: workflows orchestrate LLMs and tools through predefined code paths, agents let the model direct its own process and tool use.
- **A single agent with tools is the default baseline.** Multi-agent is an escalation you justify with a named failure of that baseline, never a starting point.
- **Multi-agent buys breadth at roughly 15x the token cost of chat.** Anthropic's Research system (Opus 4 lead, Sonnet 4 subagents) beat single-agent Opus 4 by 90.2% on an internal research eval and used about 15x chat tokens; a single agent uses about 4x.
- **Read-heavy and independent goes wide; write-heavy and coupled stays narrow.** Most coding work is the second kind.
- **A verifier is only as strong as its criteria.** Generator-verifier loops without explicit acceptance criteria produce confidence, not quality.

## What It Is

Orchestration is the composition layer above a single model call: how work is decomposed, dispatched, and recombined across calls or agents. It spans a spectrum rather than a binary, from a hard-coded sequence of prompts, through a classifier that dispatches to specialists, to a lead agent that plans and delegates to subagents it spawns at runtime. The choice determines predictability, latency, token cost, and how much of the system you can actually inspect when it goes wrong.

## Reach For It When

Work down this list and stop at the first match.

| Situation | Reach for |
|---|---|
| The task decomposes into a **known, repeatable sequence** of stages (approval chains, compliance checks, extract then validate then format) | A **workflow**: fixed control flow in code. Deterministic, cheap, debuggable. |
| Inputs fall into **known categories** each needing different handling | **Routing / classify-and-act**, dispatching to a specialist prompt or agent. |
| The task fits **one context window** and needs no parallelism | **A single agent with tools.** This is the default. Most work stops here. |
| The single-agent baseline hits a **named, concrete failure** | Escalate. The failure must be one of the three below. |
| Failure is **context-window exhaustion**: the information needed exceeds what one agent can hold | **Orchestrator-workers**, subagents each holding their own slice. |
| Failure is **wasted wall-clock on genuinely independent subtasks** | **Parallel fan-out and synthesise** (sectioning). |
| Failure is **needing an independent critique**, and you can state acceptance criteria | **Generator-verifier loop.** No criteria means do not build it. |
| None of the above bites | Stay single-agent. Give it a longer leash, better tools, or better context instead. |

Generator-verifier is additive, not a last resort: if acceptance criteria are already known and checkable, pair it with the single agent from the start. Do not wait to observe a failure first just because it is listed as an escalation.

Two counter-triggers that override everything above:

- **All agents would need the same context, or the steps depend heavily on each other.** Anthropic names this explicitly as a poor fit for multi-agent. Most coding tasks land here.
- **You cannot check the split outputs.** Separation is the demand, verification is the permission. See [[mm-routing]].

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Prompt chaining / sequential pipeline | Output of step N feeds step N+1, each with a focused prompt | Naturally ordered stages: draft, critique, refine |
| Routing / classify-and-act | Classify the input, dispatch to a specialist | Known input categories with different handling |
| Parallelisation: sectioning | Split into independent chunks, run concurrently, reduce | Subtasks that genuinely do not depend on each other |
| Parallelisation: voting | Run the same task N times, take majority or best | High-stakes judgements, generate-and-filter, ensembles |
| Orchestrator-workers (supervisor) | Lead agent plans, delegates to subagents, aggregates | Breadth-first search where scope is unknown upfront |
| Generator-verifier / evaluator-optimizer | One agent produces, another checks against criteria, loop | Only when acceptance criteria can be written down |
| Handoff / swarm | Agents transfer control peer to peer, no central hub | Escalation and expert routing, where the specialist owns the rest of the turn |
| Agents-as-tools (manager pattern) | Central agent calls specialists as tools, keeps the conversation | Bounded subtasks that should not take over the user-facing thread |
| Agent teams (persistent workers) | Workers persist across assignments and accumulate domain knowledge | Large-scale migrations where familiarity compounds |
| Message bus / event-driven | Flow emerges from events, not a predetermined sequence | Pipelines like alert triage, where new capabilities plug in without rewiring |
| Shared state / blackboard | No coordinator; agents read and write a shared store | Research synthesis where one finding should immediately inform others |
| ReAct | Interleaved reason-then-act loop | The base agent loop underlying most of the above |
| ReWOO | Plans the whole call graph upfront, then executes in parallel and solves once | Token-efficient alternative to ReAct when the plan does not depend on intermediate observations |

## Use Cases & Examples

- **Anthropic's Research feature** is the reference orchestrator-workers implementation: an Opus 4 lead spawns three to five Sonnet 4 subagents in parallel with a separate citation pass. It beat single-agent Opus 4 by 90.2% on an internal research eval, at roughly 15x the tokens of a chat turn. The write-up is candid that it suits breadth-first questions and not coupled work.
- **Claude Code** uses subagents for background codebase search while the main agent continues on the primary thread, keeping the search context out of the main window.
- **Framework convergence.** LangGraph (supervisor, swarm), the OpenAI Agents SDK (manager / agents-as-tools, handoffs), CrewAI (sequential and hierarchical processes) and the Microsoft Agent Framework (sequential, concurrent, handoff, group chat, magentic) all ship a small, overlapping set of shapes. The names differ, the underlying four are supervisor, parallel fan-out and fan-in, sequential handoff, and shared state. Microsoft additionally ships group-chat and planner-driven ("magentic") variants that the others do not name.
- **Single agent plus a skill library** is an increasingly documented substitute for multi-agent on sequential work: "When Single-Agent with Skills Replace Multi-Agent Systems and When They Fail" (arXiv 2601.04748, Jan 2026) reports substantial token and latency reductions at competitive accuracy, and finds skill selection degrades sharply past a critical library size, driven more by semantic confusability between skills than by count.

## Anti-Patterns

- **Defaulting to multi-agent.** The most commonly cited failure in 2026 sources. Build the single-agent baseline, watch it fail, name the failure, then escalate to the shape that addresses that specific failure.
- **Multi-agent on coupled work.** Shared context, heavy step interdependency, or real-time coordination between agents. Most coding tasks. The coordination overhead lands and the benefit does not.
- **Over-coordination.** Deep orchestration hierarchies add latency and token cost per layer without proportional gain. Depth is expensive; prefer width at one level.
- **Generator-verifier without criteria.** If you cannot write down what "acceptable" means, the verifier will approve almost anything and you have bought confidence rather than quality. Anthropic's stated precondition for this pattern is that a human could articulate the feedback and the model could produce it.
- **Ignoring the token multiplier.** A 15x cost is defensible for high-value research and indefensible for routine work. Price the pattern before you build it.
- **Reaching for an agent when a workflow would do.** If the sequence is known and fixed, model-driven control flow buys you nondeterminism you did not want.

## Mental Models

[[mm-routing]], [[mm-verification]], [[mm-token-economics]]

## State of Practice

As of Aug 2026:

- **Mature and settled:** the workflow-vs-agent distinction, the five Anthropic workflow patterns, and single-agent-with-tools as the baseline. These are stable across Anthropic, OpenAI, LangChain and Microsoft documentation.
- **Consensus house pattern:** supervisor plus parallel fan-out for read-heavy independent work; single agent with long context for write-heavy coupled work.
- **Still moving:** persistent agent teams, event-driven and blackboard architectures, and the single-agent-with-skills substitution. Documented and shipping, but with thinner empirical backing than the core shapes.
- **Key tools:** LangGraph, OpenAI Agents SDK, CrewAI, Microsoft Agent Framework, Claude Code subagents.
- **Evidence caveat:** Anthropic's March 2025 multi-agent write-up remains the most-cited empirical case for multi-agent value and is now well over a year old. Newer material increasingly emphasises when *not* to go multi-agent, and this catalog weights that shift.

## Links

[[context-engineering]], [[evals]], [[tools-and-mcp]], [[observability]]

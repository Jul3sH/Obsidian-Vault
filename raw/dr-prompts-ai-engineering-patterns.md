# Perplexity Deep Research Prompts — AI Engineering Patterns

> **Purpose block.** This is a working file of copy-paste prompts for Perplexity Deep Research for the [[ai-engineering-pattern-articles]] deliverable. It was created 23 Aug 2026 after Julian decided Perplexity should do the grounding research instead of Sonnet agents. **Primary route (agreed 23 Aug): the single-shot prompt below — one run producing all 8 area reports in one document, saved as `raw/dr-all-areas.md`.** The 8 individual prompts further down are the fallback: re-run one if the single-shot output is thin for that area. The workflow's Opus agents validate and draft from the saved report(s). Delete or archive this file once the research is in.

---

## SINGLE-SHOT PROMPT (primary) — all 8 areas in one run
Save output as: `raw/dr-all-areas.md`

```
I am building an AI engineering patterns catalog used to route engineering tasks to the right approach. It covers 8 pattern areas. Research ALL of them and produce ONE report with a clearly delimited section per area, in this order:

AREA 1 — CONTEXT ENGINEERING: deciding what goes into an LLM's context window and how it is structured — system prompt design, prompt structure, RAG vs long-context tradeoffs, context compression/compaction, few-shot selection, context management over long agent sessions.
AREA 2 — MEMORY: agent memory architectures — write-time vs query-time paradigms, episodic/semantic/procedural memory, vector-store-backed recall, memory decay and promotion, the product landscape (Letta/MemGPT, Zep, Mem0, built-in memory in agent tools).
AREA 3 — TOOLS & MCP: designing tools for LLM agents, function calling best practice, the Model Context Protocol and its ecosystem, tool discovery/search at scale, tool permissioning.
AREA 4 — EVALS: eval-driven development, eval types (unit-style assertions, end-to-end task evals, LLM-as-judge, human review), product evals vs benchmarks, regression suites, observability, tooling (Braintrust, LangSmith, promptfoo).
AREA 5 — ORCHESTRATION & WORKFLOW ARCHITECTURES: single-agent vs multi-agent, workflows (deterministic control flow) vs agents (model-driven control flow), the named shapes (fan-out and synthesize, classify and act, generate and filter, tournament, loop until done, adversarial verification, pipelines), when NOT to go multi-agent.
AREA 6 — SPEC-DRIVEN DEVELOPMENT: specifications as the source of truth AI coding agents implement against — spec-first workflows, plan-then-execute, acceptance criteria for agents, test-first with agents, tools (spec modes in AI IDEs, Amazon Kiro, GitHub Spec Kit).
AREA 7 — SECURITY & AGENT IDENTITY: prompt injection and mitigations, tool permission models, sandboxing, data exfiltration, supply-chain trust for MCP servers, and agent identity — how agents authenticate, workload identity, OAuth for agents acting on a user's behalf, emerging standards.
AREA 8 — GAP SCAN: survey how practitioners carve up AI engineering in 2025-2026 (AI lab engineering guides, practitioner curricula, conference tracks, respected landscape posts). Identify the strongest pattern area MISSING from areas 1-7 (candidates to test: model routing/selection, cost and token economics, fine-tuning vs prompting, human-in-the-loop and AI UX patterns, deployment/versioning). Name it, justify the choice briefly, then research it as area 8.

For EACH of the 8 areas, use exactly this section structure:

1. DEFINITION — what practitioners mean by it today (for area 1, distinguish it from "prompt engineering"; for area 2, say where memory ends and retrieval begins).
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer this pattern is the right one to reach for.
3. TECHNIQUE TAXONOMY — the named sub-techniques, each with one line on what it does and when to use it.
4. CONCRETE EXAMPLES — 3-5 current, named examples (companies, tools, published engineering practice).
5. ANTI-PATTERNS & FAILURE MODES — when this pattern is the wrong choice, and how it commonly goes wrong.
6. STATE OF PRACTICE — maturity, key tools/frameworks, notable developments since early 2025.
7. SOURCES — every claim cited with a dated source.

Constraints for the whole report: this is a breadth catalog, so aim for consistent, substantial coverage of every area rather than exhausting any one of them. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs and specs, security research, conference talks) over SEO content and news aggregators. Prioritise 2025-2026 sources and flag anything older. Flag contested or uncertain claims explicitly. Start each area with a heading in the form "## AREA N — [NAME]" so the sections can be split programmatically.
```

---

## FALLBACK — individual per-area prompts

Use these only to re-run a single area if its single-shot section comes back thin. Each is self-contained. Save outputs under the per-prompt filenames.

---

## Prompt 1 — Context Engineering
Save output as: `raw/dr-context-engineering.md`

```
Research CONTEXT ENGINEERING as practised in AI engineering in 2025-2026: the discipline of deciding what goes into an LLM's context window and how it is structured — system prompt design, prompt structure, retrieval (RAG) vs long-context tradeoffs, context compression and compaction, few-shot example selection, and context window management over long agent sessions.

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — what practitioners mean by context engineering today, and how it differs from "prompt engineering".
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer this pattern is the right one to reach for.
3. TECHNIQUE TAXONOMY — the named sub-techniques (e.g. RAG, compaction, structured prompting), each with one line on what it does and when to use it.
4. CONCRETE EXAMPLES — 3-5 current, named examples (companies, tools, published engineering practice).
5. ANTI-PATTERNS & FAILURE MODES — when this pattern is the wrong choice, and how it commonly goes wrong.
6. STATE OF PRACTICE — maturity, key tools/frameworks, and notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content and news aggregators. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 2 — Memory
Save output as: `raw/dr-memory.md`

```
Research MEMORY ARCHITECTURES for AI agents as practised in 2025-2026: how agents persist and recall information across sessions — write-time vs query-time paradigms, episodic vs semantic vs procedural memory, vector-store-backed recall, memory decay and promotion, and the current product landscape (e.g. Letta/MemGPT, Zep, Mem0, built-in agent memory in Claude Code and similar tools).

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — what practitioners mean by agent memory today, and where it ends and retrieval/context engineering begins.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer memory (rather than bigger context or plain RAG) is the right pattern.
3. TECHNIQUE TAXONOMY — the named approaches and architectures, each with one line on what it does and when to use it.
4. CONCRETE EXAMPLES — 3-5 current, named examples (products, architectures, published engineering practice).
5. ANTI-PATTERNS & FAILURE MODES — when memory is over-engineering, and how memory systems commonly fail (staleness, leakage, cost).
6. STATE OF PRACTICE — maturity, key products/frameworks, and notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 3 — Tools & MCP
Save output as: `raw/dr-tools-mcp.md`

```
Research TOOL USE AND MCP (Model Context Protocol) in AI engineering, 2025-2026: designing tools for LLM agents, function calling best practice, the MCP protocol and its ecosystem, tool discovery/search at scale, agentic tool-use patterns, and tool permissioning.

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — what tool use and MCP mean in current practice, and how MCP relates to plain function calling.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer tools/MCP integration is the right pattern for the job.
3. TECHNIQUE TAXONOMY — the named sub-patterns (tool design principles, MCP servers/clients, tool search, sandboxed execution), each with one line on what it does and when.
4. CONCRETE EXAMPLES — 3-5 current, named examples (real MCP servers, published tool-design practice, ecosystem adoption).
5. ANTI-PATTERNS & FAILURE MODES — over-tooling, tool sprawl, badly-shaped tool definitions, protocol misuse.
6. STATE OF PRACTICE — maturity of the MCP ecosystem, key registries and frameworks, notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs and specs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 4 — Evals
Save output as: `raw/dr-evals.md`

```
Research EVALS (evaluation systems) for LLM applications and agents, 2025-2026: eval-driven development, eval types (unit-style assertions, end-to-end task evals, LLM-as-judge, human review), product evals vs public benchmarks, regression suites, observability/tracing, and the current tooling landscape (e.g. Braintrust, LangSmith, promptfoo, OpenAI Evals).

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — what practitioners mean by evals today, and how product evals differ from benchmarks.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer to invest in evals (and at what point in a project's life).
3. TECHNIQUE TAXONOMY — the named eval types and methods, each with one line on what it does and when to use it.
4. CONCRETE EXAMPLES — 3-5 current, named examples of eval practice at real companies or in real products.
5. ANTI-PATTERNS & FAILURE MODES — vanity evals, judge bias, overfitting to evals, evals nobody runs.
6. STATE OF PRACTICE — maturity, key tools, and notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 5 — Orchestration & Workflow Architectures
Save output as: `raw/dr-orchestration.md`

```
Research ORCHESTRATION AND WORKFLOW ARCHITECTURES for AI systems, 2025-2026: single-agent vs multi-agent designs, workflows (deterministic, code-defined control flow) vs agents (model-driven control flow), fan-out/synthesize, pipelines, supervisor/subagent patterns, adversarial verification stages, and when each architecture wins. Include the major frameworks and the published guidance from AI labs on choosing between them.

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — the space of orchestration architectures as practitioners carve it up today, including the workflow-vs-agent distinction.
2. ROUTING TRIGGERS — the task shapes and signals that indicate which architecture fits (and when NOT to go multi-agent).
3. TECHNIQUE TAXONOMY — the named orchestration shapes (fan-out and synthesize, classify and act, generate and filter, tournament, loop until done, adversarial verification, pipelines), each with one line on what it does and when.
4. CONCRETE EXAMPLES — 3-5 current, named examples of these architectures in real products or published practice.
5. ANTI-PATTERNS & FAILURE MODES — multi-agent for its own sake, coordination overhead, error compounding across agents.
6. STATE OF PRACTICE — maturity, key frameworks, and notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 6 — Spec-Driven Development
Save output as: `raw/dr-spec-driven.md`

```
Research SPEC-DRIVEN DEVELOPMENT with AI coding agents, 2025-2026: using specifications as the source of truth that AI agents implement against — spec-first workflows, plan-then-execute patterns, PRD-to-code, acceptance criteria written for agents, test-first development with agents, and the tools built around this (e.g. spec modes in AI IDEs, Amazon Kiro, GitHub Spec Kit, similar).

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — what spec-driven development means in current AI-assisted engineering practice.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer to work spec-first rather than conversationally/iteratively.
3. TECHNIQUE TAXONOMY — the named sub-patterns (spec formats, plan approval gates, spec-to-test chains), each with one line on what it does and when.
4. CONCRETE EXAMPLES — 3-5 current, named examples (tools, published team workflows).
5. ANTI-PATTERNS & FAILURE MODES — over-specification, stale specs, specs as theatre, when iteration beats specification.
6. STATE OF PRACTICE — maturity, key tools, and notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 7 — Security & Agent Identity
Save output as: `raw/dr-security-agent-identity.md`

```
Research SECURITY FOR AI AGENTS AND AGENT IDENTITY, 2025-2026: prompt injection and its mitigations, tool permission models, sandboxing agent execution, data exfiltration risks, supply-chain trust for MCP servers and plugins, and agent identity specifically — how agents authenticate, workload identity for agents, OAuth flows for agents acting on a user's behalf, and emerging standards.

I am building a patterns catalog used to route engineering tasks to the right approach. Produce a research report (not a polished article) with exactly these sections:

1. DEFINITION — the agent security threat landscape as practitioners describe it today, and what "agent identity" covers.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer security patterns must be designed in (not bolted on) for a given piece of work.
3. TECHNIQUE TAXONOMY — the named defences and identity patterns, each with one line on what it does and when.
4. CONCRETE EXAMPLES — 3-5 current, named examples (real incidents, published mitigations, identity implementations).
5. ANTI-PATTERNS & FAILURE MODES — the common ways agent deployments get compromised or leak data.
6. STATE OF PRACTICE — maturity, key standards and tools, notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material (security research, engineering blogs of AI labs and serious companies, official docs, conference talks) over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---

## Prompt 8 — Gap Scan + Eighth Area
Save output as: `raw/dr-eighth-area.md`

```
I am building an AI engineering patterns catalog with these 7 pattern areas: context engineering, memory, tools/MCP, evals, orchestration and workflow architectures, spec-driven development, and security including agent identity. The catalog is used to route engineering tasks to the right approach.

PART 1 — GAP SCAN: Survey how practitioners carve up the AI engineering discipline in 2025-2026 (AI lab engineering guides, practitioner curricula, conference tracks, well-regarded landscape posts). Identify the major pattern areas treated as first-class that my list is missing. Candidates to test include: model routing and selection, cost and token economics, fine-tuning vs prompting, human-in-the-loop and AI UX patterns, deployment and versioning of AI systems. Rank the gaps and recommend the SINGLE strongest missing area, with your reasoning.

PART 2 — RESEARCH THE RECOMMENDED AREA: For that one recommended area, produce a research report with exactly these sections:

1. DEFINITION — what practitioners mean by it today.
2. ROUTING TRIGGERS — the task shapes and signals that tell an engineer this pattern is the right one to reach for.
3. TECHNIQUE TAXONOMY — the named sub-techniques, each with one line on what it does and when.
4. CONCRETE EXAMPLES — 3-5 current, named examples.
5. ANTI-PATTERNS & FAILURE MODES — when it is the wrong choice and how it goes wrong.
6. STATE OF PRACTICE — maturity, key tools, notable developments since early 2025.
7. SOURCES — every claim cited with a dated source. Prefer practitioner-grade material over SEO content. Prioritise 2025-2026 sources; flag anything older. Flag contested or uncertain claims explicitly.
```

---
type: index
created: 2026-08-23
updated: 2026-08-23
---

# AI Engineering Patterns

> *Navigation only: nine pattern-area reference articles, each answering "is this the pattern that applies to the job in front of me?"*

## What belongs here

Succinct, breadth-first reference articles for **pattern areas in AI engineering**,
written to route a piece of work to the right approach before anything is built.
One article per area. Each carries the same shape: what it is, reach for it when,
core techniques, examples, anti-patterns, mental models, state of practice.

Does not belong here:

- **Depth on a single tool or vendor.** That is a product reference elsewhere in
  [[technology/_index|wiki/technology/]].
- **Julian's own setup.** Skills, mirrors, and the running operating layer live in
  [[ai-os/taxonomy|wiki/ai-os/]], however closely they instantiate a pattern here.
- **The decision heuristics themselves.** Mental models are filed by
  [[mental-models-index]] and linked from each article, not stored in this folder.

Boundary test: would this still be true and useful for someone who had never seen
this vault, and does it describe a *class* of approach rather than one product? If
yes, it belongs here.

## Articles

| Article | What it is |
|---|---|
| [[context-engineering]] | What goes into the model's window at each inference step: compaction, tool-result clearing, retrieval versus long context |
| [[memory]] | Persistent agent state across sessions: the episodic / semantic / procedural split, decay, and temporal knowledge graphs |
| [[tools-mcp]] | How an agent calls external functions, the MCP wire format, and schema-constrained output |
| [[evals]] | Measuring output quality systematically before deploy: datasets, scorers, LLM-as-judge, regression suites |
| [[observability]] | Runtime tracing, online eval scoring, and drift monitoring on live traffic after deploy |
| [[orchestration]] | Composing multiple calls or agents into a system, from fixed workflows to dynamic multi-agent teams |
| [[spec-driven-development]] | Writing a versioned spec as the artefact a coding agent implements against, reviewed at the intent layer |
| [[security-agent-identity]] | The agent threat model (prompt injection, tool permissioning, MCP supply chain) and how an agent authenticates |
| [[model-adaptation]] | Shaping what a model knows or how it behaves: prompting, RAG, fine-tuning, and the hybrid |

## Reading Order

- **Building something new:** [[spec-driven-development]], then [[orchestration]],
  then [[context-engineering]] and [[tools-mcp]].
- **Something already built is not good enough:** [[evals]] first, then
  [[model-adaptation]].
- **Something already built is misbehaving in production:** [[observability]],
  then [[security-agent-identity]].
- **State is being lost between sessions:** [[memory]].

## Related

- [[mental-models-index]] - the decision heuristics these articles link out to.
- [[technology/Memory systems/_index|Memory Systems]] - depth behind [[memory]].
- [[ai-os/skills/_index|AI OS / Skills]] - the local instance of the tool-surface pattern.

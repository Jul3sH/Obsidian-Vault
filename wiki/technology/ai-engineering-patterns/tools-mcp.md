---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Tools & MCP

> This article is the catalog entry for the Tools and MCP pattern area: how an agent is given the ability to call external functions and services, and how those calls are made reliable. It exists as a routing reference, one of nine pattern articles used to decide how to attack a piece of AI engineering work before building anything. Read the "Reach For It When" section to tell whether this pattern applies to the job in front of you, then use the technique table to pick the specific mechanism.

## Key Takeaways

- Tools are the pattern when the agent must **call an external function**, whether that produces a side effect (a write) or just fetches or computes a fact it cannot know unaided. Prose the model generates without calling anything external is not your area.
- MCP is the vendor-neutral wire format for that, now governed by the Linux Foundation rather than by Anthropic.
- The dominant scaling failure is **tool-schema flooding**: dumping every tool definition into context degrades both accuracy and cost. On-demand tool loading is the fix.
- Schema-constrained decoding is a solved problem as of 2026, but only when it actually engages: refusals, truncation, and schema-complexity limits can bypass the constraint, so validate parsed output anyway. Plain JSON mode in production is an anti-pattern: it guarantees the output parses, not that it matches your shape.
- Constraining output has a measured cost on multi-step reasoning. Let the model reason free-form first, constrain only the final structured step.

## What It Is

Tool design covers how an LLM agent discovers, calls, and is permitted to use external functions: the naming, the schema, the error contract, and the permission gate. The Model Context Protocol (MCP) is the open JSON-RPC 2.0 standard for the transport layer of that, introduced by Anthropic in November 2024 and donated to the Linux Foundation's Agentic AI Foundation on 9 December 2025, so any compliant client can use any compliant server without bespoke glue. Structured output and constrained decoding sit underneath both as the reliability layer that makes a call's arguments and an agent's final answer conform to a fixed shape.

## Reach For It When

Route work here when any of these hold:

- **The agent needs real side effects.** Database writes, API calls, file operations, anything where "the model described what it would do" is not the deliverable.
- **The agent needs to fetch or compute a fact it cannot know on its own.** A live price, a search result, a calculation, a database read. No side effect occurs, but the call still needs a schema, an error contract and a permission gate, same as a write.
- **The same capability must be reachable from more than one client.** Claude, ChatGPT, Cursor, an internal agent. That is the MCP case specifically; a single-client integration does not need a protocol.
- **A downstream system consumes the output.** If a parser, a database column, or another service reads what the model emits, you need schema-constrained output, not prompt-and-hope.
- **The tool catalogue is growing past what fits comfortably in context.** Once tool definitions are a material share of the window, switch from static listing to search or on-demand loading.
- **The agent has destructive reach.** Anything that can delete, spend, or send needs a permissioning and confirmation layer designed in, not bolted on.

Do **not** route here when the work is a one-off, single-client script (write a function, skip the protocol), or when the required output is genuinely open-ended prose the model produces without calling anything external.

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Single-purpose tools | One clear job per tool, descriptively named (`search_orders`, not `do_stuff`) | Always. Overlapping tools are the top cause of wrong-tool selection |
| Model-facing descriptions | Descriptions written as prompts for the model (when to use, when not to) rather than developer docs | Every tool exposed to an LLM |
| Schema typing and validation | Strict JSON Schema, enums, business-rule checks before execution | Any tool with side effects |
| Actionable error returns | Structured errors telling the model how to recover, not stack traces | Any agent expected to self-correct in a loop |
| MCP transports | stdio for local, Streamable HTTP for remote. HTTP+SSE is deprecated | Choose on deployment topology |
| MCP authorization | OAuth 2.1 resource-server model, Protected Resource Metadata (RFC 9728), Client ID Metadata Documents | Any remote server exposing privileged operations |
| On-demand tool loading | Load names first, full schemas only when needed (Anthropic's code-execution / `search_tools` pattern) | Large tool catalogues, or when schemas dominate the window |
| Tool permissioning and gating | Minimum exposed surface, confirmation gates on destructive actions, rate limits | Any agent with real-world reach |
| Schema-constrained decoding | Masks invalid tokens at the sampler so output must match the schema | Whenever a call's arguments or a final answer must match a fixed shape |

Three tiers of output reliability, in ascending order: prompt-only JSON (no guarantee), provider JSON mode (parseable, not schema-conformant), schema-constrained decoding (conformant by construction, invalid tokens are masked at the sampler). Only the third is production-grade, and even then validate the parsed result: a refusal, a truncated response, or a schema past the provider's complexity limit can bypass the constraint entirely.

## Use Cases & Examples

- **MCP as the default integration layer.** At the Linux Foundation donation (Dec 2025) MCP had 97M+ monthly SDK downloads and 10,000+ active public servers, with native client support across Claude, ChatGPT, Gemini, Microsoft Copilot, Cursor and others. Slack, GitHub, Salesforce, Stripe and Notion servers are off-the-shelf.
- **On-demand tool loading at scale.** Anthropic's code-execution-with-MCP post (4 Nov 2025) reports cutting a scenario from 150,000 tokens to 2,000 (98.7%) by presenting tools as a filesystem the agent navigates, loading full definitions only when needed. Composio's 1,000+ toolkits and 20,000+ tools illustrate the scale that forces this.
- **Schema-constrained output across all three major providers.** OpenAI `json_schema` with `strict: true`, Anthropic `output_config.format` plus `strict: true` on tool definitions (now GA, beta header no longer required), Google Gemini `responseSchema`. Local runtimes get the same guarantee via GBNF grammars (llama.cpp, Ollama) or guided-decoding backends such as XGrammar.

## Anti-Patterns

- **Overlapping or vaguely-named tools.** The model picks the wrong one. Fix is a small, distinct surface, not a longer description.
- **Dumping every tool schema into context.** Same "lost in the middle" failure as context engineering, applied to tool definitions. Costs latency and accuracy together.
- **Plain JSON mode in production.** It guarantees parseability only. OpenAI's own docs now treat unconstrained JSON mode as legacy.
- **Constraining the whole response on a reasoning task.** Studies report meaningful degradation on multi-step reasoning under strict format constraints, and the mechanism is known: if the answer field precedes the reasoning field, the model commits before it thinks. Give it a free-form scratchpad, then constrain the final step.
- **Trusting registry adoption numbers.** MCP directories (Glama, PulseMCP, Smithery) report wildly divergent server counts on different methodologies, and survey figures for enterprise production use range from roughly 40% to claims near 80% depending on source. Treat growth as directionally strong, not precisely known. *(Contested, flagged in source research and confirmed on checking.)*
- **Building a protocol for a single consumer.** MCP earns its keep across clients. One client, one script, no protocol.

## Mental Models

[[mm-routing]], [[mm-verification]], [[mm-token-economics]], [[mm-steering]], [[mm-blast-radius]] (least privilege and the gate on destructive reach)

## State of Practice

As of Aug 2026:

- **MCP is the de facto standard**, under Linux Foundation governance, with a fast spec cadence: 2024-11-05 initial, 2025-03-26 Streamable HTTP, 2025-11-25 OAuth 2.1 and CIMD, 2026-07-28 stateless core.
- **The 2026-07-28 revision is the largest change since launch.** It removed the `initialize`/`initialized` handshake (SEP-2575) and protocol-level sessions with the `Mcp-Session-Id` header (SEP-2567), so any request can land on any server instance and sticky routing is no longer required. Roots, Sampling and Logging are now deprecated, and Dynamic Client Registration is deprecated in favour of Client ID Metadata Documents. **If you are building against MCP now, build against the stateless spec** for ordinary remote tool calls; keep a stateful or hybrid mode only where the server genuinely needs subscriptions, unsolicited server-to-client notifications, or per-client session isolation.
- **Structured output is mature.** All three major providers ship true schema-constrained decoding; it moved from a 2023-2024 pain point to a solved capability.
- **Enterprise attention has shifted** from basic integration to gateway and registry control planes, structured audit trails, and SSO-integrated auth.
- **Tool discovery at very large scale is still research.** The ToolDNS proposal (arXiv 2607.18242) benchmarks discovery across 33,688 real tools spanning MCP, A2A, REST and Skill protocols, but it is a preprint, not practice.

## Links

Related pattern articles in this folder: [[context-engineering]] (the same context-budget problem, applied to knowledge rather than tool schemas), [[evals]] (how you prove a tool surface works), [[orchestration]] (what calls the tools), [[security-agent-identity]] (permissioning, prompt injection through tool returns).

[[ai-os/skills/_index|AI OS skills]] is the local instance of this pattern: skills are the tool surface this vault actually exposes, and the same distinctness and least-privilege rules apply.

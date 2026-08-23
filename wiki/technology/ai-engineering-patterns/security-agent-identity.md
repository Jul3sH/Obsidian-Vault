---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Security & Agent Identity

> This article is one entry in the AI engineering patterns catalog: the pattern area covering the threat model unique to LLM agents (prompt injection, tool permissioning, sandboxing, data exfiltration, MCP supply-chain trust) and agent identity (how an autonomous agent authenticates and acts on someone's behalf). It exists as a routing reference: when deciding how to attack a piece of AI work, read "Reach For It When" to tell whether these patterns apply to the job in front of you. Use it to pick a technique and know what it does not cover, then follow the links for depth. It is a breadth catalog entry, not an implementation guide.

## Key Takeaways

- Prompt injection has no reliable single fix. OWASP's own position is that it cannot be fully prevented, so the design goal is limiting what a successful injection can do, not blocking every injection.
- Least-privilege tool scoping plus human approval on irreversible actions is the highest-value pair. Everything else is a supplement.
- Every third-party MCP server is a new trust boundary and a supply-chain dependency, with confirmed real-world attacks (postmark-mcp, Sept 2025) and systemic SDK-level flaws (OX Security, Apr 2026).
- Agent identity is unsettled as of Aug 2026: no ratified standard, only correct composition of existing ones (WIMSE/SPIFFE for the agent, OAuth 2.1 plus token exchange for the delegation).
- The converged production shape is layered rails, not one tool: input validation, dialog rails, output filtering, tool-call gating.

## What It Is

The set of controls that assume the model will be manipulated and the tools it holds will be abused, and that constrain the blast radius anyway. Two halves that are usually treated together: **security** (keeping untrusted content from steering the agent, and keeping a steered agent from doing damage) and **identity** (giving the agent its own verifiable credential and a scoped, delegated authority to act for a user, rather than letting it borrow a human's session token).

## Reach For It When

Apply this pattern area when any of these are true. One trigger is enough.

- **The agent ingests untrusted content.** Web pages, PDFs, emails, issue trackers, third-party API responses. Anything the agent reads that an outsider could have written is an injection channel.
- **The agent holds consequential tools.** Payments, code execution, file or record deletion, outbound email, infrastructure changes. The test is reversibility: if a wrong call cannot be undone cheaply, this area applies.
- **You are adopting a third-party MCP server.** Every external server is a new trust boundary, a new dependency, and a rug-pull risk. No exceptions for popular ones.
- **The agent needs its own credentials.** It runs unattended, on a schedule, or acts across systems where borrowing a user session is wrong or impossible.
- **Output goes somewhere you do not control.** Customer-facing surfaces, published content, anything where a PII leak or unsafe response is a real cost.

Do NOT reach for it when: the data is non-sensitive and single-tenant, no external model call, log, or tool sits between the agent and its output, no third-party servers are involved, and a human inspects the output before it is released or sent anywhere. Read-only does not by itself clear the bar: a read-only agent over trusted-but-sensitive data can still leak PII or secrets through its output, logs, or an external summarisation call. Local scratch work on your own non-sensitive files is not a threat model.

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Instruction/data separation and provenance tagging | Marks untrusted content as data, never as instructions; strips hidden text (zero-width characters, off-screen elements) before it enters context | Any agent processing external documents |
| Least-privilege tool permissioning | Scopes each tool to the minimum capability needed, read-only where write is not required | Always. The single most cited mitigation in 2025-2026 research |
| Human-in-the-loop approval gates | Mandatory confirmation before irreversible or high-impact actions | Payments, deletions, external sends. The backstop for when injection succeeds |
| Sandboxing / process isolation | Runs MCP servers and tool executors in isolated containers with restricted OS privileges | Any locally-run third-party server; contains command-injection and RCE-class flaws |
| Tool description hash-pinning | Freezes an approved tool's description at review time, requires re-approval on change | Defends against MCP rug-pull, where a trusted tool turns malicious in a later version |
| Supply-chain provenance verification | AIBOM, signed components, verified-publisher checks on every MCP dependency | Counters trojanized packages; use before adopting, not after an incident |
| Workload identity (SPIFFE/SVID, WIMSE) | Short-lived, cryptographically verifiable credential for the agent itself, not a shared secret | Answers "who is this agent". SPIFFE/SPIRE are CNCF-graduated and production-proven |
| OAuth 2.1 delegated authorization + token exchange (RFC 8693) | Scoped, narrowed tokens for what the agent may do and on whose behalf | Answers "acting for whom". Authorization is optional in the MCP spec overall (stdio needs none), but a protected HTTP MCP server must follow the OAuth 2.1 resource-server profile since the 2025-06-18 revision. RFC 8693 token exchange is broader delegation practice, not an MCP mandate |
| Cross-App Access / Identity Assertion Authorization Grant | Enterprise brokering of agent delegation across applications | Emerging IETF mechanism; watch, do not bet on it yet |
| Guardrail classifiers | A purpose-trained model classifies input/output against a hazard taxonomy (e.g. Llama Guard 4 12B, multimodal, Apr 2025) | Fast, self-hostable single-verdict content-safety check |
| Programmable guardrail frameworks | Routes requests through configurable input, dialog, retrieval, execution and output rails (e.g. NVIDIA NeMo Guardrails, Apache-2.0, Colang DSL) | When moderation is a multi-check stateful pipeline, not one classification |
| Output-validation libraries | Schema-plus-content validators with auto-correction loops (e.g. Guardrails AI) | When output must satisfy structure and content policy at once |
| Layered guardrail architecture | Input validation, dialog rails, output filtering (PII redaction, hallucination checks), tool-call gating, plus a managed moderation API as a final probabilistic check, mapped to the OWASP LLM Top 10 | The converged 2026 reference architecture. Reach for the architecture, not any single tool |

## Use Cases & Examples

- **Malicious MCP server in the wild.** The `postmark-mcp` npm package shipped fifteen clean versions before 1.0.16 silently BCC'd every processed email to an attacker address. Disclosed by Koi Security, Sept 2025, the first publicly confirmed malicious MCP server. The BCC header was a one-line change, so dependency scanners saw nothing. This is the case for hash-pinning tool descriptions and re-reviewing on version change.
- **Critical flaws in MCP infrastructure itself.** CVE-2025-6514 (CVSS 9.6, JFrog, July 2025) is OS command injection in `mcp-remote`, triggered simply by connecting to an untrusted server. OX Security's April 2026 "Mother of All AI Supply Chains" then reported a by-design command-execution path in Anthropic's official MCP SDKs (Python, TypeScript, Java, Rust), which Anthropic confirmed as intentional behaviour. The lesson is sandboxing: assume the transport layer can be turned against you.
- **Composing agent identity from existing standards.** IETF draft `draft-klrc-aiagent-auth` (first published Mar 2026, at -03 by Jul 2026) composes WIMSE, SPIFFE and OAuth 2.0 into a token carrying both the agent's workload identity and the delegated user. Microsoft (Entra Agent ID), Okta and Auth0 shipped agent-native IAM products over the same period, all converging on OAuth tokens plus agent-to-agent protocols rather than a new primitive.

## Anti-Patterns

- **Treating one filter as the whole defence.** No single control prevents prompt injection across documented variants. Relying on a single classifier or regex layer is a documented failure mode; defence-in-depth is the converging guidance.
- **Auto-approving MCP server updates or tool description changes.** This is exactly the rug-pull path. A tool that was safe at review time is not safe at version N+1 by default.
- **Leaving MCP servers unauthenticated.** A July 2025 Knostic scan found 1,862 publicly reachable MCP instances, none of which required authentication for a `tools/list` request, several with write access to production systems.
- **Keeping persistent agent memory that no requirement asks for.** Every retained turn is persistence surface for a successful injection. Memory should be justified, not default.
- **Trusting a single guardrail classifier at the edges of its training.** Llama Guard 4 scores well on short-form benchmarks (0.961 on HarmBench) but degrades badly on long agentic traces (0.602 F1, 0.516 false-positive rate). A model tuned for short exchanges will fail quietly on a long trace.
- **Mistaking an output-validation library for a security control.** Guardrails AI is built for structural and content conformance; it has a hub prompt-injection validator, but a validator library is one rail, not a security boundary.
- **Believing a vendor's "agent identity standard".** As of Aug 2026 no such standard is ratified, and the IETF's own position is that agents need no new protocol, only correct composition of existing ones. Treat definitive claims sceptically.

## Mental Models

- [[mm-blast-radius]] - the reversibility, least-privilege and approval-gate judgement this whole area is organised around.
- [[mm-routing]] - the checkability question that decides whether an agent gets a tool at all.
- [[mm-verification]] - approval gates and output validation are verification applied at the action boundary.

## State of Practice

As of **Aug 2026**, this area is a live and fast-moving problem, not settled practice. Treat any pre-2025 MCP security guidance as likely outdated.

- **MCP security: acute.** Independent scans put exploitable-flaw exposure in public MCP servers in the 30-82% range depending on class. Endor Labs' analysis of 2,614 implementations found 82% use file operations prone to path traversal, 67% use code-injection-adjacent APIs, and 34% use APIs susceptible to command injection. Note these measure risky-API surface, not confirmed exploits. 14+ CVEs were assigned to MCP implementations by July 2026.
- **Agent identity: immature.** WIMSE is a family of IETF drafts with no finished RFC. SPIFFE/SPIRE (CNCF-graduated) is the mature piece and OAuth 2.1 plus RFC 8693 is the other; the composition on top is draft-stage. Governance frameworks (CSA Agentic Trust Framework, Feb 2026; NIST NCCoE agent identity project) are arriving faster than the protocols they govern.
- **Guardrails: consolidating.** NeMo Guardrails (Apache-2.0) for programmable rails, Llama Guard 4 for self-hosted content classification, Guardrails AI for output conformance, managed moderation APIs as a final check. The maturity is in composing them, not in any one.
- **Contested:** whether observability tooling or the security layer owns tool-call gating in production, and where the boundary sits between content safety and injection defence. Vendor positioning drives much of the disagreement.

## Links

- [[tools-mcp]] - the tool and MCP layer these controls wrap.
- [[evals]] - adversarial testing and red-teaming as scheduled evaluation.
- [[observability]] - runtime detection of what the controls missed.
- [[context-engineering]] - instruction/data separation starts as a context-assembly decision.
- [[memory]] - persistent state is the surface a successful injection uses to survive the session.

---
type: index
created: 2026-05-20
---

# System Design

> *Tools and infrastructure: the architecture of the systems that support the people and processes — system principles, integration design, file conventions, and build standards.*

System Design is split into generic principles and harness-specific implementations:

- **[[generic/_index|Generic System Design]]** — Principles and conventions shared across all harnesses (Claude, Codex, OpenCode, Google CLI). Includes the [[agent-instruction-architecture|Agent Instruction Architecture]]: how `AGENTS.md` and the per-agent wrappers load.
- **[[claude/_index|Claude System Design]]** — Implementation details and integrations specific to the Claude Code harness (memory system, skills, hidden-file mirroring)
- **[[codex/_index|Codex System Design]]** — Implementation details specific to the OpenAI Codex CLI harness (AGENTS.md discovery, config, deltas)
- **[[opencode/_index|OpenCode System Design]]** — Implementation details specific to the OpenCode harness (AGENTS.md discovery, config, deltas)
- **[[google/_index|Google System Design]]** — Implementation details and integrations specific to the Google CLI harness

For the taxonomy that decides what belongs here vs. Service Design, see [[../taxonomy|AI OS Taxonomy]].

**Filing test:**
> Does this describe how the supporting tools are constructed, configured, or maintained?
> - **Yes** → file here in `wiki/ai-os/system-design/`
> - **No, it describes people/process/operations** → file in [[../service-design/_index|Service Design]]
> - **In doubt** → default to Service Design (System Design is the smaller, more specific category)

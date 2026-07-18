---
type: reference
created: 2026-06-29
---

# Codex Plugin (OpenAI) for Claude Code

> A third-party Claude Code plugin that lets Claude hand coding, diagnosis, and
> review work to OpenAI's Codex CLI (GPT-5/Codex models) from inside the Claude
> session. This article documents the plugin and Julian's configuration of it.
> It is **not** a file mirror: the plugin is vendor code, so per the
> [[hidden-file-sync|Hidden File Visibility rule]] only the setup and usage are
> documented here, not the plugin's source files.

## What it is

- A plugin installed from the `openai-codex` marketplace
  (`openai/codex-plugin-cc` on GitHub).
- Plugin name: `codex`, version `1.0.5`.
- Acts as a bridge: Claude stays the primary agent, but can delegate a task or
  request a second opinion to the Codex CLI, which runs locally and returns its
  output verbatim.

## Install & auth state (as of 2026-06-29)

| Item | State |
|------|-------|
| Marketplace | `openai-codex` (`openai/codex-plugin-cc`) added |
| Plugin | `codex@openai-codex` v1.0.5 installed |
| Codex CLI | `@openai/codex` v0.142.4 installed globally via npm |
| Auth | ChatGPT login active (`julianhart@gmail.com`) — no API key needed |
| Stop-review gate | **Off** (see decision below) |
| Runtime | Direct startup; shared runtime starts on first task/review |

Install path (hidden, not mirrored): `~/.claude/plugins/cache/openai-codex/codex/1.0.5/`.

## What the plugin adds

- **Agent:** `codex:codex-rescue` — a thin forwarder subagent that runs a Codex
  task through the shared runtime. Used when Claude is stuck, wants a second
  implementation/diagnosis pass, or should hand off a substantial coding task.
- **Commands:**
  - `/codex:setup` — checks Codex CLI readiness (Node, npm, install, auth) and
    toggles the stop-review gate.
  - `/codex:rescue` — delegates investigation or a fix to the rescue subagent.
    Flags: `--background|--wait`, `--resume|--fresh`, `--model <model|spark>`,
    `--effort <none|minimal|low|medium|high|xhigh>`.
  - `/codex:status` — runtime/job status.
- **Skills (internal):** `codex:codex-cli-runtime`, `codex:codex-result-handling`,
  `codex:gpt-5-4-prompting` — helper contracts for calling the runtime and
  composing GPT-5/Codex prompts.
- **Hooks:** 3, including the stop-review-gate hook (off by default).

## The stop-review gate (and why it's off)

When enabled, a hook fires whenever Claude is about to end a turn. If that turn
made direct code edits, the turn is sent to Codex for an adversarial review.
Codex replies `ALLOW: <reason>` (Claude may stop) or `BLOCK: <reason>` (Claude
keeps fixing). It scopes to the immediately previous turn only and auto-allows
non-code turns (status, summaries, setup output).

**Decision: left off.** This vault's work is almost entirely Markdown (wiki,
planning, Jira sync), which never triggers the gate, so it would add latency and
a Codex call for no benefit. Re-enable with `/codex:setup --enable-review-gate`
if Claude Code is later used on real code projects.

## How to use it

- Hand off a stuck or substantial coding/diagnosis task: `/codex:rescue <what to
  investigate or fix>`.
- Continue the prior Codex thread with `--resume`, or force a clean one with
  `--fresh`.
- Run `/codex:setup` anytime to re-check readiness or toggle the review gate.

## Key Takeaways

- The Codex plugin is a **second-model bridge**: Claude delegates to OpenAI's
  Codex CLI and returns its output verbatim.
- Installed and authenticated (ChatGPT login); ready to use via `/codex:rescue`.
- Stop-review gate is **off** by choice — not useful for a Markdown-only vault.
- Vendor plugin files are **not mirrored** into the wiki; only this configuration
  description is, per the hidden-file rule.

## Related

- [[skill-conventions|Skill Conventions]]
- [[hidden-file-sync|Hidden File Sync Checklist]]
- [[claude/_index|Claude System Design]]

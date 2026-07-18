# ClaudeClaw Business OS - Overview

> Pipes the `claude` CLI to your phone via Telegram. Spawns the real Claude Code binary - every skill, tool, and context from your terminal works from your phone.

**Product family:** ClaudeClaw Business OS (this page) | [[technology/claudeclaw-enterprise-os/_index|ClaudeClaw Enterprise OS]]

---

## Two Editions

| | ClaudeClaw (Public) | ClaudeClaw OS (Members) |
|---|---|---|
| **Access** | Public repo, free | Token-authenticated download, AI Early Adopters members only |
| **Repo** | [Jul3sH/claudeclaw](https://github.com/Jul3sH/claudeclaw) (fork of `earlyaidopters/claudeclaw`) | [Jul3sH/claudeclaw-os](https://github.com/Jul3sH/claudeclaw-os) (private) |
| **Created** | May 2026 | June 2026 |
| **Status** | Older, open-source baseline | Latest version |
| **Distribution** | GitHub fork | Downloaded via token from AI Early Adopters |

The members edition (claudeclaw-os) was obtained by downloading a token-authenticated package from AI Early Adopters. Because it was downloaded rather than forked, GitHub shows no parent repo.

## Versioning and Updates

Versions 1-5 are visible on the AI Early Adopters website. Current install is the latest available. To check for updates: watch the AI Early Adopters community for announcements of v6 or later. There is no `git pull` update path - a new version requires downloading a new package via the same token process.

**What to preserve across updates:**
- `.env` - API keys and config
- `store/claudeclaw.db` - memories and session data
- `~/.claudeclaw/CLAUDE.md` - agent persona

## How It Relates to Claude Code

The two environments run completely independently and share nothing except the Anthropic subscription and the global skills directory.

| | Claude Code (this session) | ClaudeClaw (Telegram bot) |
|---|---|---|
| **Runtime** | Anthropic CLI / IDE harness | Node.js process via launchd |
| **Interface** | CLI / IDE | Telegram |
| **Skills** | `~/.claude/skills/` | Same - auto-loaded from `~/.claude/skills/` |
| **Memory** | Markdown files in `~/.claude/projects/*/memory/` | SQLite (`store/claudeclaw.db`) |
| **Persona** | Project `CLAUDE.md` | `agents/<name>/CLAUDE.md` per agent |
| **Session context** | Current conversation | Per Telegram chat, stored in DB |
| **Shared** | Claude API subscription, `~/.claude/skills/` | same |

Memory, context, and session state do not cross over between environments.

## Related

- [[technology/claude-anthropic/_index|Claude and Anthropic]] - Claude API context
- [[ai-os/skills/_index|AI OS Skills]] - skills shared between both environments
- [[technology/claudeclaw-enterprise-os/_index|ClaudeClaw Enterprise OS]] - enterprise product line

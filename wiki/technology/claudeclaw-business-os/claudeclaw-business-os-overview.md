# ClaudeClaw Business OS - Overview

> Pipes the `claude` CLI to your phone via Telegram. Spawns the real Claude Code binary - every skill, tool, and context from your terminal works from your phone.

**Product family:** ClaudeClaw Business OS (this page) | [[technology/claudeclaw-enterprise-os/_index|ClaudeClaw Enterprise OS]]

---

## Repository Mapping

| Resource | Role |
|---|---|
| `/Users/julianhart/claudeclaw-business-os` | Local Business OS repo checkout |
| `Jul3sH/claudeclaw-business-os` | Private GitHub copy of the local checkout |
| `earlyaidopters/claudeclaw-os` | Upstream source line for the local checkout |
| `Jul3sH/claudeclaw-os` | Old private GitHub copy, pending manual deletion |

The local and private GitHub names now use `claudeclaw-business-os` to distinguish this product line from the placeholder [[technology/claudeclaw-enterprise-os/_index|ClaudeClaw Enterprise OS]] area. The upstream provider source line still uses `claudeclaw-os`.

## Capabilities

On top of the core Telegram-to-`claude`-CLI bridge, ClaudeClaw adds a memory layer, a scheduler, and multi-agent orchestration. The list below is **verified against the local `claudeclaw-business-os` repo** (2026-07-25), not just marketing copy.

| Capability | What it does | Verified in repo |
|---|---|---|
| **Telegram bridge** | Send a message from your phone; it runs the real Claude Code CLI on your Mac and replies. Same skills, tools, files, context as your terminal. | `src/bot.ts` |
| **Persistent memory** | SQLite DB remembers facts, decisions and session state across conversations. | `store/claudeclaw.db` (640 KB) |
| **Scheduled tasks** | Cron-scheduled prompts (e.g. "every Monday 9am"). | `dist/schedule-cli.js`, `scheduled_tasks` table |
| **Multi-agent** | Specialist sub-agents, each its own Telegram bot, with task delegation between them. | `agents/`: comms, content, health, ops, research |
| **Mission Control** | Web dashboard to monitor tasks and agents; async mission-task delegation. | `dist/mission-cli.js`, `web/` |
| **Voice in/out** | Voice notes transcribed to text; spoken audio replies. | `ELEVENLABS_API_KEY`, bot media handling |
| **Video/photo analysis** | Send media from your phone; analysed (Gemini for video). | `GOOGLE_API_KEY` (Gemini) |
| **WhatsApp bridge** | Read and reply to WhatsApp from within Telegram. | `wa_messages` / `wa_outbox` tables |
| **File sending** | Bot sends files back as Telegram attachments via `[SEND_FILE:...]` markers. | bot marker parsing |
| **Security layers** | PIN lock, idle auto-lock, emergency kill phrase, destructive-command confirmation, audit log. | `audit_log` table, `.env` config |

**In one line:** a phone interface + memory layer + scheduling system + multi-agent orchestrator, all running on top of Claude Code.

> Status note (2026-07-25): the **WhatsApp** (`wa_messages`) and **scheduled_tasks** tables currently hold 0 rows. The capabilities are wired in but not yet in active use. Source detail for the feature framing: the "Claude Claw" working doc; this section is the copied-in synthesis (see [[pointer-vs-copy|Pointer vs. Copy]]).

---

## Editions

| | ClaudeClaw (Public) | ClaudeClaw Business OS (Private copy) |
|---|---|---|
| **Access** | Public repo, free | Token-authenticated download, AI Early Adopters members only |
| **Repo** | [Jul3sH/claudeclaw](https://github.com/Jul3sH/claudeclaw) (fork of `earlyaidopters/claudeclaw`) | [Jul3sH/claudeclaw-business-os](https://github.com/Jul3sH/claudeclaw-business-os) (private copy of the `earlyaidopters/claudeclaw-os` source line) |
| **Created** | May 2026 | June 2026 |
| **Status** | Older, open-source baseline | Local private copy of the downloaded members edition |
| **Distribution** | GitHub fork | Downloaded via token from AI Early Adopters |

The members edition was obtained by downloading a token-authenticated package from AI Early Adopters. The local checkout is now named `~/claudeclaw-business-os`; its upstream source line remains `earlyaidopters/claudeclaw-os`.

## Versioning and Updates

Versions 1-5 were visible on the AI Early Adopters website when this page was first written. Treat the available product version as time-sensitive: check the AI Early Adopters community before assuming this local checkout is current. There is no upstream `git pull` update path from the private copy; a provider update may require downloading a new package via the same token process, then preserving local state.

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

- [[claudeclaw-memory-system|ClaudeClaw Memory System]] - how the bot's memory captures, recalls, and injects context
- [[technology/claude-anthropic/_index|Claude and Anthropic]] - Claude API context
- [[ai-os/skills/_index|AI OS Skills]] - skills shared between both environments
- [[technology/claudeclaw-enterprise-os/_index|ClaudeClaw Enterprise OS]] - enterprise product line

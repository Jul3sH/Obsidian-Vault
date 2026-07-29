---
type: reference
created: 2026-07-25
tags: [ai-os, system-design, claudeclaw, agentic-os, comparison]
---

# ClaudeClaw vs. agentic-os

> *Two systems built on Claude Code that solve different problems: a remote-control bridge vs. a self-contained operating system. Open this to understand what each is for and which to reach for. For the skills dimension specifically, see [[skill-scoping-user-vs-project|Skill Scoping]].*

Both run on top of the `claude` CLI, so they are easy to conflate. They are not competitors — they occupy different layers. Verified against both repos on 2026-07-25.

---

## The one-line difference

- **ClaudeClaw** is a **thin bridge** — it exposes your existing Claude Code (skills, tools, context) to your phone via Telegram, and adds a persistence/scheduling/multi-agent layer around it.
- **agentic-os** is a **self-contained operating system** — a folder of files that gives Claude Code the context-management, planning, memory, and isolation layers it lacks out of the box.

ClaudeClaw changes **where** you reach Claude. agentic-os changes **how well** Claude works.

---

## Side by side

| | ClaudeClaw | agentic-os |
|---|---|---|
| **Purpose** | Remote access + persistence for Claude Code | Context-management OS for Claude Code |
| **Primary job** | Phone ↔ terminal parity | Inject the right context at the right time |
| **Interface** | Telegram (+ voice, media, WhatsApp) | The `claude` CLI / IDE, inside the repo |
| **Runtime** | Node.js process via launchd (always-on service) | No separate runtime — it *is* the repo Claude opens |
| **Memory** | SQLite (`store/claudeclaw.db`) | Curated `MEMORY.md` + `.aos.md` logs + PGLite/pgvector store |
| **Skills** | User-level (`~/.claude/skills/`) | Project-level (`<repo>/.claude/skills/`) — see [[skill-scoping-user-vs-project]] |
| **Portability** | Machine-bound service | Travels with the repo (git clone) |
| **Multi-tenant** | Multi-agent bots (comms, ops, research, ...) | Clients/team scoping, per-tenant memory visibility |
| **Distribution** | Token-downloaded package (members) or public fork | Cloneable repo |
| **Self-maintaining** | No — a bridge | Yes — self-registers skills, updates its own docs |

---

## What each adds that Claude Code lacks

**ClaudeClaw adds** (things about *access and persistence*):
- A phone interface (Telegram) to the exact same Claude Code
- Always-on background operation (launchd), so it doesn't need you at the terminal
- Cross-conversation memory (SQLite), scheduling (cron), multi-agent sub-bots, voice/media, WhatsApp, a dashboard

**agentic-os adds** (things about *context quality*):
- Brand/business context injection so outputs sound like you
- Planning against a brief; documented processes as skills
- A real memory layer (curated + semantic recall) beyond Claude Code's weak native recall
- Clean separation of personal / client / team work

---

## They are complementary, not exclusive

The two share nothing but the Anthropic subscription and (for ClaudeClaw) the global skills dir — memory, context, and session state do not cross over. But conceptually they stack:

- **agentic-os** makes a *single, high-context* Claude session excellent inside a repo.
- **ClaudeClaw** makes *any* Claude Code setup reachable from your phone and persistent in the background.

You could run agentic-os in your terminal for deep work and ClaudeClaw for on-the-go access — they address orthogonal gaps (context quality vs. access/persistence).

---

## Which to reach for

- Need Claude **from your phone / away from the desk**, or running **on a schedule / in the background** → **ClaudeClaw**.
- Need Claude to **plan, remember, and stay in-context** across a complex body of work, or to **isolate clients/teams** → **agentic-os**.
- Need both → run both; they don't conflict.

---

## See Also
- [[skill-scoping-user-vs-project|Skill Scoping: User vs. Project]] — the skills dimension in depth
- [[session-transcripts-and-memory|Session Transcripts & the Memory Layer]] — how the memory layers are built
- [[claudeclaw-business-os-overview|ClaudeClaw Business OS Overview]]
- [[pointer-vs-copy|Pointer vs. Copy]]

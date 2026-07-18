# Claude Chat

> *The browser-based interface for conversational use of Claude — no file system access.*

tags: [technical, claude, anthropic]

Claude Chat is the web interface at [claude.ai](https://claude.ai). It's the conversational version of Claude — useful for research, writing, brainstorming, and answering questions, but without direct access to your file system.

---

## Key Differences vs Claude Code

| | Claude Chat | Claude Code |
|---|---|---|
| Access | Browser (claude.ai) | Terminal / desktop app |
| File system | No — you paste or upload content | Yes — reads and writes files directly |
| CLAUDE.md | Not applicable | Loaded automatically from project folder |
| Persistent memory | Projects feature (limited) | Via CLAUDE.md files |
| Best for | Conversations, research, writing | File work, knowledge bases, coding |

---

## Projects Feature

Claude Chat has a **Projects** feature that lets you attach files and give Claude persistent instructions within a project — the browser equivalent of CLAUDE.md. Useful for ongoing conversations that need context.

---

## Memory

Claude Chat now has a memory feature (available to all plan tiers) that creates a persistent synthesis across your conversation history:

- Claude automatically summarises your conversations and updates a synthesis every 24 hours
- This synthesis is passed as context into every new standalone chat — creating continuity without you needing to re-explain yourself
- **Each project has its own separate memory space** — project memory stays focused on that project
- You can view and edit your memory directly: **Settings > Capabilities > View and edit memory**
- You can also tell Claude what to remember mid-conversation and it updates immediately

**Control options:**
- **Pause memory** — keeps existing memory but stops new memories being formed
- **Reset memory** — permanently deletes everything and starts from scratch

---

## Chat Search

Available on paid plans (Pro, Max, Team, Enterprise). Claude can search your previous conversations to find and reference relevant information across sessions:

- Ask naturally: *"What did we discuss about X?"* or *"Can you find our conversation about Y?"*
- Searches appear as tool calls in the conversation
- Works across all standalone chats; project searches are limited to within each project
- Toggle off at **Settings > Capabilities > Search and reference chats**

**Incognito chats** are available on all plans — chats not saved to history and not included in memory or search. Accessed via the ghost icon in the chat header.

---

## Key Takeaways
- Claude Chat is the quickest way to access Claude for one-off questions and conversations
- No file system access — use Claude Code when you need to read or write files
- Memory synthesis provides continuity across sessions without manual re-briefing
- Chat search lets you retrieve context from past conversations — reduces repetition
- Projects have separate memory spaces — useful for keeping context scoped

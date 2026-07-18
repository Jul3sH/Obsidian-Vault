# CLAUDE.md and Memory

> *How Claude remembers instructions across sessions — and how to control what it knows.*

tags: [technical, claude, anthropic]

Claude Code has no persistent memory between sessions by default. `CLAUDE.md` files are the mechanism for giving it persistent instructions. They are plain markdown files that Claude reads automatically at the start of every session.

---

## The CLAUDE.md Hierarchy

Files are loaded **additively** — all applicable files are read and combined. More specific files take precedence when instructions conflict.

| Scope | Location | Loaded when |
|---|---|---|
| **Managed policy** | `/Library/Application Support/ClaudeCode/CLAUDE.md` | Always (admin-set, highest priority) |
| **User / global** | `~/.claude/CLAUDE.md` | Every session, regardless of folder |
| **Project** | `./CLAUDE.md` or `./.claude/CLAUDE.md` | When working inside that folder |
| **Local override** | `./CLAUDE.local.md` | Same as project, but gitignored — personal tweaks |

### How they interact
- All discovered files are **concatenated into context** — not replaced
- Claude walks up the directory tree and loads every CLAUDE.md it finds
- Nested CLAUDE.md files in subdirectories load on demand when Claude reads files there
- `CLAUDE.local.md` is always read after `CLAUDE.md` at each level

---

## Practical Use

- **`~/.claude/CLAUDE.md`** — global personal preferences (tone, location, habits) that apply everywhere
- **Project `CLAUDE.md`** — rules specific to one project (e.g. this knowledge base's librarian rules)
- **`CLAUDE.local.md`** — personal notes or overrides you don't want committed to a shared repo

### This vault's setup
This `Obsidian Vault/CLAUDE.md` contains the full knowledge base librarian rules. When Claude Code is opened inside `Obsidian Vault/`, it loads those rules automatically and knows how to maintain the wiki, compile raw files, and follow the index structure.

When Claude Code is opened in any other folder, it uses only the global `~/.claude/CLAUDE.md` (if it exists) — the vault rules are not active.

---

---

## Memory Files

Beyond `CLAUDE.md`, Claude Code supports a second persistence mechanism: **memory files**. These hold session-learned context — user profile, active project state, corrections — that doesn't belong in the permanent rulebook.

### Where they live

```
~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/
```

**This is a hidden folder outside Obsidian.** It will not appear in the Obsidian vault, in Finder (unless hidden files are enabled), or in any wiki navigation. The only way to see or edit these files is via terminal or Claude Code directly.

### What this means in practice

| Location | What it is | Visible in Obsidian? |
|----------|-----------|----------------------|
| `~/.claude/projects/.../memory/` | Actual runtime memory files | ❌ No — hidden path |
| `wiki/ai-os/system-design/memory/_index.md` | Documentation *about* the memory system | ✅ Yes — wiki article |

The wiki article explains the structure and conventions. The actual files that Claude reads are at the hidden path above.

### How they load

Claude reads memory files at session start, before responding to the first message. This is governed by a rule in the project-level `CLAUDE.md`. Without that rule, memory files are ignored.

### Memory file format

```markdown
---
name: short name
description: one-line summary (used to judge relevance)
type: user | project | epic | feedback
created: YYYY-MM-DD
---

Content here.
```

A `MEMORY.md` index in the same folder lists all active memory files.

---

## Key Takeaways
- `CLAUDE.md` is how you give Claude permanent, session-to-session rules
- Memory files are the learning layer — session-learned corrections and current state
- **Memory files live at a hidden path outside Obsidian** — `~/.claude/projects/.../memory/`
- The wiki article at `wiki/ai-os/system-design/memory/_index.md` documents the convention; it is not the memory itself
- Multiple `CLAUDE.md` files at different scopes are all loaded and combined
- Project-level `CLAUDE.md` only activates when working inside that folder

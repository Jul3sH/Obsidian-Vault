---
type: article
updated: 2026-06-08
---

# Memory Convention

> *How the cross-session memory system works: types, file format, loading rule, and what not to store.*

For how memory is operated at runtime (Store, Inject, Recall), see [[memory-operations|Memory Operations]].

## How It Works

Memory uses **Option 2**: `CLAUDE.md` holds permanent rules; memory files hold session-learned context and pointers. Claude reads both at session start.

**Operational location:** `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/`
(separate from the wiki — these are runtime files, not documentation)

**Loading rule:** declared in `CLAUDE.md`. Claude reads all memory files before responding to the first message of a session.

**This wiki folder documents the structure.** The actual memory content lives at the operational path above.

## Memory Types

| Type | File(s) | Purpose | When updated |
|------|---------|---------|--------------|
| **user** | `user.md` | Who Julian is: role, location, ADHD traits, workstreams, preferences | When new persistent facts about the user emerge |
| **projects** | `projects.md` | Pointer to `wiki/projects/_index.md` + currently active project | When active project changes |
| **deliverables** | `deliverables.md` | Pointer to `wiki/deliverables/_index.md` + current timebox focus | When timebox changes or top-of-queue shifts |
| **feedback** | `feedback-*.md` (multiple) | Corrections that should not be repeated | When Julian corrects Claude's behaviour |

## File Format

Each file has frontmatter:

```markdown
---
name: short memory name
description: one-line summary used to judge relevance
type: user | project | epic | reference | feedback
created: YYYY-MM-DD
---

Content here.
```

## Why This Split (vs. putting everything in CLAUDE.md)

- `CLAUDE.md` stays as the rulebook — permanent structural rules
- Memory files are the learning layer — corrections, current state, pointers
- Feedback files can be retired individually when a pattern is internalised
- Easier to audit "what is permanent vs. what was learned in a session"

## What NOT to Store in Memory

- Code patterns or wiki content (read the source instead)
- Anything already in `CLAUDE.md` (avoid duplication)
- Ephemeral task details from the current session
- Full project lists (memory points to the wiki; wiki holds the data)

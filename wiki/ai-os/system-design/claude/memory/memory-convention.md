---
type: article
updated: 2026-06-08
---

# Memory Convention

> *How the cross-session memory system works: types, file format, loading rule, and what not to store.*

For how memory is operated at runtime here, see [[memory-operations|Memory Operations]]. For the generic four-pillar model (Capture, Storage, Injection, Recall), see [[memory-observation-layer]] and [[memory-semantic-search]].

## How It Works

Memory uses **Option 2**: `CLAUDE.md` holds permanent rules; memory files hold session-learned context and pointers. Claude reads both at session start.

**Operational location:** `~/.claude/projects/-Users-julianhart-Obsidian-Vault/memory/`
(separate from the wiki — these are runtime files, not documentation)

**Loading rule:** declared in `CLAUDE.md`. Claude reads all memory files before responding to the first message of a session.

**This wiki folder documents the structure.** The actual memory content lives at the operational path above.

## Memory Types

Memory holds **three things only**, per `CLAUDE.md`. Everything else belongs in the wiki.

| Type | File(s) | Purpose | When updated |
|------|---------|---------|--------------|
| **user** | `user.md` | Who Julian is: role, location, ADHD traits, workstreams, preferences | When new persistent facts about the user emerge |
| **feedback** | `feedback-*.md` (multiple) | Behavioural corrections that should not be repeated in any future session | When Julian corrects Claude's behaviour |
| **hard rule** | e.g. `project-dad-inheritance.md` | A standing rule where getting it wrong risks real legal, financial or relational harm. Rare; must justify why memory rather than the wiki | When the underlying situation materially changes |

**Retired types.** `projects.md` and `deliverables.md` were removed. Project and deliverable state lives in the wiki (`wiki/projects/`, `wiki/deliverables/`) and is read on demand, not carried in memory.

## File Format

Each file has frontmatter:

```markdown
---
name: short memory name
description: one-line summary used to judge relevance
type: user | feedback
created: YYYY-MM-DD
---

Content here.
```

## Why This Split (vs. putting everything in CLAUDE.md)

- `CLAUDE.md` stays as the rulebook — permanent structural rules
- Memory files are the learning layer — corrections, current state, pointers
- Feedback files can be retired individually when a pattern is internalised
- Easier to audit "what is permanent vs. what was learned in a session"

## The Positive Definition: Two Branches of Storage

The rules below say what memory excludes. The positive framing, which decides the
question rather than fencing it:

| | **Canonical layer** (the wiki) | **Behavioural layer** (memory files) |
|---|---|---|
| Question it answers | **"Is this true?"** | **"Does this change how I act?"** |
| Content | Decisions, evidence, domain knowledge | Profile, standing behavioural corrections |
| Volume here | 528 files | 13 files |
| Loading | Recall, on demand | Index injected, bodies on demand |

**The test:** a fact about the world goes in the wiki however important it is. A rule
about behaviour goes in memory however trivial it is. Importance does not decide;
the kind of claim does.

Both are branches of the **Storage** pillar, not different categories. Full derivation:
[[memory-observation-layer]].

## What NOT to Store in Memory

- Code patterns or wiki content (read the source instead)
- Anything already in `CLAUDE.md` (avoid duplication)
- Ephemeral task details from the current session
- Full project lists (memory points to the wiki; wiki holds the data)

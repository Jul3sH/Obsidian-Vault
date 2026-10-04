---
type: reference
created: 2026-10-03
tags: [technical, claude, anthropic, steering, rules]
review: feature
review-start: 2026-10-03
---

# Claude Code Path-Scoped Rules

## Purpose

What a path-scoped rule is and how to write one, for anyone using Claude Code. It exists because [[mm-steering]] names the path-scoped rule as the mechanism for a constraint that binds only certain paths.

As of 3 Oct 2026 this vault has no rules: neither `.claude/rules/` nor `~/.claude/rules/` exists, and all rules sit in `AGENTS.md` and `CLAUDE.md`.

## Key Takeaways

- A rule is an ordinary markdown file in `.claude/rules/`, with a `paths:` list of glob patterns in its frontmatter.
- It loads only when Claude reads a file matching one of its patterns, so it costs no context during unrelated work.
- Without `paths:`, a rule loads every session, with the same priority as `.claude/CLAUDE.md`.
- It is still an instruction, not a guarantee. Must-happen behaviour needs a [[claude-code-hooks|hook]].

## Key Concepts

### Where rules live

| Level | Folder | Applies to |
|---|---|---|
| Project | `.claude/rules/` | That project only |
| User | `~/.claude/rules/` | Every project |

`rules` is a folder, not a file: it holds one `.md` file per rule, named for the reader (the name means nothing to Claude). Subfolders are discovered recursively, so `rules/career/tti.md` works. Symlinks are supported; a symlink pointing outside the project needs approval.

### Syntax

```markdown
---
paths:
  - "wiki/deliverables/**/*.md"
---

# Deliverable files

- Every deliverable must have a `## Prompt Zero` section before work starts.
```

The frontmatter holds the patterns; the body is plain markdown, written exactly as the same rule would be in `CLAUDE.md`. `paths` also accepts a single comma-separated string.

| Pattern | Matches |
|---|---|
| `wiki/career/**/*.md` | Any `.md` file at any depth under `wiki/career/` |
| `wiki/career/*.md` | `.md` files directly in `wiki/career/`, not its subfolders |
| `**/_index.md` | Every `_index.md` in the project |
| `**/*.{md,csv}` | Every `.md` and `.csv` file (brace expansion) |

`**` is any number of folders, `*` is anything within one name, `{a,b}` is either. Bracket expressions (`[abc]`) also work; escape a literal bracket as `\[`.

### Rule versus subdirectory CLAUDE.md

Both load on demand when Claude reads a matching file, and both are instructions. They differ in how scope is set:

| | Subdirectory `CLAUDE.md` | Path-scoped rule |
|---|---|---|
| Scope set by | Where the file sits: that folder and its subtree | Glob patterns |
| Can target | One subtree | Any pattern, including file types across folders |
| Lives | Inside the content folder | Centrally, in `.claude/rules/` |

## Guidelines

- Use a rule when a constraint follows a **kind of file** (all logs, all index files) or when you want scoped constraints reviewable in one place. Use a subdirectory `CLAUDE.md` when guidance belongs to one folder and should sit visibly beside it.
- Move place-bound sections out of the always-loaded file into rules: they stop costing context on every turn.
- Quote glob patterns in the YAML list; unquoted `*` can be misread.
- In an Obsidian vault, prefer rules over subdirectory `CLAUDE.md` files: `.claude/` is a dot-folder Obsidian ignores, whereas a `CLAUDE.md` in a normal folder is indexed as a note.

## Limitations

- **An instruction, not a guarantee.** Loading the rule does not make Claude follow it.
- **Loads on read.** A rule cannot fire on a file Claude never opens, so it cannot govern a file Claude is about to create in an empty pattern.
- **Claude Code only.** Other agents reading `AGENTS.md` do not see `.claude/rules/`, so moving a universal rule there trades portability for context savings.
- Harness-specific and perishable, as of 3 Oct 2026.

## Detail

Source: [Claude Code memory docs](https://code.claude.com/docs/en/memory.md) (Anthropic), sections on `.claude/rules/` and path-specific rules. Companions: [[mm-steering]] (why scoped constraints load on demand), [[claude-md-and-memory]] (the always-loaded layer), [[claude-code-hooks]] (when an instruction is not enough).

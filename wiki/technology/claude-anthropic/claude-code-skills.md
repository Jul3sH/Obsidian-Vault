---
type: reference
created: 2026-10-03
tags: [technical, claude, anthropic, steering, skills]
review: feature
review-start: 2026-10-04
---

# Claude Code Skills

## Purpose

What a skill is, how it loads, and what survives a compaction, for anyone using Claude Code. It exists because [[mm-steering]] names the skill as the mechanism for a procedure run the same way each time.

This setup's own skills, and the rule that each is mirrored in the wiki, are documented under [[ai-os/skills/_index|AI OS skills]]; [[claude-cowork]] covers skills alongside hooks, plugins and MCP.

## Key Takeaways

- A skill is a folder with a `SKILL.md`. Its description is in context every turn; its body loads only when the skill is invoked.
- Claude can invoke a skill on its own when the description matches, or you can call it with `/skill-name`.
- After a compaction, invoked skills are re-attached, but only the first 5,000 tokens each, within a shared 25,000-token budget.
- Keep the description sharp (it is what triggers the skill) and front-load the body (the start is what survives).

## Key Concepts

### Structure

```
my-skill/
├── SKILL.md        (required: frontmatter + instructions)
├── reference.md    (optional supporting files)
└── scripts/        (optional)
```

`SKILL.md` frontmatter:

| Field | Does |
|---|---|
| `name` | The command name; defaults to the folder name |
| `description` | When Claude should use it; always in context; truncated at 1,536 characters |
| `disable-model-invocation` | `true`: only you can invoke it, by slash command |
| `user-invocable` | `false`: hidden from the slash menu |
| `allowed-tools` | Tools pre-approved while the skill runs |
| `context` | `fork` runs it in an isolated subagent context |
| `paths` | Glob patterns limiting when it activates |

### How it loads

| Moment | In context |
|---|---|
| Every turn | The description only |
| On invocation | The full body, which stays for the rest of the session |
| After a compaction | First 5,000 tokens per invoked skill, shared 25,000-token budget filled from the most recently invoked; older skills can be dropped entirely |

## Guidelines

- A procedure in `CLAUDE.md` belongs in a skill: it then costs only its description until needed.
- Write the description as trigger situations, not a summary: it is the only part Claude sees when deciding.
- Put the rules that must survive a long session in the first 5,000 tokens of the body.
- If a skill's rules must hold all session regardless, a skill alone is not enough: re-inject with a `SessionStart` hook matching `compact`, or move the rule to an always-loaded file ([[mm-steering]] worked example).

## Limitations

- **An instruction, not a guarantee**, and invocation itself is a judgement Claude makes from the description, so a skill can fail to fire.
- **Partial survival.** Long skill bodies are cut on compaction and older skills can drop out of the budget.
- Harness-specific and perishable, as of 3 Oct 2026.

## Detail

Source: [Claude Code skills docs](https://code.claude.com/docs/en/skills.md) (Anthropic). Companions: [[mm-steering]], [[claude-cowork]], [[claude-code-subagents]] (what `context: fork` runs in).

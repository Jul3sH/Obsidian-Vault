---
type: reference
created: 2026-10-03
tags: [technical, claude, anthropic, steering, output-styles]
review: feature
review-start: 2026-10-03
---

# Claude Code Output Styles

## Purpose

What an output style is, how it differs from `CLAUDE.md`, and when to use one, for anyone using Claude Code. It exists because [[mm-steering]] names the output style as the mechanism for a different identity, and because on 3 Oct 2026 Julian asked whether a style, rather than more rules, was the fix for Opus 5.1 being verbose and jargon-heavy. As of that date no output style is set anywhere in this setup.

## Key Takeaways

- An output style changes the **system prompt**. `CLAUDE.md` arrives as a **user message after** the system prompt. That is the core difference.
- A custom style drops Claude Code's built-in engineering instructions unless it sets `keep-coding-instructions: true`.
- Built-in styles exist, including **Concise**, and keep the engineering instructions.
- Styles apply to the main conversation only. Subagents never get them.

## Key Concepts

### What a style changes

Claude Code sends the active style's instructions with every request, as part of the system prompt. A **custom** style leaves out the built-in software-engineering instructions by default; `keep-coding-instructions: true` keeps them, so the style adds to the default rather than replacing it. **Built-in** styles always keep them and add their own.

Built-in styles: Default, Proactive, Concise, Explanatory, Learning.

### Where styles live and syntax

| Level | Folder |
|---|---|
| User | `~/.claude/output-styles/` |
| Project | `.claude/output-styles/` |

```markdown
---
name: Plain
description: Short answers in plain English
keep-coding-instructions: true
---

Lead with the answer. Use plain English; if a technical term is unavoidable,
explain it in one line. Keep it short.
```

Frontmatter fields (all optional): `name`, `description`, `keep-coding-instructions`, and `force-for-plugin` (auto-applies a plugin's style when the plugin is enabled). Select a style with `/output-style <name>`, through `/config`, or with the `outputStyle` key in a settings file (the VS Code extension and desktop app also have a picker).

### Style versus CLAUDE.md versus appending

| Mechanism | Delivered as | Docs' intended use |
|---|---|---|
| Output style | Part of the system prompt | Response format, tone, voice |
| `CLAUDE.md` | User message after the system prompt | Project knowledge and rules |
| `--append-system-prompt` | Added to the system prompt for one run | One-off additions |

## Guidelines

- For tone and length (verbosity, jargon), a style with `keep-coding-instructions: true` is a reasonable first fix: it sits in the system prompt and costs nothing in engineering behaviour. **Inference, not documented:** the docs do not rank a style above `CLAUDE.md`; the case rests on position (system prompt versus user message) and should be tested, not assumed.
- Try the built-in **Concise** style before writing a custom one.
- Keep cross-agent style rules in `AGENTS.md` as well: a style is Claude Code only.
- Reserve a style with `keep-coding-instructions` unset for genuine role changes, where losing the engineering instructions is the point.
- If a style is a hidden file outside the vault, it needs a wiki mirror (AGENTS.md Hidden File Visibility).

## Limitations

- **An instruction, not a guarantee.** A style is followed probabilistically like any instruction.
- **Does not reach subagents.** There is no agent frontmatter field to assign a style; write style lines into each agent's body instead ([[claude-code-subagents]]). A fork is the exception and inherits the main context.
- **Cannot change capability.** Some verbosity is the model's own habit; model choice is a separate dial ([[mm-steering]]).
- Harness-specific and perishable, as of 3 Oct 2026.

## Detail

Source: [Claude Code output styles docs](https://code.claude.com/docs/en/output-styles.md) and [memory docs](https://code.claude.com/docs/en/memory.md) (how `CLAUDE.md` is delivered) (Anthropic). Companions: [[mm-steering]], [[claude-md-and-memory]], [[claude-code-subagents]].

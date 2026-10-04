---
type: reference
created: 2026-10-03
tags: [technical, claude, anthropic, steering, subagents]
review: feature
review-start: 2026-10-03
---

# Claude Code Subagents

## Purpose

What a subagent is, what it does and does not inherit, and how to define a custom one, for anyone using Claude Code. It exists because [[mm-steering]] names the subagent as the mechanism for an isolated side task, and because routing's "several agents" verdict ([[mm-routing]]) is built from them.

As of 3 Oct 2026 this setup uses only built-in subagents: no `.claude/agents/` folder exists.

## Key Takeaways

- A subagent starts fresh: its own system prompt, its own context. Only its final message comes back to the main session.
- It reads `CLAUDE.md` files by default, but never gets the main session's output style, system prompt or conversation.
- A custom agent is one `.md` file in `.claude/agents/`; its body **is** its system prompt.
- Steer a subagent through its own definition, not through the parent conversation.

## Key Concepts

### What a subagent gets

| Gets at start | Does not get |
|---|---|
| Its own system prompt (the definition body) | The main session's system prompt |
| The task message it was launched with | The main session's output style |
| `CLAUDE.md` files, unless `omitClaudeMd: true` | The conversation history |
| Git status, preloaded skills, managed policy files | Auto memory |

Exception: a **fork** inherits the main context, output style included.

### Defining a custom agent

```markdown
---
name: researcher
description: Researches a question and writes a short briefing
tools: Read, Grep, WebSearch
model: sonnet
---

You research a question and report back. Write in plain English, lead with
the answer, keep it short.
```

Required frontmatter: `name`, `description` (the description is what the main session reads to decide when to use the agent). Optional fields include `tools`, `disallowedTools`, `model`, `effort`, `maxTurns`, `skills`, `mcpServers`, `hooks`, `memory`, `background`, `isolation`, `omitClaudeMd`, `permissionMode`, `color`, `initialPrompt` and `experimental`. There is no field to assign an output style.

## Guidelines

- Use a subagent when you want the result, not the middle: a long search, a read across many files, an independent check.
- Put style instructions in the agent's body. For one style everywhere, keep a canonical style paragraph in the wiki and copy it verbatim into each agent and the [[claude-code-output-styles|output style]], so the copies cannot drift unnoticed.
- Write the launch prompt as a full brief: the subagent has none of the conversation, so anything not in the prompt, the definition or `CLAUDE.md` does not exist for it.
- Treat a subagent's report as unverified output ([[mm-verification]]): isolation means you did not see how it got there.

## Limitations

- **Isolation cuts both ways.** The subagent cannot see your context, and you cannot see its working.
- **Steering does not follow it.** Anything set only in the main conversation (style, ad-hoc instructions) stops at the boundary.
- Harness-specific and perishable, as of 3 Oct 2026.

## Detail

Source: [Claude Code subagents docs](https://code.claude.com/docs/en/sub-agents.md) (Anthropic). Companions: [[mm-steering]] (isolation as a mechanism), [[mm-routing]] (when several agents is the right verdict), [[claude-code-output-styles]].

---
type: reference
created: 2026-08-17
status: active
tags: [technical, claude, anthropic, context, tokens]
---

# Session Context Loading

> *What actually occupies Claude Code's context window: what assembles at session start, what accumulates as you work, and which parts load lazily. Open this when you want to know why a session is large, what a skill invocation really costs, or what "auto-loaded" does and does not include. The cost consequences and what to do about them are the separate concern of [[mm-token-economics]].*

A Claude Code session's context has two parts that behave completely differently:

| Part | Assembled | Size behaviour | Contains |
|---|---|---|---|
| **Fixed prefix** | Once, at session start | Roughly constant | System prompt, instruction files, memory index, tool and skill declarations |
| **Transcript** | Continuously | Only grows | Every message, tool call, tool result, and file read |

The prefix is bounded and re-sent unchanged each turn. The transcript is unbounded and re-sent in full each turn. Almost everything surprising about session size comes from the second one.

---

## What assembles at session start

Observed in a Claude Code session on **17 Aug 2026**. Composition is harness-version-specific and will drift; the *categories* are stable, the details are not.

| Component | Loaded | Notes |
|---|---|---|
| **Harness system prompt** | Always | Written by Claude Code, not by you. Carries identity, tool-use rules, and **environment info** (working directory, platform, git status, model). Environment info is part of this, not a separate item |
| **`CLAUDE.md`** | Always | Project file. `@path` imports are expanded inline - see [[claude-md-and-memory]] for the full hierarchy |
| **Imported files** | Always | Anything pulled through an `@import`, in full. An import is not a pointer; it is a paste |
| **Memory index** | Always (if memory is in use) | The index only. Individual memory files are read on demand |
| **Tool schemas** | Always | Full JSON schemas for the always-available tools |
| **Deferred tool names** | Always | **Names only**, no schemas. Schemas fetch on demand |
| **Skill declarations** | Always | Name plus a one-line trigger description per skill. **Bodies do not load** until invoked |
| **MCP surface** | Always | Server instructions plus connected tool names |
| **Subagent definitions** | Always | Each agent type's name, description, and tool access |
| **Hook output** | On trigger | E.g. a `SessionStart` hook injecting text into the first turn |

---

## Progressive disclosure: the mechanism that makes this affordable

The single most important behaviour here is that **breadth is declared eagerly and depth is loaded lazily**.

| Surface | Loads at start | Loads on use |
|---|---|---|
| Deferred tools | Name | Full input schema |
| Skills | Name + one-line description | The entire skill body, including references |
| Memory | Index line per file | The memory file's contents |
| Wiki | Nothing | The file, when read |

This is why a session can carry dozens of tools and dozens of skills without them dominating the prefix. Two consequences follow:

- **Adding capability is nearly free.** Registering another skill costs one description line. There is no reason to be frugal about *having* skills.
- **Using capability is not, and the cost is irreversible.** Invoking a large skill pastes its full body into the transcript, where it stays for the rest of the session. The expense lands at the moment you were thinking about the question rather than the bill.

---

## What is *not* auto-loaded

- **Wiki files.** No agent auto-loads them; they enter context only when read. This is the constraint that [[agent-instruction-architecture]] is built around - an always-on rule cannot live only in the wiki.
- **Memory file contents.** The index is loaded; the files behind it are not. A rule saying "read `user.md` at session start" is an *instruction to make a tool call*, not an automatic load, and it costs a turn.
- **Skill bodies**, until invoked.
- **Deferred tool schemas**, until fetched.

---

## What happens on each turn

The API is **stateless**. Nothing persists server-side between turns, so the entire prefix plus the entire transcript is re-sent every single time. Turn thirty sends everything from turn one.

Prompt caching is what makes this viable rather than ruinous: the unchanged leading portion is cached and re-read at a large discount. Two properties matter:

- **It is a prefix match.** Caching runs from the start of the prompt up to a breakpoint, so anything that changes early invalidates everything after it.
- **It is per-model.** Cache entries are scoped to a model, so switching models discards the discount entirely.

Entries also expire, so a long pause can cost the discount even with no other change.

---

## What grows the transcript irreversibly

Anything in this list is permanent for the session:

- File reads, including large ones read in full
- Tool results, including verbose command output
- Skill bodies, on invocation
- Fetched tool schemas
- Every message in both directions

Subagents are the exception and the escape hatch: a subagent runs with its **own** context and returns only its final report, so the material it reads never enters the parent transcript.

## Key Takeaways

- Context splits into a fixed prefix (bounded, re-sent unchanged) and a transcript (unbounded, re-sent in full). Only the transcript compounds.
- Harnesses declare breadth eagerly and load depth lazily: names and descriptions at start, schemas and skill bodies on use.
- Having a large capability surface is cheap; reaching into it is not, and the deposit is permanent for the session.
- "Auto-loaded" covers instruction files and declarations. It does not cover wiki files, memory file contents, or skill bodies.
- The API is stateless, so every turn re-sends everything; caching discounts that re-read but is prefix-shaped and per-model.

## See Also

- [[mm-token-economics]] - the operator-side model: what this costs and which habits move the number
- [[claude-md-and-memory]] - the `CLAUDE.md` hierarchy and the native memory concepts
- [[agent-instruction-architecture]] - where an operating rule should live, and why always-on rules cannot sit in the wiki
- [[session-transcripts-and-memory]] - how the transcript is persisted to disk after the fact
- [[claude-code]] - general Claude Code overview

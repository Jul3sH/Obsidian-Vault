---
type: reference
created: 2026-06-27
tags: [ai-os, system-design, multi-agent, agents-md, claude-md]
---

# Agent Instruction Architecture

> *How operating rules are layered so the same vault drives Claude Code, Codex, and OpenCode from one source of truth, with no duplicated rules and no bidirectional sync. Open this when deciding where a new operating rule belongs, or when adding a new agent.*

The vault is used by more than one coding agent. The risk that creates is **drift**: the same universal rule copied into `CLAUDE.md` and a Codex/OpenCode file, then edited in one place and not the other. This architecture removes that risk by giving every rule exactly one home, chosen by *who needs it*, not *which agent runs*.

---

## The core constraint (why "thin pointer" wrappers do not work)

An agent only reliably obeys a rule if that rule is in its **auto-loaded** context. Each agent auto-loads a specific file:

| Agent | Auto-loads | Notes |
|-------|-----------|-------|
| Claude Code | `CLAUDE.md` | Supports `@path` imports, which are expanded into context |
| Codex | `AGENTS.md` | Does not expand imports; rules must be physically present |
| OpenCode | `AGENTS.md` | Same |

A wiki file is **never** auto-loaded by any agent (it is read on demand). So a rule that must hold every turn cannot be demoted to "see `wiki/.../style.md`": the agent would have to choose to go read it, and Codex/OpenCode will not. **Always-on rules must physically live in an auto-loaded file.** This is the constraint the whole design is built around.

---

## The three layers

| Layer | File(s) | Loaded | Holds |
|-------|---------|--------|-------|
| 1. Canonical universal rules | `AGENTS.md` (vault root) | Every session, every agent | All agent-agnostic always-on rules: writing style, knowledge base rules, wiki index structure, index-navigation doctrine, folder/linking conventions, Cold Email TCO rules, operations log |
| 2. Agent wrappers | `CLAUDE.md` (and any future Codex/OpenCode-only file) | Every session of that agent | Only that agent's loading-model-specific mechanics |
| 3. Deep doctrine | `wiki/ai-os/` | On demand | Rationale, audit trail, full conventions. Layers 1-2 *point* here; they do not duplicate it |

### How the layers connect

- **Claude Code** auto-loads `CLAUDE.md`, which begins with `@AGENTS.md`. Claude expands that import, so it gets the full canonical layer plus its own Claude-only section. One physical copy of the universal rules.
- **Codex / OpenCode** auto-load `AGENTS.md` natively. They get the canonical layer directly. (When either needs agent-specific behaviour, give it its own wrapper that restates only the pointer to `AGENTS.md` plus its deltas, mirroring how `CLAUDE.md` works.)
- **Deep doctrine** stays in `wiki/ai-os/`. Both `AGENTS.md` and the wrappers reference it by path; neither copies it. The relationship is one-directional, so nothing drifts.

```
            AGENTS.md  (canonical universal rules, vault root)
           /          \
   @import /            \ native auto-load
          /              \
   CLAUDE.md          AGENTS.md consumers
   (+ Claude deltas)  (Codex, OpenCode)
          \              /
           \            /  read on demand (pointers only)
            \          /
             wiki/ai-os/  (deep doctrine, source of truth for rationale)
```

---

## How loading works, per agent

Each agent auto-loads one entry file and reaches the rest from there. The universal rules are sourced once, from `AGENTS.md`:

- **Claude Code:** auto-loads `CLAUDE.md`, which begins with `@AGENTS.md`. Claude expands that import inline, so it gets the full canonical layer plus its Claude-only sections. `CLAUDE.md` is the door; `AGENTS.md` is pulled through it. Claude does not load `AGENTS.md` as an independent file.
- **Codex:** auto-loads `AGENTS.md` directly, walking from the git/project root down to the working directory. It never reads `CLAUDE.md`.
- **OpenCode:** auto-loads `AGENTS.md` directly. If both `AGENTS.md` and `CLAUDE.md` are present, it uses only `AGENTS.md`.

All three run on the same universal rules, edited once in `AGENTS.md`.

### Two streams load at session start, do not confuse them

| Stream | What it is | Auto-loaded every session? | Where it lives |
|--------|-----------|---------------------------|----------------|
| **Instructions** | The operating rules (how to work) | Yes | `AGENTS.md` (+ `CLAUDE.md` for Claude) |
| **Profile / memory** | Facts about Julian and stable preferences (who he is); plus topic-specific memories | The always-on profile: yes. Topic memories: on demand | Shared profile in `AGENTS.md`; Claude-private topic memories in the Claude memory store |
| **Wiki** | Deep doctrine and content | No | Read only when relevant |

A rule about *how to work* is an instruction; a fact about *who Julian is* is profile. Both are always-on and cross-agent, so both belong in `AGENTS.md`. The wiki is never auto-loaded by any agent.

---

## Where does new content go? (the decision rule)

1. **Is it an always-on rule that must hold every turn, for any agent?**
   Put it in `AGENTS.md`.
2. **Is it always-on but exists only because of one agent's loading model, memory system, or skill mechanism?**
   Put it in that agent's wrapper (`CLAUDE.md` for Claude).
3. **Is it rationale, audit trail, or a full convention read on demand?**
   Put it in `wiki/ai-os/`, and add a one-line pointer from `AGENTS.md` or the wrapper if an agent must know it exists.

If in doubt, prefer `AGENTS.md` over a wrapper: universal-by-default keeps the wrappers thin and the rules shared.

### What is Claude-specific (stays in `CLAUDE.md`)

- The memory system (session-start `user.md` load, `feedback-*` files, write-confirmation rule)
- The AI OS skills rule and the skills-documented list
- The hidden-file mirroring rule (`~/.claude/` to wiki)
- Skill shared-infrastructure notes and the Hong Kong VPN environment notes

These all depend on Claude Code mechanisms that Codex and OpenCode do not share.

---

## Adding a new agent

1. Confirm the agent auto-loads `AGENTS.md` (Codex and OpenCode do). If so, it inherits the full canonical layer with no further work.
2. If the agent needs agent-specific mechanics, create a minimal wrapper for it that points to `AGENTS.md` and holds only its deltas. Do **not** copy universal rules into it.
3. If the agent supports an import mechanism (as Claude Code does), use it to pull `AGENTS.md` rather than restating its contents.

---

## Key Takeaways

- `AGENTS.md` is the single physical home of every agent-agnostic always-on rule. Edit a universal rule once, there.
- Wrappers (`CLAUDE.md`, future Codex/OpenCode files) are thin: a pointer/import to `AGENTS.md` plus that agent's own mechanics only.
- The wiki (`wiki/ai-os/`) remains the source of truth for deep doctrine and rationale; the always-on layers point to it and never duplicate it.
- Always-on rules cannot live only in the wiki, because no agent auto-loads wiki files. This is why `AGENTS.md` exists rather than thin pointers.
- One-directional relationships only (`CLAUDE.md` imports `AGENTS.md`; everything points down into the wiki), so there is no bidirectional sync to maintain.

## Related

- [[system-design-principles|System Design Principles]] - the working-memory model this refines
- [[documentation-conventions|Documentation Conventions]] - how the wiki content the layers point to is written and structured

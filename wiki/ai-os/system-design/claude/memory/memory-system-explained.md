---
type: reference
created: 2026-07-23
---

# Memory System Explained (Plain-Language / Ownership View)

> *A learner-facing explainer of how Claude's cross-session memory works and, crucially, who controls it. Complements the technical [[memory-convention]] and [[memory-operations]] docs, which specify the mechanism; this doc answers "what is this, and is it mine?"*

Written after a session where Julian saw Claude cite a rule (`feedback-overanalysis-check`) and asked what it was, where it was defined, and who decides when memories get created.

## The behaviour that prompted this

Claude referenced a rule called `feedback-overanalysis-check`. The questions it raised:

1. Is it a skill or a task I created?
2. Is it defined in AGENTS.md and imported into every session so Claude always knows it?
3. Is it Claude deciding when these get created?
4. Is this a system I ultimately defined myself?
5. Are the rules in AGENTS.md (imported) or just in CLAUDE.md?

## What a memory actually is

- **Not a skill, not a task.** It's a **memory file** — specifically a *feedback* memory: a behavioural correction that changes how Claude works in **every** future session.
- Example content (`feedback-overanalysis-check`): before Claude starts large analytical work (risk registers, scoring matrices, big spreadsheets), it must pause and ask *"do you need this level of detail, or is this overanalysis?"*
- **Origin is human, not algorithmic.** It was created 2026-07-16 after Claude built a 27-row × 16-column benefits register that was more detail than the decision needed. Julian said "make this a trigger"; Claude proposed it; Julian said "yes"; Claude wrote the file. The whole chain: *my instruction → Claude's proposal → my approval → a Write tool call.*

## Three things, three homes (don't confuse them)

| Thing | What it is | Where it lives |
|-------|-----------|----------------|
| **Skill** | A capability Claude can invoke (`/project-planner`) | `~/.claude/skills/` |
| **Task / deliverable** | A unit of *my* work | `wiki/deliverables/` |
| **Memory** | A standing rule about how Claude behaves toward me | `~/.claude/projects/.../memory/` (mirrored into the wiki so I can see it) |

## Where the rules are defined (the key answer)

- The memory rules are in **CLAUDE.md only** — **not** in AGENTS.md.
- **AGENTS.md** = universal rules, true for any agent (Codex, OpenCode, Claude). Imported into CLAUDE.md via the line `@AGENTS.md`.
- **CLAUDE.md** = Claude-specific mechanics. Memory is Claude-specific (other agents don't have it), so it stays here. The `# Memory` section sits *after* the AGENTS.md import, written directly in CLAUDE.md.
- **The test that decides where a rule goes** (from CLAUDE.md's own header): *"if the rule is universal, put it in AGENTS.md. If it exists only because of Claude Code's memory, skills, or hidden-path mirroring, keep it here."*
- **Caveat:** one *related* rule IS universal and lives in AGENTS.md — **Hidden File Visibility** (mirror hidden files into the wiki so I can see them). That governs *mirroring*, not the memory logic itself.

## How Claude stays aware of memories across sessions

- `user.md` (my profile) is loaded **in full** at the start of every session.
- `MEMORY.md` is an **index** — a table listing every memory file + a one-line description. The index loads every session, so Claude always *knows the memory exists*.
- The full **body** of each memory loads **on demand**, only when relevant.
- Net effect: **"index always on, bodies just-in-time."** Claude won't forget a memory exists, but doesn't carry every memory's full text into every session.

## Who decides when a memory gets created (the authority split)

- **Two-key system:** Claude **notices and proposes** (its key); I **approve** before it's written (my key). Default rule: *"confirm before writing any new memory file... wait for agreement."*
- **One exception:** if I explicitly flag a wrong behaviour, Claude captures the correction immediately — but still tells me it did.
- Claude can **miss** candidates (I can force one with "remember this") and can **over-propose** (the confirm gate is my filter against memory bloat). Claude **cannot** decide something is important enough to bypass my approval.

## Key Takeaways

- A memory is a **standing rule about how Claude treats me**, executed by Claude but owned by me — not a skill and not a task.
- The rules live in **CLAUDE.md** (Claude-specific), not AGENTS.md (universal). The `@AGENTS.md` import pulls in universal rules; memory sits after it.
- **Index always loaded, bodies on demand** — Claude always knows a memory exists, loads the detail when relevant.
- Memories are created by a **two-key process**: Claude proposes, I approve. The only unilateral case is capturing a correction I've just flagged.
- **It's my system.** Defined in files I own (CLAUDE.md, AGENTS.md), indexed where I can see it (MEMORY.md), and every entry mirrored into the wiki. Nothing is baked into the model — delete the `# Memory` block and the scheme stops. Claude operates it; I define it.
- Related: [[memory-convention]], [[memory-operations]], [[hidden-file-sync]]

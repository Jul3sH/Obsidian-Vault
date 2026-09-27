---
name: feedback-delegate-execution-to-subagents
description: "Main thread thinks, briefs and verifies; the actual execution (multi-file edits, restructures, sheet work, bulk repointing) goes to subagents"
metadata:
  node_type: memory
  type: feedback
  created: 2026-09-27
---

**Correction (27 Sep 2026, UK relocation companion restructure):** I ran a multi-file restructure (move sections between two wiki notes, rename a file, repoint ten inbound links, rewrite indexes and the project surface) inline in the main thread. Julian: *"You should be using sub agents for the actual work."*

**Why it matters:** the main thread is the expensive, context-heavy surface. Doing execution there burns its tokens (this session reached 1.1M effort tokens), bloats the context that later reasoning has to carry, and repeats the pattern Julian flagged on 26 Sep when Codex did the heavy lifting while the thinking sat in the $100 Claude thread. He wants the split the other way round: cheap execution, expensive judgement.

**How to apply:**
- Main thread: decide, write the exact brief (files, anchors, target text, done-criteria), then verify the result by reading it back.
- Subagent: every execution step that is more than one small edit. Multi-file edits, renames and link repointing, index and status-surface updates, spreadsheet reads and writes, bulk verification arithmetic. Use a cheaper model where the work is mechanical.
- Exceptions: a single small edit, or reading a file the main thread needs in context anyway.
- Log the subagent's token total in the deliverable's Time and Token Log in the same operation, as AGENTS.md already requires.

Related: [[mm-token-economics]] (the card this instance is logged against, "delegate the grinding"), [[feedback-verify-before-writing]] (the main thread still verifies).

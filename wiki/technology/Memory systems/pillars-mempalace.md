---
type: reference
updated: 2026-08-01
concept: product-evaluation
product: MemPalace
---

# MemPalace, Scored Against the Four Pillars

> *How MemPalace scores on **Capture, Storage, Injection, Recall**. Scoring only. Model: [[memory-pillars]].*

> [!note] Status: reference, not an adopted design
> An assessment of someone else's product against the four-pillar model. Nothing here is running in this vault.

Source: verified directly against `/Users/julianhart/mempalace` on 2026-08-01 - `mempalace/hooks_cli.py`, `.claude-plugin/hooks/hooks.json`, `.claude-plugin/skills/mempalace-recall/SKILL.md`, README.md. No prior wiki or secondary-source material existed for this product before this assessment.

## Key Takeaways

- **The only system of the four assessed that answers the compaction question directly.** A `PreCompact` hook fires unconditionally before every compaction event and synchronously ingests the transcript so nothing is lost. This is a real, verified mechanism for the exact problem discussed earlier in this vault's memory doctrine ([[memory-pillars]], "Compaction and context rot").
- **Storage is verbatim by design, the opposite pole from every other product assessed.** The README states it explicitly: "It does not summarize, extract, or paraphrase." ClaudeClaw, agentic-os, and MemSearch all synthesise at ingest; MemPalace deliberately does not.
- **Capture cadence is periodic, not continuous or boundary** - a default save every 15 human messages (`SAVE_INTERVAL = 15`). Now folded into [[memory-pillars]] as the third capture mode, with this system as the verified example.
- **No injection layer exists at all**, confirmed by direct code inspection, not by absence of a doc. `hook_session_start` initialises tracking state only and injects nothing; there is no `UserPromptSubmit` hook. Recall is 100% pull, driven by a "search-before-answer" skill protocol.
- **An unusual dual-mode capture design**: the default ("silent") mode saves programmatically with no agent involvement; a legacy opt-in mode instead *blocks* the Stop event and instructs the agent to write its own diary entry via MCP tools - agent-authored capture, not external summarisation.
- **Cites an external benchmark** - 96.6% R@5 on LongMemEval - the only one of the four systems assessed to ground a capability claim in a named, published benchmark rather than internal description.

---

## Scorecard

| Pillar | Sub-type | MemPalace |
|---|---|---|
| **Capture** | Continuous / periodic / boundary | **Neither cleanly - periodic.** Default: every 15 exchanges via `Stop`. Plus unconditional synchronous capture on `PreCompact` and a final flush on `SessionEnd` |
| **Storage** | Kind of claim | **Undifferentiated**, but structurally scoped: Wings (people/projects) > Rooms (topics) > Drawers (original content), for scoped rather than flat search |
| **Storage** | Form | **Verbatim.** Explicitly not summarised, extracted, or paraphrased - the only system assessed on this pole |
| **Storage** | Retention | **Comprehensive** by default; no importance gate found |
| **Injection** | Scheduled / triggered | **Neither. No injection layer exists** - confirmed by reading `hook_session_start` directly, not inferred from a missing doc |
| **Recall** | Write-time / query-time | **Query-time**, semantic search over verbatim content via a pluggable backend (ChromaDB by default) |

## Capture

Three hooks, each covering a different loss scenario, none of them per-turn in the ClaudeClaw/agentic-os/MemSearch sense.

**`Stop` - periodic checkpoint.** Counts human messages since the last save; triggers only when `since_last >= SAVE_INTERVAL` (15). This is neither continuous (it does not fire meaningfully every turn) nor boundary (it is not tied to session end) - it is **periodic**, now the third capture mode in [[memory-pillars]].

Two capture modes exist, selected by config, and the default changed at v3.3.0:

- **Silent (default since v3.3.0):** saves directly via a Python API call - `_save_diary_direct` plus `_ingest_transcript` - with no agent involvement. Produces a `systemMessage` like *"2 memories woven into the palace - themes"*.
- **Legacy (opt-in):** returns `{"decision": "block", "reason": ...}`, which blocks the Stop event and instructs the agent itself to call `mempalace_diary_write` and `mempalace_add_drawer` via MCP tools before it is allowed to finish. This is **agent-authored capture** - the model decides what is worth recording, in the moment, with full context - a mechanism none of the other three systems assessed implement. It is not the default, and the source comment marks it "legacy."

**`PreCompact` - the compaction answer.** Always runs synchronously, with no interval gate and no silent/legacy split: ingests the transcript and mines it into the palace *before* compaction proceeds. The hook's own constant names the intent: `PRECOMPACT_BLOCK_REASON = "MemPalace emergency save - compaction imminent... save ALL content before context is lost."` This is the mechanism now documented in [[memory-pillars]]'s compaction section as the structural fix: **capture triggered specifically by the event that causes loss**, not by a fixed schedule that might miss it - a firing condition layered onto this system's periodic checkpoint rather than a fourth granularity of its own.

**`SessionEnd` - final flush**, for anything the periodic checkpoint had not yet caught.

## Storage

**Verbatim, and this is the article's headline claim, verified rather than assumed.** The README: *"It does not summarize, extract, or paraphrase."* Every other system in this comparison set - ClaudeClaw, agentic-os, MemSearch - synthesises at ingest. MemPalace is the clean example of the opposite pole on the form axis in [[memory-pillars]].

**Structured for scoped search, not flat retrieval.** Content is organised as Wings (people or projects) containing Rooms (topics) containing Drawers (original verbatim content) - a search can be scoped to a wing or room rather than run against the entire corpus. None of the other three systems assessed have an equivalent structural scoping layer; ClaudeClaw and MemSearch both search a flat store.

**Pluggable backend, ChromaDB by default.** The interface is defined in `backends/base.py` and alternative backends can be substituted without touching the rest of the system - a degree of storage-engine abstraction none of the other three products expose.

## Injection

**There is none, and this was checked directly rather than inferred.** `hooks.json` wires only `Stop`, `SessionEnd`, and `PreCompact` - no `SessionStart`, no `UserPromptSubmit`. `hook_session_start` does exist in the Python source, but reading its body confirms it only initialises session-tracking state and surfaces daemon-readiness problems; it returns a bare `{}` with no `additionalContext` field.

**Recall is entirely pull, and the pull is protocol-driven rather than incidental.** The `mempalace-recall` skill instructs the agent: *"Search the palace before answering whenever the user asks about something that may be filed"* - a search-before-answer rule, not a hint. Compare this to MemSearch's per-turn nudge (see [[pillars-memsearch]]): MemPalace has no equivalent nudge mechanism at all, relying entirely on the skill instruction and the agent's judgement to invoke `mempalace_search`.

**Consequence, by the trigger hierarchy in [[memory-pillars]]:** this sits purely on option 2 (the agent decides), with not even a deterministic per-turn reminder pushing toward it. Of the four systems assessed, this is the weakest position on Injection - weaker than MemSearch's nudge, and far weaker than ClaudeClaw's per-turn content injection.

## Recall

Semantic search over verbatim text via the pluggable backend (ChromaDB by default), scoped by the Wings/Rooms/Drawers structure. The README cites a specific external benchmark: **96.6% R@5 raw on LongMemEval, zero API calls** - the only one of the four systems in this comparison to ground a retrieval-quality claim in a named published benchmark rather than an internal description.

"Zero API calls" implies the default embedding path runs locally, consistent with the "local-first" framing throughout the README, though the exact embedding model was not verified in this pass.

## What it would and would not solve here

| | |
|---|---|
| **Would add** | A genuine, verified answer to the compaction-loss question via `PreCompact` - the strongest single finding across all four products assessed for that specific problem. Verbatim storage, which this vault's own wiki-as-canonical-layer approach already provides in a different form (curated prose rather than raw verbatim, but load-bearing rather than disposable, unlike MemSearch's shadow index) |
| **Would duplicate** | Capture, already covered by native JSONL - though the periodic/PreCompact/SessionEnd triage pattern is a genuinely different design worth studying independently of whether the tool itself is adopted |
| **Would not solve** | Injection. This is the weakest Injection implementation of the four systems assessed, weaker even than doing nothing deliberately - MemSearch at least nudges every turn |
| **Notable** | The legacy agent-authored capture mode (block-and-instruct rather than externally-summarise) is a capture *pattern*, not just an implementation, that none of ClaudeClaw, agentic-os, or MemSearch use |

## Related

- [[memory-pillars]] - the model being applied; the PreCompact finding is directly relevant to its "Compaction and context rot" section and the periodic-capture finding to its Capture sub-types
- [[pillars-memsearch]] - contrast: MemSearch's per-turn nudge vs. MemPalace's total absence of any injection signal
- [[pillars-claudeclaw]] - contrast: true per-turn content injection vs. none
- [[pillars-agentic-os]] - contrast: scheduled injection vs. none

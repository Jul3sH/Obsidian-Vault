---
type: reference
updated: 2026-08-01
concept: product-evaluation
product: MemSearch
---

# MemSearch, Scored Against Pillars, Use Cases, and Capabilities

> *How MemSearch (zilliztech) scores on **Capture, Storage, Injection, Recall**, plus the [[memory-use-cases]] and [[memory-capabilities]] those pillars support. Model: [[memory-pillars]].*

> [!note] Status: reference, not an adopted design
> An assessment of someone else's product against the four-pillar model. Nothing here is running in this vault.

Source: verified directly against `/Users/julianhart/memsearch` on 2026-08-01 - `plugins/claude-code/hooks/*.sh`, `hooks.json`, README.md. Not sourced from the earlier Google Doc summary, which is corrected below.

## Key Takeaways

- **A correction to the earlier secondary-source summary.** The Google Doc's comparison table says MemSearch "relies on default Claude Code injection." That is wrong: it ships its own `SessionStart` hook that injects real content, plus a `UserPromptSubmit` hook on every turn.
- **The `UserPromptSubmit` hook does not inject memory content.** It posts a cheap, deterministic hint ("[memsearch] Memory available") that nudges the agent toward invoking the recall skill. The actual retrieval stays agent-decided. This is trigger option 3 in [[memory-pillars]]: not scheduled, not true per-turn content injection like ClaudeClaw's option 4 - a deterministic nudge toward option 2 (the agent decides) rather than a replacement for it.
- **Storage architecture inverts the usual canonical/derived relationship.** Markdown journals are the durable source of truth; the Milvus vector index is explicitly described as a disposable, rebuildable "shadow index."
- **Comprehensive retention**, not curated - captures every non-trivial turn, unlike ClaudeClaw's importance-gated capture.
- **The only system of the four assessed with genuine cross-agent federation**: one memory store shared across Claude Code, Codex CLI, OpenClaw, and OpenCode. This is a direct, working instance of the federation gap flagged in [[memory-model-adoption]].
- **Two capabilities beyond the four pillars**: background-maintained curated `PROJECT.md`/`USER.md` notes (a semantic distillation layer over the raw journals), and "skills from memory" - mining repeated workflows into portable, installable Agent Skills, a procedural memory layer neither pillar nor enabler in the current model.
- **Capability shape:** strongest on cross-agent federation, hybrid recall, scheduled context, source-grounded recall, and procedural memory generation; weakest on scope isolation and temporal fact recall.

---

## Scorecard

| Pillar | Sub-type | MemSearch |
|---|---|---|
| **Capture** | Continuous / periodic / boundary | **Continuous** - `Stop` fires per-turn (Claude Code semantics); parses and summarises the last turn each time |
| **Storage** | Kind of claim | **Undifferentiated journal**, with an optional curated layer (`PROJECT.md`/`USER.md`) maintained in the background |
| **Storage** | Form | **Synthesised-at-ingest as canonical, with the vector index explicitly disposable** - markdown is the source of truth; Milvus is a "shadow index... derived, rebuildable cache" |
| **Storage** | Retention | **Comprehensive** - captures every turn with real content; skips only empty/near-empty transcripts, no importance gate |
| **Injection** | Scheduled / triggered | **Scheduled (real) plus a per-turn nudge (not real content injection)** - see Key Takeaways |
| **Recall** | Write-time / query-time | **Query-time**, hybrid: dense vector + BM25 sparse + RRF reranking, 3-layer progressive disclosure (search → expand → transcript) |

## Use Case and Capability Coverage

| Use case | Capability | Coverage | Why |
|---|---|---|---|
| [[memory-use-cases|Know the user]] | [[memory-capabilities|Identity persistence]] | **Strong / partial** | `USER.md` distillation plus session-start injection can provide identity, though it is optional background-maintained material |
| [[memory-use-cases|Resume the work]] | [[memory-capabilities|Critical context availability]] | **Strong / partial** | `PROJECT.md`, recent daily journals, and scheduled injection directly target current work context |
| [[memory-use-cases|Survive compaction]] | [[memory-capabilities|Compaction survival]] | **Partial** | Continuous capture reduces disk-loss risk and the per-turn nudge may prompt recall, but no hook injects retrieved content deterministically |
| [[memory-use-cases|Preserve reasoning]] | [[memory-capabilities|Working reasoning preservation]] | **Strong / partial** | Comprehensive turn capture and transcript escalation preserve residue, though the primary stored layer is summarised at ingest |
| [[memory-use-cases|Recall old knowledge]] | [[memory-capabilities|Long-term knowledge recall]] | **Strong** | Dense vector plus BM25 sparse search with RRF reranking is the strongest ranking stack assessed |
| [[memory-use-cases|Reconstruct what happened]] | [[memory-capabilities|Episodic recall]] | **Strong / partial** | Three-layer progressive disclosure can escalate to transcript, while markdown journals remain canonical |
| [[memory-use-cases|Keep memory healthy]] | [[memory-capabilities|Retention management]] | **Partial** | Content hashing and rebuildable indexing help maintenance, but comprehensive retention means no strong pruning/decay policy was identified |
| [[memory-use-cases|Turn patterns into rules]] | [[memory-capabilities|Pattern-to-rule promotion]] | **Strong / partial** | `PROJECT.md` / `USER.md` distillation promotes useful summaries, though not with this vault's explicit canonical/behavioural split |
| [[memory-use-cases|Find unlocated context]] | [[memory-capabilities|Unlocated context discovery]] | **Strong** | Hybrid retrieval plus a deterministic per-turn nudge is stronger than agent-decided recall alone |
| [[memory-use-cases|Navigate curated knowledge]] | [[memory-capabilities|Curated knowledge navigation]] | **Partial** | Markdown journals are human-readable and canonical, but not a curated index hierarchy |
| [[memory-use-cases|Share memory across agents]] | [[memory-capabilities|Cross-agent memory federation]] | **Strong** | One memory store spans Claude Code, Codex CLI, OpenClaw, and OpenCode |
| [[memory-use-cases|Keep scopes separate]] | [[memory-capabilities|Scope-isolated recall]] | **Missing** | The assessed design indexes into one global space and has no scope model |
| [[memory-use-cases|Recall what was true then]] | [[memory-capabilities|Temporal fact recall]] | **Missing** | No temporal validity model or entity graph was identified |
| [[memory-use-cases|Trace to source]] | [[memory-capabilities|Source-grounded recall]] | **Strong** | Markdown journals are canonical, the vector index is disposable, and recall can escalate to transcript |
| [[memory-use-cases|Turn workflows into procedures]] | [[memory-capabilities|Procedural memory generation]] | **Strong** | Skills from Memory directly turns repeated workflows into skill candidates |

## Capture

`Stop` fires at the end of every agent turn. `stop.sh` parses the transcript for the last turn only, summarises it via `claude -p` (Haiku by default, configurable), appends the summary under a session heading in a daily markdown journal (`.memsearch/memory/{date}.md`), then re-indexes immediately.

**No importance gate.** Unlike ClaudeClaw, there is no threshold that discards low-value turns - the hook only skips genuinely empty or near-empty transcripts (fewer than 3 lines). This is a comprehensive-retention design, matching the "captures everything" characterisation from the earlier secondary source, which on this pillar was accurate.

**A loop guard exists**: if `stop_hook_active` is true (this Stop was itself triggered by a prior Stop hook), the hook exits immediately to prevent recursive summarisation.

## Storage

Markdown files under `.memsearch/memory/` are the canonical store - human-readable, git-trackable, directly editable. Milvus holds the vector index built from those files, and the README states this explicitly: **"Milvus is a 'shadow index': a derived, rebuildable cache."** If the index is lost or corrupted, it is rebuilt from the markdown, not from a backup - the markdown is authoritative, not merely a copy of it.

**This is a distinct position on the form axis from every other product assessed.** ClaudeClaw and agentic-os both treat their vector store as load-bearing. MemSearch's design means losing the vector index is a performance problem (re-index), not a data-loss problem.

Two extensions beyond the base journal:

- **Curated notes** (`PROJECT.md`, `USER.md`) - an optional background-maintained distillation layer over the raw daily journals, closer in spirit to the behavioural branch described in [[memory-pillars]], though MemSearch does not itself distinguish canonical from behavioural content.
- **Skill distillation** ("Skills from Memory") - a third, explicitly named "procedural memory" layer. The agent can turn a repeated workflow into a portable Agent Skill on request (*"make a skill out of what we just did"*), stored inert in a git-tracked `skill-candidates/` directory until the user installs one. This does not map onto any of the four pillars as currently defined - it is closer to a memory system generating a new *enabler* (a skill) than to storing or retrieving a fact.

## Injection

**Two hooks, two different mechanisms - and only one injects content.**

`session-start.sh` fires on `SessionStart` and does inject real content: it reads the two most recent daily journal files, extracts their recent non-empty sections, and returns them as `additionalContext`, alongside a status line (embedding provider, Milvus URI, index health). This is genuine scheduled injection, on a par with ClaudeClaw's `user.md`-style snapshot.

`user-prompt-submit.sh` fires on every `UserPromptSubmit` and does **not** inject memory content. Its own comment states the design intent precisely: *"lightweight hint reminding Claude about the memory-recall skill. The actual search + expand is handled by the memory-recall skill (pull-based, context: fork)."* It returns only a `systemMessage`: `"[memsearch] Memory available"`. Short prompts (under 10 characters) are skipped entirely.

**This is worth naming as a distinct pattern.** It is not scheduled (it fires every turn, not once). It is not triggered in ClaudeClaw's sense (it does not itself place memory content in context). It is now folded into [[memory-pillars]] as trigger option 3: a **deterministic per-turn nudge toward an agent-decided pull**, cheaper than option 4's true content injection because it costs no retrieval unless the agent acts on the hint, but more reliable than option 2 alone because the reminder is unconditional rather than left entirely to the agent's judgement.

## Recall

Query-time, and the most retrieval-sophisticated of the four systems assessed on the search step itself: **hybrid dense vector plus BM25 sparse search, combined via reciprocal rank fusion (RRF) reranking**, rather than similarity threshold alone.

**Progressive disclosure, three layers** - search, expand, transcript - the same escalation shape independently documented for agentic-os (see [[pillars-agentic-os]]), which makes sense given agentic-os states it replaced MemSearch and appears to have kept the retrieval ladder design.

Indexing is incremental and cheap to re-run: SHA-256 content hashing skips unchanged files, and a file watcher (`start_watch`) keeps the index live between explicit Stop-triggered updates.

## What it would and would not solve here

| | |
|---|---|
| **Would add** | Query-time Recall with hybrid ranking. Cross-agent federation - the clearest working example of the gap [[memory-model-adoption]] flags as unsolved here |
| **Would duplicate** | Capture (native JSONL), and partially Storage (this vault's canonical branch already plays the "markdown is source of truth" role MemSearch's journal plays) |
| **Would partially solve** | Injection - the scheduled half genuinely, mid-session recall only via the nudge-and-hope pattern, which is weaker than deterministic triggered injection |
| **Notable** | The skill-distillation feature has no equivalent anywhere in this vault's tooling and does not map onto the four-pillar model at all |

## Related

- [[memory-pillars]] - the model being applied; the nudge-pattern finding above is a candidate refinement to it
- [[memory-use-cases]] - use case catalogue used for the coverage table
- [[memory-capabilities]] - capability catalogue used for the coverage table
- [[memory-features]] - feature catalogue used for implementation examples
- [[pillars-claudeclaw]] - contrast: true per-turn content injection vs. MemSearch's per-turn nudge
- [[pillars-agentic-os]] - the system that replaced MemSearch in that codebase, and appears to have kept its retrieval ladder
- [[memory-model-adoption]] - the federation seam this system's cross-agent design directly addresses

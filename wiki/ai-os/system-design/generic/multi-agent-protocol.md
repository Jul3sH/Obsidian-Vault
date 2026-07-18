---
type: reference
created: 2026-07-09
tags: [ai-os, system-design, multi-agent, llm, protocol]
---

# Multi-Agent Protocol

> How Claude, Codex, Fable, and other LLM sessions communicate and hand off work in this AI OS. Covers model roles, the research-review-write pipeline, output file conventions, source document integrity, and handoff discipline. The **enforceable rules** (frontmatter validity, review-file separation) live in [[AGENTS]] under "Source Document Integrity and Adversarial Review Protocol". This article explains the design rationale and how the pieces fit.

---

## Why this protocol exists

Multiple LLMs - or multiple sessions of the same LLM - share this wiki. They share files but not conversation history. Without explicit conventions:

- One model's output can corrupt another's work (concrete example: Codex 2026-07-09 injected its review summary table into the YAML frontmatter of a source report it was reviewing, corrupting the file)
- Reviews can amplify the bias they were meant to catch (confirmation-amplification: errors lean toward the user's preferred answer)
- Source documents and review documents can diverge silently

This protocol makes inter-model communication explicit: each model writes to a defined output type, reads from defined source files, and does not contaminate files it is reviewing.

---

## Model roles

| Model | Role | Typical use | When NOT to use |
|---|---|---|---|
| **Opus** | Deep research, wide-net synthesis | 20+ source feasibility passes, complex multi-dimensional judgment | Simple edits; anything a Fable review hasn't cleared yet |
| **Fable** | Adversarial reviewer | Before writing any report; hunts confirmation-amplification in BOTH directions | First-pass research (Opus or Perplexity goes first) |
| **Sonnet** | Coordination, verification, fixes | Fast turns, context management, verifying other models' work, fixing corruption | Deep research requiring source breadth |
| **Codex** | Independent second-opinion review | Reviewing reports without shared session context; parallel code/file edits | Tasks that require Julian's conversation history |
| **Haiku / small models** | Cheap classification, triage | High-volume cost-sensitive passes | Complex reasoning or high-stakes judgment |

The shared principle: each model is used for what it is independently good at, not for convenience. Using Haiku for adversarial review defeats the point; using Opus for a quick number check wastes cost and time.

---

## The standard research pipeline

For any significant research question:

```
1. Opus       → wide-net research          → raw research file (wiki/[domain]/)
2. Perplexity → cross-check pass (optional) → Julian's own search; paste findings back
3. Fable      → adversarial review          → findings reviewed, inflations corrected
4. Claude     → write the final report      → wiki/[domain]/[topic].md
                using ONLY Fable-verified facts
```

**Fable reviews BEFORE the report is written, not after.** A report built on unreviewed research carries the researcher's biases into the permanent record. Once written, Fable's corrections become marginal notes on a done document; caught before, they shape the document from the start.

**Why Fable for adversarial review:** Fable is instructed to hunt confirmation-amplification in BOTH directions. In the UK relocation research, Fable caught move-leaning inflations in the UK research and stay-leaning inflations in the HK research in the same project. A model instructed only to "check the work" tends to confirm it. Fable is specifically positioned as a hostile reviewer.

---

## Output file conventions

| Output type | Where it goes | Notes |
|---|---|---|
| Research working files | Same wiki folder as the destination report | Provisional; can be deleted after the report is written |
| Final reports | `wiki/[domain]/[topic].md` | Source of truth. Frontmatter: `authority: Fable-reviewed` once reviewed |
| Adversarial review files | `wiki/[domain]/[topic]-[reviewer]-review-[date].md` | Review record. Never a substitute for the source |
| Review prompts | `wiki/[domain]/[topic]-review-prompt.md` | Reusable prompt for re-running the same review |

The naming convention makes the relationship obvious: `uk-vs-hk-earning-comparison.md` is the source; `uk-vs-hk-earning-comparison-codex-review-2026-07-09.md` is the review.

---

## Source document integrity

This is the rule that Codex violated in July 2026, and the reason this protocol exists.

**The principle:** a review document references a source. The source document does NOT reference the review while the review is in progress. The review file is the output of the reviewing agent; the source file is its input. Outputs do not contaminate inputs.

**What a reviewing model may do to a source document:** correct specific factual errors the review identified - update a stale number, reframe a biased claim. One change at a time, traceable to a specific finding.

**What a reviewing model may NOT do to a source document:** inject its verdict, add a summary table of its own review, add cross-references to its review file, or insert any metadata about the review itself. All of that belongs in the review file.

**Why this matters:** when review output appears inside the source, three things break simultaneously:
1. The source is no longer a clean record of the original work
2. YAML frontmatter can be corrupted if the injection lands in the wrong place (this is exactly what happened)
3. Future reviews compare against a corrupted baseline, not the original

The AGENTS.md rules (read by all agents every session) enforce this. The concrete rules are there; this section explains the intent behind them.

---

## Handoff discipline

**Written output, not verbal summary.** The handoff between models is always a wiki file. If a model's work is not written to the wiki, it did not happen and cannot be verified.

**Label the authority level.** Use frontmatter to signal review status. `authority: Fable-reviewed` marks a file as reviewed and authoritative. Absence of this field means provisional.

**Independent re-derivation, not repetition.** When Codex reviews a Claude report, Codex re-derives from the source data, not from Claude's summary. The value of independent review IS independence. A review that restates the original caught nothing.

**Flag, do not silently fix.** When a reviewing model finds a conflict with the source-of-truth, it flags the conflict in its review file and proposes a correction. It does not silently rewrite the source. The correction is made in a separate step, by the coordinating model (Sonnet) or Julian, with the flag preserved in the review record.

---

## Confirmation-amplification: the core bias

Documented across the UK relocation research (July 2026): assisting-model errors consistently leaned toward the user's preferred answer. Concrete examples found:

- UK research (early draft): headline verdict "highly realistic" sat above evidence that topped at £85-130k
- HK research: percentile-basis mismatch and a 1.6-1.8x tax multiple that secretly compared different gross figures
- Both inflations were caught by Fable in separate passes

The guard:
1. Use an adversarial reviewer before any report feeds a real decision
2. Instruct the reviewer to hunt BOTH directions explicitly
3. Treat the reviewer's corrections as authoritative and fold them in before writing

---

## Related

- [[AGENTS]] - enforceable rules including "Source Document Integrity and Adversarial Review Protocol"
- [[documentation-conventions]] - how wiki documents are structured and linked
- [[agent-instruction-architecture]] - how the three-layer instruction model loads across agents
- [[project-workflow]] - where research and review tasks fit in the project cycle

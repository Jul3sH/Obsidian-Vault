---
type: reference
created: 2026-07-31
status: adopted
---

# Memory Model (Adopted)

> *This environment reasons about memory using the **four-pillar model**: Capture, Storage, Injection, Recall. Adopted 2026-07-31. This is the decision record and what it obligates. The model itself, its derivation and its enabler technologies are theory and live at [[memory-pillars]].*

Applies to every harness (Claude, Codex, OpenCode), not just one.

## The adopted frame

```
Capture   (continuous | boundary)
   ↓
Storage   (canonical | behavioural)
   ↓
Injection (scheduled | triggered)
   ↓
Recall    (write-time | query-time)
```

Dependency runs downward only: Recall cannot return what Storage never kept; Storage cannot keep what Capture never recorded; Injection depends on Recall having something to give it.

**Every pillar sub-divides.** Naming the sub-type is not optional, because "improve Recall" and "improve Recall (query-time)" are different pieces of work.

## What it replaced

The previous framing was **Store, Inject, Recall** (Simon Scrapes' three pillars), recorded in [[memory-operations]]. It bundled capture into storage, which made it impossible to express the state this environment is actually in: *capture is already paid for by the platform, storage is not*. That bundling caused a real misjudgement before it was caught, so the amendment is load-bearing rather than cosmetic.

## What adoption obligates

1. **Any memory proposal is scored per pillar**, in dependency order, with a separate "is this solved, and by whom?" answer for each. A proposal that prices a pillar the platform already provides is rejected on that basis alone.
2. **Any new memory document names the pillar and sub-type it addresses.** Enabler documents declare it in frontmatter (`serves: recall (write-time)`).
3. **Pillars are never conflated with enablers.** A pillar is a function the system must perform; an enabler is a technology that performs it. Naming a design after an enabler and then filling it with pillar doctrine is the error this model exists to prevent, and it has been made twice here already.
4. **Terminology is fixed.** "Observation layer" means Capture. "Semantic search" means Recall (query-time) plus triggered Injection. They are not interchangeable, and a retrieval argument never justifies capture spend.

## How the pillars are currently configured here

Recorded in [[memory-operations]], not duplicated. Summary of where the environment stands as at adoption:

| Pillar | State |
|---|---|
| Capture | **Solved.** Native JSONL transcripts, continuous, complete |
| Storage | Curated markdown. Canonical branch is the wiki; behavioural branch is the memory files |
| Injection | **Scheduled only.** No triggered injection exists |
| Recall | Write-time only: curated index plus bare wikilinks. No query-time index |

**The binding constraint is Injection**, not Capture or Storage. This was not visible before the model separated the pillars, because a strong canonical Storage branch made the whole system look healthy.

## Known seam: federation

The model does not cleanly accommodate **multiple agents each with their own capture and storage** (Claude Code transcripts, Codex sessions and its memory database, and a second Claude project's sessions). This is a plurality-of-stores problem sitting underneath all four pillars rather than inside any one of them.

It can be modelled as Storage with multiple backends, which is probably right, but it is a genuine seam. If cross-agent work grows, this is where the model will strain first and should be revisited.

## Scope of the adoption

**Adopted:** the model, as the frame for reasoning about memory in this environment and when assessing others.

**Not adopted:** any enabler, any implementation, any verdict. Nothing has been built. The assessments in the technology articles are point-in-time evaluations, not commitments.

## Related

- [[memory-pillars]] - the model itself, its derivation, and the enabler map (theory)
- [[memory-operations]] - how the pillars are configured here, and the standing no-query-time-index decision
- [[memory-convention]] - the behavioural branch of Storage: types, format, loading rule
- [[agent-instruction-architecture]] - the parallel three-layer model for instructions

---
type: reference
created: 2026-09-24
status: active
tags: [working-with-genai, cognitive-bias, verification, mental-models]
---

# MM: Fluency Bias

## Purpose

The Fluency Bias card: AI output is always polished, in its prose and in its certainty,
so polish tells you nothing about whether it is right. The counters are to keep asking
what it actually means, and to check for evidence whenever it declares something
certain. It exists because both questions have repeatedly uncovered real errors in
polished AI work that would otherwise have been acted on.

**One-liner:** Always seek clarity, because it will often uncover errors. Don't skip it
because something is polished: with AI, everything looks polished. And when it sounds
certain, ask what checked it.

**Reach for it when:** reading or reviewing AI output you will act on, especially when
it reads fine and you are about to accept a passage you could not explain in your own
words, or when it declares something confirmed, impossible, irreversible or settled.

**Position:** alongside verification. Verification asks whether a check is affordable;
this names the checks that are nearly free and get skipped because the output looks
finished. The bias is described in [[verification-bottleneck]] (Fluency, one of three
biases that erode checking).

## Key Takeaways

- **With human work, junk reads like junk. With AI it doesn't.** Prose quality used to
  tell you where to slow down; AI output removes that signal, so wrong material is as
  polished as right material.
- **Polish comes in two forms: polished prose and polished certainty.** The first hides
  a gap in meaning; the second hides a gap in evidence. Each has its own question.
- **"What does this actually mean?" is a verification question**, not a style one. It
  finds errors at a rate that justifies asking it of everything you will act on.
- **When an LLM uses language that declares certainty, check for the evidence behind
  it.** A model states its conclusion with the confidence of its reasoning, not the
  confidence of the facts it started from, so sound logic on an unchecked fact comes
  out sounding settled.
- **Compression is where errors hide.** A summary written after the analysis inherits
  its conclusions without its caveats, so the top of a document is more dangerous than
  the middle.

## Principles

- **Demand plain restatement, and treat resistance as a signal.** If a sentence cannot
  be said in ordinary words, either it is not understood or it is not right. Both
  warrant stopping.
- **Certainty words are claims that need evidence.** "Confirmed", "cannot",
  "irreversible", "no fallback", "always" and "never" assert closure. Each must be
  earned by something checked; if nothing checked it, it is an assumption written as a
  conclusion.
- **A conclusion is no more certain than its weakest input.** If one fact in the chain
  was assumed, recalled or single-sourced, the conclusion is too, however clean the
  logic between them.
- **A settled-sounding claim stops being questioned** - by you, by reviewers, and by
  whoever reads it next. That is why the certainty words are the ones to hunt.
- **Intention is not impossibility.** "He will not do X" and "he cannot do X" are
  different claims; only the second closes the question.
- **Self-reported completion is testimony, not evidence.** A model or subagent saying
  it did something must be confirmed against something that could have disagreed - see
  [[mm-verification]].
- **Jargon is unexamined content.** A technical term stands in for reasoning; until it
  is unpacked, nothing behind it has been checked.
- **The summary is the least trustworthy part of a document.** Check it against the
  body rather than reading it as the body's digest.
- **The same discipline applied when writing is [[mm-write-for-the-stranger]].** This
  card is the reading half; that one is the writing half.

## Guidelines

- Read anything you will act on with the question "could I explain this to someone
  without the context?" Where the answer is no, stop and unpick it.
- Ask the model to **restate a passage plainly** rather than to check it. Restatement
  surfaces the gap; "is this right?" invites agreement.
- On every certainty word, ask **"what checked this?"** If the answer is a named source,
  fine. If it is memory, an assumption or the model's own reasoning, the claim is
  conditional and should say so.
- Challenge every term used before it is defined, especially in summaries and opening
  sections.
- Re-read corrections. A patched sentence often keeps the confidence of the version it
  replaced.
- When a clarification or an evidence check turns up an error, add it to the Evidence
  table below. The examples are what make the card persuasive next time.

## Limitations

- Asking for clarity finds ambiguity, not a wrong claim stated clearly. "The rate is
  20%" when it is 40% reads plainly and carries no certainty word, so it survives both
  questions - that is what [[mm-verification]] and adversarial review are for.
- Hedging everything is its own failure. Verified statute, arithmetic and direct
  quotation warrant definitive language; the aim is confidence that matches the
  evidence, not uniformly low confidence.
- It costs real time. On low-stakes output the reading is not worth the errors it
  would find.
- Taken too far it becomes editing for its own sake. The test is whether a
  clarification changes what the document means, not whether it reads better.

## Detail

[[verification-bottleneck]] (the Fluency bias and its two siblings, track record and
template blindness). Related: [[mm-verification]], [[mm-facts-first]],
[[mm-write-for-the-stranger]]. Rows in [[biases-index]] and [[mental-models-index]].

## Evidence

**Polished prose: found by asking "what does this mean?"**

| Date | The polished claim | What was uncovered | Source |
|------|--------------------|--------------------|--------|
| 2026-09-23/24 | Summary: "three of four conditions already met" | One of the four had not been met; it only completed weeks later | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "The clean route does not depend on counting days at all" | It did: that route carries its own day limits | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "90 days" used throughout | Two different 90-day rules were being used as if they were the same thing | [[uktax-srt-fy26-27]] |

**Polished certainty: found by asking "what checked this?"**

| Date | The certain claim | What was actually true | Source |
|------|-------------------|------------------------|--------|
| 2026-09-23/24 | Hong Kong flat "Confirmed" as a home | A judgement call; HMRC could take a different view | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "Crossing 90 days is irreversible" | A stated intention, not law; the option was still legally open | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "He cannot do X" | A stated intention not to do X, written up as a legal impossibility | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "There is no fallback" | A second route existed | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | A subagent reported it had started a background job | It never had; caught only by checking the job list, not by believing the report | [[uktax-srt-fy26-27]] |

The law was right at every review round of that analysis; roughly forty corrections
were nearly all one of these two shapes. None was found by asking "is this correct?".

## Document Log

| Date | Change |
|------|--------|
| 2026-10-01 | Merged in `mm-confidence-inheritance` (deleted): polished certainty added as the second form of fluency, with Julian's rule "check for evidence when an LLM uses language that declares certainty without supporting evidence"; its five instances added to the Evidence table. |
| 2026-10-01 | Renamed from `mm-clarity-is-verification` to `mm-fluency-bias` and reframed around the bias, with clarity-seeking as the counter. One-liner rewritten in Julian's words; examples moved into an Evidence table; linked to [[verification-bottleneck]]; added to [[biases-index]]. |
| 2026-09-24 | Created as "MM: Clarity Is Verification" from the UK residence analysis. |

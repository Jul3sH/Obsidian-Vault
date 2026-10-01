---
type: reference
created: 2026-09-24
status: active
tags: [working-with-genai, cognitive-bias, verification, mental-models]
---

# MM: Fluency Bias

## Purpose

The Fluency Bias card: AI output is always polished, so polish tells you nothing about
whether it is right, and the counter is to keep asking what it actually means. It
exists because asking for clarity has repeatedly uncovered real errors in polished AI
work that would otherwise have been acted on.

**One-liner:** Always seek clarity, because it will often uncover errors. Don't skip it
because something is polished: with AI, everything looks polished.

**Reach for it when:** reading or reviewing AI output you will act on, especially when
it reads fine and you are about to accept a passage you could not explain in your own
words.

**Position:** alongside verification. Verification asks whether a check is affordable;
this names the check that is nearly free and gets skipped because the output looks
finished. The bias is described in [[verification-bottleneck]] (Fluency, one of three
biases that erode checking).

## Key Takeaways

- **With human work, junk reads like junk. With AI it doesn't.** Prose quality used to
  tell you where to slow down; AI output removes that signal, so wrong material is as
  polished as right material.
- **"What does this actually mean?" is a verification question**, not a style one. It
  finds errors at a rate that justifies asking it of everything you will act on.
- The passages that resist plain restatement are the ones to distrust. Vagueness is
  often the residue of reasoning that did not fully close.
- **Compression is where errors hide.** A summary written after the analysis inherits
  its conclusions without its caveats, so the top of a document is more dangerous than
  the middle.

## Principles

- **Demand plain restatement, and treat resistance as a signal.** If a sentence cannot
  be said in ordinary words, either it is not understood or it is not right. Both
  warrant stopping.
- **Jargon is unexamined content.** A technical term stands in for reasoning; until it
  is unpacked, nothing behind it has been checked. Terms used before they are defined
  are the clearest case.
- **The summary is the least trustworthy part of a document.** It is written last, from
  conclusions, and compression strips the conditions those conclusions depended on.
  Check it against the body rather than reading it as the body's digest.
- **The same discipline applied when writing is [[mm-write-for-the-stranger]].** This
  card is the reading half; that one is the writing half.
- **The clarity pass is cheap and the accuracy pass is not** - so run the cheap one over
  everything and let it point at where the expensive one is needed.

## Guidelines

- Read anything you will act on with the question "could I explain this to someone
  without the context?" Where the answer is no, stop and unpick it.
- Ask the model to **restate a passage plainly** rather than to check it. Restatement
  surfaces the gap; "is this right?" invites agreement.
- Challenge every term used before it is defined, especially in summaries and opening
  sections.
- When a clarification turns up an error, add it to the Evidence table below. The
  examples are what make the card persuasive next time.
- Prefer two shorter passes on different days to one long one. Returning without the
  previous day's context reproduces the future reader's position naturally.

## Limitations

- It finds ambiguity and unstated reasoning, not a wrong claim stated clearly. "The rate
  is 20%" when it is 40% reads perfectly plainly and survives this check - that is what
  [[mm-verification]] and adversarial review are for.
- It costs real time. On low-stakes output the reading is not worth the errors it
  would find.
- Taken too far it becomes editing for its own sake. The test is whether a
  clarification changes what the document means, not whether it reads better.

## Detail

[[verification-bottleneck]] (the Fluency bias and its two siblings, track record and
template blindness). Related: [[mm-verification]], [[mm-confidence-inheritance]],
[[mm-facts-first]], [[mm-write-for-the-stranger]]. Rows in [[biases-index]] and
[[mental-models-index]].

## Evidence

| Date | The polished claim | What asking "what does this mean?" uncovered | Source |
|------|--------------------|----------------------------------------------|--------|
| 2026-09-23/24 | Summary: "three of four conditions already met" | One of the four had not been met; it only completed weeks later | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "The clean route does not depend on counting days at all" | It did: that route carries its own day limits | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "90 days" used throughout | Two different 90-day rules were being used as if they were the same thing | [[uktax-srt-fy26-27]] |
| 2026-09-23/24 | "He cannot do X" | It was a stated intention not to do X, written up as a legal impossibility | [[uktax-srt-fy26-27]] |

None of these was found by asking "is this correct?". All were found by asking "what
does this mean?", while Julian was trying to make the document readable rather than
checking it.

## Document Log

| Date | Change |
|------|--------|
| 2026-10-01 | Renamed from `mm-clarity-is-verification` to `mm-fluency-bias` and reframed around the bias, with clarity-seeking as the counter. One-liner rewritten in Julian's words; examples moved into an Evidence table; linked to [[verification-bottleneck]]; added to [[biases-index]]. |
| 2026-09-24 | Created as "MM: Clarity Is Verification" from the UK residence analysis. |

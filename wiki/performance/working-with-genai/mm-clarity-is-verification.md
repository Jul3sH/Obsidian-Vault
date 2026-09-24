---
type: reference
created: 2026-09-24
status: active
tags: [working-with-genai, verification, mental-models]
---

# MM: Clarity Is Verification

This card names a discovery from the UK residence analysis of 23-24 Sept 2026: Julian
set out to make the document readable and ended up finding its errors. Every time he
pulled on a piece of jargon, a term used before it was defined, or a compressed
sentence, there was a discrepancy underneath. The clarity pass and the accuracy pass
turned out to be the same activity.

**One-liner:** If you cannot say plainly what it means, that is often because it does
not mean what it says.

**Reach for it when:** reviewing AI output you will act on, and deciding whether to
read for meaning or only for correctness. Also when tempted to skip a passage because
it "reads fine".

**Position:** alongside verification. Verification asks whether a check is affordable;
this names a check that is nearly free and that people skip because it looks cosmetic.

## Key Takeaways

- **"What does this actually mean?" is a verification question**, not a style one. It
  finds errors at a rate that justifies asking it of everything you will act on.
- Fluent writing hides faults that clumsy writing exposes. A model's prose is always
  fluent, so fluency carries no information about correctness.
- The passages that resist plain restatement are the ones to distrust. Vagueness is
  often the residue of reasoning that did not fully close.
- **Compression is where errors hide.** A summary written after the analysis inherits
  its conclusions without its caveats, so the top of a document is more dangerous than
  the middle.
- Reading for a reader who lacks the context is the same discipline as reading for
  truth - both force every step to be stated rather than assumed.

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
  card is the reading half; that one is the writing half. They share a mechanism -
  forcing every step to be stated rather than assumed.
- **The clarity pass is cheap and the accuracy pass is not** - which is the argument
  for running the cheap one over everything and letting it point at where the expensive
  one is needed.

## Guidelines

- Read anything you will act on with the question "could I explain this to someone
  without the context?" Where the answer is no, stop and unpick it.
- Challenge every term used before it is defined, especially in summaries and opening
  sections. That ordering fault is a reliable marker for an inherited conclusion.
- When a clarification turns up an error, note that it did. The pattern is the evidence
  that clarity work is verification work, and it is easy to forget afterwards.
- Ask the model to restate a passage plainly rather than to check it. Restatement
  surfaces the gap; "is this right?" invites agreement.
- Prefer two shorter passes on different days to one long one. Returning without the
  previous day's context reproduces the future-reader's position naturally.

## Limitations

- It finds ambiguity and unstated reasoning, not factual error in a clearly-stated
  claim. A confidently wrong sentence written in plain English survives this check -
  that is what [[mm-verification]] and adversarial review are for.
- It costs real time. On low-stakes output the reading is not worth the errors it
  would find.
- Taken too far it becomes editing for its own sake. The test is whether a
  clarification changes what the document means, not whether it reads better.

## Detail

Instance: [[uktax-srt-fy26-27]]. Julian's questions about jargon and undefined terms
repeatedly surfaced substantive faults - a summary asserting "three of four conditions
already met" when one completed weeks later; "the clean route does not depend on
counting days at all" when it carries its own day limits; two different meanings of
"90 days" used interchangeably; and a stated intention recorded as a legal
impossibility. None was found by asking "is this correct?". All were found by asking
"what does this mean?".

Related: [[mm-verification]], [[mm-confidence-inheritance]], [[mm-facts-first]].
Row in [[mental-models-index]].

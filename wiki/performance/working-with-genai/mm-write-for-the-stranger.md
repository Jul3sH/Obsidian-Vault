---
type: reference
created: 2026-09-24
status: active
tags: [working-with-genai, documentation, mental-models]
---

# MM: Write For The Stranger

This card is about who a technical document is written for. The answer is not the
person who just did the work - it is the person who returns to it in a year with none
of the context, and that person is usually Julian. Written after the UK residence
analysis of 23-24 Sept 2026, where the reason for insisting on plain English was
explicitly future usability rather than present comprehension.

**One-liner:** Write for the version of you who has forgotten everything except that
this mattered.

**Reach for it when:** producing anything technical you will return to - an analysis, a
model, a decision record, a configuration - especially where an AI drafted it and it
reads well on the day.

**Position:** at output. Verification decides whether the content is right; this decides
whether it will still be usable once the reasoning behind it has left your head.

## Key Takeaways

- **Technical material is transparent while you are inside it and opaque afterwards.**
  The comprehension you feel on the day is borrowed from working context that will not
  survive.
- The stranger you are writing for is you, with the stakes intact and the reasoning
  gone. They will trust the document because they wrote it, which makes an unclear
  document worse than no document.
- **AI output is unusually prone to this.** It is fluent, confident and dense with
  terminology, so it reads as clear on the day while carrying the highest jargon load.
- A term used before it is defined is invisible to the author and fatal to the
  stranger - and it is the most common fault in a summary.
- Conclusions survive; conditions do not. A document that records "the answer is X"
  without "because Y, provided Z" will be misapplied when Y and Z are forgotten.

## Principles

- **Define before you use, especially in summaries.** The section written last is read
  first, and it is where inherited vocabulary accumulates. Ordering faults there do the
  most damage.
- **State the mechanism, not just the conclusion.** "You are safe to 182 days" is
  unusable a year on; "you are safe to 182 days because you hold one tie, and no band
  is triggered by one tie" survives, because it can be re-tested when the facts change.
- **Record what a claim depends on, next to the claim.** Conditions kept in a separate
  register drift from the conclusions they qualify, and the stranger reads only one of
  them.
- **Spell out your own shorthand.** Anything compressed because "obviously that means X"
  is exactly what will not be obvious. The compression saved seconds and costs an hour.
- **A document you cannot hand to someone else is one you cannot hand to yourself
  later.** The test for both is identical, which makes it easy to apply: could a
  competent outsider act on this?

## Guidelines

- Before finishing, reread the opening sections as if you had not read the rest. Terms
  that have not yet been earned will stand out.
- Where a term is unavoidable, define it in place rather than by cross-reference. A
  pointer to another section is a step the stranger will not take.
- Prefer a sentence of mechanism over a cross-reference. Links rot, move and renumber;
  a stated reason does not.
- Leave the working in. The derivation of a date or figure is what lets it be checked
  and rebuilt later; the bare number cannot be.
- Say what was assumed as well as what was established - see
  [[mm-confidence-inheritance]]. The stranger cannot tell them apart otherwise.

## Limitations

- Conversational and throwaway output does not warrant it; the cost is real and is
  justified by the document's expected lifespan, not its length.
- It does not make wrong content right. A clearly written error is more dangerous than
  an unclear one, because it will be acted on - [[mm-verification]] still applies.
- Over-applied it produces documents that explain everything and say nothing. Explain
  the terms the argument turns on, not every term.

## Detail

Instance: [[uktax-srt-fy26-27]]. Julian's stated reason for insisting on plain English
was that technical understanding built over two days would be gone in a year, and a
document he could not re-enter would be worthless at exactly the point he needed it -
when the facts changed and the analysis had to be re-run.

The related discovery is that this discipline doubles as a check:
[[mm-clarity-is-verification]] - demanding plain restatement surfaces errors as well as
ambiguity.

Related: [[mm-clarity-is-verification]], [[mm-confidence-inheritance]].
Row in [[mental-models-index]].

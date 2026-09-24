---
type: reference
created: 2026-09-24
status: active
tags: [working-with-genai, verification, mental-models]
---

# MM: Confidence Inheritance

This card is about how confidently a conclusion is *stated*. A model reasons from
inputs to an answer, then reports the answer with the confidence of its **reasoning** -
not the confidence of the **facts it started from**. Sound logic applied to an
unverified fact comes out sounding settled. Written after the UK residence analysis of
23-24 Sept 2026, where the law was right at every review round and roughly forty
corrections were all the same shape: a conclusion stated as definitive on an input
nobody had checked.

**One-liner:** A conclusion can be no more certain than its weakest input - and should
not sound it.

**Reach for it when:** reading or writing anything that will be acted on, especially
where the reasoning is solid and the facts came from memory, assumption or a single
source.

**Position:** alongside verification. Verification asks whether a check is affordable;
this asks whether the claim **advertises that it needs one**. A claim written as settled
suppresses the check rather than inviting it.

## Key Takeaways

- Confidence is inherited from the reasoning, not the inputs, unless something forces
  it the other way. The default is wrong.
- **"Confirmed", "irreversible", "no fallback", "cannot"** are the words to hunt. Each
  asserts closure, and closure is exactly what an unverified input cannot support.
- A reader cannot see that an input was assumed. The conclusion looks identical
  either way, which is what makes it dangerous.
- Anything reported by the thing that did the work is an unverified input, including
  a subagent saying it finished. Self-report is not evidence.
- **A conclusion stated as settled stops being questioned** - by you, by reviewers,
  and by whoever reads it next.

## Principles

- **Confidence flows from the weakest input, not the strongest reasoning.** If one
  fact in the chain is assumed, the conclusion is assumed, however clean the logic
  between them.
- **Say what the claim rests on, in the claim.** Not in a footnote, not in a register
  elsewhere. Someone reading only the conclusion should be able to see it is
  conditional.
- **Watch the vocabulary of closure.** Words like confirmed, settled, irreversible,
  always and never are claims about certainty, not about content. Each one should be
  earned by something checked.
- **A statement of intention is not a statement of law.** "He will not do X" and "he
  cannot do X" are different claims; only the second closes the question. Recording
  intention as impossibility removes an option that still exists.
- **Self-reported completion is an input like any other.** A model, a subagent or a
  tool saying it did something is testimony, not evidence. Confirm against something
  that could have disagreed - see [[mm-verification]].

## Guidelines

- Before writing a conclusion, ask: **which fact here have I not actually checked?**
  Then phrase the conclusion so a reader can see it.
- Keep the confidence wording and the evidence in the same sentence. Split across a
  document, they drift apart under editing - the register says "assumed" while the
  body says "confirmed".
- When you mark something confirmed, name what confirmed it. If you cannot, it is
  not confirmed.
- In any register of open items, distinguish **loose ends** from **prerequisites**.
  A prerequisite recorded as a loose end is the specific failure this card exists to
  catch.
- Re-read your own corrections. A patched sentence often keeps the confidence of the
  version it replaced.

## Limitations

- Hedging everything is its own failure; a document where nothing is stated plainly
  is unusable. The aim is confidence that matches the evidence, not uniformly low
  confidence.
- Some things genuinely are settled and should be said so. Verified statute, arithmetic
  and direct quotation all warrant definitive language.
- Calibrated language does not replace checking. It tells a reader where to look; it
  does not do the looking.

## Detail

Instances from [[uktax-srt-fy26-27]]: the Hong Kong flat recorded as "Confirmed" a
home when its status is a fact-sensitive judgement HMRC could take a different view
on; "crossing 90 days is irreversible" written from a stated intention rather than
law, when the option remained legally open; "there is no fallback" when a second
route existed; and a subagent reporting a background job it had never started, caught
only by querying the job registry rather than believing the report.

Related: [[mm-verification]] (whether a check is affordable and can fail
independently), [[mm-facts-first]] (closing the fact base before the analysis starts).
Row in [[mental-models-index]].

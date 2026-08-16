---
type: reference
created: 2026-08-13
status: active
tags: [working-with-genai, the-human-mind, verification]
---

# The Verification Bottleneck

This is the principle that checking, not producing, is the limit on how much AI work
is actually worth having. It was extracted from [[routing-work-to-agents]], where it
had been doing the job of justifying one gate, because it is a general fact about
working with generative AI rather than a routing rule. Read it once to understand why
"I'll review it" is not a plan, and return to it whenever you are about to increase
the volume of AI output you are responsible for.

## Key Takeaways

- **Generation scaled and verification did not.** Everything else here follows from
  that one asymmetry.
- **A good run is the condition under which you stop checking.** Reliability causes
  the failure; it does not prevent it.
- **The failure mode is not catching fewer errors. It is believing you are still
  checking when you have stopped**, while the record says the work was reviewed.
- **Checking has to be built, not resolved upon.** Intention degrades under exactly
  the volume that makes it necessary.

## The asymmetry

The capacity to produce work has gone up by orders of magnitude. The capacity to
confirm it is correct is still one human reading one thing at a time.

That is the whole principle. Every rule below is a consequence of it.

## What it is called

The burden goes by several names depending on who is writing: the **verification
gap**, **review fatigue** or **approval fatigue**, and in older human-factors
research **automation bias** and **automation complacency**. The last two are the
useful ones, because they are decades old, they come from aviation and clinical
medicine rather than from anyone selling a tool, and they describe the mechanism
rather than the symptom.

The favourable case has its own names, and these are the ones the AI community
recognises (verified against usage, Aug 2026). The property that some work is much
easier to verify than to generate is the **asymmetry of verification**, coined by
Jason Wei along with **verifier's law**: the ease of training AI on a task is
proportional to how verifiable it is. Karpathy's version: *"Software 2.0 easily
automates what you can verify."* Research literature measures the same thing as the
**generation-verification gap** (GV-Gap). When speaking to the community, say
"generation" and "verification", not "production" and "checking". One 2026 finding
worth holding: for coding agents the asymmetry is argued to be *reversing* -
generating a plausible solution has become easy, and reliably verifying it is now
the harder problem - which is this article's thesis stated from the other side.

## Three findings that matter

**Reliability makes it worse, not better.** Parasuraman and colleagues found that
when automation was consistently reliable, operators detected only about 30% of its
errors. When the system visibly failed from time to time, detection rose to roughly
75%. This is the finding to sit with: a long run of good output is the condition
under which you stop catching things. "It has been fine so far" is not evidence that
you are checking. It is the mechanism by which you stopped.

**Expertise does not protect you.** In a 2023 radiology study, experienced
radiologists reviewing mammograms alongside incorrect AI suggestions fell from 82%
accuracy to 45.5%. Inexperienced ones fell from around 80% to under 20%. Seniority
softened the fall; it did not prevent it.

**Intention is not behaviour.** Sonar's survey found 96% of developers do not fully
trust AI output while only 48% verify it. Everyone knows to check. Under volume,
roughly half do.

## Why volume degrades checking, rather than just exceeding it

The obvious cost of high volume is that there is too much to get through. That is not
the interesting one.

**Attention is a fixed budget, and reviewing spends it whether or not you find
anything.** You have some amount of genuinely sharp reading in you before quality
drops. One agent hands you three pages and you read them properly, checking claims
against what you know. Five agents hand you forty. By page twelve you are not
checking, you are skimming for shape, because that is what happens to everyone. The
errors are still sitting there. You are no longer the kind of reader who would catch
them.

So wading through the volume spends your attention on low-value reading, and the
sharp judgement you needed for the one paragraph that is wrong is gone by the time
you reach it. **The volume does not merely outlast your attention. It consumes the
specific attention the errors required.**

Three biases stack for AI output specifically. They defeat different parts of your
checking, which is why they are worth naming separately.

**Track record.** The good run sets up the miss: the first four agents being correct
is precisely what stops you catching the fifth, per the reliability finding above.
This one operates *across* outputs, lowering how much checking you attempt at all.

**Fluency.** With human work, junk usually reads like junk: prose quality is a
working signal for thinking quality, and it tells you where to slow down. AI output
severs that signal. Wrong material is exactly as polished as right material, so the
checking that survived the first bias has nothing to snag on. This one operates
*within* an output.

**Template blindness.** Consistent formatting and structural repetition habituate
the eye. By the thirtieth identically shaped output you are pattern-matching the
template rather than reading the content, and anything sitting inside the expected
shape passes unseen. Fluency kills the signal; this one kills the attention.

The human analogue that holds all three: a sloppy junior gets read line by line,
because the errors advertise themselves. A polished senior gets skimmed, and has
earned it. AI is the pathological case: the track record and polish of the senior
with the error profile of a confident junior, and no sloppiness signal marking where
the errors sit.

## The failure mode

It is not that you catch fewer errors. It is that **you keep believing you are
checking while you have stopped**, and the record still says the work was reviewed.

Oversight quietly becomes a rubber stamp, which is worse than no oversight because it
manufactures confidence. No-one is alarmed by unreviewed work. Everyone relies on
work that was reviewed, including work that was only nominally reviewed.

## What follows from it

**"I'll review it" is not a check.** It is an intention, and it degrades under
exactly the volume that creates the need for it. A check has to be a thing you build
rather than a thing you resolve to do, which means anything you cannot name in
advance counts as a fail.

**Make checking affordable by design rather than by resolve.** The aim is to keep
your attention **sub-linear to the volume**: require source citations you can click,
so you verify three of thirty and trust the pattern; structure output so a wrong
answer looks wrong; sample rather than sweep. Attention spent on things a cheaper
layer would have caught is attention you no longer have for the judgement calls only
you can make. The machinery for this is the three forms below.

**More output is not automatically more value.** Any decision that increases the
volume of AI work you are answerable for should be costed against the checking it
creates, not just the producing it saves.

**Where the judging is the work, no architecture helps.** This is what "taste work"
means wherever it appears in this folder: **work with no external criterion to check
the answer against, so your judgement does not verify the output, it is the
output.** Product naming is the clean example: generating options is nearly free,
and picking the winner is the entire job. More agents produce a larger pile of
fluent candidates without making the final call any cheaper. The test that catches
this is comparative - **is verifying cheaper than generating?** - and taste work
fails it by definition.

Two boundaries keep the term precise. Taste work is not the same as
**hard-to-verify** work: a legal summary has a right answer that is expensive to
check, and a better-designed check can sometimes fix that; taste work has no right
answer to check against, because the choosing defines what is right, and no check
design fixes that. And it does not mean AI is useless there: it can generate the
options and argue the trade-offs. It means AI cannot **scale** it - thirty options
cost the same to judge as ten - so the judgement stays human (yours, or a trusted
second read), and the routing consequence is chat or by hand, never a fleet.

## The three forms, and how they shrink the gap

Every check is one of these, or a layering of them. This is the canonical statement;
[[routing-work-to-agents]] and [[mm-verification]] summarise it and are corrected
from here.

| Form | Catches | Fails when |
|---|---|---|
| **Deterministic** | Mechanical. Does it run, does it reconcile, do the citations resolve. | There is nothing to assert against, or the question needs meaning. |
| **Agent eval** | Semantic, at volume. On brief, self-consistent, claim actually supported. | It shares the worker's model or its information, so it confirms the error. |
| **Human judgement** | Whether it is the right thing at all, whether it matches what you know, whether the framing is acceptable. | Volume. It degrades quietly, not loudly. |

**Deterministic checks are the strongest form**, because they cannot be wrong in the
same direction as the work. A test that runs, a number that reconciles, a schema that
validates, a link that resolves.

**An agent eval counts only if it can fail independently.** If the eval agent shares
the worker's model, context and blind spot, it certifies the error instead of
catching it. Independence comes three ways: a different model, different source
information, or a ground truth to compare against. Information independence is the
one people skip, and it is free.

**Human judgement is the irreducible layer.** Whether this is the right thing at
all, whether it matches what you know to be true, whether the framing is acceptable.
No other layer can do this, and its failure mode is the volume mechanism this whole
article describes.

**The layering is how the gap gets shrunk.** The generation-verification gap you
personally pay is not a fixed property of the work: it is the residual left for
human judgement after the cheaper layers have caught what they can. Every assertion
moved into a deterministic check, and every criterion an independent eval can grade,
narrows what remains for you to judge. That is what keeps attention sub-linear to
volume, and it is why building the verification layers is not overhead on the work
but the mechanism that makes the volume ownable at all. Layer cheapest first, and
spend judgement only where it discriminates.

**If you cannot name which of the three you would use, you do not have a check.**

The practical tactics for building each layer, ordered by leverage, are in
[[verification-tactics]].

## Where this applies

Beyond choosing how to route work, this is live wherever generated volume lands on
you as the reviewer:

- **Splitting work across agents** - the original case, in [[routing-work-to-agents]],
  where an unverifiable split is worse than no split.
- **Long generated documents you commissioned** - registers, matrices, scoring
  frameworks and research briefings, which is the same instinct the
  overanalysis check exists to catch upstream.
- **Anything fluent in a domain you do not know well**, where template blindness and
  absent ground truth compound.
- **Work that will be acted on by someone else**, where a rubber stamp transfers
  unearned confidence rather than merely holding it.

Related: [[system-1-thinking-and-ai-options]] argues the upside of keeping the human
in the loop on AI-generated options. This article is the constraint on that argument.
Being in the loop is only worth something while you are still genuinely reading.

## Sources

[Jason Wei, Asymmetry of verification and verifier's law](https://www.jasonwei.net/blog/asymmetry-of-verification-and-verifiers-law),
[Weaver: shrinking the generation-verification gap (Stanford)](https://arxiv.org/abs/2506.18203),
[The Verification Horizon: the asymmetry reversing for coding agents](https://arxiv.org/abs/2606.26300),
[Parasuraman on automation complacency](https://github.com/brennhill/looprails/blob/main/article-automation-bias.md),
[the HITL rubber-stamp problem](https://tianpan.co/blog/2026-04-15-human-in-the-loop-rubber-stamp),
[Sonar's verification-gap survey](https://www.sonarsource.com/company/press-releases/sonar-data-reveals-critical-verification-gap-in-ai-coding/),
[human oversight and overload (arXiv)](https://arxiv.org/pdf/2606.05770),
[automation bias in medical decision-making (arXiv)](https://arxiv.org/pdf/2411.00998).

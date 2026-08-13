---
type: reference
created: 2026-08-13
updated: 2026-08-13
status: active
---

# Routing Work to Agents

This decides one thing: how to run a piece of work. There are four answers. Paste it
into chat, give it to one agent, split it across several agents, or do it by hand
yourself.

It came from reverse-engineering Nate B Jones's One-Minute Test in August 2026, then
correcting the places where that tool's own logic turned out to be wrong or blind.

Use it before setting up any substantial piece of AI work: walk the four questions
in the ladder below, in order. The sections after that explain why the answers fall
where they do, and the numbers near the end are only needed when a case sits right
on a line.

Two companions. [[routing-work-mental-model]] is the same model stripped to
one screen of statements, for recall once you already understand it.
[[routing-work-to-agents-evidence]] holds the test data behind every claim made
here.

## Key Takeaways

- **Split on need, not on size.** Big work still goes to one agent when there is
  nothing to separate, and small work still faces the check when there is.
- **Never split what you cannot check.** An unverifiable split is worse than no
  split, because you end up with volume you cannot trust.
- **Never build what will not repeat or will not matter.** Either one alone is
  enough. Middling at both is fatal.

## The ladder

Four questions. The first one branches, the last one applies to everything.

1. **Does this work need to be done by minds that cannot see each other?**
   That is the first question. Not how big the job is.
2. **If yes, can you check the results cheaply?**
   No, so do it by hand. Yes, so split it across **several agents**.
3. **If no, does the whole job fit in one window?**
   Yes, so paste it into **chat** and you are finished. No, so give it to
   **one agent**.
4. **Then, for anything you are about to set up: does it repeat often, or does it
   matter a lot?** Neither, so do it by hand this once. Chat is exempt from this
   one.

## The three rules in full

### Split on need, not on size

Size is the wrong question and it fails in both directions.

**Big never means many.** A job at maximum size with nothing to separate still
routes to a single agent. Volume is a reason to give an agent a longer leash, not a
reason to hire more agents. Reaching for a fleet because the work looks large is the
instinct this whole model exists to kill.

**Small does not protect you.** The mirror image, and the half nobody expects. A
twenty-minute job that genuinely needs separate minds goes straight into split logic
and faces exactly the same check as a huge one. Being quick is not a reason to skip
the verification question.

So what is the need? Two things at once: parts that can genuinely be worked
independently, **and** a reason they should not see each other's work. The second is
the one people drop. Wanting things done in parallel is not separation, it is
impatience.

**The test to apply:** ask what would actually go wrong if a single mind did all of
it and saw everything. If the honest answer is "nothing, it would just take longer",
you do not have a split. You have one agent and a bigger brief.

### Never split what you cannot check

Every other failure in this model demotes you gracefully. Fail the separation
question and you get one agent. Fail the size question and you get chat. Fail the
check and you do not drop a rung, you fall off the ladder entirely and end up doing
it by hand.

That asymmetry is deliberate and it is worth understanding. A split multiplies the
output you have to trust. One agent produces one thing you can read before it
counts. Five agents produce five, and if you cannot verify them cheaply you are not
getting leverage, you are getting a large volume of confident work of unknown
quality. That is why **high separation with a weak check is worse than low
separation**: the more successfully you split, the more unverified output you
generate.

**The practical consequence:** decide how you will check the work before you decide
the architecture. The check is the binding constraint, not the complexity of the
job. If you cannot name the check, you have already answered the question. See
[[#The one move worth remembering]] for what to do about it.

### Never build what will not repeat or will not matter

This one kills work that has passed every other test. A perfectly separable job with
an easy check still gets refused if it happens once and does not much matter.

But the two conditions are alternatives, not a combined score. Either one alone
rescues it:

- A genuinely valuable one-off earns the setup, even if you never run it again.
- A low-value job you run constantly earns it too, because the setup amortises.

**What fails is being middling at both**, and this is the part that catches people
out, because moderate value plus moderate frequency feels like it should add up to a
pass. It does not. Two separate bars, and you have to clear one of them outright.

**The test to apply:** if you are hesitating, you are probably in the middling zone.
Do it by hand this once, and let the second or third occurrence make the case for
building it.

## What the model cannot see

Hold these yourself. Nothing in the four questions asks about them.

- **Blast radius.** Cheap-to-check and catastrophic scores identically to
  cheap-to-check and trivial. There is no lever for how bad being wrong is.
- **Intrinsic check cost.** The model treats verification as a volume problem. One
  output can still be genuinely hard to check: a legal summary, a financial model,
  a confident claim in a domain you do not know. One output is not the same as
  inspectable. Ask which kind of hard-to-check you are facing.
- **Latency and cost.** No lever for either.

Related to the second point: in single-agent mode the source tool reports the check
as affordable at every value including zero, so substantial unverifiable work routed
to one agent is the quadrant where you are told everything is fine. The check
question is only asked of splits, so ask it yourself of everything else.

## Why verification is the bottleneck

This is the reason the check is a hard gate rather than a preference, and it is the
most important section in this document.

Generation scaled and verification did not. The capacity to produce work has gone up
by orders of magnitude; the capacity to confirm it is correct is still one human
reading one thing at a time. Every rule above follows from that asymmetry.

The burden goes by several names depending on who is writing: the **verification
gap**, **review fatigue** or **approval fatigue**, and in older human-factors
research **automation bias** and **automation complacency**. The last two are the
useful ones, because they are decades old, they come from aviation and clinical
medicine rather than from anyone selling a tool, and they describe the mechanism
rather than the symptom.

Three findings from that literature matter here.

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

The failure mode is not that you catch fewer errors. It is that **you keep believing
you are checking while you have stopped**, and the record still says the work was
reviewed. Oversight quietly becomes a rubber stamp, which is worse than no oversight
because it manufactures confidence. Reviewing AI output also invites skimming in a
way human output does not: it is fluent, consistently formatted and structurally
repetitive, so it reads as correct, a habit sometimes called **template blindness**.

Two consequences for routing.

**"I'll review it" is not a check.** It is an intention, and it degrades under
exactly the volume that splitting the work creates. That is why the check has to be
a thing you build rather than a thing you resolve to do, and why the bar sits above
the midpoint: anything you cannot name counts as a fail.

**This is what makes an unverifiable split worse than no split.** It does not just
leave errors uncaught. It produces fluent, plausible, high-volume output that
consumes the attention you would need to catch them, and returns a feeling of
progress either way.

Sources:
[Parasuraman on automation complacency](https://github.com/brennhill/looprails/blob/main/article-automation-bias.md),
[the HITL rubber-stamp problem](https://tianpan.co/blog/2026-04-15-human-in-the-loop-rubber-stamp),
[Sonar's verification-gap survey](https://www.sonarsource.com/company/press-releases/sonar-data-reveals-critical-verification-gap-in-ai-coding/),
[human oversight and overload (arXiv)](https://arxiv.org/pdf/2606.05770),
[automation bias in medical decision-making (arXiv)](https://arxiv.org/pdf/2411.00998).

## What counts as a check

Not specifically an agent-run eval. "Can you check it" is about the **cost of
verification**, whoever or whatever performs it. The test is whether that cost stays
flat as the work multiplies, rather than consuming your attention one output at a
time. Three things achieve that.

**Deterministic checks.** A test that runs, a number that reconciles, a schema that
validates, a link that resolves. The strongest kind, because they cannot be wrong in
the same direction as the work.

**Agent-run evals.** A separate agent grading the output against criteria. These
count, but they are the weakest by default, and the reason matters. If the eval
agent shares the worker's model, context and blind spot, it certifies the error
instead of catching it. A check that fails in the same direction as the thing it
checks is not a check. It earns the name only if it can fail independently: different
information, different criteria, or a ground truth to compare against. Independence
is not just a property of the workers. It applies to the verifier too.

**Human judgement.** The irreducible layer. Whether this is the right thing at all,
whether it matches what you know to be true, whether the framing is acceptable. No
other layer can do this, and its failure mode is volume, which it meets quietly
rather than loudly.

Which means human judgement has to be made affordable by design rather than by
resolve. Require source citations you can click, so you verify three of thirty and
trust the pattern. Structure the output so a wrong answer looks wrong. Sample rather
than sweep. The aim is to keep your attention sub-linear to the volume, because
attention spent on things the first two layers would have caught is attention you no
longer have for the judgement calls.

**Most real checks combine all three, layered cheapest first.** Deterministic where
something can be asserted, agent eval where meaning has to be judged at volume, your
own judgement reserved for what only you can settle. If you cannot name which of the
three you would use, you do not have a check.

## The one move worth remembering

When work lands on *by hand* because you cannot check it, the instinct is to
simplify the work, cut the scope, reduce the separation. That is the wrong move.

**Build the check instead.** Every other input is a property of the task, which you
can only observe. The check is a property of your setup, which you construct. Moving
it converts *by hand* straight into *several agents* without changing the work at
all, and no other input in the model offers that.

## The numbers, if a case feels borderline

This is the source tool's arithmetic, on its 0 to 100 sliders. Skip it unless a case
sits right on a line.

- **How much it wants splitting** = (0.6 x how separable the parts are) + (0.4 x how
  much they need to not see each other). Separability counts for one and a half
  times as much. Above roughly 50 and you are a split candidate, whatever the size.
- **How easy it is to check must clear 60** before a split is allowed. A fixed bar,
  unrelated to anything else, and set above the midpoint on purpose, so anything
  ambiguous counts as a fail. The burden of proof sits on the check.
- **Size only sorts work that is not splitting.** Below 36 it goes to chat, which is
  also exempt from the repeat-or-matter test. From 40 up, that test is live.
- **Repeat-or-matter passes at recurrence above roughly 33, or value above roughly
  48.** Two separate bars, either one sufficient, and no adding them together.

## Status

As of 13 Aug 2026: the split formula and the checkability bar are confirmed by
repeated testing across widely spaced inputs. The economic veto is confirmed as
universal (it kills a fully qualified split), but the OR rule and its two thresholds
are fitted to a partial grid and should be treated as provisional until the
compensating cases are tested. Whether the size-40 economics trigger also applies
inside split mode is untested. The blind spots listed above are corrections to the
source tool, not findings from it.

Full test data, including the two observations that overturned the original model,
is in [[routing-work-to-agents-evidence]]. Source analysis sits at
`raw/Nate B Jones one-minute-test analysis.md`, not yet compiled into the wiki.

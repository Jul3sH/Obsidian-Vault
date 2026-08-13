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

Companion: [[routing-work-mental-model]] is the same model stripped to one screen of
statements, for recall once you already understand it.

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

The check is a hard gate rather than a preference for one reason: generation scaled
and verification did not. The capacity to produce work has gone up by orders of
magnitude; the capacity to confirm it is correct is still one human reading one thing
at a time. Every rule above follows from that asymmetry.

The full principle, the automation-bias research behind it, and the other places it
applies are in [[verification-bottleneck]]. Two consequences for routing
specifically.

**"I'll review it" is not a check.** It is an intention, and it degrades under
exactly the volume that splitting the work creates. That is why the check has to be
a thing you build rather than a thing you resolve to do, and why the bar sits above
the midpoint: anything you cannot name counts as a fail.

**This is what makes an unverifiable split worse than no split.** It does not just
leave errors uncaught. It produces fluent, plausible, high-volume output that
consumes the very attention those errors required, and returns a feeling of progress
either way.

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
  ambiguous counts as a fail. The burden of proof sits on the check. It is an
  absolute bar, not a comparison against the split score: a case can beat its own
  split score on checkability and still fail.
- **Size only sorts work that is not splitting**, into three bands: chat below 36,
  one agent from 36 to 39, and one agent again from 40 up. The bands matter for one
  reason only. **Repeat-or-matter is consulted in the top band alone**, so anything
  below 40 passes zero recurrence and zero value untouched. And 40 is where that
  question starts being asked, not where it fails: a large job with both levers at
  the midpoint still routes to one agent.
- **Repeat-or-matter passes at recurrence above roughly 33, or value above roughly
  48.** Two separate bars, either one sufficient, and no adding them together.
  Recurrence is the easier bar to clear, at about two thirds of the value threshold.

### Spend Pressure is a display, not a gate

The tool shows a Spend Pressure score with a Low/Moderate/High label. **It decides
nothing.** A case showing Moderate 49 fails while a case showing High 65 passes, which
rules out any threshold reading of it.

What it represents: roughly the total work the job implies, discounted by how valuable
it is. A cost-justification readout, which is why it moves with almost everything and
gates nothing.

What changes it, per unit of each input:

| Input | Effect |
|---|---|
| Size | about +0.35, the strongest driver |
| Recurrence | about +0.25 |
| Value | about **-0.16**, higher value *lowers* displayed pressure |
| Separation | about +0.15 |
| Independence | about +0.11 |
| Checkability | none at all, confirmed flat across a full sweep |

Fitted: `28 + 0.35(Size) + 0.15(Sep) + 0.11(Indep) + 0.25(Recur) - 0.16(Value)`. This
reproduces every recorded observation within about a point, but the Separation and
Independence coefficients are soft, as no deliberate single-lever sweep was run for
them.

**The practical point is the minus sign on Value.** Two jobs of identical size and
frequency display different pressure purely because one is worth more, so a high
reading can mean "this is big" or it can mean "this is not worth much". It is not a
warning, and it is not an input to any of the four questions.

## Status

As of 13 Aug 2026: the split formula and the checkability bar are confirmed by
repeated testing across widely spaced inputs, the blend formula exactly across seven
observations and the checkability bar at three widely separated split scores. The
economic veto is confirmed as universal (it kills a fully qualified split), but the
OR rule and its two thresholds are fitted to boundary cells only and are provisional.

**One test would settle the OR rule:** recurrence 30 with value 45, both just short
of their bars. OR predicts it fails; any additive rule predicts it passes. Two
smaller gaps remain: the split threshold is known only to sit somewhere between 51
and 56, and whether the size-40 economics trigger also applies inside split mode is
untested.

The blind spots listed above are corrections to the source tool, not findings from
it. The tool encodes its whole state in the URL fragment, in the order
`#Size.Independence.Separation.Checkability.Recurrence.Value`; setting states by URL
rather than dragging sliders is how the rules above were measured and how to resume.
Source analysis sits at `raw/Nate B Jones one-minute-test analysis.md`, not yet
compiled into the wiki.

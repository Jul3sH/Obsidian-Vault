---
type: reference
created: 2026-08-13
status: active
---

# Routing Work to Agents

This is the decision model for choosing how to run a piece of work: paste it into
chat, hand it to one agent, split it across several, or do it by hand. It was built
by reverse-engineering Nate B Jones's One-Minute Test through systematic slider
testing in August 2026, then corrected where the tool's own logic proved wrong or
blind. Read it before setting up any substantial piece of AI work and walk the four
questions in order. The numbers at the bottom are only needed when a case feels
borderline.

## Key Takeaways

- **Size gets you out of chat. Separation gets you to a split. Checkability licences
  the split. Recurrence pays for it.**
- Big never means many. A huge job with nothing to separate goes to **one** agent.
- A failed split does not fall back to one agent. It falls back to your hands.
- Checkability is the only input that describes you rather than the work, so it is
  the only one you can move.

## The ladder

Four questions, in order. Stop at the first failure.

1. **Does it fit in one window?** Yes, then **chat**. Nothing else is consulted.
2. **Does it need genuinely separate minds?** No, then **one agent**.
3. **Can you check the output at volume?** No, then **by hand**.
4. **Does it recur often enough to be worth building?** No, then **by hand**.

All four clear, then **several agents**.

## The four things that surprise you

**Big never means many.** Size only decides whether you leave the chat window. A
job at maximum size with no separation still routes to a single agent. Reaching for
multiple agents because the work is large is the instinct this model exists to kill.

**A failed split drops off the ladder, not down it.** Fail the size question and you
get chat. Fail the separation question and you get one agent. Both are graceful.
Fail the check and you get *do it by hand*, which is not a rung at all. High
separation with a weak check is actively worse than low separation, because you end
up with volume you cannot trust.

**Two different failures both land on "by hand", and they need opposite fixes.**
Cannot check it, so build the check. Will not repeat, so just do it this once and
stop designing.

**Checkability only bites once you are splitting.** Below the split line it is inert,
and worse than inert: the tool reports the check as affordable at the exact settings
where it is not. Substantial work, single agent, unverifiable output is the quadrant
where you get told everything is fine.

## What the model cannot see

Hold these yourself. Nothing in the four questions asks about them.

- **Blast radius.** Cheap-to-check and catastrophic scores identically to
  cheap-to-check and trivial. There is no lever for how bad being wrong is.
- **Intrinsic check cost.** The model treats verification as a volume problem. One
  output can still be genuinely hard to check: a legal summary, a financial model,
  a confident claim in a domain you do not know. One output is not the same as
  inspectable. Ask which kind of hard-to-check you are facing.
- **Latency and cost.** No lever for either.

## The one move worth remembering

When work lands on *by hand* because you cannot check it, the instinct is to
simplify the work, cut the scope, reduce the separation. That is the wrong move.

**Build the check instead.** A test, an eval, a required source citation, a reviewer
who can spot-check in minutes. Every other input is a property of the task that you
observe. Checkability is a property of your setup that you construct, and moving it
converts *by hand* straight into *several agents* without changing the work at all.

## The numbers, if a case feels borderline

On 0 to 100 sliders:

- **Split need = (0.6 x separation) + (0.4 x independence).** Separation is worth
  1.5 times independence. Above roughly 50 you are a split candidate.
- **Checkability must clear 60** to licence the split. A fixed bar, not relative to
  anything else, and set above the midpoint deliberately, so ambiguous counts as
  fail. The burden of proof sits on the check.
- **Below size 36** everything is chat. **From size 40 up** the economics can veto.

## Status

As of 13 Aug 2026: the split formula and the checkability bar are confirmed by
repeated testing across widely spaced inputs. The economic veto's exact rule is not
yet measured, and whether it can kill a *several agents* verdict rather than only a
*one agent* one is still open. The blind spots listed above are corrections to the
source tool, not findings from it.

Source analysis sits at `raw/Nate B Jones one-minute-test analysis.md`, not yet
compiled into the wiki.

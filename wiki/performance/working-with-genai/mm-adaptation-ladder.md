---
type: reference
created: 2026-08-23
status: active
tags: [working-with-genai, model-adaptation, mental-models]
---

# MM: Adaptation Ladder

This is the Adaptation Ladder mental model: when a model's output is not good
enough, deciding whether the fix is giving it better information or changing how
it behaves, and how far up the cost ladder you are allowed to climb. It was
written because [[mm-routing]] chooses the architecture and [[mm-steering]]
configures it, but neither asks what kind of shortfall you are actually looking
at. Read it the moment you are tempted to reach past the prompt.

**One-liner:** Ask whether the model is missing information or missing a habit,
then climb one rung at a time.

**Reach for it when:** a model's output is not good enough and you are choosing
what to change.

**Position in the chain:** after steering. Verification decides what is possible,
routing decides the architecture, steering configures it; the adaptation ladder is
what you reach for when steering has run out and the answer is still wrong.

## Key Takeaways

- One question routes the whole decision: is the gap knowledge or behaviour?
- Missing or stale facts go to retrieval. A format or reasoning pattern the model
  will not hold goes to weights.
- Teaching facts by fine-tuning is the most-cited mistake in the area: slower,
  costlier, less accurate, and a wrong fact then needs a retrain rather than a
  document edit.
- You cannot claim a rung failed without a measurement, so evals are the
  prerequisite for climbing, not the follow-up.
- Each rung up costs more to set up and more to change your mind about. Climb only
  on evidence.

## Principles

- **Knowledge or behaviour is the first cut, and it is usually obvious.** If the
  model would be right given the document in front of it, the gap is knowledge and
  the fix is retrieval. If it has everything it needs and still writes it wrong,
  the gap is behaviour.
- **Start at prompting and mean it.** Zero infrastructure, instant iteration, and
  it is the baseline everything above must beat. Most teams who climbed early
  regretted it, and the regret is expensive because the rung above locks in
  whatever the model was already doing wrong.
- **A rung is only exhausted if you measured it.** "Prompting did not work" without
  an eval is a feeling. This is where the ladder meets [[mm-verification]]: the
  check is what licenses the escalation, and without it the climb is taste.
- **Cost is a legitimate reason to climb, and a different one.** Making a smaller
  model do a bigger model's job at volume is a real trigger, separate from quality.
  Price it rather than assume it: caching a repeated prefix often removes the cost
  argument entirely.
- **The rungs compose.** Fine-tune for stable behaviour and retrieve for volatile
  fact is the production shape for high-stakes work, not an admission that one
  rung failed.

| The gap looks like | The rung | Reach past it when |
|---|---|---|
| Wording, structure, missing examples | Prompting and few-shot | Measured and still wrong |
| Facts it does not have, or that change | Retrieval | The facts are right and the output still is not |
| A habit it will not hold, at volume | Weight change (PEFT first) | Rarely, and never for facts |
| Both at once, high stakes | Hybrid | It is the destination, not the fallback |

## Guidelines

- Write the failing examples down before choosing a rung. The pattern in them
  usually names knowledge or behaviour for you.
- Check availability before choosing: frontier closed models are not fine-tunable
  through their primary APIs, so "fine-tune" can quietly mean "change model
  family".
- Anything the fine-tune bakes in ages silently, so a weight change that carries
  facts needs drift monitoring attached at the same time.
- Prefer the reversible rung. A prompt change is undone in a minute, a retrain is
  not.
- Below sustained volume, the cheaper rung stays cheaper. Compute the crossover
  for your own workload rather than copying a published figure.

## Limitations

The model assumes the shortfall is real and measured; it has no view on whether
the task was worth doing or whether the output can be checked at all. It is also
tied to the current shape of the market: the availability of fine-tuning, the
price of caching, and the relative strength of retrieval all move, and a rung that
is uneconomic this year may not be next. It says nothing about blast radius
([[mm-blast-radius]]) or token cost over a session
([[mm-token-economics]]).

## Detail

[[model-adaptation]] (the full technique table, the evidence, and what is
contested), [[evals]] (the measurement that licenses each step up). If this model
and those articles disagree, the articles win and this file is corrected.

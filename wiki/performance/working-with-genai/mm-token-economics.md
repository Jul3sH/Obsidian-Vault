---
type: reference
created: 2026-08-17
status: active
tags: [working-with-genai, token-economics, mental-models]
---

# MM: Token Economics

This is the Token Economics mental model: what a session actually costs to run,
and which of your habits move that number. It was written after a session in which
loading reference material on a cheap model and then switching to an expensive one
turned out to move cost rather than remove it. Read it before loading a lot of
material into a session, switching models mid-session, or deciding whether to keep
a long session going.

**One-liner:** Context is rent, not a purchase.

**Reach for it when:** you are about to load a lot of material into a session,
switch models part-way through, or wonder why a long session has become expensive.

**Position:** alongside the chain rather than in it. Verification decides what is
possible, routing decides the architecture, steering configures it; token economics
prices what routing chose. It rarely changes the verdict, but it changes how you
execute it.

## Key Takeaways

- A session has two cost curves: a **fixed prefix** re-read every turn, and a
  **transcript** that only ever grows. Only the second one compounds.
- You pay for the whole transcript on **every turn**, not once when it loads.
- Caching discounts that re-read to roughly a tenth. It does not remove it.
- The discount is per-model and prefix-shaped, so switching models, or changing
  anything early, throws it away.
- Delegation beats switching: a subagent's reading never enters your transcript.
- The cheapest context is the context you never loaded.

## Principles

- **The API is stateless; the transcript is the state.** Nothing persists between
  turns on the provider's side, so the entire conversation is resent each time.
  Context is therefore a *recurring* cost proportional to session length, not a
  one-off charge at load time.
- **A session has two cost curves, and only one of them compounds.** The fixed
  prefix is re-read every turn but stays roughly constant in size; the transcript
  grows with everything you do. Trimming the prefix has a hard ceiling; controlling
  what enters the transcript does not.
- **Breadth is cheap, depth is not.** Capabilities are declared cheaply and loaded
  in full only when used, so *having* a large tool and skill surface costs almost
  nothing while *reaching into it* costs a lot. The trap is that the charge is a
  one-way deposit, permanent for the rest of the session, and it lands at the moment
  you were thinking about the question rather than the cost.
- **Caching is a prefix match, so cost is shaped by order, not just volume.**
  Content is cached from the start of the prompt up to a breakpoint. Anything that
  changes early invalidates everything after it, however stable that later content
  is. Stable material belongs at the front, volatile material at the back.
- **The discount is per-model.** Switching model invalidates the cache entirely.
  The first turn on a model is a cold, full-price read of the whole transcript, plus
  a premium to write the new cache.
- **Switch cost scales with transcript length.** Switching at turn three is nearly
  free; switching at turn sixty is not. Any plan that loads material *first* and
  switches *after* has the order backwards.
- **A subagent has its own context and returns only its answer.** This is the one
  mechanism that buys cheap bulk work without depositing the bulk in your transcript.
- **A cheap model is not cheap if you keep its reading.** Exploring on a cheap model
  still leaves every file it opened in the transcript, where the expensive model
  pays for it on every subsequent turn.

## Guidelines

- Pick one model per session and delegate the grinding, rather than swapping under
  yourself.
- If you must switch, switch early, while the transcript is still small.
- Treat a fresh session as a legitimate optimisation. Once a transcript stops
  earning its keep, starting again beats any tactic applied inside it.
- Keep the stable prefix stable. It sits at the front of every request, so changing
  it mid-session is the most expensive edit available.
- Watch what loads in bulk. A large skill invocation or a big file read is permanent
  for that session, so notice it as it happens rather than afterwards.
- Put summaries in the transcript, not raw material.

### Illustrative numbers (Anthropic API list prices, source table cached 24 Jun 2026)

Recorded 17 Aug 2026 from a cached reference rather than a live pricing check, so
verify before relying on a figure. Treat these as shape rather than fact.

| Item | Cost |
| --- | --- |
| Cache read | ~10% of normal input price |
| Cache write | 1.25x input (5-minute TTL), 2x (1-hour TTL) |
| Haiku 4.5 | $1 / $5 per million tokens in / out |
| Sonnet 5 | $3 / $15 ($2 / $10 introductory to 31 Aug 2026) |
| Opus 5 | $5 / $25 |
| Fable 5 | $10 / $50 |

One timing trap worth carrying: cache entries expire, so switching *back* to a model
within the window costs only the turns added since you left it, while switching back
after expiry costs the whole transcript again.

## Limitations

This model prices options; it does not choose between them. Whether the cheaper
model is *good enough* is [[mm-routing]]'s question, and whether the output can be
checked at all is [[mm-verification]]'s. Optimising tokens on work that should not
have been commissioned is the expensive mistake, not the cheap one.

It also assumes per-token billing. Subscription plans meter usage differently; the
relative shape holds, but absolute figures do not map across.

## Detail

[[session-context-loading]] holds the mechanics this model prices: what assembles at
session start, what loads lazily, what is never auto-loaded, and what grows the
transcript irreversibly. Go there for how it works; stay here for what it costs.

Efficiency tactics accumulate in this file until there are enough to warrant their
own article. If this model and the mechanics article disagree, the article wins and
this file is corrected.

---
type: reference
created: 2026-09-04
status: active
tags: [finance, airmiles, mental-models]
---

# MM: Airmiles Redemption

This is the Airmiles Redemption mental model: how to decide whether a rewards
flight is worth booking with miles, and how far to push a miles-plus-cash
slider. It was created (4 Sep 2026) from Julian's BA Avios analysis of a
Bangkok to London booking. Consult it whenever a rewards flight is being considered, on
any scheme. Scheme-specific numbers, worked examples, and cancellation terms
live in the per-scheme detail files ([[ba-avios-redemption]] for BA Avios;
Asia Miles and others to be added as they are used); if this model and a
detail file disagree, the detail file wins.

**One-liner:** Judge each redemption by the cash fare you avoid, not by the
number of flights you can spread miles across.

**Reach for it when:** considering booking any flight with airmiles or points,
or choosing between the options on a miles-plus-cash slider.

## Key Takeaways

- Value per mile = (cash fare you would realistically buy - cash co-pay on the
  award ticket) / miles used. Plan at roughly **1p per Avios**; each scheme's
  detail file carries its own calibrated default.
- Check cash first: if the award's cash co-pay is near, equal to, or above the
  real cash fare, pay cash and keep the miles.
- Value each **slider increment**, not the total: stop adding miles once the
  next increment saves cash below your target rate. The maximum-miles option
  is frequently the worst value.
- Miles earn their keep on expensive dates and premium cabins; cheap Economy
  almost never justifies them.
- Run it as [[mm-work-types]] Analysis: paste every miles+cash option and
  cash fare into the chat, let the LLM compute the arbitrage, and keep the
  logic-check and judgement calls yourself.

## Principles

- **Core calculation:** value per mile = (realistic cash fare - cash co-pay) /
  miles used. Redeem at or above the scheme's target value; hold the miles
  below it unless flexibility or conserving cash is worth more at the time.
  *Why:* miles have no fixed cash value, so a redemption is not "points
  converted to cash at some rate". It is an **arbitrage between two prices for
  the same seat**: what the airline charges in cash, and what it charges in
  miles plus co-pay. The redemption is worth exactly the cash it stops you
  spending, so value appears wherever those two price lists diverge, and
  disappears where they track each other.
- **The benchmark is the fare you would actually buy.** Same route, dates,
  cabin, baggage, passenger count, and fare conditions. Never compare an award
  against an expensive fully flexible fare you would never purchase.
  *Why:* the arbitrage is only real if the cash side of it is real. Money you
  were never going to spend is not money avoided, so benchmarking against an
  inflated fare manufactures value that does not exist and makes a poor
  redemption look good.
- **Cash-first check:** before analysing any slider, compare the award's cash
  co-pay against the straight cash fare. If the co-pay alone approaches the
  cash price, the award costs more cash *and* consumes miles.
  *Why:* an award is a purchase in two currencies at once. If the cash
  component by itself already buys the ticket, the miles handed over on top
  are a pure loss, whatever nominal rate they convert at. No arbitrage exists
  on that booking; the check costs seconds and screens it out before any
  slider analysis is wasted on it.
- **Incremental slider valuation:** incremental value = (reduction in cash
  co-pay) / (extra miles used). Choose the last step that still converts miles
  to cash savings at your target rate or better; steps beyond it often return
  half the target value.
  *Why:* the slider is not one deal, it is a series of separate mile-for-cash
  exchanges, each at its own exchange rate, and the rate usually worsens as
  you slide. Judging the total averages a few good exchanges with several bad
  ones, so the blended number hides that the last steps are selling your
  miles cheap. Buy the good exchanges and refuse the bad ones.
- **A premium cabin can beat cheap Economy on the same itinerary.** The award
  is priced against the cabin's cash fare, so the cabin with the biggest gap
  between cash fare and co-pay wins, not the cheapest seat.
  *Why:* airlines price cash cabins steeply (Premium Economy or business at
  multiples of Economy) but award pricing climbs far more gently, so the
  divergence between the two price lists is widest in the premium cabins.
  In the Bangkok to London example, moving up to Premium Economy cost roughly HK$6,188
  in cash but only 5,500 Avios + HK$1,557 via the award: the upgrade itself
  was the arbitrage.
- **Flexibility is a real benefit with a real price.** Cancellable award
  bookings justify a slightly lower per-mile result, but flexibility must
  never turn an otherwise poor redemption into a routine use of points.
  *Why:* an award normally returns the miles and cash for a small fee if
  cancelled, an option a cheap non-refundable cash fare does not carry, and
  that option is genuinely worth something when plans are uncertain. But it
  is a tie-breaker between decent redemptions, not a rescue: if it routinely
  excuses sub-1p value, it has quietly become a licence to burn miles badly.

## Guidelines

1. Value miles at the scheme's planning rate (1p per Avios) before looking at
   any specific booking.
2. Check the equivalent cash fare first.
3. Calculate value per mile using the fare avoided minus the award's cash
   co-pay.
4. Use the slider only up to the last increment worth the target rate.
5. Pay cash for cheap Economy; reserve miles for peak dates, premium cabins,
   partner awards, and one-ways with disproportionate cash fares.
6. Before booking, check the cancellation cost and decide between a return
   award and two one-ways based on which direction(s) might change.

**Human/LLM split.** Running this model on a live booking is
[[mm-work-types]] **Analysis** work: the machine derives the numbers, the
judgement and the check stay human.

- **The LLM calculates and compares.** Paste the raw options into the chat
  session: every miles+cash slider point per cabin, for each airline being
  considered, plus the realistic cash fares. GenAI is very effective at
  computing value-per-mile, the incremental slider rates, and the best
  arbitrage across cabins and schemes from that input, applied against this
  model.
- **You review and decide.** Check that the calculation logic holds and is
  aligned with this model (right benchmark fare, incremental slider values
  rather than blended totals, cash-first check actually run), and that the
  pasted inputs were read correctly. The calls no calculation settles stay
  yours: which fare you would genuinely buy, what flexibility is worth on
  this trip, and whether conserving cash beats redeeming today.

## Limitations

Calibrated (Sep 2026) on a single scheme, BA Avios, and a single worked
booking; the thresholds are Julian's planning defaults, not market truths, and
each new scheme needs its own detail file with its own rates. The model says
nothing about *earning* miles, scheme devaluations, or status benefits, only
about spending what is already held. Cancellation and co-pay mechanics are
scheme-specific and change; verify against the scheme's current terms at
booking time.

## Detail

[[ba-avios-redemption]] (BA Avios: value thresholds, slider worked examples,
cash-first comparisons, cancellation terms). Per-scheme files for Asia Miles
and others will be added here as they are analysed.

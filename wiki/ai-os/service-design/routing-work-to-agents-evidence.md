---
type: reference
created: 2026-08-13
status: active
---

# Routing Work to Agents: Evidence

This is the test record behind [[routing-work-to-agents]]. It holds every
observation taken from Nate B Jones's One-Minute Test during the 13 Aug 2026
investigation, the formulas fitted to them, the claims from the original analysis
that testing overturned, and the questions still open. Read the model article for
the decision rules; come here only to check what a rule rests on, to settle a
disagreement about a number, or to pick up the investigation where it stopped.

Sections: **Method** (how states were set), **Confirmed rules** (five findings with
their data), **Spend Pressure** (a display, not a gate), **Superseded claims** (what
the original analysis got wrong and why), **Open questions** (what to run next).

## Method

The tool encodes its full state in the URL fragment, in this order:

```
#Size.Independence.Separation.Checkability.Recurrence.Value
```

Confirmed against the original real-world case `#73.90.58.82.70.74`. States were set
by URL rather than by dragging sliders. Every observation records the verdict, the
verbatim "why" sentence including its bracketed numbers, the Spend Pressure label
and score, and whether the map dot rendered solid or hollow.

The bracketed numbers in the why text are the tool reporting its own internal state.
They were more informative than the verdicts and are the reason the blend formula
could be solved exactly.

The four verdicts: **Chat**, **One agent**, **Several agents**, **Don't bother**.
The article renames the last of these *by hand*, which is what the tool's own
description says to do.

## Confirmed rule 1: the blend formula

**Split need = (0.6 x Separation) + (0.4 x Independence)**

A plain weighted average, no intercept. Seven observations, all exact:

| Separation | Independence | Predicted | Tool reported |
|---|---|---|---|
| 58 | 90 | 70.8 | 71 |
| 80 | 50 | 68 | 68 |
| 100 | 50 | 80 | 80 |
| 60 | 50 | 56 | 56 |
| 50 | 50 | 50 | 50 |
| 20 | 50 | 32 | 32 |
| 100 | 100 | 100 | 100 |

Several of these came from tests aimed at something else, which is the strongest
form of confirmation available here. Separation carries 1.5 times the weight of
Independence.

## Confirmed rule 2: the split threshold

Blend must exceed roughly 50 to enter split-evaluation mode. Blend 50 returns One
agent; blend 56 is already in split mode. The exact boundary sits between 51 and 56
and has not been bisected.

## Confirmed rule 3: Checkability is a fixed bar at 60

Three widely spaced blends, all flipping at exactly the same Checkability value:

| Separation | Independence | Blend | Flip point |
|---|---|---|---|
| 100 | 50 | 80 | 60 (59 fails, 60 passes) |
| 80 | 50 | 68 | 60 (59 fails, 60 passes) |
| 60 | 50 | 56 | 60 (59 fails, 60 passes) |

The decisive trace, at blend 56 with Size 73, Recurrence 50, Value 50:

| Checkability | Verdict | Why text |
|---|---|---|
| 40 | Don't bother | "needs separate minds (56) but the check is expensive (40)" |
| 50 | Don't bother | "needs separate minds (56) but the check is expensive (50)" |
| 55 | Don't bother | "needs separate minds (56) but the check is expensive (55)" |
| 56 | Don't bother | equal to the blend, still fails |
| 57 | Don't bother | exceeds the blend, still fails |
| 59 | Don't bother | "needs separate minds (56) but the check is expensive (59)" |
| 60 | Several agents | "splits across minds (56), the check is cheap (60), and it earns setup (50 + 50)" |

Rows 56 and 57 are the important ones. They disprove the original analysis's
`Checkability >= blend` rule directly: Checkability exceeds the blend and the verdict
still fails. The gap between blend and flip point varies (80-60=20, 68-60=8,
56-60=-4), so it is not a constant offset either, and the ratio varies (0.75, 0.88,
1.07), so it is not proportional. It is an absolute bar.

## Confirmed rule 4: Checkability is inert outside split mode

Sweep at Size 73, Separation 50, Independence 50 (blend 50, below the split
threshold), Recurrence 50, Value 50:

| Checkability | Verdict | Why text | Spend Pressure |
|---|---|---|---|
| 0 | One agent | "bounded work (73) with a check you can afford (0)" | High · 58 |
| 10 | One agent | "bounded work (73) with a check you can afford (10)" | High · 58 |
| 25 | One agent | "bounded work (73) with a check you can afford (25)" | High · 58 |
| 40 | One agent | "bounded work (73) with a check you can afford (40)" | High · 58 |
| 50 | One agent | "bounded work (73) with a check you can afford (50)" | High · 58 |

Checkability changes neither the verdict nor the Spend Pressure. Its only effect is
cosmetic: the map dot renders hollow, per the tool's legend "hollow means the answer
is hard to check".

**The why text at Checkability 0 is wrong on its face.** It asserts a check you can
afford while displaying the value that says you cannot, and the same value of 50
reads as "expensive" in split mode. The single-agent branch uses a fixed template
that never evaluates the input. This is why the article carries an explicit warning
about the substantial-work, single-agent, unverifiable quadrant: it is the one case
where the tool actively tells you the opposite of the truth.

## Confirmed rule 5: the economic veto is universal

Recurrence and Value do change verdicts. The original analysis concluded they never
did, because it only ever swept them one at a time with the other held at 50, and a
single lever at zero is survivable.

Two states establish the veto beats everything else in the model:

| State | Verdict | Why text | Spend Pressure | Dot |
|---|---|---|---|---|
| `73.90.58.82.0.0` | Don't bother | "real work (73) that barely recurs (0) for modest value (0)" | High · 58 | Hollow warning |
| `100.100.100.100.0.0` | Don't bother | "real work (100) that barely recurs (0) for modest value (0)" | High · 75 | not captured |

The first passed both the separation gate (blend 71) and the checkability gate
(82, comfortably over 60) and still died. The second had every other lever at
maximum.

### The rule is an OR of two unequal thresholds

Boundary cells, at Size 73, Separation 20, Independence 50 (blend 32, no split),
Checkability 50:

| Recurrence | Value | Verdict | Spend Pressure |
|---|---|---|---|
| 0 | 0 | Don't bother | Mod · 49 |
| 0 | 30 | Don't bother | Mod · 44 |
| 0 | 45 | Don't bother | Mod · 42 |
| 0 | 50 | **One agent** | Mod · 41 |
| 10 | 30 | Don't bother | Mod · 47 |
| 10 | 40 | Don't bother | Mod · 45 |
| 10 | 50 | **One agent** | Mod · 44 |
| 20 | 0 | Don't bother | Mod · 54 |
| 30 | 0 | Don't bother | Mod · 56 |
| 35 | 0 | **One agent** | Mod · 57 |
| 40 | 0 | **One agent** | High · 59 |
| 45 | 0 | **One agent** | High · 60 |

Three candidate rules, tested against these cells:

- **Sum fails.** Recurrence 0 / Value 50 passes at sum 50, but Recurrence 10 /
  Value 40 fails at the same sum.
- **Weighted sum fails.** Fitting weights to the single-lever thresholds (35 and 50)
  predicts Recurrence 10 / Value 40 passes. It does not.
- **OR fits every cell.** Pass if Recurrence is above roughly 33 **or** Value is
  above roughly 48. Two independent bars, neither compensating for the other.

Recurrence is the easier bar to clear, at roughly two thirds the value threshold.

**Caveat, as of 13 Aug 2026:** this is fitted to boundary cells only. The full grid
was not run, and the decisive falsifying cells are the compensating ones. Under OR,
Recurrence 30 with Value 45 must fail, both being just short. Under any additive
rule it should pass. That single cell settles it.

## The size zones, and the correction to them

Bisection at Separation 50, Independence 50 (blend 50, no split), Checkability 50,
Recurrence 0, Value 0:

| Size | Verdict | Why text |
|---|---|---|
| 30 | Chat | "fits one window (30) with nothing to split (50)" |
| 35 | Chat | "fits one window (35) with nothing to split (50)" |
| 38 | One agent | "bounded work (38) with a check you can afford (50)" |
| 39 | One agent | "bounded work (39) with a check you can afford (50)" |
| 40 | Don't bother | "real work (40) that barely recurs (0) for modest value (0)" |

Three bands, named by the tool's own vocabulary: **"fits one window"** below 36,
**"bounded work"** at 36 to 39, **"real work"** from 40 up. Economics is consulted
only in the third band. The 36-to-39 window passes zero recurrence and zero value
untouched.

Size 40 is not itself an economic threshold. At Recurrence 50 / Value 50, Size 40
returns One agent. Forty is where economics starts being consulted, not where it
fails.

**These bands only apply to work that is not splitting.** See the next section.

## Superseded claims

Everything below was stated in the original analysis and disproved by testing.

| Original claim | What testing showed | Killed by |
|---|---|---|
| "Checkability >= blended score gives Several agents" | Fixed absolute bar at 60, unrelated to the blend | Blend 56 with Checkability 57 still failing |
| Separation 100 / Independence 50 blends to 75 | It blends to 80 | Re-measurement; the formula gives 80 and the misread was one of only three points the original model rested on |
| "Recurrence and Value never change the verdict category" | They are a universal veto that kills a fully qualified split | `73.90.58.82.0.0` returning Don't bother |
| "Spend Pressure is driven by Recurrence and Value" | Size and Separation feed it too; a two-lever model misses the observed value by about 14 points | Real-world case at 65 against a predicted 51 |
| Size below 36 gives Chat with nothing else consulted | Chat requires small size **and** low blend. High separation overrides a small size entirely | `20.100.100.0.0.0` returning Don't bother |
| Separation 50 / Independence 100 stays at One agent | Inconsistent with every other observation; the formula puts it at blend 70, well into split mode | Not retested. Treat as a recording error unless it reproduces |

The last row of the size correction is the one that reshaped the model. At Size 20,
maximum separation and independence, zero checkability, the tool returned **Don't
bother** with the why text *"needs separate minds (100) but the check is expensive
(0)"*, not Chat.

The Chat why-text had been telling us this all along. *"Fits one window (20) with
nothing to split (32)"* is a conjunction, and every Chat observation until then
happened to carry a low blend, so a two-condition rule read as a one-condition rule.
Separation is the first branch; size only sorts what is not splitting.

## Spend Pressure: a display, not a gate

Spend Pressure does not determine any verdict. `73.50.20.50.0.0` shows Moderate 49
and fails; the original real-world case shows High 65 and passes. A lower score
failing while a higher score passes rules out any threshold reading.

Single-lever effects, measured from comparable states:

| Lever | Effect on Spend Pressure |
|---|---|
| Size | about +0.35 per unit (50 to 73 moved it 50 to 58; 20 to 73 moved it 30 to 49) |
| Recurrence | about +0.25 per unit |
| Value | about -0.16 per unit (higher value lowers displayed pressure) |
| Checkability | **none**, confirmed constant at 58 across a 0 to 50 sweep |
| Separation | small and positive, roughly +0.15 per unit |
| Independence | small and positive, roughly +0.11 per unit |

Fitting those gives:

```
Spend Pressure ~= 28 + 0.35(Size) + 0.15(Separation) + 0.11(Independence)
                     + 0.25(Recurrence) - 0.16(Value)
```

This reproduces all eight recorded observations within about a point, including the
real-world case at 65 and the all-maximum case at 75. **It is a fit, not a
confirmed rule**, because the deliberate single-lever sweep for Separation and
Independence was never run. Those two coefficients are the soft ones.

Read plainly, the formula says Spend Pressure is the total work implied by the job,
discounted by how valuable it is. It is a cost-justification readout, which is why
it moves with everything and decides nothing.

## Open questions, as of 13 Aug 2026

Ordered by what would change the model most.

1. **Does economics apply to a small split?** Test `20.100.100.100.0.0`: split mode,
   checkability passed, size below 40, economics zeroed. If it returns Don't bother,
   the veto ignores size entirely. If it returns Several agents, the size-40 trigger
   holds inside split mode too.
2. **Is the economic rule really an OR?** Test Recurrence 30 with Value 45 at
   `73.50.20.50.30.45`. OR predicts failure; any additive rule predicts a pass.
3. **Where exactly is the split threshold?** Somewhere between blend 51 and 56.
   Sweep Separation 51 to 60 at Independence 50 with Checkability 100 so the
   checkability gate cannot mask the result.
4. **Does the size band shift in split mode?** The 36 and 40 boundaries were
   measured at blend 50 only.
5. **Confirm the Spend Pressure coefficients** for Separation and Independence with
   a deliberate sweep, holding Recurrence and Value at 50.
6. **Retest Separation 50 / Independence 100** to confirm the original One agent
   record was an error.

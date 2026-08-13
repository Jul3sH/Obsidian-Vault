# The One-Minute Test: Consolidated Logic Report

## Part 1 — Logic Conclusions

The tool produces one of **four verdicts** based on six sliders, but the sliders don't act independently — they combine into three underlying checks applied in sequence.
## The decision sequence

**Step 1 — Does the job fit in one window? (Size)**  
If Size is below a threshold of roughly **36–39** (with other levers at moderate/neutral settings), the verdict is **Chat**, regardless of the other five levers. Above that threshold, the job is "too big for chat" and the remaining checks take over.

**Step 2 — Does it need genuinely separate minds? (Separation + Independence, blended)**  
The tool computes an internal "splits across minds" score from a blend of **Separation** and **Independence** — not from Separation alone. Observed blends: Separation 58 + Independence 90 → score 71; Separation 80 + Independence 50 → score 68; Separation 100 + Independence 50 → score 75. If this blended score is low/moderate, the verdict stays at **One agent**. If it clears roughly the mid-50s to 70s range, the job "wants" to be split — but whether it's actually allowed to be split depends on Step 3.

**Step 3 — Can the split work be verified cheaply? (Checkability, gating)**  
This is the decisive, non-negotiable gate. The blended "splits across minds" score from Step 2 is compared directly against **Checkability**:

- Checkability ≥ blended score → **Several agents**
    
- Checkability < blended score → **Don't bother** (a warning/hollow dot appears on the map), even though the job "wants" multiple agents
    

I confirmed this boundary precisely: at a blended score of 68, Checkability 58 produced "Don't bother," while Checkability 60 flipped the same case to "Several agents." This means high Separation/Independence with weak Checkability is actively worse than low Separation — it doesn't default back to One agent, it drops to **Don't bother**, because unverifiable split work is judged riskier than not splitting at all.

**Step 4 — Is it worth setting up? (Recurrence + Value — economics, not architecture)**  
Recurrence and Value never changed the verdict category by themselves in testing (sweeping each from 0→100 alone, with everything else at 50, always stayed at "One agent"). Instead they drive **Spend Pressure**: Recurrence 0/50/100 → Spend Pressure ≈38/50/63 (roughly linear, higher recurrence = higher justified pressure); Value 0/50/100 → Spend Pressure ≈58/50/43 (higher value _reduces_ displayed pressure, i.e. it makes the spend easier to justify). The tool's own "why" text explicitly cites Recurrence + Value together as the reason a Several-agents verdict "earns setup" — but this is a justification layer on top of Steps 1–3, not a trigger for the split itself.

## Net logic summary

|Gate|Lever(s)|Effect|
|---|---|---|
|1. Fits one window?|Size|No → stops at **Chat**|
|2. Needs separate minds?|Separation × Independence (blended)|Low → **One agent**; High → proceeds to gate 3|
|3. Can you check it cheaply?|Checkability vs. blended score|Yes → **Several agents**; No → **Don't bother** (overrides everything)|
|4. Worth the setup?|Recurrence + Value|Doesn't change verdict category; adjusts **Spend Pressure** and justifies the verdict already reached|

Applied to the original real-world inputs (Size 73, Independence 90, Separation 58, Checkability 82, Recurrence 70, Value 74): Size clears gate 1; Separation+Independence blend to ~71, clearing gate 2; Checkability 82 comfortably exceeds 71, clearing gate 3; Recurrence+Value confirm the setup is worth it. Result: **Several agents**.

---

## Part 2 — Supporting Investigative Evidence

## Baseline and verdict definitions

The four verdicts, as displayed by the tool:

|Verdict|On-screen description|
|---|---|
|**Chat**|"Paste it in and ask. The whole job fits one clean window, and you can judge the answer yourself before anything depends on it."[[unlock-ai.natebjones](https://unlock-ai.natebjones.com/demos/one-minute-test#73.90.58.82.70.74)]|
|**One agent**|"Set a goal, a done state, and one visible check. Let a single accountable agent make its pass, then inspect the result before it counts."[[unlock-ai.natebjones](https://unlock-ai.natebjones.com/demos/one-minute-test#73.90.58.82.70.74)]|
|**Several agents**|"Split the work. Use independent workers, keep access away from output, and require sources or checks before the result counts."[[unlock-ai.natebjones](https://unlock-ai.natebjones.com/demos/one-minute-test#73.90.58.82.70.74)]|
|**Don't bother**|"Keep a human on it. The setup is not earned yet — run it by hand this time, and put the dot back on the map when it starts repeating."|

The map itself has two visible axes: **work required** (x, driven by Size) and **separation** (y, a derived/blended score — not the raw Separation slider value).[[unlock-ai.natebjones](https://unlock-ai.natebjones.com/demos/one-minute-test#73.90.58.82.70.74)]

## Evidence for Gate 1 (Size / Chat threshold)

Holding Independence, Separation, Checkability, Recurrence, and Value at 50, I bisected the Size threshold:

|Size|Verdict|"Why" text|
|---|---|---|
|5|Chat|"fits one window (5) with nothing to split (50)"|
|15|Chat|"fits one window (15) with nothing to split (50)"|
|20|Chat|"fits one window (20) with nothing to split (50)"|
|30|Chat|"fits one window (30) with nothing to split (50)"|
|35|Chat|"fits one window (35) with nothing to split (50)"|
|40|One agent|"bounded work (40) with a check you can afford (50)"|
|73|One agent|"bounded work (73) with a check you can afford (50)"|
|100|One agent|"bounded work (100) with a check you can afford (50)"|

This places the Chat/One-agent boundary at roughly Size 36–39. Size 100 with everything else at 50 stayed at **One agent**, never reaching Several agents — confirming Size alone cannot trigger a multi-agent verdict; it only decides whether the job leaves "one clean window" territory.

## Evidence for Gate 2 (Separation × Independence blend)

|Separation|Independence|Blended "splits across minds" score reported|
|---|---|---|
|58|90|71|
|80|50|68|
|100|50|75|
|50|0|(below threshold — stayed "One agent")|
|50|100|(below threshold — stayed "One agent")|

Independence moved alone from 0→100 (Separation fixed at 50) did not flip the verdict on its own, confirming it contributes to the blend but isn't independently decisive at moderate Separation.

## Evidence for Gate 3 (Checkability as a hard gate)

With Separation fixed at 80 and Independence at 50 (blended score ≈ 68), I swept Checkability:

|Checkability|Verdict|"Why" text|
|---|---|---|
|50|Don't bother|"needs separate minds (68) but the check is expensive (50)"|
|55|Don't bother|"needs separate minds (68) but the check is expensive (55)"|
|58|Don't bother|"needs separate minds (68) but the check is expensive (58)"|
|60|Several agents|"splits across minds (68), the check is cheap (60), and it earns setup (50 + 50)"|
|68|Several agents|"splits across minds (68), the check is cheap (68), and it earns setup (50 + 50)"|
|90|Several agents|"splits across minds (68), the check is cheap (90), and it earns setup (50 + 50)"|
|100|Several agents|"splits across minds (68), the check is cheap (100), and it earns setup (50 + 50)"|

This pinpoints the flip between Checkability 58 and 60 against a blended score of 68 — i.e., the verdict flips once Checkability crosses the blended separation score, not at some fixed absolute number. Critically, "Don't bother" appeared with a distinct hollow/warning dot on the map, visually distinguishing "unverifiable" from ordinary low-need cases[screenshot showing warning dot at Separation 100, Independence 50, Checkability 50].

Separately, at maximum stress (Separation 100, Independence 90, Checkability 50 — i.e., original real values but Checkability capped at 50), the tool also returned **Don't bother**, reinforcing that Checkability shortfall overrides even very strong separation/independence signals.

## Evidence for Gate 4 (Recurrence + Value → Spend Pressure, not verdict)

With Size, Independence, Separation, and Checkability fixed at 50:

|Recurrence|Value|Verdict|Spend Pressure|
|---|---|---|---|
|0|50|One agent|Moderate · 38|
|50|50|One agent|Moderate · 50|
|100|50|One agent|High · 63|
|50|0|One agent|High · 58|
|50|100|One agent|Moderate · 43|

The verdict category never changed across any of these; only the Spend Pressure score and label moved. This confirms Recurrence and Value operate as an economic overlay (cost-justification), not as inputs to the architectural decision itself — though the tool's generated "why" explanations reference them ("earns setup") once a Several-agents verdict has already been reached via Gates 1–3.

## Confirmation with real-world values

Original inputs — Size 73, Independence 90, Separation 58, Checkability 82, Recurrence 70, Value 74 — produced:

- **Verdict: Several agents**
    
- **Why:** "splits across minds (71), the check is cheap (82), and it earns setup (70 + 74)"
    
- **Spend Pressure: High · 65**
    

This is consistent with the four-gate model: Size (73) clears gate 1; the Separation/Independence blend (71) clears gate 2's "wants splitting" threshold; Checkability (82) comfortably exceeds 71, clearing gate 3; and Recurrence+Value (70/74) are cited as justifying the setup cost, consistent with their role as an economic overlay rather than a verdict trigger.
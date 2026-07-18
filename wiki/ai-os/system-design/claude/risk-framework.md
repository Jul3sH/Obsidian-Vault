# Risk Framework and Methodology

Mirror of: `AGENTS.md` - Risk Framework section (source of truth)

Risk registers (e.g., decision-support judgement tools) use a **cause -> event -> effect -> response** chain to surface, assess, and track both **risks (threats)** and **opportunities**. This section defines the universal structure so all projects use the same format.

## Risk Anatomy: The Cause-Event-Effect Chain

**Cause** - A root condition or uncertainty that creates the risk environment. Example: "Limited cash and poor job prospects".

**Risk Event** - A specific triggering event that flows from the cause. There can be many events from one cause. Example: "Stay in Hong Kong for a year and don't get a job".

**Risk Effect** - The specific harm (for threats) or positive outcome (for opportunities) that flows from the event. Multiple effects can flow from one event, and each effect has its own impact/probability/response. Format: *bold scenario sentence* (memorable, salient, like you would speak it aloud) followed by impact and probability reasoning (high/medium/low justification in plain language).

Example effect: "**Sophia gets another year behind with French, creating a significant two-year gap** - High impact as two years may be unaddressable and will impact GCSE grades. High probability as two years is significant and hard to bridge."

**Response** - An action that addresses the effect. For threats: reduces impact or probability. For opportunities: exploits, enhances, or accepts the upside. Keep descriptions simple and actionable; long sentences overcomplicate.

## Structure: One Response Row Per Effect

Each risk or opportunity effect gets **one** response row. The Response column names the action type:

**For threats (RISK):**
- **Reduce Impact** - makes the effect less severe if it occurs
- **Reduce Probability** - makes the event less likely to occur
- **Reduce Impact & Probability** - does both; use labelled prefixes in Response Description:

```
Probability: [probability actions, semicolon-separated]
Impact: [impact actions, semicolon-separated]
```

For single-type threat rows, no prefix is needed - list the actions directly, semicolon-separated.

**For opportunities (OPP):**
- **Exploit** - take action to ensure the opportunity occurs; highest-priority response
- **Enhance** - increase the probability or magnitude of the opportunity
- **Accept** - no proactive action; capture it if conditions allow

## Style Conventions (match Julian's register)

Learned from Julian's own edits. Match these when writing rows:

- **Risk Cause** - a terse noun phrase naming the driver, NOT a full sentence. Examples: "Hybrid job requirement", "DBIS has no French curriculum", "Malvern is an interim solution", "Relocation required mid-term". Compress; do not write "Crash-pad interim needs a London hybrid job while the family is Malvern-based".
- **Risk Event** - a terse phrase naming the trigger, not a sentence. Examples: "In London midweek nights away (Tue-Thu)", "Relocate to London from Malvern mid term".
- **Risk Effect** - two parts:
  1. A **bold scenario sentence**, simple and speakable - something Julian would say out loud and remember (e.g. "Sophia loses her bedtime cuddle and Dad's presence 3 nights a week").
  2. Impact and probability reasoning in **Julian's own first-person voice**, short and plain (e.g. "Medium impact as not preferable but manageable. She's mature, loves granny." / "High probability based on the jobs analysis as hybrid has best prospects"). Each on its own line beginning "- ".
- **Response Description** - simple, actionable, semicolon-separated. For threat "Reduce Impact & Probability" rows, prefix each block: "Probability: [text]" then "Impact: [text]" on separate lines. For opportunity rows, plain description of the action to realise or enhance. Long sentences overcomplicate.
- **Assumptions vs supporting evidence** - cite the artefact or source that grounds the assessment (e.g. "Adzuna pull 11 Jul: ~40% of London roles explicitly hybrid"), and flag where it is still an assumption pending due diligence.

## Impact and Probability Assessment

**Impact** (High / Medium / Low) - How severe is the harm if the risk occurs? Consider: financial loss, relationship/wellbeing cost, delay to critical path, or degree of disruption.

**Probability** (High / Medium / Low) - How likely is the risk event to occur? Consider: historical frequency, control strength, external factors, and your confidence level.

**Risk Score** - Calculated as the average of Impact and Probability. If no obvious midpoint, take the higher value:
- High + High = High
- High + Medium = High (take higher)
- High + Low = Medium (average)
- Medium + Medium = Medium
- Medium + Low = Medium (take higher)
- Low + Low = Low

## Residual Risk (Post-Mitigation)

After mitigations are in place, reassess:

**Residual Impact (IMPR)** - The severity of the effect *after* mitigation is applied.

**Residual Probability (ProbR)** - The likelihood of the event *after* mitigation is applied.

**Residual Risk (RiskR)** - Recalculated using the same average logic as pre-mitigation Risk.

## Financial Exposure (for Money-Related Risks Only)

For risks with direct financial impact:

**Residual Impact HK$** - The monetary impact post-mitigation (in HK dollars or applicable currency). Example: cost of moving to Malvern instead of London.

**Residual Probability %** - The percentage likelihood of the risk occurring post-mitigation. Example: 60% chance of running out of cash.

**Exposure(R) HK$** - Calculated as: `Residual Impact HK$ * Residual Probability %`. This quantifies your financial risk exposure and helps prioritise which risks warrant most effort.

## RAG Status (Red / Amber / Green)

A judgment call on residual urgency, based on the residual score and your risk appetite:

**For threats (RISK):**
- **Red** - Residual risk is unacceptable; requires immediate escalation or a new response
- **Amber** - Residual risk is elevated but managed; monitor closely, execute responses as planned
- **Green** - Residual risk is acceptable; monitor as part of standard operations

**For opportunities (OPP):**
- **Green** - Opportunity well-secured and likely to be realised; no blocking dependencies
- **Amber** - Opportunity dependent on something not yet secured; execute realisation action
- **Red** - Opportunity speculative, blocked, or at serious risk of being missed

## Decision Impact

**The most important column in a decision-support register.** With many risks, the operative question is NOT "how urgent is the residual risk" but "does this risk materially affect WHICH option is chosen?" A risk moves the decision only if it is (a) materially worse under one option than the others, AND (b) severe enough that it could tip the choice. A risk that is common to all options, or too small to matter, does not help decide - it is noise for the decision even if it is a real risk to manage.

Scale:
- **Material** - could change the chosen option; must be weighed directly in the decision.
- **Marginal** - informs but does not decide; worth noting, not load-bearing. (E.g. a risk that differentiates "move vs stay" but not the live question of "London vs Malvern".)
- **Immaterial** - common to all options or too small; log and monitor, but it does not help choose.

Keep any acceptance judgement or conditions (e.g. "accepted as real but low-probability now; managed by a paid-carer contingency") in the RAG column or the residual columns; Decision Impact answers only the "does it change the choice?" question.

## Supporting Evidence and Due Diligence

Record the facts, research, and due diligence that informed your Impact, Probability, and Residual assessments. This separates assumptions from validated facts and makes it clear which risks need more investigation.

Examples:
- "Adzuna job-market pull: 80 count-queries; 375 real-salary listings"
- "Cecil Road council tax band confirmed Band E from local authority"
- "Sophia's school transition: assumptions on resilience, not yet tested"

## Risk Categories

**Wellbeing** - Threats to mental/emotional/physical health, state, and resilience (individual or collective). Examples: Sophia's distress from separation, grades impacted by transition stress, Julian's financial anxiety, energy/burnout from extended search.

**Relationships** - Threats to the quality, trust, dynamics, or stability of a specific relationship. Examples: Joanne does not commit to UK future, father-daughter relationship strained by midweek absence, communication breakdown with key stakeholder.

**Financial** - Threats to cash reserves, runway, wealth preservation, or ability to fund the plan. Examples: Run out of money during job search, early pension drawdown, substantial wealth depletion.

**Note:** A risk's *cause* may be relational (e.g., father away from daughter), but if the *harm* is to wellbeing (her distress, her grades), it belongs in Wellbeing. Conversely, if the harm is to the relationship itself (trust eroded, dynamic deteriorates), it belongs in Relationships.

## Scenario Mapping

For decision-focused risk registers, tie each risk to the scenario(s) it applies to. This lets decision-makers filter: "If I choose Path X, what risks do I face?" Examples:

- **Scenario: Stay in Hong Kong** - risks around job prospects, extended savings drain, Sophia's education stagnation
- **Scenario: Move to London** - risks around school transition, higher burn rate, upfront moving costs
- **Scenario: Move to Malvern (crash-pad interim)** - risks around Sophia's midweek absence, Mum dependency, tenancy timing, drift trap

When building the register, record which scenario(s) each risk applies to. This supports both risk *surfacing* (what could go wrong in each path) and risk *comparison* (which path faces the most risk, or the highest-impact risks).

## Register Column Schema (live Google Sheet - canonical column order)

> The decision risk register (the live Google Sheet) uses the 24-column layout below (23 data columns + 1 blank separator). **Match this exact order and these headers when adding rows** so entries paste cleanly and stay consistent across projects. This is the operational form of the cause-event-effect method above.
>
> **Scoring:** Impact, Probability, and Risk all use **High / Medium / Low** - both in the register and when writing rows here. The Risk column is derived from Impact + Probability using the H/M/L averaging logic in the "Impact and Probability Assessment" section above. For **threats**: High Risk = bad (minimise). For **opportunities**: High Risk = desirable (well-secured, high-value upside). Residual columns (Imp(R), Prob(R), Risk(R)) follow the same H/M/L convention.
>
> **Non-financial rows:** leave the three HK$ exposure columns (16-18) as `n/a`; they apply only to money-related threats.
>
> **Decision Impact is column 7 (before scoring).** It is assessed immediately after describing the effect, before impact/probability are scored. This forces the decision-relevance test before scoring effort is spent on immaterial rows.
>
> **Migrating existing risk rows:** insert a new column 2 (RISK/OPP), type "RISK" for all existing rows, and rename "Mitigation" → "Response" and "Mitigation Description" → "Response Description" in the header. All other data is unchanged.

| # | Column header | What goes in it |
|---|---------------|-----------------|
| 1 | Scenario | The option/path this row assesses (e.g. London-direct / Malvern interim / Stay-HK). One row per scenario where the risk or opportunity is material. |
| 2 | RISK/OPP | "RISK" for a threat; "OPP" for an opportunity. Filter this column to view threats and opportunities separately or together. |
| 3 | Category | Wellbeing / Relationships / Financial / Career / Education / execution SPOF etc. Harm-based for threats; benefit-domain for opportunities. |
| 4 | Risk Cause | Terse noun phrase naming the driver (not a sentence). Same convention for opportunities: the upstream condition that makes the event possible. |
| 5 | Risk Event | Terse phrase naming the trigger (not a sentence). For opportunities: the enabling action or condition that unlocks the upside. |
| 6 | Risk Effect | Speakable scenario sentence + reasoning in Julian's first-person voice. For opportunities: the positive outcome gained. Plain text in the sheet (no markdown bold). |
| 7 | Decision Impact | Material / Marginal / Immaterial - does it change which option is chosen. Assessed before scoring so immaterial rows are deprioritised upfront. |
| 8 | Impact | Severity (threats) or magnitude (opportunities) if the event occurs: High / Medium / Low. |
| 9 | Probability | Likelihood the event occurs: High / Medium / Low. |
| 10 | Risk | H/M/L averaged from Impact + Probability using the framework averaging logic. High = bad for threats; High = desirable for opportunities. |
| 11 | Response | Threats: "Reduce Impact" / "Reduce Probability" / "Reduce Impact & Probability". Opportunities: "Exploit" / "Enhance" / "Accept". One row per effect. |
| 12 | Response Description | Threats (single-type): actions semicolon-separated. Threats ("Reduce Impact & Probability"): two labelled lines — "Probability: [actions]" then "Impact: [actions]". Opportunities: plain description of the action to realise or enhance. |
| 13 | Imp(R) | Residual impact/magnitude after response: High / Medium / Low. |
| 14 | Prob(R) | Residual probability after response: High / Medium / Low. |
| 15 | Risk(R) | Residual score: H/M/L averaged from Imp(R) + Prob(R) using the framework averaging logic. |
| 16 | Imp(R) HK$ | Residual monetary impact (money threats only; else n/a). |
| 17 | Prob(R) % | Residual probability as a percentage (money threats only). |
| 18 | Exposure(R) HK$ | Imp(R) HK$ x Prob(R) % (money threats only). |
| 19 | *(blank separator)* | Leave empty - visual break between the financial exposure block and the RAG/narrative block. |
| 20 | RAG(R) | Threats: Red/Amber/Green on residual risk. Opportunities: Green = well-secured; Amber = dependent on something unsecured; Red = speculative or blocked. |
| 21 | RAG Description | One-line justification / acceptance conditions. |
| 22 | Assumptions | Facts/evidence grounding the assessment + what is still assumed pending due diligence. |
| 23 | LLM Next Actions: | Actions for the agent (draft content, track a reply, update scores). |
| 24 | My Next Actions: | Actions for Julian. |

*The two "Next Actions:" headers carry a trailing colon in the live sheet - keep it.*

## Workflow

1. **Identify risks and opportunities** from project analysis, prior experience, and stakeholder interviews. Record cause, event, effect, RISK/OPP type, and which scenario(s) it applies to.
2. **Assess impact and probability** pre-response. Make your judgment explicit with reasoning.
3. **Calculate score** (Impact x Probability, 1-25). For threats: high score = bad. For opportunities: high score = desirable.
4. **Identify responses** - one row per effect. Threats: Reduce Impact / Reduce Probability / Reduce Impact & Probability. Opportunities: Exploit / Enhance / Accept.
5. **Reassess residual** (IMPR, ProbR, RiskR, financial exposure if applicable).
6. **Assess Decision Impact** (Material / Marginal / Immaterial) - does this row change which option is chosen? Keep acceptance judgement/conditions in RAG or residual columns.
7. **Record evidence** - facts that support your assessments, gaps that need more due diligence.
8. **Monitor and revisit** - update the register as responses are executed and new facts emerge.

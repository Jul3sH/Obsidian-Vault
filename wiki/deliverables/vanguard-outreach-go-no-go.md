---
project: cold-outreach-real-estate
workstream: career
type: enabler
enabler-type: Exploration
size: 1
hours: 1-4h
created: 2026-08-05
status: queued
jira-key:
---

# Vanguard Outreach Go/No-Go Assessment

## Enabler Type
**Exploration** - a 2-hour spike that resolves one question before anything else in this Project moves: does Julian personally participate in Adam's B2C cold outreach campaign, and on what terms.

## Technical Objective
Produce a three-page report on the Hong Kong regulatory position for Vanguard's B2C property-investment outreach, classify every identified risk by treatment, and reach a go/no-go verdict on Julian's own participation.

## What This Unblocks
- **[[outreach-b2c-risk-assessment|B2C Risk & Strategy Assessment]]** (size 3) - the deeper three-path strategy piece only runs if this returns a "go". If the verdict is "no", that enabler is cancelled rather than queued.
- **[[outreach-email-campaign|Email Campaign]]** and **[[outreach-run-campaign|Run Campaign & Measure]]** - both sit downstream of the risk assessment.
- **The infrastructure decision** - two email domains and the SalesHandy subscription are currently in Julian's name and warming. This determines whether they transfer, stop, or continue.

## Success Criteria
1. Spike capped at **2 hours**. The report exists regardless of how conclusive it is.
2. All three pages present: HK regulations (including SFC where relevant, with assumptions flagged), risks framed as "if we do this, then that could happen" with one-line candidate mitigations, and an action plan.
3. **Every identified risk has a named treatment and none is left unclassified**: transferred to Adam, mitigated, accepted by Adam, avoided by Julian (not proceeding), or accepted by Julian.

## Definition of Done
A three-page report exists that Julian can hold in his head and take into a conversation with Adam. Every risk it identifies carries a named treatment, including the risks that cannot be moved off Julian. The report ends in a verdict on Julian's participation, and a verdict of "no route exists that transfers enough risk, so I don't execute" closes this enabler successfully.

## Load-Bearing Assumptions

| # | Assumption | Cheapest test |
|---|---|---|
| 1 | Pure execution does not implicate Julian if Adam supplies the lists and takes responsibility | Read §4.9 of [[hk-b2c-outreach-uemo-pdpo]] closely. Its UEMO s.59-60 quote reads *"treated as done or engaged in by his employer **as well as by him**"*, which points the other way. Zero cost, do it first. |
| 2 | UEMO and PDPO are the whole regulatory picture | The research document's own scope note excludes SFC rules, estate-agency rules and AML. Assisted-living and commercial schemes are the risky end. One search on whether these are collective investment schemes. |
| 3 | The partner's whisky-investment contacts can be repurposed for property marketing | Already answered at no cost in §2.3 of the same document: DPP3 prohibits use for a new, unrelated purpose without express consent. |

All three surfaced during `/prompt-zero`. Assumption 1 is the one the spike exists to resolve.

## Payoff Test
- **Payoff: defensive, not commercial.** Confirmed 2026-08-05 as a **pure favour** to Adam with no income to Julian. The partnership may continue through separate legal routes such as LinkedIn advertising; this is not one of them. The payoff is avoided legal exposure on infrastructure already standing in Julian's name, plus preserving the relationship and the legal-route partnership.
- **Note on the gate:** the Payoff Test's two branches are commercial (who pays) and corporate (which role responsibility). Neither fits defensive work. Recorded here as defensive rather than forced into "speculative", which would misdescribe it.
- **Silence test:** pass. Julian would do this if he could never tell anyone.
- **Good enough when:** 2 hours are up and every risk has a named treatment, so Julian can tell Adam yes, no, or yes-on-these-terms. **Not** when he fully understands Hong Kong marketing law.

## Output
**[[vanguard-outreach-go-no-go-report]]** (draft, 2026-08-05). Verdict: **no-go on execution, go on advice.** All 11 risks classified; R6 (Julian pressing send) and R8 (SFO s.114, HK$5m and 7 years) cannot be transferred, mitigated, or accepted by Adam, and are avoidable only by Julian not executing. Awaiting Julian's review.

## Prompt Zero
Written 2026-08-05, graduated to its own file for length: **[[vanguard-outreach-go-no-go-prompt-zero]]**. Read it in full before starting this enabler.

## Links
- **Project:** [[../projects/cold-outreach-real-estate|Cold Outreach - Prove the Real Estate Lead Gen Model]]
- **Workstream:** [[../career/_index|Career]]
- **Source research:** [[hk-b2c-outreach-uemo-pdpo]]
- **Blocks:** [[outreach-b2c-risk-assessment|B2C Risk & Strategy Assessment]]

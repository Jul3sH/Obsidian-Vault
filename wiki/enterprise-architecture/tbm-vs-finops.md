---
type: reference
tags: [enterprise-architecture, cost-management, tbm, finops]
created: 2026-07-03
---

# TBM vs FinOps

> Two IT cost-management disciplines that are often conflated. They are not the same thing at different sizes: **FinOps is the cloud slice; TBM is the whole estate.** Getting this distinction right is a seniority signal in any CFO/CIO conversation.

## The distinction

| Dimension | FinOps | TBM |
|---|---|---|
| Full name | Cloud Financial Operations | Technology Business Management |
| Origin | FinOps Foundation, ~2019 (Linux Foundation) | TBM Council, ~2012; ATUM taxonomy (Apptio) |
| Scope | Public cloud spend (AWS/Azure/GCP). The 2025 "Scopes" / "Cloud+" expansion reaches toward SaaS, on-prem and AI spend | The **entire** technology estate: infrastructure, data centre, network, storage, **applications**, software licences, **labour**, outsourced/managed services, **and** cloud |
| Altitude | Operational: real-time cloud cost ops, engineering + finance collaboration | Strategic: enterprise-wide cost transparency, bill-of-IT, cost-to-value, run-vs-grow, IT-as-a-business |
| Core question | "Are we running the cloud efficiently?" | "Is our **total** technology spend delivering business value?" |
| Cost model | Variable, pay-as-you-go OpEx | All cost pools: capex + opex, fixed + variable, people + kit + contracts |

## The relationship

TBM is the whole-estate financial-management framework; FinOps is the cloud-native operational discipline that lives inside it. They increasingly **coexist** (the FinOps Foundation runs a FinOps + TBM coexistence working group), and FinOps's "Scopes" expansion is deliberately encroaching on TBM's whole-estate turf. **Apptio embodies both**: a TBM platform (ATUM taxonomy) that acquired the FinOps/cloud vendor Cloudability, which is why IBM's ~US$4.6B Apptio acquisition (2023) spans both disciplines at once.

## Where AI is (and isn't) automating this

Full analysis, five-lens and citation-verified: [[tbm-finops-ai-automation-briefing]] (Storm Research v2, 18/18 citations checked).

- **The operational cloud-FinOps layer is commoditising toward free/native.** The hyperscalers ship it (AWS/Azure/GCP cost tooling, AWS FinOps Agent) and autonomous tools run it. It is not a defensible edge.
- **The whole-estate TBM cost-to-value layer stays unautomated.** Mapping general-ledger spend up to business capabilities across infra, apps, licences and labour is org-specific business-rule logic, and the data is fragmented across CMDBs, the GL, HR, licence managers and contracts.
- **The unautomatable part is not the analytics, it is the cross-organisational allocation politics and data trust.** AI can generate candidate allocation rules in seconds; it cannot supply the neutral human who gets Finance and Engineering to agree on the model and own the number.
- **Structural reason it stays defensible:** no single hyperscaler can automate the whole-estate view, because it spans boundaries and systems they do not own (and they have a conflict of interest in tools that might argue against their own bill).

## The FinOps operating model (centralise governance, federate execution)

Distinct from the *scope* distinction above: this is the FinOps *organisational* pattern, and it is a reusable operating-model template beyond cloud cost.

- **Centralise the commercial/governance levers, decentralise execution.** A central function owns commitment purchasing (Reserved Instances, Savings Plans, Committed Use Discounts), rate governance, tagging/allocation policy and provisioning guardrails. The engineering teams (the SMEs) own *usage* — what they run and how — because they hold the domain knowledge. The centre never dictates how to build.
- **Why centralising captures value: aggregation and commitment risk.** The centre pools demand across teams, so it hits higher discount tiers and can commit with confidence, and it takes the "will we actually use this" risk off individual teams. A single team can't commit, because it lacks the portfolio view and the risk appetite. The centre can, because it sees the aggregate.
- **This is a general federated-governance pattern.** The same shape applies to enterprise architecture: centralise principles, reference architectures and adoption decision rights; federate implementation to regional/domain solution architects. The centre can commit to a shared platform because it sees the whole portfolio; a single region can't, so it silos. Applied to TTI's regional application-stack alignment in [[tti-ea-governance-value]].
- **The honest boundary:** FinOps rate optimisation is mechanical and cleanly quantifiable; softer governance domains (EA conformance, standards adoption) are more political and less precisely measurable. The transferable claim is the operating-model *shape*, not the precision of the savings number.

## Key Takeaways

- **FinOps = cloud financial management (a corner); TBM = the whole technology estate (everything).** Not the same principles scaled up.
- The commoditising, low-defensibility work is cloud FinOps; the scarce, defensible work is **whole-estate TBM cost-to-value**.
- The strategic play for an operator: **leverage commodity FinOps tooling** for the cloud slice, and **own the whole-estate TBM allocation and brokering** where no vendor can reach.

## Related
- [[ai-strategy/_index|AI Strategy & Organisation]] — enterprise AI adoption patterns
- [[tbm-finops-ai-automation-briefing]] — the verified deep dive (Storm Research v2)
- [[tti-value-proposition]] — where this positioning is applied (career)
- [[tti-ea-governance-value]] — the FinOps operating-model pattern applied as an EA-governance analogy (career)

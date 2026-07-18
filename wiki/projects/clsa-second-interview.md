---
workstream: career
created: 2026-06-30
status: active
flow: ready
t-shirt: M
wsjf: 3.8
status-updated: 2026-06-30
por-key: POR-21
jira-key: BWS-18
---

# CLSA — Second Interview (Deputy CIO)

## Status (as of 2026-06-30)

**Position:** Just defined and ranked. Not started. Sibling to the now-closed [[clsa-role|CLSA — First Interview]] (Done).

**Next action:** Run `/define-user-story` / `/define-task` to break into deliverables (start with the MVP: scope doc + sharpest operational-risk story), then `/jira-sync`.

**Waiting on:** Interview date confirmation from Rob - flagged as **possibly this week**.

**Scheduling note:** WSJF ranks this 4th (3.8, per-effort), but the interview is a **hard external deadline** that overrides the discretionary queue - this is worked **now**, not 4th. WSJF efficiency ≠ schedule when a cliff exists.

**Detail tier:** [[clsa-engagement-timeline]] (engagement history) · [[clsa-salary-strategy]] (salary + Zhong Bing wider-remit lever).

### Status log (newest first)
| Date | Update |
|------|--------|
| 2026-06-30 | Project defined, scored (WSJF 3.8), spun out as a sibling of the closed First Interview project. Created on the POR board as POR-21 (Ready); First Interview POR-19 reconciled to Done. |

---

## Objective
Walk into the second interview able to deliver a tight, reality-grounded set of stories and talking points that give the operationally-focused Deputy CIO an overwhelming sense of value beyond the Head of Network Services role - enough that he champions me to CITIC for an above-band offer.

## Outcomes / Outputs
1. **Output** — MoSCoW scope doc agreed (in-scope + explicit out-of-scope talking-point themes, with rationale), produced by one LLM and evaluated by another.
2. **Output** — Curated, evidence-cited story set (service-design/ITIL, contract insight, AIOps/NetAI-replication, AI-OS pipeline) passing the answer-4 rubric, loaded into NotebookLM as flashcards.
3. **Outcome** — Interview-ready: every Must-have talking point delivered fluently, no notes, before the interview date.

## Hypothesis
> *"We believe **anchoring my stories to the Deputy CIO's specific operational anxieties** (undetected port misconfigurations, holding the vendor to contract, AIOps value without the full NetAI spend) - grounded in my ITIL-Expert and service-design track record - will make him **perceive value beyond the Head of Network Services role and advocate for me to CITIC**. We'll know it's working when **each story survives a second-LLM 'is this credible and achievable?' challenge and I can deliver it fluently in rehearsal**."*

## Confidence
**Medium.** Outcome bet - depends on the Deputy CIO's and CITIC's response, against a stated Mandarin-speaking-candidate preference. Strong leverage (prior CLSA engagement, Rob's advocacy, ITIL Expert, contract knowledge), but the response isn't in my control. Admitted **cheapest-test-first**: the MVP and Leading Indicator are the real gate, not an exhaustive prep pack.

## Evaluation Rubric (the answer-4 guardrail)
Every artefact (scope doc, each story) must pass a second-LLM challenge on all five before it's accepted. This is the explicit defence against the "polished but wrong" failure mode:
1. **Succinct** over comprehensive - a talking point, not an essay.
2. **Flexible** over prescriptive - room for the conversation to breathe; no rigid script.
3. **Achievable by Julian** over impressive - grounded in ITIL/service-design reality; sells no dream I can't deliver.
4. **Story-led with citations** - a narrative backed by a real, referenced fact.
5. **Minimises my distillation work** - arrives usable; I rehearse and own it, I don't re-process it.

## Future Leverage
- Reusable **AIOps/NetAI research** + any bespoke **data-ingestion-pipeline demo** built as a talking-point artefact - feeds Performance's Q4 *AI Agent Builder* objective and serves the role itself if landed.
- The **produce/evaluate interview-prep workflow** (one LLM produces, `/llm-council` evaluates) becomes a reusable asset for future interviews.

## Existing Leverage
- **AI OS skills**: `deep-research` (research artefacts), `notebooklm-py` (flashcards), and **`/llm-council` as the primary story-evaluation mechanism** (the cross-model Codex-as-skeptic loop).
- **`/codex:adversarial-review`** - Codex adversarial evaluator reserved for any built **code/pipeline demo** design (it reviews git diffs, not prose); the story evaluation reuses the same skeptic *pattern* via `/llm-council`.
- **Prior CLSA wiki corpus**: [[clsa-engagement-timeline]], [[clsa-salary-strategy]], the Zhong Bing wider-remit lever, and the just-tailored resume.
- **Story raw material already held**: ITIL Expert, service-design pedigree, BT/Telstra/CLSA engagements - curating, not researching from zero.
- **Rob as a live insider source** for the Deputy CIO's actual operational anxieties.

## Leading Indicators
The **first Must-have story**, run through the produce → evaluate loop, passes the answer-4 rubric within one or two evaluation passes and rings true as hitting the Deputy CIO's actual operational pain. If the first story takes five rounds and still feels oversold, that's the early warning the anchoring thesis (or the rubric) needs a rethink - before hours are sunk into the whole set.

## MVP (build first)
Scope doc + the **single sharpest "I understand your operational risk" story** (the port-misconfig / contract-enforcement angle), taken all the way through produce → evaluate → fluent delivery. If the interview lands sooner than expected, that MVP is 80% of the value. Everything else scales up from a thing that already works.

## Effort
**T-shirt size:** M (17-40h), held to a **20h forcing-function cap** driven by interview timing. Natural estimate ~22-34h (mid-M) recorded for baseline - the squeeze is deliberate, the story-iteration loop is the overflow risk.

## WSJF Scoring
| Component | Score | Rationale |
|-----------|-------|-----------|
| Value | 8 | Transformative: direct lever on the most live, highest-value career opportunity - the offer + above-band salary serving Career O2, raising the Finance floor, funding Sophia. |
| Time Criticality | 8 | Window closes: interview possibly this week. One shot, imminent, severe concrete consequence if under-prepared. A measurable cliff, not mood-driven urgency. |
| Risk / Opportunity | 3 | Reusable AIOps research + pipeline demo (feeds Performance AI-Agent-Builder) and the reusable prep workflow. Counterfactual applied: the offer/income payoff is Value, not RO - not double-counted here. |
| Job Size | M = 5 | 17-40h band; 20h capped target. |
| **Cost of Delay** | **19** | 8 + 8 + 3 |
| **WSJF** | **3.8** | 19 ÷ 5 |

## Rough Work Breakdown
Informal, for sizing only - not committed. Becomes deliverables via `/define-user-story` / `/define-task`.

| Work | ~Hours |
|------|--------|
| Scope doc (produce → review → `/llm-council` eval) | 2-3 |
| AIOps/NetAI research artefacts (`deep-research` + eval) | 3-4 |
| Contract-insight talking points (Julian's read + AI synthesis) | 2-3 |
| Curated stories: produce → evaluate → iterate to fluency *(the hard part)* | 6-8 |
| NotebookLM flashcards from the stories | 1-2 |
| Interview-question prep + rehearsal | 3-4 |
| **Total** | **17-24h** → held to 20h, Must-haves first |

## Completed
Nothing completed yet.

## Deliverables
| Deliverable | Hours | Status |
|-------------|-------|--------|
| [[../deliverables/clsa-second-interview-scope-doc\|MoSCoW Scope Doc]] | 1h | queued |
| [[../deliverables/clsa-deputy-cio-story-ops-risk\|Ops-Risk Talking Point]] | 3h | queued |

## Funnel
| Item | Intent | Added |
|------|--------|-------|

## Links
- **Workstream:** [[../career/_index|career]]
- **Sibling (closed):** [[clsa-role|CLSA — First Interview (Head of Network Services)]]
- **Related engagement:** [[clsa-engagement-timeline]] · [[clsa-salary-strategy]]

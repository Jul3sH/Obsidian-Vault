---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Production Observability & Drift Monitoring

> This is the catalog entry for production observability and drift monitoring, one of nine AI engineering pattern areas surveyed for 2025-2026 practice. It exists as a routing reference: when you are deciding how to attack a piece of AI engineering work, "Reach For It When" tells you in a few lines whether this pattern is the one that applies. Read it before instrumenting an agent, before buying an observability platform, and whenever a system that passed its evals is behaving worse in production than it did in test. Sibling articles cover the other eight areas; the index links them all.

## Key Takeaways

- Observability is three layers, not one: **tracing** (what did it do), **online eval scoring** (is it good enough), **drift detection** (is it *still* good enough). Shipping only the first and calling it observability is the most-cited mistake in the 2026 literature.
- Evals and observability overlap but differ in temporal scope: evals are point-in-time checks against a curated dataset, observability watches uncurated live traffic continuously. This catalog treats observability as the superset, but the boundary is **contested** and the terminology is not standardised.
- "Drift" is at least five different problems (input distribution, retrieval corpus, prompt, judge calibration, agent step). Buying one tool for all five is how teams end up monitoring the wrong thing.
- OpenTelemetry is the de facto instrumentation substrate, but the GenAI semantic conventions are **not yet stable** (all `gen_ai.*` attributes still marked Development as of July 2026). Instrument on OTel; do not assume the attribute names are frozen.
- The regulatory driver is real but now on a later timeline: the Digital Omnibus entered into force 27 Jul 2026, postponing EU AI Act high-risk obligations (Articles 12 and 19, automatic logging, minimum six-month retention) for Annex III systems from 2 Aug 2026 to 2 Dec 2027, and for Annex I embedded product systems to 2 Aug 2028.

## What It Is

Capturing the full runtime execution of an LLM or agent system as structured traces (every prompt, response, tool call, retrieval, token count, latency, and cost), then continuously monitoring that live traffic for quality degradation, distribution shift, and failure patterns. The distinguishing move over ordinary logging is that a trace reconstructs a whole multi-step run as a tree of spans, so a failure three tool calls deep can be attributed to the step that caused it rather than inferred from a flat log.

## Reach For It When

Route work here when any of these hold:

- **An agent runs autonomously across multiple steps or sessions and a failure cannot be reproduced from logs.** This is the load-bearing trigger. Multi-step autonomy is what makes flat logging insufficient.
- **You need to attribute cost, latency, or quality to a specific step** in a pipeline, not to the pipeline as a whole. Per-step attribution is the thing tracing gives you and nothing else does.
- **The eval suite passes but users report worse quality.** That gap is the signature of production-input distribution diverging from the eval dataset, which offline evals cannot see by construction.
- **You depend on a provider-hosted model whose weights can change under you.** Silent model updates are only detectable by replaying a fixed reference set.
- **You are subject to audit or record-keeping obligations** (EU AI Act high-risk classification, or an internal equivalent). At that point trace retention and PII redaction are compliance features, not engineering conveniences.

Do **not** route here when the system is a single-shot prompt with a deterministic, human-inspected output, or when the work is pre-deploy quality gating. That is [[evals]], not this.

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Distributed tracing / spans | Captures each LLM call, tool invocation, and retrieval as a named span with model, tokens, latency, cost | Foundational. Any production LLM system, first thing you install |
| Span-attached online evals | Runs LLM-as-judge or rubric scorers on a sampled slice of live traces, attaches scores as span attributes | Once tracing exists and you need a continuous quality signal on real traffic |
| Golden-set replay | Scheduled replay of a curated reference set (order of 50-500 traces) through the current pipeline | To catch regressions from silent provider model updates, prompt edits, tool schema changes |
| Drift detection (five sub-types) | Statistical monitoring of input distribution, retrieval corpus, prompt, judge calibration, and agent-step behaviour | When live behaviour changes without a code change. Pick the method matching your sub-type |
| Cost and latency attribution | Per-request, per-tenant, per-feature tagging of spend and latency | When cost anomalies need to alert independently of quality metrics |
| Context / session fingerprinting | Logs a hash or snapshot of active context (instructions, tools, constraints) per turn | When behaviour diverges and you need to trace it to a specific context-state change |
| Tiered trace storage | Hot (full trace, days), warm (span summaries, months), cold (metadata only, indefinite) | Long-running agents where full-fidelity retention is cost-prohibitive |
| Alerting policy tiers | Page-worthy vs ticket-worthy vs dashboard-only severity bands | Before turning alerts on, to avoid the fatigue that gets them muted |

**On sampling rates:** the report's "5-20% plus 100% of errors" is one of several circulating heuristics, not a settled number. Published guidance ranges from 1-5% for a baseline trend up to 10-20% for a frontier-model judge, with the constraint being cost: an LLM-judge call on every request roughly doubles inference spend. Start low, sample 100% of errors regardless, and layer explicit triggers on top so you are not relying on chance to catch what matters.

## Use Cases & Examples

- **Langfuse** as the open-source default: MIT-licensed core, OTel-native SDK, tracing plus prompt management plus evals in one product. Acquired by ClickHouse in January 2026 (announced alongside a $400M Series D); the MIT licence and self-hosting were publicly committed to as unchanged. Pick it when you want self-hosting without feature gating.
- **Arize Phoenix** for drift and embedding work: Elastic License v2 (source-available, free to self-host, but restricted from being resold as a hosted service), built on OpenTelemetry with OpenInference instrumentation, ships embedding clustering and outlier detection inherited from the team's ML-observability heritage. Pick it when your failure mode is distribution shift rather than trace debugging.
- **LangSmith** for LangChain/LangGraph runtimes: native graph semantics and near-zero-friction capture inside that ecosystem, at the cost of being tied to it.
- **Pair the LLM-specific platform with whole-stack APM** (Datadog, Honeycomb). They operate at different layers and the practitioner guidance is consistently to run both rather than choose.

## Anti-Patterns

- **Tracing alone, labelled "observability."** Spans show what happened, not whether the system is still working. Without the eval-scoring and drift layers you have a debugger, not a monitor.
- **Pre-deploy golden set only, no production scoring.** Golden-set replay catches fixed-reference regression; live scoring catches distribution shift. They catch different failure classes and neither substitutes for the other.
- **Treating drift as one undifferentiated phenomenon.** Five sub-types, five detection methods. Teams that skip this buy the wrong tool for their actual failure mode.
- **Default trace retention (1-7 days) on long-running autonomous agents.** Incidents found a fortnight later are then undebuggable. Tiered storage is the corrective.
- **Alert thresholds not tuned against historical noise.** Alerts that fire on ordinary variance get muted, which defeats the entire drift-monitoring investment.
- **Assuming the OTel GenAI attribute names are stable.** They are not (see State of Practice). Wrap them rather than hard-coding them across a codebase.

## Mental Models

[[mm-verification]] (this pattern is verification moved to runtime: you are building the check that tells you an unattended system is still correct), [[mm-token-economics]] (sampling rate, judge model choice, and trace retention are all cost decisions before they are quality decisions).

## State of Practice

As of Aug 2026:

- **Maturing but still consolidating.** The category moved from "did the prompt and response get logged" to an architectural decision spanning OTel-native vs proprietary span formats, eval-coupled vs eval-decoupled design, and multimodal support.
- **Vendor consolidation is visible.** ClickHouse acquired Langfuse (Jan 2026, confirmed by ClickHouse's own announcement). Two further acquisitions in the same window, Mintlify/Helicone and Cisco/Galileo, are reported by secondary sources and worth confirming before relying on them. One widely-cited survey narrows the production-grade field to roughly six platforms (LangSmith, Langfuse, Arize Phoenix, Helicone, Datadog LLM Observability, Honeycomb LLM Observability); treat the exact count as one source's framing rather than a fact.
- **OpenTelemetry GenAI conventions: adopted in practice, not stable on paper.** As of July 2026 no `gen_ai.*` span, metric, event, or attribute is marked Stable; all carry Development status, and the conventions moved to their own `semantic-conventions-genai` repository (main repo v1.42.0, June 2026, deprecated and relocated the content). Core chat and embedding attributes are settled enough to build on; agent and tool-orchestration conventions are still moving.
- **Outcome-aware sampling is off-the-shelf but not GA.** The OTel collector's tail-sampling processor is available and widely deployed, but is still marked Beta with no proposed GA date. The report's framing of it as a 2026 maturity milestone overstates its formal status.
- **Regulation is a live driver, now on a settled but later timeline.** The Digital Omnibus entered into force 27 Jul 2026, postponing EU AI Act Article 12 (record-keeping) and Article 19 (automatically generated logs, minimum six-month retention) for Annex III high-risk systems from 2 Aug 2026 to 2 Dec 2027, and for Annex I embedded product systems to 2 Aug 2028. Audit trails and PII redaction stay on the mandate track for in-scope systems, just with more runway than originally set.
- **The evals/observability boundary remains contested.** Some sources sell one combined "evals and observability" category; others insist on strict three-layer separation. This catalog takes the superset view, and flags that the terminology is not industry-standard.

## Links

- [[evals]] - the pre-deploy, dataset-driven sibling. The two are routinely sold as one product; route here for live traffic, there for gating a deploy.
- [[orchestration]] - multi-step agent architectures are what create the need for span-level attribution.
- [[context-engineering]] - context fingerprinting sits on the boundary between the two patterns.
- [[security-agent-identity]] - audit trails, PII redaction, and approval-gate logging overlap with compliance-driven observability.
- [[model-adaptation]] - silent provider-side model changes are the drift class that golden-set replay exists to catch.

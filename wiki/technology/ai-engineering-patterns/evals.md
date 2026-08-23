---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Evals

> This article is the catalog entry for **evals**, the engineering pattern of measuring LLM and agent output quality systematically rather than by impression. It exists as a routing reference: one of nine AI engineering patterns written so that someone deciding how to attack a piece of AI work can tell quickly whether this pattern is the one that applies. Read "Reach For It When" first, then use the technique table to pick a specific approach, and follow the links at the bottom to the adjacent patterns.

## Key Takeaways

- Evals are the permission slip for everything else. If you cannot measure whether a change helped, you cannot safely change prompts, models, or agent design.
- **Product evals beat public benchmarks.** A leaderboard score measures generic capability, not whether your application does its job.
- Two layers, run together: a code-first framework gating CI before deploy, and an observability platform scoring live traffic after.
- For agents, score the **outcome and the end state**, not just the final message. Anthropic's own guidance is that a confirmation message is not proof the booking exists.
- LLM-as-judge is useful but not free: calibrate it against human labels, and never let the judge come from the same model family as the system being tested.

## What It Is

Eval-driven development treats measurement of output quality as a first-class engineering practice, the probabilistic analogue of test-driven development. Where a unit test asserts one correct answer, an eval scores a distribution of acceptable ones, using deterministic assertions where they work, model-based graders where they do not, and human review to keep the graders honest. The unit of work is a versioned dataset plus a scorer, run repeatedly so that quality changes become visible as numbers rather than as vibes.

## Reach For It When

Reach for this pattern when:

- **You are about to change a prompt, a model, or an agent's workflow** and cannot otherwise say whether the change made things better or worse. This is the core trigger.
- **A feature is going to production.** Any non-trivial LLM feature that real users touch needs a regression suite before it ships and monitoring after.
- **You are choosing between models or vendors.** Build a small task-specific set instead of reading a leaderboard.
- **Outputs are open-ended text** with no exact-match ground truth: use LLM-as-judge with a rubric.
- **The system is an agent with tool calls.** Score the trajectory and the resulting environment state, not the last message.
- **Stakes are high or the judgment is genuinely ambiguous.** Route to human review, and use those labels to calibrate the automated graders.
- **You lack enough test data and manual curation is too expensive to scale alone.** Start from a small human-reviewed seed set, then use synthetic generation to expand it, filtered hard. Do not gate CI on a synthetic-only suite: both the cases and the judgments would come from a model, so there is no trusted anchor.

Do not reach for it when the work is a one-off with a human reading every output anyway. At that point you are the eval, and building a suite is overhead. See [[mm-routing]] for the recurrence-or-value bar.

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| Unit-style assertions | Deterministic checks: regex, schema validation, exact match, compile-and-run | Structured or constrained outputs; anything with one right answer |
| End-to-end task evals | Scores whether the agent achieved the real outcome across a full trajectory | Agentic workflows with tool use and external state |
| LLM-as-judge | A separate model scores outputs against a written rubric | Open-ended text, multiple valid answers, tone and nuance |
| Human review | Manual annotation and grading | High-stakes calls, and calibrating LLM-as-judge before its scores are trusted |
| Regression suites | Versioned datasets run in CI on every change | Pre-deploy gate; catching quality regressions from prompt or model changes |
| Trace-level scoring | Captures and scores full traces across tool calls and retrieval on live traffic | Post-deployment; finding *where* in a trajectory a failure happened |
| Red-teaming / adversarial evals | Systematic attempts to break the app before release | Safety, injection resistance, robustness validation |
| Synthetic eval-set generation | A teacher model generates edge cases and adversarial inputs at scale | Expanding a golden set beyond what manual curation can reach |

## Use Cases & Examples

- **CI gate plus live monitoring, run in tandem.** The standard production shape as of Aug 2026 pairs a code-first framework (promptfoo, DeepEval, RAGAS) that fails the build on regression, with an observability platform (LangSmith, Langfuse, Braintrust) that scores real traffic. Neither substitutes for the other: promptfoo is CLI and CI oriented and does not close the loop on production behaviour.
- **Three-layer agent evals.** Anthropic's "Demystifying evals for AI agents" (Jan 2026) describes grading at session outcome, trace quality, and tool-call correctness, and warns explicitly against grading only the path the agent took, which penalises valid approaches the designer did not anticipate. It also documents benchmark failure modes: Opus 4.5 initially scored 42% on CORE-Bench because of rigid grading of valid answers, and METR found tasks that rewarded models for ignoring stated instructions.
- **Golden dataset composition.** The most effective sets mix human-crafted edge cases, PII-scrubbed samples pulled from real production traffic, and synthetic expansions aimed at scenarios the first two underrepresent.

## Anti-Patterns

- **Validating a product feature with public benchmarks.** MMLU-style leaderboards measure generic capability. They say nothing about whether your retrieval pipeline answers your users' questions, and saturation means genuine gains show up as noise-sized increments.
- **Shipping promptfoo with no observability layer.** A green CI run tells you the system passed the cases you thought of. It leaves you blind to live traffic.
- **Scoring only the final output of a multi-step agent.** The score tells you it failed, not where. Trace-level scoring is what turns a red number into a fix.
- **Letting the generator and the judge share a model family.** This is the best-evidenced failure in the whole pattern: "preference leakage" (arXiv 2502.01534) shows contamination when generator and judge are the same model, share an inheritance relationship, or come from one family, and separate work shows LLM evaluators recognise and favour their own generations. The eval quietly becomes optimistic. Use a distinct family as judge, and prefer consensus across several judges.
- **Trusting an uncalibrated judge.** Judge models drift, carry position and verbosity biases, and reward plausible-but-wrong reasoning. Calibrate against human-labelled examples before believing the number.
- **Building the suite before the product has a shape.** Evals encode what "good" means. Written too early they lock in the wrong definition and then defend it.

## Mental Models

[[mm-verification]] (evals are how verification gets built rather than assumed), [[mm-routing]] (the recurrence-or-value bar decides whether a suite is worth building at all).

## State of Practice

**As of Aug 2026: maturing, commercially active, still fragmenting.** Two distinct segments have settled out and most serious teams run one of each.

| Segment | Tools | Notes |
|---|---|---|
| Code-first / CI gating | promptfoo, DeepEval, RAGAS | Open source, config-driven, local and CLI oriented; promptfoo also carries the strongest built-in red-teaming |
| Platform / production monitoring | LangSmith, Langfuse, Braintrust, Arize Phoenix | Tracing, datasets, online evals on live traffic |

Notes on the vendors, checked Aug 2026:

- **Braintrust** is independent and well funded: $36M Series A (Oct 2024) and an $80M Series B led by ICONIQ (2026), with Notion, Stripe, Vercel, Airtable, Dropbox and Coursera among named customers, and a purpose-built log store (Brainstore) behind full-trace scoring. It confirmed an AWS breach exposing customer API keys in May 2026, which is worth weighing for regulated data.
- **LangSmith** is LangChain's hosted platform and has the deepest automatic instrumentation for LangChain and LangGraph, but it is framework-agnostic rather than LangChain-only.
- **Langfuse** is MIT-licensed with all core features available self-hosted. **Arize Phoenix** is Elastic License v2, which is source-available rather than OSI open source and restricts offering it as a hosted service.
- **Anthropic** acquired Humanloop in 2025 and folded it into the Console's evaluation surface. It did not acquire Braintrust, despite some secondary sources conflating the two.

Synthetic eval-set generation matured through 2026 around three generation patterns (persona-prompted phrasing, taxonomy-stratified coverage, and evolution-based difficulty escalation in the Evol-Instruct line) with filter intensity varying by purpose: strictest for eval sets, looser for fine-tuning sets, and inverted for red-team sets, where only unrealistic attacks are rejected rather than difficult ones. The specific judge-score thresholds circulating in vendor guides are rules of thumb, not established practice, and should be tuned per set rather than adopted as numbers.

The production-monitoring and drift-detection layer is increasingly treated by practitioners as a separate discipline from eval-driven development proper. That split is real, and it is covered in the observability article rather than here.

## Links

[[observability]] (the live-traffic half of the pair; drift detection and trace monitoring), [[orchestration]] (what you are scoring when the system is multi-step), [[spec-driven-development]] (specs are where the definition of "good" comes from before it becomes an eval), [[model-adaptation]] (evals are the gate that decides whether prompting, RAG, or fine-tuning actually won), [[context-engineering]] (most eval failures on retrieval systems are context failures, not model failures).

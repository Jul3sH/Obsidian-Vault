---
type: reference
created: 2026-08-23
updated: 2026-08-23
---

# Model Adaptation: Prompting vs RAG vs Fine-Tuning

> This article is the catalog entry for **model adaptation**, the engineering pattern of shaping what a pre-trained model knows or how it behaves, using prompting, retrieval-augmented generation, fine-tuning, or a combination. It exists as a routing reference: one of nine AI engineering patterns written so that someone deciding how to attack a piece of AI work can tell quickly whether this pattern is the one that applies. Read "Reach For It When" first, then use the technique table to pick a specific approach, and follow the links at the bottom to the adjacent patterns.

## Key Takeaways

- **Knowledge or behaviour: that one question routes the whole decision.** Missing or stale facts go to RAG. A format, tone, or reasoning pattern the model will not hold goes to fine-tuning.
- **Fine-tuning is a weak and expensive way to teach facts.** The controlled comparison (Ovadia et al., EMNLP 2024) found RAG consistently beat unsupervised fine-tuning for knowledge, both for facts seen in training and for entirely new ones.
- **Exhaust prompting first, and mean it.** The Applied LLMs practitioner collective's guidance is explicit: consider fine-tuning only once prompt engineering cannot reach the required performance, and most teams who fine-tuned early regretted it.
- **When you do fine-tune, PEFT is the 2026 default.** LoRA trains well under 1% of weights and can beat full fine-tuning by avoiding catastrophic forgetting; QLoRA puts a 65B fine-tune on a single 48GB GPU.
- **Hybrid is the production shape, not a fallback.** Fine-tune for stable behaviour, layer RAG on top for volatile citable facts.

## What It Is

Model adaptation is the set of competing techniques for making a general-purpose model do a specific job. They sit on two independent axes. Prompting and RAG operate at inference time and never touch model weights; fine-tuning modifies the weights. Separately, prompting and RAG mostly address *knowledge* (what the model has in front of it), while fine-tuning mostly addresses *behaviour* (how the model acts by default). Newer academic work proposes "post-training adaptation" as a more precise umbrella for the weight-modifying half, but "model adaptation" remains the term in day-to-day practitioner use.

## Reach For It When

Every substantial piece of LLM work makes this choice, usually implicitly. Make it explicitly, in this order:

- **Always start at prompting.** Zero infrastructure, instant iteration, and it is the recommended first step in every serious framework. A detailed system prompt plus three to five few-shot examples is the baseline everything else must beat.
- **Escalate to RAG when the failures trace to missing knowledge.** Proprietary documents, events after the training cutoff, anything that changes weekly, and anything that must be citable back to a source. If the model would be right *given the document*, the problem is retrieval, not the model.
- **Escalate to fine-tuning only when the failures trace to behaviour.** The hard gate: you have tried a detailed system prompt with few-shot examples and the output is *still* inconsistent on a narrow, high-volume, well-defined task. Output format, house tone, domain vocabulary, or a reasoning pattern the model cannot reliably hold.
- **Fine-tune to make a smaller model do a bigger model's job.** A distinct and legitimate trigger: cost and latency reduction at scale, or moving proprietary examples out of every request and into the weights.
- **Go hybrid when both apply.** High-stakes production systems (legal, medical, regulated finance) fine-tune for reliable form and retrieve for current fact.
- **Do not reach for fine-tuning at low volume.** It is a one-off setup cost amortised over inference. Below sustained production traffic, prompting stays cheaper; the exact crossover depends on your token mix, so compute it rather than copying a figure.

**Routing check before you escalate at all:** you cannot tell whether prompting failed without a measurement. Evals are the prerequisite, not the follow-up. See [[evals]].

## Core Techniques

| Technique | What it does | When to use it |
|---|---|---|
| **Zero-/few-shot prompting** | Steers behaviour with instructions and 3-5 in-context examples, no infrastructure | First attempt at every new task. The thing everything else must beat |
| **Prompt caching** | Serves a repeated prompt prefix at roughly 0.1x input price after a 1.25x write | When the answer is "few-shot works but is too expensive". Often removes the cost argument for fine-tuning entirely |
| **Retrieval-augmented generation (RAG)** | Injects retrieved, source-attributable documents into the prompt at query time | Knowledge is dynamic, must be cited, or is too large to fit in weights |
| **Full fine-tuning (SFT)** | Updates all weights on a labelled task dataset | Largest behaviour shift, highest compute and data cost, highest catastrophic-forgetting risk. Reserve for cases where PEFT demonstrably underfits |
| **LoRA** | Freezes the base model, trains small low-rank matrices in attention and MLP layers, typically well under 1% of parameters | The default fine-tuning method when GPU memory allows. Also the safer one: it preserves base-model capability |
| **QLoRA** | 4-bit NF4 quantisation of the frozen base plus LoRA adapters, cutting VRAM sharply | Consumer-GPU or budget-constrained fine-tuning. The standard entry point |
| **DoRA** | Splits the weight update into magnitude and direction, applying LoRA to direction only | Often outperforms LoRA on downstream tasks. Benchmark before adopting: unmerged DoRA can add real runtime and memory overhead versus LoRA, and the zero-overhead case only holds once adapters are merged for inference |
| **Preference optimisation (DPO / RLHF / GRPO)** | Post-SFT alignment on preference pairs or verifiable rewards | Polishing style and safety after base fine-tuning. Behaviour shaping, never knowledge injection |
| **Continued pre-training (CPT)** | Further pre-training on large volumes of raw domain text before task tuning | Deep terminology grounding in high-stakes domains, ahead of SFT. Expensive; rarely the right first move |
| **Distillation** | Trains a small student to mimic a large teacher | Cost and latency reduction at serving time, not new knowledge or behaviour |
| **Hybrid fine-tune + RAG** | Fine-tuned behaviour with retrieval layered on for volatile facts | The production consensus for high-stakes systems |

## Use Cases & Examples

- **Support assistant over a changing product wiki.** Pure RAG. The failure mode is the model not knowing this week's pricing, which fine-tuning cannot fix without a retrain. Retrieval also gives you the citation the support team needs.
- **Structured extraction at scale on a fixed schema.** Prompting with few-shot plus structured-output constraints usually holds. If it still drifts across thousands of calls, that is the textbook fine-tuning case: narrow, high volume, behavioural, and cheap to evaluate.
- **Regulated-domain assistant (legal or medical).** Hybrid. Published 2026 scoping reviews catalogue fine-tune-plus-RAG systems evaluated for medicine, including federated-RAG and knowledge-graph variants, but the evidence base is small (single digits of eligible studies) and framed as promising rather than proven at deployment. Treat hybrid as the right shape to design toward, gated by clinical validation and governance before production, not as an already-deployed pattern.
- **Cost reduction on a proven pipeline.** Once a large model's behaviour is settled and you have thousands of good input-output pairs, QLoRA a smaller open-weights model onto that behaviour. The economics here are the strongest argument for PEFT: a small-model QLoRA run costs single-digit dollars of GPU time, orders of magnitude below a full-parameter run of the same model.

## Anti-Patterns

- **Fine-tuning to inject facts.** The most-cited failure in the whole area. It is slower, costlier, and less accurate than retrieval, and correcting a wrong fact requires a full retrain instead of a document edit.
- **Fine-tuning before exhausting prompting.** Spends a one-off setup cost on a problem a better system prompt would have solved, and locks in whatever the model was already doing wrong.
- **Full fine-tuning by default.** Catastrophic forgetting is real: specialising the model degrades its general capability. This is the single largest reason LoRA and QLoRA displaced full-parameter updates.
- **Fine-tuning on a snapshot with no refresh plan.** Baked-in knowledge ages silently and nothing alerts you. If a fine-tune carries facts at all, pair it with drift monitoring. See [[observability]].
- **Assuming fine-tuning is available.** Availability varies by provider as of Aug 2026: Anthropic's Claude API exposes prompting, prompt caching, tools, and retrieval with no fine-tuning endpoint, while OpenAI and Azure offer hosted fine-tuning for selected closed models (GPT-4.1 SFT/DPO, GPT-5 RFT in preview). Check the target provider and model first: choosing "fine-tune" can mean choosing a different provider or model family, but not always.
- **Treating distillation as free.** Contested: a 2025 arXiv paper on distilled pretraining finds it improves test-time scaling but can impair in-context learning through the same mechanism. Not yet reflected in practitioner guidance, and worth flagging as an open research question rather than settled.

## Mental Models

- [[mm-model-adaptation]] - the knowledge-or-behaviour cut and the one-rung-at-a-time escalation rule, in short form.
- [[mm-routing]] - the recurrence-or-value bar that decides whether any of this gets built.
- [[mm-token-economics]] - prompting, caching, RAG, and fine-tuning are four different cost curves for the same output.
- [[mm-verification]] - you cannot claim an escalation was justified without a check that prompting actually failed.
- [[mm-steering]] - the prompting rung of the ladder is steering; escalate only when steering demonstrably runs out.

## State of Practice

As of Aug 2026:

- **Consensus is unusually strong here.** Default to prompting, add RAG for facts, reserve fine-tuning for behaviour, combine both for high stakes. That ordering appears near-identically across practitioner frameworks, vendor documentation, and the peer-reviewed comparison. Vendor guidance converges too: OpenAI's own optimisation documentation orders it evals, then prompt engineering, then fine-tuning if needed.
- **PEFT is mature and production-ready.** LoRA and QLoRA carry the bulk of fine-tuning work, with mature tooling (Unsloth, Axolotl, Hugging Face PEFT). Full-parameter tuning is reserved for maximum-quality cases or where PEFT underfits.
- **QLoRA plus DoRA is a rising combination** for new fine-tuning projects, but benchmark it: unmerged DoRA can carry meaningfully higher inference overhead than LoRA, so the choice should follow measurement, not default assumption.
- **Contested (unchanged from the source research):** the distilled-pretraining trade-off above, where improved test-time scaling appears to come at the cost of in-context learning.
- **Weakly evidenced, treat with care:** specific dollar thresholds for when fine-tuning pays back. The order-of-magnitude gap between PEFT and full fine-tuning is well corroborated; precise per-run figures and monthly-spend crossover points circulate mainly through low-quality content and should be recomputed for your own workload.

## Links

- [[context-engineering]] - what actually reaches the model. RAG is a context-assembly problem before it is a model problem.
- [[evals]] - the measurement that licenses any escalation up the ladder.
- [[memory]] - the adjacent question of what persists across sessions, versus what is retrieved per query.
- [[observability]] - drift monitoring, which is how baked-in or retrieved knowledge is caught going stale.
- [[tools-mcp]] - giving the model live access instead of baking knowledge in, often the cheapest answer of all.

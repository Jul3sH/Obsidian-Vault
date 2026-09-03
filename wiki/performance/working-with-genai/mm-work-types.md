---
type: reference
created: 2026-09-03
status: active
tags: [working-with-genai, work-types, mental-models]
---

# MM: Work Types

This is the Work Types mental model: classifying a piece of work by how its
output gets checked, before deciding anything else about it. It was created
(3 Sep 2026) as the missing first step of the [[genai-task-workflow]] chain,
when designing [[genai-task-workflow-log]] exposed that routed work had no shared vocabulary
to be recorded or recalled in. Read it when routing any piece of work to AI, and
when writing a [[genai-task-workflow-log]] entry.

**One-liner:** Classify work by how it gets checked, not what it is about.

**Reach for it when:** routing any piece of work to AI, and when writing a
[[genai-task-workflow-log]] row.

**Position in the chain:** first. Work types classifies, verification permits,
routing decides the architecture, steering configures it. Full chain:
[[genai-task-workflow]].

## Key Takeaways

- The check profile is the cut: two types checked the same way route the same
  way, whatever their subject.
- The type carries its default check; [[mm-verification]] then tests whether that
  check holds for this instance.
- Artefacts are bundles, not types - decompose them into typed runs, or classify
  a whole-artefact run by its dominant check.
- The list is provisional by design: the log's entries are the evidence that
  amends it.

## Principles

The seven types. Check-form vocabulary is defined in [[mm-verification]] (the
three forms) and [[verification-tactics]] (independence routes); this table uses
it and does not restate it.

| Work type | Description | Check form | How the check is done |
|---|---|---|---|
| **Research sweep** | Gathering material from outside sources and synthesising it into findings | Agent eval + Deterministic | Clickable source per claim (link resolves or it does not); a different model reads the sources - not the worker's summary - and checks every claim. Residual no check catches: what the research never went looking for |
| **Extraction** | Pulling structured items out of a defined source set | Deterministic | Count returned vs expected; totals sum; format validates. A script could do it |
| **Analysis** | Deriving a conclusion, comparison, or numbers from material you supply | Agent eval + Human judgement | A different model re-derives the numbers against acceptance criteria written before the run; the assumptions and judgement calls underneath stay yours |
| **Taste work** | Output where being right means matching your judgement: messages in your voice, naming, framing, tone | Human judgement only | No external criterion exists, so no machine check does. You hold the pen; AI critiques and fact-checks. Defined in [[verification-bottleneck]] |
| **Critique** | Reviewing something that already exists for errors, gaps, false claims | Human judgement (cheap) | Read each finding, decide in seconds whether it is fair - and check the critic: findings can themselves be wrong |
| **Build** | Code, scripts, skills, hooks, automations | Deterministic | Run it and see. Test every branch before declaring it done |
| **Wiki ops** | Filing, indexing, mirroring, compiling, link fixes | Deterministic | Sections present, links resolve, frontmatter parses, mirror matches source. Wrong is obvious and cheap to undo |

The ordering the table exposes: three types are deterministic (cheap to delegate
at volume), two are eval-covered (delegate with an independent checker), two land
on your judgement (critique cheaply, taste work irreducibly).

## Guidelines

- Classify a whole-artefact run by its dominant check; better, decompose the
  artefact into typed runs (evidence-gathering is a sweep, scoring is analysis,
  wording in your voice is taste work, filing is wiki ops).
- Amendment rule: do not add a type until three real log entries refuse to fit an
  existing one; merge any two types that turn out to be checked identically.
- The Check line of a [[genai-task-workflow-log]] entry takes only the canonical values from
  [[mm-verification]], plus the independence route where the check is an eval.

## Limitations

Derived from ~3 months of routed work in this vault, not a proven taxonomy - the
log is the test, and the list only needs to be good enough to start. Says
nothing about whether the work is worth doing, what it costs, or its blast
radius; those are [[mm-token-economics]] and [[mm-blast-radius]]. Only one term
(taste work) has an external definition; the other six are labels coined here
for buckets whose checking doctrine is existing wiki content.

## Detail

[[mm-verification]] and [[verification-tactics]] (the check forms and how evals
earn independence), [[genai-task-workflow-log]] (the accumulating evidence),
[[genai-task-workflow]] (the chain this model opens).

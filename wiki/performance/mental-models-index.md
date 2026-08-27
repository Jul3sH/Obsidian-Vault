# Mental Models Index

> *Navigation only: every mental model in the vault, listed by workstream. Each line is the model's one-liner. Models follow the six-slot format defined in `documentation-conventions.md`; after writing a new mental model, add it here.*

## What belongs here

Every mental model (`mm-*.md`) in the vault is listed here, whatever folder it
lives in. A model lives beside its detail articles, not in this index's folder.
The vault-wide convention is two-tier: a model is the reach-for layer (one
pattern, six-slot format, evidence table linking its original sources); its
detail articles hold the fuller framework, linked from the model's Detail slot,
and the articles win if they disagree. Each folder's own index maps its
articles to the models built on them.
For AI-related models, the folder is decided by the subject of the model's
sentences:

- Subject is **you** (your judgement, checking, dispatch, configuration) →
  `performance/working-with-genai/`
- Subject is **the system** (its architecture, what it must do to work) →
  `technology/`
- Tie-breaker: the **Reach for it when** slot. Reached for while doing your work →
  operator discipline; reached for while evaluating or building a system →
  technology.

## Wellbeing

*(none yet)*

## Relationships

*(none yet)*

## Finance

*(none yet)*

## Career

*(none yet)*

## Performance

### The human mind

- [[mm-confirmation-bias]] - You will find what you're looking for, so look for the disconfirming case

### Working with others

- [[mm-sell-their-benefit]] - People don't buy your idea, they buy what it does for them
- [[mm-never-say-youre-wrong]] - A correction only lands as an option that saves face
- [[mm-choose-winnable-battles]] - A battle you can't win costs credibility even when you're right
- [[mm-never-bitch]] - Every complaint reaches its subject eventually, and jokes count
- [[mm-assume-it-gets-repeated]] - Say and write only what survives being forwarded
- [[mm-bring-solutions]] - A problem without a mitigation is a complaint
- [[mm-results-are-the-currency]] - Results are the currency; effort and intentions don't spend
- [[mm-clarify-before-starting]] - The clarifying question is always cheaper than the rework
- [[mm-evaluate-before-committing]] - Can-do without evaluation is how you end up owning the impossible
- [[mm-listen-then-speak]] - Hear all of it, prove you heard it, then answer what was asked
- [[mm-write-it-down]] - In political environments, if it isn't written down it didn't happen
- [[mm-delegate-the-what]] - Delegate early, specify the what, never the how
- [[mm-proximity-is-infrastructure]] - Proximity is a career asset, and the window to build it closes fast
- [[mm-prepare-every-engagement]] - If you cannot state the point of the meeting before you walk in, you are not ready for it
- [[mm-deliberate-brand]] - How you come across is a decision, not a mood
- [[mm-surface-risk-formally]] - Raise it formally, or wear it silently; there is no third option
- [[mm-share-the-credit]] - Frame the win as joint before your manager frames it as solo
- [[mm-assertiveness-is-professional]] - Pushing back is professional; being a walkover costs the respect it was meant to buy

### Working with yourself

- [[mm-never-react]] - Between the trigger and the response, walk away
- [[mm-verify-before-acting]] - However convincing it looks, verify it before you act on it
- [[mm-start-to-start]] - Fear and stress shrink the moment you start; they never shrink while you wait
- [[mm-fear-wears-a-disguise]] - Fear presents as a reasonable objection; name it before believing it
- [[mm-ship-early]] - Early and done beats late and polished
- [[mm-setbacks-are-glitches]] - Recover fast: a setback is a data point, not a verdict
- [[mm-ease-and-grace]] - The composed persona is a decision made in advance, not a mood
- [[mm-commit-with-a-forcing-function]] - Analysis ends when a deadline, booking, or written choice forces it
- [[mm-guard-the-critical-path]] - Firefighting is optional; the critical path is not
- [[mm-price-the-priority]] - Prioritise by tangible cost, not by interest or comfort
- [[mm-start-with-the-deliverable]] - Open the deliverable first and let the work organise itself around it
- [[mm-competence-as-fuel]] - Confidence is downstream of delivery, not a precondition for it
- [[mm-integrity-is-binary]] - A commitment to yourself is on or off; there is no version of it that bends for a good reason
- [[mm-systems-are-motivation]] - The tracker is not overhead on the work, it is the engine that gets the work done
- [[mm-timebox-the-rabbit-hole]] - Curiosity without a timebox is scope creep wearing a productive disguise
- [[mm-impaired-state-rules]] - Tired, drinking, or emotional: the rule decides, not you
- [[mm-payoff-vs-prestige]] - Learn for what it produces, not for how impressive you'll sound explaining it
- [[mm-visual-representation-bias]] - A vivid picture of the good day is not a decision; ask for the ordinary bad day too
- [[mm-be-coachable]] - You hired the coach; interrupting them to correct them is paying to not listen

### Working with GenAI

- [[mm-rule-layering]] - Fast learns, slow remembers - and must is not should
- [[mm-verification]] - Generation scaled and verification did not
- [[mm-routing]] - Pick the lightest tool that still leaves you a result you can inspect
- [[mm-steering]] - An instruction is not a guarantee
- [[mm-token-economics]] - Context is rent, not a purchase
- [[mm-blast-radius]] - Assume the wrong call happens, then decide whether you could live with it
- [[mm-model-adaptation]] - Ask whether the model is missing information or missing a habit, then climb one rung at a time

[[mm-verification]], [[mm-routing]] and [[mm-steering]] chain: verification decides
what is possible, routing decides the architecture, steering configures it.
[[mm-model-adaptation]] continues the chain when steering runs out and the answer
is still wrong. [[mm-token-economics]] sits alongside them and prices what routing
chose; [[mm-blast-radius]] sits alongside them and bounds how much reach it gets.

## Personal

*(none yet)*

## Technology

- [[mm-memory-pillars]] - Memory is four jobs in dependency order, and injection is the one nobody builds

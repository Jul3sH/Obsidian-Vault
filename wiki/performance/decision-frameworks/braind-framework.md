---
type: reference
created: 2026-06-20
source: Medical informed consent literature; widely adapted for general decision-making
---

# BRAIND Framework

## Purpose

BRAIND (Benefits, Risks, Alternatives, Intuition, Need time / Nothing, Decision) is Julian's default framework for evaluating one option in depth before committing to it. It is used for any decision that gets a journal entry, and for decisions that have outgrown [[first-decision-framework|FIRST]].

Sections: The Variants · The Questions · When to Use (incl. the Assumptions section) · Complex decisions · How It Compares to the 7-Step Process · Key Takeaways · Links · Document Log

## The Variants

BRAIND comes from the medical informed-consent checklist BRAIN and its variants. It keeps every element of them.

| Letter | BRAIN | BRAN | BRAND | BRAIND |
|--------|-------|------|-------|--------|
| **B** | Benefits | Benefits | Benefits | Benefits |
| **R** | Risks | Risks | Risks | Risks |
| **A** | Alternatives | Alternatives | Alternatives | Alternatives |
| **I** | Intuition (gut feeling) | - | - | Intuition |
| **N** | Need time / Nothing (is inaction better?) | Need time / Nothing | Need time / Nothing | Need time / Nothing |
| **D** | - | - | Decision (explicit final choice) | Decision |

**On the name:** BRAIND is BRAIN plus the D step: all six elements, none dropped. It was first written "BRAINED" (on [[dec-uk-move|the UK-move decision]], see [[why-brained]]); BRAIND has been the standard spelling since 4 Sep 2026.

### Which variant to use

| Variant | Use when |
|---------|----------|
| **BRAIN** | You want to include gut feeling as a legitimate input |
| **BRAN** | You want to stay objective and remove personal bias |
| **BRAND** | You want a formal close - the D forces an explicit commitment at the end |
| **BRAIND** | You want *both* the gut named (I) and a forced final choice (D) - all six elements |

**Julian's default: BRAIND.** The **I** step names the gut as a legitimate input (his gut is often load-bearing) and the **D** step forces a dated commitment (his diagnosed failure mode is commitment, not analysis - see [[decision-maker-profile]]). Framing cons as **R**isks also lets fear-driven beliefs be probability-tested via [[belief-assumption-testing]] rather than accepted as fact. A journalled decision run in anything other than BRAIND records why in its entry.

## The Questions

- **Benefits:** What are the benefits of this option?
- **Risks:** What are the downsides and potential harms?
- **Alternatives:** What other options exist? Any of them may become a BRAIND of its own.
- **Intuition:** What is my gut telling me, and what is it relying on?
- **Need time / Nothing:** Do I need more time? Is doing nothing a better option?
- **Decision:** Based on the above, what am I choosing? Dated, and locked.

## When to Use

- Getting it wrong would be expensive or hard to undo, or the decision earns a journal entry
- The issue will not fit in a sentence after [[first-decision-framework|FIRST]] step 2
- You have one clear option to evaluate before committing (yes/no, or option A with alternatives named)

A BRAIND run is written as a `<Question>-BRAIND.md` file in the fixed format in [[documentation-conventions]] Part 1; reference implementation [[HK-Return-BRAIND]]. Beyond the six steps, the file carries an **Assumptions and the plan to clear them** section between I and N: a numbered table of every assumption the B, R, A and I sections rest on, each with the action that clears it, who and when, open items first. It turns the analysis into checks that can be closed, rather than doubts that keep the decision open.

## Complex decisions

When a decision touches several areas of life at once, or depends on things not yet settled, three methods map into the framework. All three were used on [[HK-Return-BRAIND]]; the formatting rules for each are in [[documentation-conventions]] Part 1.

| Method | Applies to | How |
|--------|-----------|-----|
| **1. Split by workstream** | B, R, A, I | Give each section a subsection per workstream the decision affects (Wellbeing, Relationships, Finance, Career, Performance, Personal), and include only the ones that apply. This shows where the benefits and risks actually sit, and stops one workstream (usually Finance) from crowding out the rest. |
| **2. Clarify the intuition** | I | Run [[counterfactual-questioning]] to find which factor is driving the gut feeling (remove one factor at a time and see if the feeling changes), then [[belief-assumption-testing]] to label the beliefs behind it as Fact, Assumption or Belief and test them. The Intuition section then says what the gut is telling you and what it rests on, not just how it feels: each core intuition is a numbered point, with the runs that support or contradict it and the beliefs behind it nested beneath. |
| **3. Conditions and dependencies** | D | When the decision is dictated by terms still to be met, or by events outside your control, write it as a conditional decision: the decision sentence, then the **conditions** (the terms that must hold for a yes), the **dependencies** (what else must happen, with owner and where it stands), and **what happens otherwise** if a condition fails or the deadline passes. |

On HK-Return the raw intuition captures, the counterfactual runs and the beliefs each live in their own file ([[HK-Return-Intuition]], [[HK-Return-Counterfactuals]], [[HK-Return-Beliefs]]), and the I section holds a signed-off summary linking to them.

## How It Compares to the 7-Step Process

| 7-Step | BRAIND coverage |
|--------|----------------|
| 1. Identify the decision | Assumed - run [[first-decision-framework\|FIRST]] step 2 first if it is fuzzy |
| 2. Gather information | Assumed - you have enough to evaluate |
| 3. Identify alternatives | Yes (A) |
| 4. Weigh the evidence | Partial - B and R cover pros/cons but not a full matrix |
| 5. Choose among alternatives | Yes (D) |
| 6. Take action | Not covered |
| 7. Review | Not covered |

BRAIND is a pre-commitment evaluation tool, not a full process. Pair it with [[first-decision-framework|FIRST]] step 5 (Then: next steps) once the D step is done.

## Key Takeaways

- BRAIND is the default for any journalled decision; FIRST comes first and escalates here.
- The N step (Need time / Nothing) is the most important for avoiding sunk-cost decisions - it gives explicit permission to pause or walk away.
- BRAIND is not a replacement for problem definition. If the problem is still fuzzy, run [[first-decision-framework|FIRST]] step 2 (Issue) first.
- The I step is valid - intuition encodes pattern-matched experience. Name it so it can be weighed alongside evidence, and on complex decisions clarify it with counterfactual questioning and belief testing.
- For multi-dimensional decisions, split B, R, A and I by workstream so no area of life is left out.
- Every assumption gets an action that clears it. A decision that hangs on unmet terms is written with its conditions, dependencies and fallback, so it can still be locked.

## Links

- [[choosing-a-decision-framework|Choosing a Decision Framework]] - which framework to use and when
- [[documentation-conventions|Documentation Conventions]] Part 1 - the fixed file format for a BRAIND run; reference implementation [[HK-Return-BRAIND]]
- [[first-decision-framework|FIRST Decision Framework]] - the first pass for small decisions; where a decision starts before it grows into a BRAIND
- [[counterfactual-questioning]] and [[belief-assumption-testing]] - the tools that clarify the I step
- [[seven-step-decision-process|Seven-Step Decision Process]] - full deliberate process for high-stakes decisions

## Document Log

| Date | Entry |
|------|-------|
| 2026-10-01 | Assumptions section added under When to Use; Complex decisions extended to three methods (nested runs and beliefs under each intuition; conditions and dependencies in D), matching documentation-conventions rows 6 and 9. |
| 2026-10-01 | Renamed from brain-brand-framework to braind-framework at Julian's instruction; variant column spelled BRAIND; default changed from BRAND to BRAIND; Purpose and the "Complex decisions" section (workstream split, intuition clarification) added. |

---
type: reference
created: 2026-08-13
status: active
---

# Routing Work: Mental Model

This is the recall card for deciding how to run a piece of work. It is the whole
model compressed into statements of the form *this input decides this thing*, with
no explanation attached, so it fits on one screen and can be held in your head.

Read it before starting substantial AI work. When a statement needs justifying, or a
case sits on a line and you need the arithmetic, go to
[[routing-work-to-agents]], which is the canonical version and carries the evidence.
If the two ever disagree, that one wins and this one gets corrected.

## The routing

| Input | Decides |
|---|---|
| **Size** | Chat or one agent. Nothing else, and only when you are not splitting. |
| **Separation + independence** | Whether the work **wants** splitting. |
| **Verification** | Whether it is **allowed** to split. |
| **Recurrence or value** | Whether it gets built at all. |

Separation and verification answer different questions. One is demand, the other is
permission. You can want a split and be refused one.

## What each failure costs you

| Fail this | You get | What you lose |
|---|---|---|
| Size | Chat | Nothing. Chat was the right tool. |
| Separation | One agent | Nothing. One agent was the right tool. |
| Verification | You do it yourself | All of it. No AI on this job. |
| Economics | You do it yourself, this once | All of it, for now. Do it again and it may qualify. |

The first two just point you at a simpler tool and you keep the leverage. The last
two take AI off the table for this piece of work, which is why they are the two
worth designing around rather than discovering.

## The verification layer

| Input | Decides |
|---|---|
| **Verification design** | Whether multi-agent is on the menu at all. |
| **Verification cost** | Part of the setup cost, so it feeds the worth-building test. |
| **Different vendor** | Model independence. |
| **Different source information** | Information independence. The one people skip, and it is free. |
| **What each layer can catch** | Who checks what. |

## The three forms of verification

Every check is one of these, or a layering of them.

| Form | Catches | Fails when |
|---|---|---|
| **Deterministic** | Mechanical. Does it run, does it reconcile, do the citations resolve. | There is nothing to assert against, or the question needs meaning. |
| **Agent eval** | Semantic, at volume. On brief, self-consistent, claim actually supported. | It shares the worker's model or its information, so it confirms the error. |
| **Human judgement** | Whether it is the right thing at all, whether it matches what you know, whether the framing is acceptable. | Volume. It degrades quietly, not loudly. |

Layer them cheapest first, and spend judgement only where it discriminates.
Attention spent on what the first two layers would have caught is attention you no
longer have for the third.

## The two orderings

- **Conventional:** pick the architecture, then add verification.
- **Correct:** design the verification, and the architecture falls out.

This is the only statement here that changes what you do first.

## The three rules, if you remember nothing else

1. Split on need, not on size.
2. Never split what you cannot check.
3. Never build what will not repeat or will not matter.

And the one-line version of all of it: **pick the lightest tool that still leaves you
a result you can inspect.** Chat is not the weak answer, it is the clean one.

Setup templates for each route: [[routing-work-prompts]].

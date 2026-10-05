---
name: feedback-invoke-behaviour-check
description: "When a conversation enters one of behaviour-check's trigger situations, invoke the skill; never raise a bias or mental-model card informally in passing instead."
metadata:
  type: feedback
  created: 2026-10-05
---

# Invoke behaviour-check; don't paraphrase it

**The correction (5 Oct 2026):** in one session on the TTI message to Stephan, three behaviour-check triggers arose (interpreting Stephan's missed call as avoidance; weighing the HK lean against the UK lean; the send point for the message). Claude mentioned matching cards informally (the boring explanation, wishful thinking) but never invoked the skill, so the indexes were never read. Commitment-stalling, the card that fitted the send point, went unraised until Julian asked. Julian: "some of these should have fired", "it's important and should have a memory."

**Why it matters:** the skill's value is a fresh, narrow read of [[biases-index]] and [[mental-models-index]] at the moment it can still change the outcome. An informal mention from memory picks the card Claude happens to recall, skips the precedence rules, and misses new cards.

**How to apply:**
- When a trigger situation in the behaviour-check description arises, call the Skill tool with `behaviour-check` at that moment, before continuing the work. Do not substitute a paraphrased card.
- Highest-risk moments: a send or commit point on outbound messages, interpreting someone's silence or motives, and weighing life or career options. These fire mid-conversation, inside other work, which is when it is easiest to skip.
- The skill's own rules still apply: at most two cards, brief, and Julian overrules freely (5 Oct: he rejected commitment-by-proxy for a message he had asked Claude to draft; accepted, nothing logged).

Related: [[feedback-narrative-fill]] (one bias that also acts outside decision points); [[feedback-visual-representation-bias]].

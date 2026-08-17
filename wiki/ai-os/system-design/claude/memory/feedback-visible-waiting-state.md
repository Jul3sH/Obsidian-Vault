---
name: feedback-visible-waiting-state
description: "When blocked on Julian's input, the ask must be unmissable - a single explicit question at the end of the turn, never folded into a status paragraph"
metadata: 
  node_type: memory
  created: 2026-08-17
  type: feedback
  originSessionId: 1046345e-3f48-473b-9dbf-e1c6926daa52
  modified: 2026-08-17T19:53:28.268Z
---

# Make the Waiting State Unmissable

**The correction (17 Aug 2026):** During the AI Engineering Concept Map planning session, the interview sat blocked on Julian's confirmation for three turns while other work (goal syncs, subagent fixes) churned on. The pending question was restated each time, but buried inside multi-topic status updates. Julian: "It was not clear you are waiting for me."

**Why:** Julian has ADHD traits and multi-threads heavily. A question embedded in a paragraph of status reporting reads as commentary, not as a blocker. If he doesn't see the ask, the thread silently stalls and he attributes the stall to the agent, not to a pending input. The cost compounds: each turn that re-buries the question adds noise that makes it harder to spot.

**How to apply:** When a turn ends blocked on Julian's decision or confirmation:
- Put the ask as the LAST thing in the message, on its own line or short paragraph, phrased as a direct question.
- Prefix it visibly (e.g. bold "**Waiting on you:**" or "**Question for you:**") so it survives skimming.
- One question per turn where possible; if several are pending, number them explicitly rather than scattering them.
- Status updates go ABOVE the ask, never after it - the ask is the closing line.

Related: [[feedback-commitment-forcing]] (force a written choice), [[feedback-bare-identifiers]] (don't make him reconstruct context to answer).

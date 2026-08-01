---
name: feedback-verify-before-writing
description: "Verify a checkable claim in the same turn you write it into a file, not the turn after Julian questions it"
metadata:
  node_type: memory
  type: feedback
  created: 2026-08-01
  originSessionId: 45855fa6-bf25-4723-b105-e2fcc79eae6d
  modified: 2026-08-01T05:00:23.822Z
---

When writing a factual claim into a wiki file, verify it in the same turn. Do not publish a claim that a single command would settle and leave the checking to Julian.

**Why:** on 2026-07-31/08-01 I made six errors of one shape in a single session: asserting a checkable fact without checking it, then running the confirming command only after Julian pushed back. Examples: claimed an agreement "had no home" when it was written at `multi-agent-protocol.md:51`; published a "human re-narration tax" finding into the wiki, then measured it at 0.95x (false); said a retrieval scheme was "already documented" when it had no article; preserved a claim about a "principles register" that does not exist; wrote a `grep` anchored to `[[` into a link-hunting rule, which silently misses every path link. Every one was one bash call away. The effect is that Julian becomes the verifier for claims I could check myself, and unverified sentences become wiki facts.

**The trigger condition is a mode switch.** In *analysis* mode every claim came from a script just run, and nothing shipped unverified. In *authoring* mode claims came from recall and inference but kept the same confident register and got published. Errors cluster in authoring mode. Two amplifiers: fast accept-and-build rhythm removes the natural verification pause, and taxonomy/model work rewards internal consistency, which feels like evidence and is not.

**How to apply:**
- Before writing a factual claim into any file, run the check. Especially: "X is documented at Y", "Z does not exist", "A already covers B", and any command or code snippet placed in a rule (run it before publishing it).
- Mark measured versus inferred explicitly in the body, not only in a caveats section.
- Treat "this model feels clean" as a prompt to test it, not to ship it.
- Related: [[feedback-assumption-audit]] (challenge load-bearing assumptions at definition time) and [[feedback-overanalysis-check]].

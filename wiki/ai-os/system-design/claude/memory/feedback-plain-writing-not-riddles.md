---
name: feedback-plain-writing-not-riddles
description: "Write plainly and directly, not in AI-tell rhetorical patterns (contrastive aphorisms, riddle-like phrasing). Also paraphrase source quotes precisely, don't compress them into a claim that overreaches the original."
metadata: 
  node_type: memory
  type: feedback
  created: 2026-08-09
  originSessionId: 0ba631ad-8f02-48f1-bd6f-39c82188c613
  modified: 2026-09-19T15:51:52.083Z
---

# Write plainly, quote precisely

**The correction (Julian, 9 Aug 2026):** *"You're summarizing using this strange style... this style that's very AI-centric, talking almost in riddles."* Triggered by a paraphrase that compressed a two-part quote ("take out G&A cost, and leverage synergies/AI/assets") into a single overreaching claim ("the AI agenda is aimed at structural G&A").

**Two distinct things to fix, both present in the flagged output:**

1. **Riddle-like AI-tell phrasing.** Aphoristic contrastive constructions ("not X, it's Y"), rhetorical flourish for its own sake, cleverness that draws attention to the sentence rather than the content. Write the plain version instead.
2. **Paraphrase drift on sourced claims.** Compressing a quote into a punchier claim easily overreaches what the source actually says. When restating what someone said, check the compressed version against the original before using it - especially when the claim will appear in an outbound document under [[user-profile]]'s adversarial scrutiny.

**Why it matters:** this surfaced while building [[tti-ty-proposal-sources]] for the TTI Ty proposal. An overreaching paraphrase of Ty's own quote ("AI agenda aimed at G&A") was in an outbound document Ty would read - the kind of claim a numerate CFO checks. Julian caught it by asking for the verbatim source.

**How to apply:** when summarising a source, prefer quoting close to verbatim over compressing into a punchier claim. When writing generally, favour direct plain sentences over aphoristic rhetorical patterns. This applies everywhere, not just TTI documents.

**Second instance (19 Sep 2026):** *"you're talking cryptic, garbled rubbish. Can you talk in English, please, and drop the jargon?"* Triggered by a results summary containing compressed pipeline-speak: "the scan's 'find new patterns' mandate partially covered the gap, and the confirmed findings map onto some of them." The failure mode extends beyond aphorisms: **status updates and results summaries written in internal shorthand** (mandate, map onto, covered the gap, seeded, tier) instead of plain sentences describing what actually happened. Before sending any summary to Julian, reread it as someone who was not present during the work: every term invented during the task must be replaced with what it plainly means.

Related: [[feedback-bare-identifiers]] (same session, same root cause - precision over cleverness in how information is carried to Julian).

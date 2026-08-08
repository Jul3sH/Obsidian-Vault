---
name: feedback-bare-identifiers
description: "Never use a bare identifier (F1, S3, §4, BWS-39, POR-3) for work Julian isn't actively holding in his head - always give the identifier plus what it says and which document it lives in"
metadata: 
  node_type: memory
  type: feedback
  created: 2026-08-08
  originSessionId: 0ba631ad-8f02-48f1-bd6f-39c82188c613
  modified: 2026-08-08T12:26:06.107Z
---

# Bare identifiers are cryptic - always carry the context

**The correction (Julian, 8 Aug 2026):** *"When you're referring to deliverables that I'm not currently working on, you can just stop using acronyms or deliverable numbers, because they have no meaning. I need some context. I need to know F1 from the document, whatever it is. Otherwise it looks very cryptic, and I was trying to work out what deliverable you are referring to."*

**What triggered it:** repeated use of "F1", "S3", "S7", "§4" across a conversation about the TTI Ty proposal. Each was a real reference (Codex review finding IDs, a section of `tti-ea-governance-value`), but Julian had to reverse-engineer which document each belonged to - and initially read "F1" as a *deliverable* number rather than a review finding.

**Why it matters:** Julian runs six workstreams and dozens of live artefacts. An identifier that is obvious inside one document is meaningless the moment it leaves that document. Making him decode a reference costs him more than the shorthand saves, and it undermines the [[user-profile]] preference for outputs he can hold in his head.

**How to apply:**
- **First mention in any turn:** identifier + what it actually says + which document. *"F1 - the Codex review's only fatal finding, that month 1 reads as discovery so Ty commits before the value case exists"* - not *"F1"*.
- **Applies to:** review finding IDs (F1, S3, M2), Jira keys (BWS-39, POR-3), section numbers (§4), version labels (v1, v3), and any deliverable slug he is not actively working on in that session.
- **Exception:** once established in the current turn, short form is fine for the rest of that turn.
- **Same principle for section references:** *"§4, the mandate section - where the board's authority comes from"* - never a bare *"§4"*.

Related: [[user-profile]] (concise outputs he can hold in his head), and the `AGENTS.md` writing-style rule that length is a defect - brevity must not be bought with decodability.

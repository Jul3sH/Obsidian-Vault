> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/section0-mapping.md`
> Do not edit here — edit the source file and re-sync.

# Section 0: JD-to-Resume Mapping

## Purpose
Create a complete mapping between the target JD requirements and the master resume evidence before any content is written. This ensures nothing is missed and gaps are identified upfront.

## Procedure

### Step 1: Extract Prioritized Map from Input 2 (JD)

Output one Markdown table:

| Priority | Category | JD-stated requirement |
|----------|----------|----------------------|

Rules:
- Priorities allowed: `Core`, `High`, `Medium` only.
- Categories: Skills, Responsibilities, Qualifications/Certs, Tools/Platforms, Domain, Outcomes.
- Each requirement must be a single line — no sub-bullets or wrapped multi-line cells.
- Extract every requirement from the JD. Do not summarise or merge requirements.

### Step 2: Map Each JD Requirement to Verbatim Evidence from Input 3

Output one Markdown table:

| JD-stated requirement | Mapped evidence (Input 3) |
|----------------------|--------------------------|

Rules:
- `JD-stated requirement` text must match Step 1 wording exactly (copy/paste).
- Evidence must come from **Input 3 only** (not Input 1).
- Every quote must be **verbatim** from Input 3.
- Prefix each quote with role context: `Role: <title>, <company> — "<verbatim line>"`
- If role context unavailable: `Section: <section name> — "<verbatim line>"`
- If no evidence exists: `Not evidenced in Input 3.`

### Step 3: List Explicit Gaps

Output one Markdown table:

| Gap | JD asks for | Input 1/3 evidence |
|-----|-------------|---------------------|

Rules:
- List every JD requirement that is `Not evidenced in Input 3` from Step 2.
- `Input 1/3 evidence` must be either:
  - `Not evidenced in Input 1 or Input 3.`
  - OR a verbatim quote with `[Input 1]` / `[Input 3]` tags proving it IS evidenced (meaning it should not be a gap).
- Note where equivalent customer-facing or internal-team evidence may serve as transferable evidence for partner-facing or other gaps. Flag these explicitly so the user can decide whether to use them.

## Decision Gate

End Section 0 with exactly: "Proceed, or iterate further?"

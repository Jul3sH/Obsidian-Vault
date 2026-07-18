> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/section3-skills.md`
> Do not edit here — edit the source file and re-sync.

# Section 3: Skills and Areas of Expertise

## Purpose
Produce a prioritised list of skills aligned to the JD, validated against Input 3 evidence, with missing and implied skills clearly identified.

## Procedure

### Step 1: Extract Required Skills from the JD
Identify all explicitly required skills from Input 2 across: Responsibilities, Qualifications/Certifications, Tools/Platforms/Frameworks.

**Keep two judgements separate (mandatory).** For every candidate skill, evaluate these as *distinct* questions and never conflate them:
- **(a) Evidenced?** — is it backed by Input 3 (a listed skill, role, cert, or achievement)?
- **(b) JD-demanded?** — does Input 2 actually ask for it?

A skill can be evidenced but not JD-demanded (a personal strength the JD never mentions), or JD-demanded but not evidenced (a genuine gap). When you present the candidate table, show the JD basis *only* where a real JD line exists — quote or paraphrase it. If a skill is included on master-evidence alone with no JD hook, say so explicitly ("master evidence; JD does not ask for this") and treat it as a bench/optional item, never as JD-aligned. Presenting master-evidence as though it were a JD requirement is a logged failure mode (see `process-quality-log.md`).

### Step 2: Output Format

Output each skill as one numbered line:

```
1. [ ] **Skill label** - context
```

Rules:
- Use **numbered** items only (no dash bullets).
- Square-bracket marker:
  - `[ ]` for evidenced skills
  - `[*]` for not clearly evidenced in Input 3
- Skill label: bold, max 34 characters including spaces, max 3 words, JD-like wording.
- Context: quote/paraphrase JD text only; aim ≤ 150 characters.
- Prioritise skills in descending order of relevance to Input 2 (JD): most relevant first.

### Validation Gate (before marking anything as missing)

Before marking any skill with `[*]` or placing it in Missing Skills:
1. Search Input 3 for the exact term AND common variants (e.g., TOGAF/EA; ITIL/ITSM; AWS/Azure/Cloud).
2. If found anywhere in Input 3 (including Skills, Education/Certifications, or any role), treat it as evidenced — do NOT mark with `[*]`.
3. Only include genuinely absent items in Missing Skills.

If you later discover an item was incorrectly marked missing, correct it and explain the error.

### Step 3: Output Structure

Produce exactly these three blocks in order:

**1. Prioritized Skills.**
The numbered list from Step 2.

**2. Missing skills**
Only `[*]` skills. For each, provide 3 resume-friendly evidence options framed as "If you can supply proof…"

**3. Implied skills**
Reasonable implications from the JD not explicitly stated. Explain rationale briefly for each.

### Where Skills Can Be Combined

If two JD requirements overlap significantly and evidence supports both under a single label, they can be combined into one skill. Flag this to the user with rationale. This keeps the list focused and avoids redundancy, especially when fitting into a fixed-size table on the resume.

## Decision Gate

After producing the three blocks, ask exactly:
1. "Do you want any Missing skills or Implied skills added to the Prioritized Skills list (only if evidenced in Input 3), or should they remain separate?"
2. "Is this output what you wanted?"

Then STOP and wait.

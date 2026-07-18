---
name: ats-checker
description: >
  Audit a resume against a job description to predict ATS (Applicant Tracking System) ranking.
  Use this skill whenever the user wants to check if a resume will pass ATS filters, optimize
  for keyword matching, check formatting compliance, or get a match-score report against a specific JD.
  Also trigger when the user mentions "ATS score", "ATS optimization", "will this get through the bots",
  "keyword matching", or wants to verify a resume before submitting.
---

# ATS Checker

Audit a resume against a job description to predict ATS ranking OR check your master resume for role fit. Supports two modes: Master Resume Coverage Check (should I apply?) or Tailored Resume ATS Check (will this get through ATS?). Provides keyword-match scoring, coverage reports, format compliance checking, and prioritized fix lists.

## What This Does

This skill supports two scenarios:

**Scenario 1: Master Resume Coverage Check** — Should you apply to this role?
- Extracts required keywords from the JD
- Scans your comprehensive master resume for evidence
- Produces a coverage report showing which requirements you have, which you're missing, and where the evidence lives
- Helps you decide fit and identify gaps to address in a tailored resume

**Scenario 2: Tailored Resume ATS Check** — Will this get through ATS?
- Extracts required keywords from the JD
- Scans your tailored/completed resume for matches
- Audits formatting for ATS parseability (no graphics, standard headings, readable fonts, etc.)
- Produces a scored ATS report with a match percentage, confidence level, format violations, and prioritized fixes

Both modes extract must-have keywords and scan for keyword matches. The difference is the output and whether we audit formatting.

## Model Selection

This is extraction and checklist work. **Use Sonnet** — it's fast, accurate at keyword scanning, and cost-efficient.

## Inputs Required

- **Input 1**: Resume file (docx, pdf, or text)
- **Input 2**: Job description (full JD text)

If Input 2 is missing, respond: "Please provide the job description so I can run the audit." Then STOP.

For .docx files, extract text using Python's `docx` library. For PDFs, extract text appropriately.

## Core Principle: Match-Based Scoring

ATS systems look for keyword presence, not interpretation. A keyword match is literal (or a very close variant). This skill searches for matches the same way an ATS parser would:

- Exact phrase matches count as 100% match.
- Synonym/variant matches (e.g. "Vue" vs "Vue.js", "API" vs "REST API") count as partial matches.
- Absence = no match.
- Never invent keywords the resume doesn't contain. Always verify by quoting the resume text.

## Workflow Overview

| Section | What it does | Reference |
|---------|-------------|-----------|
| Pre-flight | Confirm both inputs provided; identify document type (master vs tailored) | Inline |
| Step 1 | Extract JD must-haves and extract-keywords (high-medium-low priority) | `references/jd-keyword-extraction.md` |
| Step 2 | Scan document for keyword matches and record quote evidence | `references/resume-keyword-scan.md` |
| Decision Gate | Choose output mode: Master Resume Coverage or Tailored Resume ATS Check | Inline |
| Step 3a (Master) | Generate coverage report — which requirements you have, which you're missing | Inline (below) |
| Step 3b (Tailored) | Format audit — parseability checklist | `references/format-audit.md` |
| Step 4 (Tailored) | Generate scored ATS report with prioritized fixes | Inline (below) |

## Pre-Flight

Confirm both inputs (resume/master resume file + JD text) are provided. If either is missing, ask for it and STOP. Do not proceed.

**Clarify the document type:** Ask the user which scenario they're in:
1. **Master Resume Coverage Check** - "I want to know if my master resume has evidence for all the required skills in this JD. Should I apply?"
2. **Tailored Resume ATS Check** - "I've already tailored a resume for this role. Will it get through ATS?"

This determines the output mode after Step 2.

## Step 1: JD Keyword Extraction

Read `references/jd-keyword-extraction.md` for the full procedure.

**Summary**: Parse the JD to extract must-have keywords, organized by priority (Core/Must-have, High, Medium). Core keywords are non-negotiables; missing any is often a disqualifier. High keywords are strong preference signals. Medium are nice-to-haves. Output a table with keyword, category, and example usage from the JD.

## Step 2: Document Keyword Scan

Read `references/resume-keyword-scan.md` for the full procedure.

**Summary**: For each keyword from Step 1, search the document (master or tailored resume) for matches (exact, variant, or none). Record the match type and quote the text where found. Produce a match table showing coverage rate (e.g. "12 of 15 Core keywords matched").

## Decision Gate: Output Mode

After Step 2, ask the user: "Based on this scan, would you like a coverage report for your master resume decision, or an ATS compliance check for your tailored resume?"

- If **Master Resume Coverage**: Proceed to Step 3a
- If **Tailored Resume ATS Check**: Proceed to Step 3b

## Step 3a: Master Resume Coverage Report (optional)

**When to run**: Only when the user is checking their master resume to decide whether to apply.

After Step 2, produce a coverage report:

```
MASTER RESUME COVERAGE REPORT
=============================

Job: [JD title/company]
Master Resume: [filename]
Scan Date: [today]

REQUIREMENTS COVERAGE
---------------------
Core Requirements:    28 / 31  (90%)
  ✅ Terraform (Role #3: "Designed Terraform modules...")
  ✅ FedRAMP (Role #2: "Maintained FedRAMP compliance...")
  ✅ Kubernetes (Role #4: "Managed k8s clusters...")
  ❌ Stakeholder Management - NOT FOUND in master resume
  ❌ Cost Optimization - NOT FOUND in master resume
  ❌ Healthcare Domain - NOT FOUND in master resume

High Requirements:     9 / 10  (90%)
  ✅ [keyword with quote]
  ...
  ❌ [missing keyword]

Medium Requirements:   6 / 6  (100%)
  ✅ All medium requirements covered

OVERALL COVERAGE: 43 / 47 (91%)

VERDICT
-------
Your master resume covers 91% of stated requirements. You are a strong fit.

Missing Core requirements: 3 (Stakeholder Management, Cost Optimization, Healthcare Domain)
- Stakeholder Management: You have evidence of cross-functional leadership in Roles #2 and #5 but not under that specific phrase. Consider whether you can reframe.
- Cost Optimization: Not evidenced. If this role emphasizes it heavily, consider whether you're a fit.
- Healthcare Domain: No healthcare background. Evaluate role requirements — is domain experience mandatory or nice-to-have?

RECOMMENDATION: Apply. You have strong coverage on Core requirements and could reframe some evidence during interviews. Address the 3 gaps in your tailored resume if you proceed.
```

Rules for the report:
- Show every single keyword matched or unmatched with quote evidence where matched
- Organize by priority tier (Core / High / Medium)
- Count totals per tier and overall
- For each unmatched Core requirement, assess: can you reframe existing evidence, or is it genuinely missing?
- Verdict should answer: "Should I apply?"
- Tone: honest assessment of fit, not judgment

## Step 3b: Format Audit (optional)

Read `references/format-audit.md` for the full procedure.

**When to run**: Only when the user is checking a tailored resume for ATS compliance (not master resume mode).

**Summary**: Run a checklist of ATS-safe formatting rules. Identify any violations (graphics, complex tables, non-standard headings, etc.) and flag them for fixing.

## Step 4: Generate Scored ATS Report (optional)

**When to run**: Only when the user is checking a tailored resume for ATS compliance (after Step 3b format audit).

After completing Steps 1-3b, produce a single report output:

```
ATS AUDIT REPORT
================

Resume: [filename]
Job: [JD title/company if provided]
Scan Date: [today]

KEYWORD MATCH SCORE
-------------------
Core Keywords:    12 / 15  (80%) ⚠️ Missing: Terraform, FedRAMP, stakeholder management
High Keywords:     8 / 10  (80%) ✅
Medium Keywords:   5 / 6   (83%) ✅

OVERALL ATS MATCH:  25 / 31  (81%)

CONFIDENCE: Medium
  - Your keyword coverage is solid on high-priority items
  - 3 Core keywords missing; if the role emphasizes any of these, ATS may deprioritize
  - Format is ATS-safe

FORMAT AUDIT
------------
✅ Standard headings
✅ No graphics or complex tables
✅ Readable fonts (no decorative fonts)
⚠️ Inline citations present in Role #2 — remove before submitting

PRIORITIZED FIXES (in order)
----------------------------
CRITICAL (if missing Core keywords are deal-breakers):
- Add evidence for [keyword] if you have it; otherwise flag this role as not a fit

HIGH IMPACT:
- Remove inline citations in Role #2
- Add [synonym/variant] if you have evidence (currently missing but high-priority)

OPTIONAL:
- Consider rewording to include [medium-priority keyword] if natural

VERDICT
-------
This resume will likely pass initial ATS screening for this role (81% match),
but the 3 missing Core keywords may cause it to be deprioritized relative to
candidates who have all 15. If those keywords are critical to the role, consider:
1. Rewriting to emphasize related evidence you do have
2. Confirming whether the role is a fit
3. Submitting anyway and monitoring for callback

Recommended action: [recommendation based on verdict]
```

Rules for the report:
- `OVERALL ATS MATCH` is the percentage of total keywords matched (matched / total).
- `CONFIDENCE` is your assessment: High (90%+), Medium (70-89%), Low (<70%). At Low, the resume may be auto-screened out.
- Flag every Core keyword miss explicitly — do not bury them.
- Prioritize fixes by impact: critical (missing core keywords), high (format violations, frequently-required keywords), optional (nice-to-haves).
- The VERDICT should be honest: will this resume likely pass ATS? If not, why?
- Keep tone neutral and actionable — this is data, not judgment.

## Decision Gate (Master Resume Mode)

After producing the coverage report, ask: "Does this help you decide whether to apply? Would you like me to highlight specific areas where you could reframe existing evidence in a tailored resume?"

Do not proceed beyond the report without the user confirming next steps.

## Decision Gate (Tailored Resume Mode)

After producing the ATS report, ask: "Would you like to make any of the recommended changes, or would you like me to re-scan after you revise?"

Do not proceed beyond the report without the user confirming next steps.

## Interaction Protocol

- Work through Steps 1-2 sequentially for all scenarios.
- After Step 2, stop and present the Decision Gate question to determine mode (master resume vs tailored resume).
- **Master Resume Mode**: After presenting coverage report, stop and ask for next steps.
- **Tailored Resume Mode**: Continue through Steps 3b-4 (format audit + ATS report). Never skip Step 3b — parseability issues are silent killers.
- If the user asks to re-run after revisions (tailored mode), repeat Steps 2, 3b, and 4 only (keyword scan + format audit + new report); you can reuse Step 1 output if the JD hasn't changed.
- If the user wants to switch modes (e.g., went master-mode but now wants tailored ATS check), restart the full flow.

## Related Skills

This skill audits a resume after the fact. If you need to *tailor* a resume to match a JD in the first place, use the [[resume-tailor]] skill. ats-checker is the final check before you submit.

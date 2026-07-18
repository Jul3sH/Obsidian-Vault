---
name: storm-research
description: Use when Codex should run STORM research, create a Storm Research report, produce a multi-perspective briefing, or investigate a topic through practitioner, academic, skeptic, economist, and historian lenses with citation verification. Best for topics where conflicting viewpoints, source quality, and claim safety matter. Overkill for simple factual lookups.
---

# Storm Research

## Overview

Turn one topic into a verified, multi-perspective HTML briefing. Use five expert lenses, map their contradictions, synthesize a self-contained report, then verify citations and revise before delivery.

Run the full pipeline end to end. Do not skip verification.

## Scope The Topic

1. Identify the topic from the user request. Ask only if the topic is genuinely ambiguous.
2. State the interpreted topic in one line and proceed.
3. Identify the reader role for the actionable section. Infer it from context, ask in one line if necessary, or default to "a practitioner or decision-maker in this field."
4. Derive a kebab-case `topic-slug` for the filename.
5. Tell the user the pipeline is running.

## Research Requirements

- Use real web research for current or source-sensitive claims.
- Prefer primary sources, official data, peer-reviewed papers, regulator filings, direct product docs, public company reports, and original datasets.
- Treat secondary coverage as leads, not final evidence.
- Track source URLs and the exact claim each source supports.
- Cut or demote any claim that cannot be verified.

## Phase 1: Five Expert Lenses

Research the same topic through five lenses. If parallel research agents are available, run all five concurrently. If not, research them sequentially and keep each lens brief separate until synthesis.

Use these lenses:

### Practitioner

Focus on daily operating reality. Prioritize recent sources, case studies, practitioner discussions, operator data, implementation failures, workflow friction, and what actually works.

Return:
- Core position in 2 sentences
- Strongest evidence, 3-5 bullets with concrete data, cases, named sources, and URLs
- The one thing only a practitioner would say

### Academic

Focus on peer-reviewed evidence, causal claims, effect sizes, and where rigorous evidence contradicts popular belief.

Return:
- Core position in 2 sentences
- Strongest evidence, 3-5 bullets tied to named studies or reports, URLs, and actual findings
- Peer-review status: published, working paper, preprint, or unclear
- The one thing only an academic would say

### Skeptic

Build the strongest rigorous counterargument. Look for failures, backlash, contradicting data, regulatory changes, debunkings, and inconvenient caveats.

Return:
- Core position in 2 sentences
- Strongest evidence, 3-5 bullets with concrete sources and URLs
- The one thing only a skeptic would say

### Economist

Follow the money. Research revenues, valuations, market size, funding flows, unit economics, incentives, and who benefits from the dominant narrative.

Return:
- Core position in 2 sentences
- Strongest evidence, 3-5 bullets with real numbers and URLs
- The one follow-the-money insight

### Historian

Find genuine historical parallels. Look for prior technologies, manias, regulatory shifts, adoption cycles, and market structure changes with dates and outcomes.

Return:
- Core position in 2 sentences
- Strongest evidence, 3-5 bullets with specific cases, dates, outcomes, and URLs
- The pattern only a historian would surface

After all five lenses are complete, give the user a short progress update: where the lenses converge and the sharpest disagreement.

## Phase 2: Map Contradictions

Working from the five briefs, identify:

- Direct conflicts: specific clashing claims, not just themes
- Strongest evidence: rank by evidence quality
- Weakest evidence: name what rests on analogy, anecdotes, preprints, or single-source claims
- Resolving question: the empirical question that would settle the biggest conflict
- Universal agreement: what every lens confirms, even opponents
- Blind spot: the missing 6th lens that could change the conclusions

Use this map as synthesis material. It is not a separate deliverable unless the user asks for it.

## Phase 3: Build The HTML Report

1. Read `assets/report-template.html` from this skill folder.
2. Clone the template into the working directory. Do not rebuild the CSS.
3. Fill every visible section and delete instructional comments.
4. Write the report to `storm-reports/{topic-slug}-briefing.html` relative to the current working directory.
5. Create `storm-reports/` if needed.

Map the research into the template:

- 60-second summary: lead with the settled fact, then the contested interpretation
- Five key findings: ranked by evidence reliability, each with a 1-10 reliability score
- Supported-by and challenged-by chips: drawn from the contradiction map
- Contested signal: claims that are plausible but weak, preprint-only, commissioned, or disputed
- Hidden connection: the non-obvious link visible only across multiple lenses
- Missing 6th lens: the blind spot from Phase 2
- Actionable insight: 3-6 specific moves for the reader role
- Claim safety guide: safe to assert, say with caveat, do not assert
- Frontier question: the one question that would change the conclusion
- References: every citation with a verification status

## Phase 4: Verify And Revise

Before delivery, perform adversarial verification:

1. Score each finding 1-10 for reliability based on evidence quality, not confidence.
2. Name the weakest link and what would verify it.
3. Run a bias check: which lens dominated, what was underweighted, and which 6th perspective is missing.
4. Verify every distinct citation cluster against the primary source where possible.
5. Correct wrong figures, titles, dates, sample descriptions, venues, or characterizations.
6. Downgrade preprints, commissioned surveys, single-source claims, and contested claims.
7. Fill the verification banner truthfully: checked count, fabricated count, corrected count, demoted count.
8. Populate the claim safety guide from the verification results.

Citation verdicts:

- Confirmed: primary source supports the claim as written
- Corrected: primary source exists but required a material correction
- Demoted: source exists but evidence is weaker than the report originally implied
- Unverified: no reliable primary source found
- False: source contradicts the claim

Never present an unverified or false claim as fact.

## Output

Deliver:

- The final HTML file path
- Verification tally
- Universal finding
- Frontier question
- Claim safety summary: what is safe to assert, what needs caveats, and what to avoid

Open the HTML file for the user only when doing so is appropriate in the current environment. If opening a local GUI app requires approval, ask first or provide the path.

## Guardrails

- Disclose that the five-lens panel is author-built. Agreement across lenses is a strong hypothesis, not field consensus.
- Keep the template's visual style and CSS unless the user explicitly asks for a redesign.
- Use the reader role to shape action items. Keep them generic only if no role is known.
- Keep fan-out controlled: five lenses, then verification by citation cluster.
- For simple factual questions, do a normal lookup instead of running STORM.

> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/section2-summary.md`
> Do not edit here — edit the source file and re-sync.

# Section 2: Professional Summary

## Purpose
Draft a concise professional summary aligned to the JD and fully evidenced from Inputs 1/3, then verify coverage of all JD themes before finalising.

## Procedure

### Step 1: Agree Character Limit
Ask the user for their preferred character limit. **Default suggestion: 560 characters including spaces.** Respect the user's choice if they specify a different limit. Always state and count the limit as "including spaces" — never leave it ambiguous.

**Why 560 (the rationale — articulate this if the user asks):**
- A two-page resume summary block typically renders as **5 rows of ~120 characters** in Calibri 10pt. 5 × 120 = **600 characters is the absolute hard ceiling**, including spaces.
- You should not set the limit *at* 600. Text wraps between words ("ragged right"), so the last word on each row rarely fills all 120 characters, and a single long word (e.g. "infrastructure") at the wrong point can push the final words onto a **6th row** and break the layout.
- **560 builds in a ~40-character (~7%) buffer** below the 600 ceiling — enough to absorb word-wrap waste and the occasional long word so the summary reliably stays within 5 rows. 580 is the aggressive maximum; below ~545 leaves space on the table.
- If the target document uses a different font/size/column width, recompute: (rows available) × (chars per row) × ~0.93 for the wrap buffer.

### Step 2: Draft Two Variants

**Variant A — Conservative:** Direct, factual. Sticks closely to evidenced language.

**Variant B — High-impact:** Still fully evidenced, but sharper phrasing. May use JD-aligned language where supported by evidence.

Rules:
- Both variants must be within the agreed character limit.
- After each variant, output: `Character count: <number>/<limit>`
- Every claim must be traceable to Input 1 or Input 3.
- Include relevant certifications if space permits — prioritise those that match the JD.

Ask the user to select or edit.

### Step 3: Coverage Review Gate (mandatory)

After the user selects a variant, output a coverage table mapping **every** row from Section 0 Step 1 against the selected summary:

| JD Theme (from Section 0 Step 1) | Priority | Addressed? | How |
|---|---|---|---|

Rules:
- Include **all** rows from the Section 0 Step 1 table. Do not cherry-pick or shorten the list.
- Use exactly these markers: `✅ Yes`, `⚠️ Partial/Implicit`, `❌ No`.
- For `❌ No` items, note whether evidence exists in Inputs 1/3 that could be worked in.
- Be honest about partial coverage — if a theme is only implied, mark it `⚠️` not `✅`.

After the table, summarise:
- Total ✅ / ⚠️ / ❌ counts
- Note that a summary cannot cover all themes — the purpose is to ensure Core and High priorities are well represented, with remaining themes picked up in Skills, Responsibilities and Achievements sections.

### Step 4: Revise if Requested

If the user identifies gaps to address, produce a revised variant:
- Stay within the character limit.
- Show the character count.
- Explain what was added and what was traded off to make room.

Repeat the coverage review if the user requests it.

## Decision Gate

Ask exactly: "Would you like to revise the summary to address any of the gaps, or are you happy to proceed to Section 3?"

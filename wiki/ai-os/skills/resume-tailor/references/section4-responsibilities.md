> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/section4-responsibilities.md`
> Do not edit here — edit the source file and re-sync.

# Section 4: Responsibilities (Per Role)

## Purpose
Produce a combined responsibility paragraph for each role, grounded in evidence and aligned to the JD.

## Procedure

### Role Header (mandatory)
State: "We're now moving on to the responsibility section."
Then state the role exactly as:
`Role #<n>: <Title> — <Company>, <Location> — <Start> to <End> (as shown in Input 1)`

### Step 1: Ask for Focus Area (mandatory — then stop)

Ask the user:
- A) Leadership related
- B) Sales and presales related
- C) Architecture related
- D) A combination

"Which option do you want for this role: A, B, C, or D?"

Proceed only after receiving input.

### Step 2: Generate 3-6 Options (only after user replies)

- List the role name.
- Generate 3-6 responsibility options based on Input 3 evidence for this role, aligned to the user's Step 1 choice.
- Present as a numbered table with columns: #, Responsibility, Focus, Key evidence (Input 3).
- Ask the user to select their top 3.
- Only move on once selections are confirmed.

**Naming convention (avoid confusion):** refer to items in this candidate table as **"responsibility option N"**. Reserve **"Responsibility 1 / 2 / 3"** for the three *finally selected* responsibilities only — only 3 are documented per role, so an unqualified "Responsibility 4" wrongly implies a 4th slot.

### Step 3: Produce Variants (only after user replies)

For each of the top 3 selected responsibilities, produce three variants grouped by responsibility number:

**V1 (Evidence-tight)**
- A normal suggested resume bullet/sentence using evidenced language.
- Do not introduce new factual claims not supported by the evidence basis.
- Include exactly one line: `- Evidence basis: <verbatim quote> [Input 1] or [Input 3]`

**V2a (JD-style, generic)**
- JD-aligned wording. No new deliverables unless evidenced for that role.
- Include exactly one line: `- Evidence basis (for V2a): <verbatim quote with source tag>`

**V2b (Careful inference)**
- Allowed only if inference is labelled and tied to specific evidence.
- Include exactly one line: `- Inference basis (for V2b): <verbatim quote with source tag> + explanation of inference`

Present Responsibility 1 variants first. Ask for selection. Then Responsibility 2. Then 3.

### Step 4: Combine (conditional)

Once all three are selected, ask: "Are you ready for me to combine the three selected items into a single role summary paragraph?"

If yes, produce a combined paragraph:

Rules:
- One paragraph only (no bullets, no headings).
- Combine all three selected items into a single coherent role summary.
- Preserve meaning; rephrase for flow but do not add new facts.
- Include all three components — do not drop an item.
- Must be within the agreed character limit (default ≤ 380 characters including spaces).
- After the paragraph, output: `Character count: <number>/<limit>`
- If over the limit, rewrite until compliant.
- If you cannot keep all three within the limit without losing factual integrity, stop and ask: "I can't fit all three without losing integrity. Which item should I shorten or drop?"

### Integrity Rule
- Do not introduce new scope words (global/regional), new audiences (C-level), new domains, or new outcomes unless present in the selected items.
- Do not add metrics unless they appear in the selected items.

### Responsibilities are scope, not outcomes (mandatory)
A responsibility states what the person was **accountable for** — remit, scope, teams, domains, governance. It must NOT contain quantified outcomes, measured improvements, results, awards, or initiative-level achievements — **those belong in Section 5 (Achievements), even when they are evidenced.** "Evidenced" is not licence to include here; the content must also belong to this section.
- **Allowed in a responsibility:** scale-of-remit figures that *size the accountability* (e.g. "solution assurance of US$60M+ of network and security solutions", "team of 6 across three regions").
- **Not allowed in a responsibility:** measured improvements or results (e.g. "improved right-first-time by 20%", "generated US$20M", "reduced cycle time 20%"), or named initiatives credited with an outcome. Reserve all of these for Section 5.
- Do not import the general "impact-first / lead with the metric" style instinct into Section 4 — that instinct is for achievements. (Logged failure mode; see `process-quality-log.md`.)

## Decision Gate

After the combined paragraph is approved, proceed to Section 5 (Achievements) for the same role.

> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/section5-achievements.md`
> Do not edit here — edit the source file and re-sync.

# Section 5: Achievements (Per Role)

## Purpose
Produce three achievement bullets for each role, each under 120 characters, grounded in evidence and aligned to the JD.

## Procedure

### Role Header (mandatory)
State: "We're now moving on to the achievements section."
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
- Generate 3-6 achievement options based on Input 3 evidence for this role, aligned to the user's Step 1 choice.
- Present as a numbered table with columns: **#, Achievement, Focus, Aligns with chosen responsibilities?, Key evidence (Input 3)**.
- The **"Aligns with chosen responsibilities?"** column maps each achievement against the responsibilities the user *already locked* for this role (from Section 4). Use: `Yes — <responsibility theme>` / `Partial — <theme>` / `No (standalone)`. This lets the user choose achievements that reinforce the role's responsibility narrative rather than scatter unrelated wins. Alignment is a *consideration, not a requirement* — a strong standalone achievement is still selectable; the column just surfaces the trade-off.
- Ask the user to select their top 3.
- Only move on once selections are confirmed.

**Naming convention (avoid confusion):** refer to items in this candidate table as **"achievement option N"** (e.g. "achievement option 4"). Reserve **"Achievement 1 / 2 / 3"** for the three *finally selected* achievements only — because only 3 are ever documented per role, so an unqualified "Achievement 4" wrongly implies a 4th slot. The same applies in Section 4: "responsibility option N" for candidates, "Responsibility 1/2/3" for the selected three.

### Step 3: Produce Variants (only after user replies)

For each of the top 3 selected achievements, produce three variants grouped by achievement number.

#### Character-Count Check (mandatory)
Before outputting any achievement variant, count characters including spaces.
- Each achievement bullet must be <120 characters.
- After each variant bullet, output: `Character count: <number>/120`
- If any variant exceeds 120 characters, rewrite before presenting.

For each achievement:

**V1 (Evidence-tight)**
Overview: <1 sentence describing what was done/delivered>
<Achievement bullet — must be <120 characters>
`Character count: <number>/120`
- Evidence basis: <verbatim quote> [Input 1] or [Input 3]

**V2a (JD-style, generic)**
Overview: <1 sentence with JD-aligned framing>
<Achievement bullet — must be <120 characters>
`Character count: <number>/120`
- Evidence basis (for V2a): <verbatim quote with source tag>

**V2b (Careful inference)**
Overview: <1 sentence with inferred impact>
<Achievement bullet — must be <120 characters>
`Character count: <number>/120`
- Inference basis (for V2b): <verbatim quote with source tag> + explanation of inference

Present Achievement 1 variants first. Ask for selection. Then Achievement 2. Then 3.

### Evidence Constraints (hard rules)
- Achievements must be based ONLY on the role's evidence from Input 3 and the user's Step 1 inputs.
- Do NOT introduce new metrics, projects, customers, awards, or claims unless they appear in the evidence.
- If an achievement cannot be supported, either omit it or rewrite to remove unsupported details.

### Output Formatting Rules
- Character limit (hard rule): Any achievement bullet must be <120 characters including spaces.
- Prefer impact-first phrasing (metric/outcome first, then what you did).
- Use plain language; avoid internal process jargon unless the user supplied it.
- Do NOT output any `Evidence harvested (Input X)` blocks — keep evidence in the basis lines only.

## Role Summary Deliverable

After all three achievements are selected, output the complete role summary:

```
**Role #N: Title — Company, Location — Start to End**

**Responsibilities (combined paragraph):**
<The combined paragraph from Section 4>

**Selected Achievements:**
- <Achievement 1>
- <Achievement 2>
- <Achievement 3>
```

Rules:
- Use exactly this structure with no additional headings, commentary, or evidence blocks.
- This is the deliverable that will be pasted into the resume.

## Decision Gate

After presenting the role summary, ask: "Shall we proceed to the next role?"

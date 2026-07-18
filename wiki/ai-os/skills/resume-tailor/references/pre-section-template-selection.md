> **Mirror copy.** Source: `~/.claude/skills/resume-tailor/references/pre-section-template-selection.md`
> Do not edit here — edit the source file and re-sync.

# Pre-Section: Template Selection

## Purpose
Evaluate a folder of existing resume templates against the target JD to identify the best starting template (Input 1) before tailoring begins.

## Inputs Required

Before starting, verify these inputs are present:

- **Input 2**: Target job description (full JD text)
- **Input 3**: Master resume (the reference canon of all facts)
- **Resume folder**: A folder containing multiple resume templates to evaluate

If the JD or master resume is missing, ask for them.

## Procedure

### Step 0: Storage Selection (mandatory — then stop)

Ask the user where their resume templates are stored. Present the following options:

- A) Google Drive
- B) Dropbox
- C) OneDrive
- D) Local filesystem / uploaded files
- E) Other

"Where are your resume templates stored?"

Wait for the user to respond. Then:

**If Google Drive (A):**
- Ask: "Which Google Drive folder contains your resume templates? Please provide the folder name or share a link."
- Use Google Drive search tools to locate and list the folder contents.

**If Dropbox (B):**
- Ask: "Which Dropbox folder contains your resume templates? Please provide the folder path (e.g., /Resumes/2026)."
- Use available Dropbox connector or MCP tools to list and retrieve folder contents.
- If no Dropbox connector is available, advise: "I don't currently have a Dropbox connector active. You can either: (1) upload the files directly, (2) connect Dropbox via Settings → Connectors → Add custom connector, or (3) point me to a different storage location."

**If OneDrive (C):**
- Ask: "Which OneDrive folder contains your resume templates? Please provide the folder path or share a link."
- Use available OneDrive connector or MCP tools to list and retrieve folder contents.
- If no OneDrive connector is available, advise the user of the same options as Dropbox above.

**If Local filesystem / uploaded files (D):**
- Ask: "Please upload your resume templates, or if using Cowork, tell me the folder path on your local machine."
- For uploads, check `/mnt/user-data/uploads` for available files.
- For Cowork local paths, access files directly from the specified folder.

**If Other (E):**
- Ask: "Which storage service are you using? I'll check whether I can connect to it, or you can upload the files directly."

Once the folder is located and files are confirmed, proceed to Step 1.

### Step 1: Extract JD Requirements (reuses Section 0 Step 1)

Extract a prioritized requirements map from Input 2 (JD). Output one Markdown table:

| Priority | Category | JD-stated requirement |
|----------|----------|----------------------|

Rules:
- Priorities: `Core`, `High`, `Medium` only.
- This is the same table that will be reused in Section 0 — produce it once here and carry it forward.

### Step 2: Retrieve Templates

- List all documents in the specified folder using the appropriate tool for the selected storage.
- For each document, extract the text content.
- For .docx files, extract text using Python's `docx` library.
- For PDFs, extract text appropriately.
- Report how many templates were found and list their names.

If any files cannot be accessed or parsed, report them and continue with the files that can be read.

### Step 3: Quick Scan (all templates)

For each template, perform a lightweight keyword and theme match against the Step 1 requirements table.

For each template, count:
- How many **Core** requirements have at least one keyword or phrase match
- How many **High** requirements have at least one keyword or phrase match
- How many **Medium** requirements have at least one keyword or phrase match

Output a ranked summary table:

| Rank | Template name | Core matches (of N) | High matches (of N) | Medium matches (of N) | Total score |
|------|--------------|--------------------|--------------------|---------------------|-------------|

Scoring formula: Core match = 3 points, High match = 2 points, Medium match = 1 point. Rank by total score descending.

Rules:
- This is an approximate scan based on keyword presence, not a deep evidence review.
- Be transparent that this is a rough ranking — the deep review in Step 4 will be more accurate.
- If there are 3 or fewer templates, skip the quick scan and go directly to Step 4 (deep review) for all of them.

### Step 4: Deep Review (top 3 templates only)

For the top 3 ranked templates from Step 3, run the full Section 0 Step 2 evidence mapping process:

For each of the top 3 templates, output:

**Template: <name>**

| JD-stated requirement | Evidence found in template |
|----------------------|---------------------------|

Rules:
- Use the same JD requirements from Step 1.
- Evidence must be verbatim quotes from the template.
- If no evidence exists for a requirement: `Not addressed in this template.`
- After the table, output a coverage summary: `Core: X/N | High: X/N | Medium: X/N`

### Step 5: Present Ranked Shortlist

Output a final comparison table of the top 3 templates:

| Rank | Template name | Core coverage | High coverage | Medium coverage | Strengths | Gaps |
|------|--------------|--------------|--------------|----------------|-----------|------|

For each template, provide:
- **Strengths**: Which JD themes are already well-addressed (2-3 bullet points)
- **Gaps**: Which Core/High JD themes are missing and would need the most tailoring work (2-3 bullet points)

### Step 6: User Selection

Ask: "Based on this analysis, which template would you like to use as the starting point (Input 1) for tailoring? Or would you like me to review any of them in more detail?"

Wait for the user to select. Once confirmed, the selected template becomes **Input 1** and the process continues to Section 0 (which can reuse the Step 1 requirements table already produced).

## Decision Gate

After the user selects a template, confirm: "Template selected: <name>. Proceeding to Section 0: JD-to-Resume Mapping. The JD requirements table from the pre-section will be carried forward. Proceed, or iterate further?"

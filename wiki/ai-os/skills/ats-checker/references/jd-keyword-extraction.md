# Step 1: JD Keyword Extraction

Extract must-have keywords and phrases from the job description, organized by priority.

## Procedure

1. **Read the JD carefully.** Identify sections that list requirements: "Required Skills", "Must-have Experience", "Responsibilities", "Qualifications", etc.

2. **Extract keywords into three priority tiers:**

   - **Core (Must-have)**: Non-negotiables. Often stated as "Required", "Must have", or appear multiple times. Examples: specific programming languages, certifications, years of experience, clearances, exact role keywords. Missing any Core keyword is often a disqualifier.
   - **High (Strong preference)**: Frequently mentioned, valuable but not explicitly required. Examples: frameworks, methodologies, soft skills like leadership, industry knowledge. Missing one may deprioritize the resume.
   - **Medium (Nice-to-have)**: Listed but not emphasized. Examples: related certifications, bonus technologies, specialized knowledge. Missing these rarely disqualifies.

   **Tiering Signal Key** — use these section and wording cues to assign each keyword's tier:

   | Tier | Section / Heading Signal | Wording Signal |
   |------|--------------------------|-----------------|
   | Core | Listed under an "Essential", "Required", "Must-have", or "Requirements" heading | "must", "required", "essential", "proven experience", "strong understanding" — or the term appears repeatedly across multiple sections (e.g. role title, recurring domain terms) |
   | High | Listed under a "Desirable" heading with no further softening, OR appears once in an Essential section but is reinforced repeatedly in the duties/responsibilities section | "preferred", "comfortable with", "familiarity with", "strong preference" |
   | Medium | A single, unreinforced mention anywhere, OR explicitly softened | "optional", "nice to have", "bonus" |

   A wording signal overrides a section signal: e.g. an item under "Desirable" marked "(preferred)" is High, while an item in the same list marked "(optional)" is Medium.

3. **For each keyword, note:**
   - The keyword or phrase as it appears in the JD (verbatim or normalized)
   - Priority tier (Core / High / Medium)
   - A quote or context from the JD showing where it came from
   - Any synonyms or acceptable variants (e.g. "React" vs "React.js" vs "ReactJS")

4. **Skip generic jargon** that almost every resume contains (e.g. "communication", "collaboration", "results-driven"). These are not differentiators and don't help ATS scoring — focus on specific, job-unique requirements.

5. **Organize by priority** and output as a table:

   | Priority | Keyword / Phrase | Variants | JD Context |
   |----------|------------------|----------|-----------|
   | Core | Terraform | terraform, terragrunt | "5+ years with Terraform on AWS" |
   | Core | FedRAMP certification | FedRAMP | "Must have FedRAMP authorization" |
   | High | Kubernetes | k8s, K8s | "Experience with container orchestration (Kubernetes preferred)" |
   | Medium | Helm | helm charts | "Bonus: Helm chart experience" |

## What Counts as a Keyword

- **Specific technologies**: Python, React, Postgres, Docker, AWS
- **Methodologies**: Agile, Scrum, SAFe, Six Sigma
- **Certifications**: PMP, CISSP, FedRAMP, AWS Certified Solutions Architect
- **Industry knowledge**: Healthcare IT, FinTech, SaaS, healthcare compliance, HIPAA
- **Role keywords**: "Engineering Manager", "Platform Engineer", "Staff Engineer", "Solutions Architect"
- **Years of experience**: "5+ years", "10+ years"
- **Soft skills that are specific**: "mentoring", "cross-functional leadership" (yes); "communication" (no — too generic)

## What Does NOT Count

- Generic corporate language ("driven", "results-focused", "proactive")
- Common sense expectations ("works well in teams", "attention to detail")
- Role titles that are obvious from context ("engineer")

## Output

**MANDATORY — do not skip:** Display the full table (columns: Priority | Keyword / Phrase | Variants | JD Context) as visible chat text, listing every Core, High, and Medium keyword. This table must be shown to the user in the conversation itself before any confirmation question is raised — asking the confirmation question via a question tool without first showing this table does not satisfy this step.

Only after the table has been displayed, ask: "Does this keyword list align with the role's actual requirements, or would you like me to adjust?"

Do not proceed until the user confirms the list.

# Step 2: Resume Keyword Scan

Search the resume for matches to the keywords extracted in Step 1. Record evidence with quotes.

## Procedure

1. **For each keyword from Step 1**, search the resume (both document body and headers/metadata if available).

2. **Classify each search result as one of:**

   - **Exact match**: The keyword appears verbatim in the resume (e.g. "Terraform" appears as-is).
   - **Variant match**: A close variant or synonym is found (e.g. "Vue.js" for "Vue"; "k8s" for "Kubernetes"; "React" for "ReactJS"). Record both the variant found and the original keyword.
   - **No match**: The keyword does not appear anywhere in the resume.

3. **For every match (exact or variant), quote the exact text from the resume** where it appears. Include 1-2 words of context so you can verify the quote is real.

   Example: "Found 'Terraform' in Role #2 responsibilities: 'Designed Terraform modules for multi-region AWS deployments.'"

4. **For every non-match, note the absence clearly.** Do not invent text.

5. **Organize by priority tier** and output as a table:

   | Priority | Keyword | Match Type | Quote from Resume | Status |
   |----------|---------|-----------|------------------|--------|
   | Core | Terraform | Exact | "Designed Terraform modules for..." | ✅ |
   | Core | FedRAMP | None | — | ❌ |
   | High | Kubernetes | Variant | "Managed k8s clusters" (k8s = Kubernetes) | ✅ |
   | Medium | Helm | None | — | ❌ |

6. **Calculate match rates by priority:**

   - Count: total keywords in each tier
   - Matched: exact + variant matches
   - Rate: matched / total (e.g. "12 / 15 Core keywords matched = 80%")

7. **After the table, summarize:**

   ```
   MATCH SUMMARY
   Core Keywords:    12 / 15 matched (80%)  [Missing: Terraform, FedRAMP, stakeholder management]
   High Keywords:     8 / 10 matched (80%)
   Medium Keywords:   5 / 6 matched (83%)
   ```

## Match Validation Rules

- **Exact match is literal**: "Python" matches "Python", not "Python 3.9" (though the latter contains it). Be precise.
- **Variant matches must be defensible**: "React" for "React.js" is acceptable. "Node" for "Node.js" is acceptable. "Java" for "JavaScript" is not. Use your judgment; when in doubt, classify as a partial or no-match.
- **Context matters**: If the resume says "SQL Server experience" and the JD requires "SQL", that's a match — but if it requires "NoSQL" and the resume says "SQL", that's a non-match (different thing).
- **Don't be creative**: If a keyword doesn't appear, it doesn't appear. Do not infer or assume.

## Output

Present the full match table and the match summary. Then ask: "Does this match assessment align with your sense of the resume, or would you like me to reconsider any of these matches?"

Do not proceed until the user confirms the keyword scan.

## Notes for Resume Parsing

- If the resume is in .docx or PDF format, extract all text carefully, preserving section headers and role context.
- Keywords may appear in headers, bullet points, or embedded in sentences — search all sections.
- If a keyword appears multiple times, record the first occurrence (unless later occurrences are in different contexts — then note both).

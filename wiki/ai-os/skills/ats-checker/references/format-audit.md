# Step 3: Format Audit

Check the resume for ATS parser safety. ATS systems can struggle with certain formatting; files that fail this audit may be rejected before keyword scoring even happens.

## Checklist

Run through each item below. Mark as ✅ (pass), ⚠️ (warning), or ❌ (violation).

### Structure & Headings

- ✅ **Standard section headings** — uses common resume headings like "Professional Experience", "Skills", "Education", "Summary", etc. (ATS expects these).
  - ❌ **Non-standard headings** — uses creative or unusual section names like "Where I've Made an Impact" or "Key Wins" (ATS may not parse them as resume sections).

- ✅ **Single-column layout** — resume is laid out in a single column from top to bottom.
  - ❌ **Multi-column or sidebar layout** — text is in multiple columns or a side panel (ATS parsers read top-to-bottom and may lose content from side panels).

- ✅ **Clear role structure** — each role has a clear format: "Title, Company, Location, Dates" or similar.
  - ⚠️ **Inconsistent role formatting** — role headers vary in format or are unclear (ATS may struggle to parse role boundaries).

### Content & Formatting

- ✅ **No graphics, logos, or images** — resume is text-only.
  - ❌ **Graphics or logos embedded** — resume contains company logos, icons, QR codes, charts, or other images (ATS parsers often skip or corrupt these).

- ✅ **No complex tables** — resume avoids tables, or uses simple, single-cell-per-item tables at most.
  - ❌ **Complex tables, matrices, or grids** — resume uses multi-column tables, skill matrices, or complex layouts (ATS parsers may misread table content).

- ✅ **Readable fonts** — uses standard fonts (Arial, Calibri, Times New Roman, Helvetica, Tahoma, Georgia, etc.).
  - ❌ **Decorative or unconventional fonts** — uses script, decorative, or unusual fonts (ATS may not parse or may default to unreadable fallbacks).

- ✅ **Black text on white/light background** — good contrast for both human and machine reading.
  - ⚠️ **Colored text or background** — uses colors, shading, or background fills (ATS parsers handle color inconsistently; may reduce contrast or cause parsing issues).

- ✅ **Consistent formatting within sections** — bullets, indentation, spacing are uniform across roles.
  - ⚠️ **Inconsistent spacing or indentation** — roles or bullets vary in formatting (ATS may misread hierarchy).

### Special Elements

- ✅ **No headers or footers containing critical info** — contact info, key qualifications, or links are in the main body, not in page headers/footers.
  - ❌ **Critical info in headers/footers** — resume puts contact info or key content in page headers or footers (ATS often skips these).

- ✅ **No inline citations or footnotes** — no superscript numbers, asterisks, or footnotes pointing to sources.
  - ⚠️ **Inline citations present** — resume includes references like [1], [source], or superscript citations (ATS may skip them or misformat).

- ✅ **No hyperlinks or special formatting on links** — if links are included, they're plain text (e.g. "github.com/username"), not colored or underlined.
  - ⚠️ **Colored or styled hyperlinks** — links are formatted with colors or underlines (ATS behavior with links is inconsistent).

- ✅ **No special characters or Unicode** beyond standard punctuation — uses ASCII characters and common punctuation.
  - ⚠️ **Bullet points use standard hyphens or dashes** — if using bullet symbols (•, -, *, etc.), they parse consistently.
  - ❌ **Uncommon symbols or special Unicode** — uses curved quotes, dashes, or other Unicode that may not parse correctly in plain-text conversion.

### File Format

- ✅ **Submitted as .docx or text-based PDF** — file formats ATS parsers handle best.
  - ⚠️ **Image-based PDF** — PDF created from a scanned document or converted to images (ATS cannot read text from images).
  - ⚠️ **Other formats** — .odt, .pages, .rtf (ATS support varies; not guaranteed).

## Procedure

1. **Go through each item** in the checklist above.
2. **For every ✅ or ⚠️ item**, move on.
3. **For every ❌ item**, record it as a violation and note what needs to be fixed.
4. **For ⚠️ items**, note them as "cautions" — they may cause issues but aren't hard violations.

## Output

Produce a simple checklist summary:

```
FORMAT AUDIT RESULTS
====================

✅ Standard headings
✅ Single-column layout
✅ No graphics or logos
❌ Complex skills table — needs to be simplified to bullet list
⚠️ Colored section headers — ATS may render inconsistently
✅ Standard fonts (Arial)
✅ Black text on white background
✅ No headers/footers with critical info
⚠️ Inline citations in Role #2 — remove if possible
✅ Plain text links
✅ File format: .docx
```

Then summarize:

**Violations (must fix before submitting):** [list]
**Cautions (consider fixing):** [list]
**Safe to submit:** Yes / No (yes if no violations; no if any violations exist)

## Notes

- ATS systems vary in parser sophistication. These rules target the most common and safest practices.
- When in doubt, simpler is better. A plain, boring resume is more likely to parse than a fancy one.
- Always save the final resume as .docx or a text-based PDF before submitting through an ATS application system.

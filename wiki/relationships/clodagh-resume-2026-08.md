This is a wiki copy of Clodagh's CV as reproduced for her, with the Waterford address and Irish mobile number substituted in place of the original Hong Kong details. It exists so the content can be reviewed here without opening the PDF, and so the exact reproduction method is on record if the same "recreate this CV in a new PDF" task comes up again (for Clodagh or anyone else). Julian reviews the content below for accuracy; the finished PDF was generated separately and is not stored in the wiki (see Output below).

## Output

- **Finished PDF:** `~/Desktop/Clodagh Hart CV August 2026.pdf` (not in the wiki - PDFs aren't wiki content)
- **Source changed:** Location, Tel, and Residential Status (now "Irish Resident", was "Hong Kong Permanent Resident"). Everything else (email, all professional content) carried over unchanged from the original CV Clodagh supplied.

## CV Content

**Ms. Clodagh Hart**

| | |
|---|---|
| **Location:** | 2 Bromley Crescent, Ardkeen Village, Waterford |
| **Residential Status:** | Irish Resident |
| **Nationality:** | Irish |
| **Languages:** | English & French |
| **Contact:** | Email: clodaghhart@icloud.com &nbsp;&nbsp; Tel: 083 8877131 |

### Education
- **MBS, Master's In Business Economics** - University College Cork, Ireland (October 2004 - October 2005)
- **B.A. Honours Economics/ French** - University College Cork, Ireland (October 2001 - June 2004)

### Personal Interests
- Running - 2013 Dublin & London Marathons; 2018 Paris & NYC Marathons
- Theatre, travel & reading

### Professional Training
- ACAMS Qualifications (Association of Certified Anti-Money Laundering Specialists - in progress)
- MLRO Certification (Money Laundering Reporting Officer)
- Diploma in IAQ (Investment Administration Qualification)
- Regulatory Landscapes of Alternative Investments Certification
- Compliance and Regulations for Generative AI Certification
- Ethical and Regulatory Implications of Generative AI Certification
- Leveraging AI for Governance Risk and Compliance Certification
- Blockchain: Beyond the Basics Certification
- Corporate Finance: ESG Certification
- ESG and Procurement certification

### Profile Summary
A highly accomplished and results driven Regional Director/Senior Manager with over 15 years international financial services experience gained through roles at global institutions including HSBC, MUFG, Deutsche Bank and JP Morgan. Proven track record of providing independent Regulatory Compliance Advisory advice to the business in conjunction with directing and executing complex reviews and assurance programs across Investment Banking, Corporate Banking and 2nd line functions including Anti Financial Crime. Experience also spans payments, operational risk, vendor management, transaction reporting and trade Operations, with regional leadership across Asia Pacific.

### Key Areas of Expertise
- **Risk and Controls Excellence** - surveillance, monitoring and assurance work meeting global testing benchmarks; control design, operating effectiveness, impact and root cause analysis.
- **Stakeholder Management** - articulating Compliance advice and escalating findings to Country Heads, Business Heads, Regional and Global Compliance Senior Management.
- **Governance, Oversight, and Regulatory Expertise** - HKMA, SFC and international regulator relationships; enquiries, trade reporting, inspections, licensing, audits.
- **Talent Management & Leadership** - led regional teams of 13 across Hong Kong, Singapore and UK.

### Professional Experience

| Employer | Role | Dates |
|---|---|---|
| HSBC, Hong Kong | Senior Manager, Global Markets Central Services Team, Regulatory Compliance Advisory | April 2021 - June 2022 |
| MUFG, Hong Kong | Director, Regional Head of Monitoring, Surveillance & Control | Sept 2018 - December 2020 |
| Deutsche Bank AG, Hong Kong | VP, APAC Regional Head of CRegO Assurance & Testing | March 2016 - August 2018 |
| Deutsche Bank AG, Hong Kong | VP, Corporate Finance/ Transaction Banking Advisory Compliance | January 2015 - March 2016 |
| Deutsche Bank AG, Hong Kong | VP, Compliance Control Room | September 2013 - January 2015 |
| Deutsche Bank AG, London | GTB Advisory Compliance Officer | July 2011 - September 2013 |
| Deutsche Bank AG, Hong Kong | Corporate Finance Advisory Compliance Officer | March 2010 - July 2011 |
| Deutsche Bank AG, Hong Kong | Compliance Control Room | June 2008 - March 2010 |
| JP Morgan, London | Markets Intelligence & Investigation Unit, EMEA | October 2007 - June 2008 |
| HSBC, London | Operational Risk Assistant, Operations & Regulatory Control Division | March 2006 - September 2007 |

Full bullet-level responsibilities for each role are in the PDF (see Output above) - not duplicated here to keep this review copy short; ask if the full text needs to be pulled into the wiki too.

## Reproduction Instructions

How this PDF was built, kept here so the same "recreate a CV in a new PDF, same format" task can be repeated without re-deriving the method.

**Method:** hand-built HTML/CSS matching the source PDF's layout, rendered to PDF with headless Chrome (no third-party PDF library needed - Chrome is already on the machine).

1. Transcribe the source CV's full text and structure into an HTML file (name, contact block, education, interests, training, profile, expertise, then one block per job with a right-aligned date line and a bulleted responsibilities list).
2. Apply this CSS, tuned by trial rendering until the page count matches the original:
   - `@page { size: A4; margin: 17mm 16mm 14mm 16mm; }`
   - Body font: Calibri/Candara/Segoe UI/Arial fallback stack, 10pt, line-height 1.26
   - Each page is a `<div class="page">` with `display:flex; flex-direction:column; min-height:254mm`
   - Footer is a flex child with `margin-top:auto` so it sits pinned to the page bottom regardless of how much content precedes it: `CONFIDENTIAL` / `Page X of N` / `USE ONLY`
   - Page breaks: `page-break-before: always` on every page div after the first
   - Job header line uses a two-column table so the employer name is left and the date range is right-aligned on the same line
3. Render: `google-chrome --headless --disable-gpu --no-pdf-header-footer --print-to-pdf="output.pdf" --print-to-pdf-no-header "file:///path/to/file.html"` (on this Mac: `/Applications/Google Chrome.app/Contents/MacOS/Google Chrome`)
4. **Check page count and footer placement before calling it done.** The first render came out at 7 pages with an overlapping header/footer, because the initial spacing (10.5pt, looser margins, an absolute-positioned footer) made page 1's content taller than the printable area, so content spilled onto a near-blank extra page each time a forced break landed early. Fixing it meant tightening spacing (10pt font, tighter margins/line-height/list spacing) until each page's real content fit inside the printable area on its own, and switching the footer from `position:absolute` (fragile, caused the overlap) to a flexbox `margin-top:auto` child (robust regardless of content length).
5. Re-render and re-check the page count/footer against the original before delivering.

**Why this approach over a PDF library:** no Python PDF package was installed (`pip install` is blocked by this Mac's externally-managed-environment guard), but Chrome was already present, so HTML-to-PDF via headless Chrome was the fastest path with zero new dependencies.

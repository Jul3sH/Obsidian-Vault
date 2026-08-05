---
deliverable: vanguard-outreach-go-no-go
project: cold-outreach-real-estate
workstream: career
type: report
created: 2026-08-05
status: draft
---

# Vanguard Outreach: Go/No-Go Report

*Output of [[vanguard-outreach-go-no-go]]. Brief at [[vanguard-outreach-go-no-go-prompt-zero]]. High level by design; detail belongs in later artefacts.*

> [!warning] What this is and is not
> Regulatory mapping and risk structuring, not legal advice. **I can tell you where the rules sit and where the exposure lands. I cannot tell you whether a given mitigation would survive a regulator.** Points needing a Hong Kong lawyer are marked **[LAWYER]**. One factual question drives everything and only Adam can answer it, marked **[ADAM]**.

## The headline

**The regime your research document excluded is the one that matters most.** UEMO and PDPO carry fines of HK$100k to HK$1m. If Vanguard's products are collective investment schemes, **SFO s.114 carries HK$5,000,000 and 7 years**, and it bites the person *conducting the business of promoting*, which is the execution role you assumed was the safe one.

---

# Page 1: The regulations

| # | Regime | Governs | Binds | Max penalty |
|---|---|---|---|---|
| 1 | **PDPO** Part 6A (Cap. 486) | The *data*. Consent before marketing to a named individual | The data user, regardless of where data came from | HK$500k + 3yr; HK$1m + 5yr if data passed to a third party for gain |
| 2 | **UEMO** (Cap. 593) | The *sending*. Sender ID, unsubscribe, no harvesting | Sender, principal, **agent, contractor, employee, officer** | HK$100k first conviction, HK$500k later, + daily penalties |
| 3 | **SFO** Part IV, ss.103/114 | *Promoting a CIS* to the HK public | Whoever issues the advertisement, and whoever promotes as a business | **s.103:** HK$500k + 3yr on indictment. **s.114: HK$5m + 7yr** |
| 4 | **Estate Agents (Exemption from Licensing) Order** | Selling overseas property unlicensed | Anyone dealing exclusively with non-HK property | Exemption lost if its condition is not met |

**1. PDPO is the binding constraint on the email itself.** UEMO is opt-out for email; PDPO is opt-in for named individuals. Satisfying UEMO does not make the campaign lawful. Silence is not consent, and a first unsolicited email cannot be the mechanism for obtaining consent to send it. Full detail: [[hk-b2c-outreach-uemo-pdpo]].

**2. UEMO reaches past the principal.** s.59-60: *"Any act done or conduct engaged in by an agent or the outsourced service provider will be treated as done or engaged in by the principal"*, and for employees, *"treated as done or engaged in by his employer **as well as by him**"*. **This kills the "pure execution is safe" assumption.** The statute treats the executing party as a person who did the act, not as a neutral pipe.

**3. SFO is the new finding, and it is the serious one.** A CIS has four elements (SFO Schedule 1): arrangements in respect of property; investors lack day-to-day control; the property is managed as a whole and/or contributions are pooled; the purpose is for investors to receive returns. The SFC states plainly that *"'Property' is also widely defined under the SFO and includes 'land' or any estate in land so **real estate in Hong Kong or overseas is covered**."* UK property is in scope.

The SFC names the risky categories directly:

> "real estate projects involving interests in hotels/holiday resorts, **serviced apartments, student accommodation** and shopping malls are more likely to be a CIS because it is more likely that they need to be managed on behalf of investors. It is also more likely that real estate projects with **'buy-to-let' or 'buy and leaseback'** features could be a CIS as they often involve a centralized letting and management service."

**Assisted living sits squarely in that family.** So does any unit sold with a rental guarantee, leaseback, or centralised letting. Three further points close the usual escape routes: pooling is *not* required (Q6); **all** investors must have day-to-day control for it not to be a CIS, so one passive investor is enough (Q8); and a right to be consulted is not control (Q9).

**The professional investor exemption does not help a cold list.** s.103(3)(k) requires a portfolio of ≥HK$8m, and "portfolio" means securities, custodied money and certificates of deposit. Property equity does not count, and you cannot know a cold prospect's portfolio.

**4. Estate agency is the cheap one.** Unlicensed persons may promote overseas property, but the Exemption Order requires the person to state *in every advertisement and document* that **they are not licensed to deal with any property situated in Hong Kong**. The EAA's heavy due-diligence circular (23-02) binds licensees, not unlicensed promoters, so it does not apply to you, but the statement does.

**Out of scope of this report:** Trade Descriptions Ordinance, AML, UK-side law, and tax.

---

# Page 2: The risks

*Format: if we do this, then that could happen.*

| # | If we do this | Then this could happen | Candidate mitigation |
|---|---|---|---|
| R1 | Email named HK individuals about property investment without prior PDPO notice and consent | Part 6A offence on the **first** email. HK$500k + 3yr | Consent-first funnel instead of cold email; or B2B-only to corporate addresses **[LAWYER]** |
| R2 | Use the partner's whisky-investment contacts | DPP3 new-purpose breach. Consent for whisky is not consent for property | Do not use them. No mitigation short of fresh consent |
| R3 | Use the previously purchased list | No documentary consent evidence; obligation follows the data user regardless of source | Do not use unless the exact consent, data categories and marketing class are documented |
| R4 | Scrape or enrich addresses | UEMO ss.15-19 harvesting offence, separate and heavier than the sending rules | Do not scrape or enrich. This one is unambiguous |
| R5 | Send from Julian's domains and SalesHandy account | Julian is the identifiable sender and registrant; UEMO s.59-60 reaches the agent directly | Transfer domains and subscription to Adam before any send |
| R6 | Julian presses send, on Adam's written instruction | s.59-60 treats the executing party as having done the act. Written indemnity is a private contract; it does not bind a regulator | **Julian does not execute.** Advice only **[LAWYER]** |
| R7 | Promote a product that is a CIS, to the HK public, unauthorised | s.103 offence: HK$500k + 3yr on indictment | Establish CIS status per project **[ADAM]**; do not promote any project that is or may be a CIS |
| R8 | Do that repeatedly, as a business | **s.114: HK$5m + 7yr.** This is the largest exposure in the document and it attaches to the promoter, not the owner | Same as R7. Volume and repetition are what convert R7 into R8 |
| R9 | Omit the Exemption Order statement | Lose the unlicensed-promotion exemption | One line in every email: not licensed to deal with any property situated in Hong Kong |
| R10 | Broken or slow unsubscribe, incomplete sender details | UEMO Part 2 enforcement notice, then offence | Working unsubscribe, 10 working days, 3-year records, Vanguard named as sender not the sending tool |
| R11 | Adam proceeds knowing it is unlawful, having been advised by Julian | Advising with knowledge is a materially worse position than advising in ignorance | Put the advice in writing, keep it, and stop at advice **[LAWYER]** |

**R6 and R8 are the two that decide this.** Everything else is either cheaply fixed or Adam's to carry.

---

# Page 3: Action plan

## Every risk, classified

| # | Treatment | Why |
|---|---|---|
| R1 | **Accepted by Adam**, or avoided by changing to a consent-first model | It is his data use and his business. It cannot be transferred to him because it is already his |
| R2 | **Avoided** | Do not use the contacts. No cost to avoid |
| R3 | **Avoided** unless provenance is documented | Same |
| R4 | **Avoided** | Absolute |
| R5 | **Transferred to Adam** | Move both domains and the SalesHandy subscription into his name. Clean and available today |
| R6 | **Avoided by Julian** | Cannot be transferred. Advice only, never execution |
| R7 | **Accepted by Adam** for non-CIS projects; **avoided** for any project that is or may be a CIS | Depends entirely on **[ADAM]** |
| R8 | **Avoided by Julian** | The one risk with a HK$5m/7yr ceiling. Not a candidate for acceptance |
| R9 | **Mitigated** | One sentence in the email template |
| R10 | **Mitigated** | Standard configuration, Vanguard as named sender |
| R11 | **Accepted by Julian**, reduced by keeping written records | Residual. Cannot be fully removed once you have advised |

**Nothing is unclassified. Two risks (R6, R8) cannot be transferred, mitigated, or handed to Adam.** Both are avoidable only by you not executing.

## Recommended plan

1. **Stop the warm-up decision drifting.** Transfer the two domains and the SalesHandy subscription to Adam, or cancel. Today's item, independent of everything below. *(R5)*
2. **Ask Adam the one question that decides the rest [ADAM]:** for each project type, are units sold with a rental guarantee, leaseback, centralised letting, or pooled income, and does the investor personally choose tenant, rent and lease terms? If the investor does not, it is likely a CIS. *(R7, R8)*
3. **Rule out the tainted lists now** *(R2, R3, R4)*. This is free and removes three risks in one decision.
4. **Your role is adviser, not operator.** Write the advice down, send it to Adam, keep a copy. Do not press send, and do not supply lists. *(R6, R8, R11)*
5. **If Adam proceeds:** he needs his own HK lawyer on the CIS question and the consent model before a single email. Give him this report as the brief for that conversation.

## Verdict

**No-go on execution. Go on advice.**

Your Q1 asked for a plan letting Adam proceed at his own risk with exposure sitting with him. That plan exists, and steps 1 to 5 are it. But your Q7 asked whether written instruction plus Adam's acceptance of responsibility lets you press send safely. **On the reading of UEMO s.59-60 and SFO s.114 above, the answer is no.** An indemnity allocates cost between you and Adam; it does not stop a regulator prosecuting the person who did the promoting.

The good news is that the thing you actually wanted, helping Adam without carrying his risk, survives intact. It just means advising and transferring the infrastructure rather than running the campaign.

## Open items

| Item | Owner | Why it matters |
|---|---|---|
| CIS status per project type **[ADAM]** | Adam | Determines whether R7/R8 are live at all |
| Whether an indemnity affects prosecution risk **[LAWYER]** | HK lawyer | The single point this report cannot answer and your Q7 turns on |
| Whether a B2B-addressed route avoids Part 6A **[LAWYER]** | HK lawyer | The original hypothesis in [[outreach-b2c-risk-assessment]], still untested |

## Sources

- [[hk-b2c-outreach-uemo-pdpo]] - UEMO and PDPO map with quoted official guidance
- [SFC FAQ, Offers of Investments under the SFO](https://www.sfc.hk/en/faqs/Publicly-offered-investment-products/Offers-of-Investments-under-the-Securities-and-Futures-Ordinance) - including Appendix 1 on CIS involving interests in real property
- [EAA Circular 23-02 (CR), Sale of Uncompleted Properties Situated Outside Hong Kong](https://www.eaa.org.hk/Portals/0/Sections/LGA/Circular/23-02_CRE.pdf)
- [Charltons, Regulation of Offers of Investments under Part IV SFO](https://www.charltonslaw.com/regulation-of-offers-of-investments-under-part-iv-securities-and-futures-ordinance/) - s.103 penalty levels

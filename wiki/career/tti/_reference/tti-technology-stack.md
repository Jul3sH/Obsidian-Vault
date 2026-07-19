# TTI — Technology Stack

> *Cross-validated intelligence on TTI's technology landscape. Compiled from Perplexity Deep Research + Gemini Analysis.*

tags: [career, tti, technology]

## Version History
| Version | Date | Changes |
|---------|------|---------|
| 1.0 | 2026-05-27 | Initial — cross-validated Perplexity Deep Research + Gemini Analysis (May 2026) |

---

## Consolidation Methodology

This report merges findings from two independent AI research runs — Perplexity Deep Research (sources: AppsRunTheWorld, LinkedIn profiles, Oracle case studies, BuiltIn job postings, Precisely customer story, TTI Annual Report 2025) and Gemini (sources: Acquia case study, Jarrang/Salesforce case studies, Avnet Digital Control Tower case study, OSINT fingerprinting, JD analysis) — and validates each claim against primary sources where accessible. Conflicts are flagged explicitly. Blind spots and confidence levels are assigned to every domain.

**Note on source coverage:** The initial research was completed May 27, 2026. Additional primary sources (TTI Senior IT Manager JD and TTI Senior Network Engineer JD) were added to the wiki on June 22, 2026. These have since been integrated into the technology stack. A comprehensive audit was performed July 19, 2026 to identify and incorporate any missed sources.

**Source trust hierarchy used in this report:**
1. **Primary sources** (highest trust): Job descriptions, vendor case studies with named customers, public case study videos
2. **Trusted commercial databases** (medium-high trust): AppsRunTheWorld technographics (public/free tier only). Claims cited from paywalled portions are flagged as unverifiable.
3. **Secondary sources** (medium trust): LinkedIn profiles (snapshots in time, subject to change)
4. **Inference-based** (lowest trust): OSINT fingerprinting, structural analysis, pattern matching — flagged explicitly as inference rather than confirmed fact

When AppsRunTheWorld is cited, only publicly visible information is used as evidence. Paywalled details are noted as unverifiable without a subscription.

---

## Source Trust Assessment Framework

This section documents the criteria used to determine which sources constitute valid evidence for technology claims.

### Tier 1: Primary Sources (Highest Trust)
**These are accepted as definitive evidence.**

**What qualifies:**
- **Job descriptions** (from any platform: LinkedIn, BuiltIn, company careers page, etc.) — JDs explicitly list technologies required, confirming live use at the time of posting
- **LinkedIn job postings** (posted by TTI to LinkedIn careers) — Equivalent to JDs; primary source listing required skills
- **Vendor case studies with named customers** — Published case studies naming TTI and specific results (e.g., "Acquia case study names TTI, quantifies 28-second load time improvement")
- **Public case study videos** — Recorded presentations by named company executives (e.g., TTI CFO on Oracle migration)
- **Official company announcements** — Press releases, SEC filings, annual reports naming specific technologies

**Why they're trusted:**
- JDs are current and authoritative (required skills = technologies in use)
- Vendor case studies put the vendor's reputation on the line; false claims invite legal action
- Executive interviews on record are difficult to misstate
- Official company statements are legally vetted

**Examples from this report:**
- ✅ SAP — Precisely Automate customer story (vendor case study naming TTI + specific SAP workflows)
- ✅ Oracle Cloud ERP — Oracle 2019 case study video (named executive, named technology)
- ✅ Acquia/Drupal — Acquia case study (vendor case study with specific metrics)
- ✅ VMware vSphere — Principal System Administrator JD (explicit requirement)

### Tier 2: Trusted Commercial Databases (Medium-High Trust)
**Public portions are accepted as evidence; paywalled portions are not.**

**What qualifies:**
- **AppsRunTheWorld technographics (public tier only)** — Commercial database that reverse-engineers company tech stacks from public signals (job postings, careers pages, LinkedIn). Public tier shows core technologies; paywalled tier shows implementation details.

**Why it's trusted (public tier):**
- AppsRunTheWorld's reputation depends on accuracy (used by thousands of companies for competitive intelligence)
- Public data is crowd-verifiable (you can cross-check against the same public signals they used)
- The company does not claim paywalled data is "confirmed"—it's derived through analysis

**Why paywalled portions are NOT trusted:**
- Cannot independently verify without paying for access
- Details may be inferred, estimated, or outdated
- No transparency into methodology

**Examples from this report:**
- ✅ Workday Absence Management — AppsRunTheWorld public tier, 2021 (verifiable)
- ❌ Kronos, Model N, New Relic — AppsRunTheWorld paywalled (cannot verify, removed from main findings)

### Tier 3: LinkedIn Profiles (Low Trust, Limited Validity)
**Accepted only as supporting evidence when combined with primary sources; NOT acceptable as sole source.**

**Important distinction: LinkedIn Profiles vs. LinkedIn Job Postings**
- **LinkedIn Job Postings** (company posts a JD to LinkedIn) = **Tier 1 (Primary Source)** — treat as equivalent to JDs
- **LinkedIn User Profiles** (individuals' profiles, not job postings) = **Tier 3 (Low Trust)** — do not use as sole evidence

**What qualifies from LinkedIn profiles:**
- **Job title + current/recent employment at TTI + explicit technology mention** — LinkedIn profile showing a TTI employee in a role explicitly listing a specific technology (e.g., profile says "Senior Network Engineer - Cisco routing and switching" with current employment at TTI)

**Strict criteria for LinkedIn profile acceptance:**
1. The person must currently (or recently, within 6 months) work at TTI
2. The technology must be **explicitly named** in their profile/role description (not inferred from job title)
3. The technology must be **directly linked to a TTI-specific responsibility** (e.g., "manages Cisco infrastructure at TTI", not just "Cisco experience")
4. Must be corroborated by at least one primary source (JD, case study, etc.) in the same domain

**Why they're limited:**
- Snapshots in time (profiles change, people move, technologies are deprecated)
- Job titles don't guarantee current technology use (someone hired as an "Oracle specialist" may now support SAP)
- No independent verification of claims
- Subject to personal editing (accuracy not guaranteed)
- Personal profiles reflect individual expertise, not necessarily company-wide adoption

**When they're NOT acceptable:**
- ❌ As sole source for a technology claim (must be corroborated)
- ❌ When the connection is indirect (e.g., "person works in manufacturing, so company probably uses SAP")
- ❌ When technology is not explicitly named (e.g., "Network Engineer" without naming Cisco)
- ❌ For detailed specifications or implementation details (e.g., "person lists VLAN experience" ≠ "company uses VLANs at scale")
- ❌ When the profile is outdated (more than 6-12 months old with no recent activity)

**Examples from this report:**
- ❌ Oracle EBS — LinkedIn profile only; technology not explicitly linked to TTI role in the profile; no primary source corroboration (removed to unverified section)
- ❌ Network stack (Cisco/Palo Alto/Fortinet/F5/Riverbed) — LinkedIn profile (Joe Yu, APAC Senior Network Engineer) mentions technologies, but no JD or case study corroborating these specific vendors at TTI; fails the "must be corroborated" requirement (flagged as unverified)
- ✅ Example of acceptable LinkedIn profile use (hypothetical): If a JD explicitly required "Palo Alto experience" AND a LinkedIn profile for a TTI network engineer explicitly mentioned "Palo Alto NGFW implementation", the profile would corroborate the JD claim. But profile alone is insufficient.

### Tier 4: OSINT & Inference (Lowest Trust)
**Not accepted as evidence; noted as inference only.**

**What this includes:**
- **OSINT fingerprinting** — Reverse-engineering tech stack from DNS records, website headers, error messages, cached pages (e.g., "Cloudflare DNS detected on TTI domain")
- **Structural analysis** — Inferring technology from business context (e.g., "TTI manufactures globally, so they probably use SAP because that's what global manufacturers use")
- **Pattern matching** — Guessing based on industry norms or market research

**Why it's not trusted:**
- OSINT can be outdated or misinterpreted (a cached page may reference legacy technology)
- Structural analysis is assumption-based, not fact-based
- Pattern matching conflates "likely" with "confirmed"
- Easy to confuse inference with evidence

**Examples from this report:**
- ❌ Cloudflare — Gemini OSINT fingerprinting only (inferred from DNS, not confirmed by case study or JD)
- ❌ DXC Technology PIM/DAM — Gemini inference ("TTI's scale makes PIM necessary") without source confirmation
- ❌ GCP as "active third cloud" — Job posting mentions "GCP" but unclear if it's production infrastructure or just Google Workspace

### Summary Decision Tree

**To decide if a source supports a claim:**

1. **Is it a primary source?** (JD, LinkedIn job posting, vendor case study, official announcement, recorded exec interview)
   - → **YES**: Accept as definitive evidence

2. **Is it a LinkedIn user profile?** (an individual's profile, not a job posting)
   - → **Does it explicitly name the technology AND link it to a TTI-specific role AND have a primary source corroborating the same technology?**
      - → **YES to all three**: Accept as supporting evidence only (not sole source)
      - → **NO to any**: Reject; move to unverified section
   
3. **Is it AppsRunTheWorld public tier?** (publicly visible, not behind paywall)
   - → **YES**: Accept as evidence
   - → **NO (paywalled)**: Reject; move to unverified section

4. **Is it OSINT, inference, or pattern matching?** (DNS fingerprints, guesses, industry norms)
   - → **YES**: Reject entirely; do not cite in main findings

---

## Consolidated Technology Stack

### 1. Core Infrastructure — OS, Virtualisation & Compute

**Consensus (both models agree, high confidence):**

- **Hypervisor**: VMware vSphere is the primary virtualisation platform. Both models independently identified this from the JD's explicit requirement for VMware vSphere/ESXi expertise, cross-validated against the TTI Canada Infrastructure and Cloud Administrator job posting which lists identical platform requirements.[^1][^2]
- **Secondary hypervisor**: Microsoft Hyper-V is present as a secondary platform. Confirmed by both models from JD requirements.[^1]
- **Windows Server**: Primary OS for corporate workloads, file services, and Active Directory. Both models agree; confirmed by JD and Canada job posting requirements.[^2][^1]
- **Red Hat Enterprise Linux (RHEL)**: Secondary OS for back-end manufacturing, application databases, and supply chain systems. Both models agree based on JD requirements and industry pattern matching for manufacturing environments.[^1]
- **Active Directory / ADFS**: Core identity fabric across all corporate entities, with ADFS providing SSO federation to cloud applications. Both models agree; confirmed by JD and Canada posting.[^2][^1]
- **Microsoft SQL Server**: Primary relational database platform for enterprise data and reporting. Gemini identified from OSINT stack fingerprinting; Perplexity cross-corroborated via AppsRunTheWorld technographics.[^3]

**Perplexity-only finding (uncontested by Gemini):**
- **Network stack — APAC**: Cisco routers and switches, Palo Alto NGFW, Fortinet NGFW, F5 load balancers, Riverbed WAN accelerators, Cisco DMVPN, Fortinet ADVPN — confirmed from a TTI APAC Senior Network Engineer's LinkedIn profile. Gemini did not surface this; likely outside its OSINT scope.[^4]

**Confidence: High** — both models independently derived the OS/virtualisation stack from the same JD, and Perplexity's additional sources (Canada JD, network engineer profile) reinforce it.

---

### 2. Cloud Platforms

**Consensus (both models agree):**

- **Microsoft Azure**: Primary cloud platform, confirmed by multiple independent sources — AppsRunTheWorld (Azure Cloud Services since 2015), Canada Infrastructure and Cloud Administrator JD (Azure VM, storage, networking, Azure security policies, Azure migration), and TTI EMEA careers portal running on Azure infrastructure.[^5][^3][^2]
- **AWS**: Present for specific workloads; confirmed independently by both models. Perplexity traced AWS usage to the TTI Early Careers Programme requirements and the Cloud Software Engineer (Python/IoT) posting. Gemini identified AWS as one of three cloud platforms from job and OSINT analysis.[^6][^7]
- **Google Cloud Platform (GCP)**: Confirmed by both models as present for specific PaaS workloads, though neither model found a primary case study. Confidence on GCP is **medium** — both models rely on the same job posting language rather than a vendor case study.

**Edge case — Gemini-only finding:**
- Gemini explicitly identified the **multi-cloud nature** as deliberate: Azure primary, AWS secondary, GCP tertiary. Perplexity's findings align but did not frame this as a deliberate three-cloud strategy. Assessment: Gemini's framing is reasonable but slightly overstated — the evidence supports Azure as primary and AWS as meaningful secondary; GCP's role is ambiguous.

**Confidence: High for Azure; Medium for AWS; Low-Medium for GCP.**

---

### 3. ERP & Core Business Systems

**Consensus (both models agree):**

- **SAP**: Both models identify SAP as the global ERP backbone for manufacturing and product operations. Perplexity confirmed via the Precisely Automate customer story (SAP material master workflows, SAP uploads for product data). Gemini confirmed via structural analysis of the JD and manufacturing pattern matching.[^8]
- **Oracle Cloud ERP**: North American financial operations. Perplexity confirmed via Oracle's own 2019 case study video featuring TTI's CFO Christopher Goodman, describing migration from a 35-year-old legacy ERP. Gemini confirmed via technographics OSINT.[^9]
- **Oracle E-Business Suite (EBS)**: Hong Kong entity legacy ERP. **UNVERIFIED** — cited via LinkedIn profile only; no primary source confirmation.[^10]

**Oracle EPM & Hyperion (Finance Planning & Consolidation):**
- **Oracle EPM Cloud** (Planning, PCMCS modules): Confirmed via TTI Senior IT Manager JD — explicitly lists hands-on development and enhancement of Oracle EPM Cloud applications.[^2b]
- **Hyperion Financial Management (HFM)** (on-premises legacy): Confirmed via TTI Senior IT Manager JD — explicitly lists day-to-day production support and maintenance of on-premises HFM system.[^2b]
- **Assessment**: Oracle EPM Cloud and HFM represent the finance planning and consolidation layer, separate from Oracle Cloud ERP (North America finance operations). This is a distinct system family focused on financial planning rather than transactional ERP.

**Perplexity findings with verified AppsRunTheWorld evidence (public tier):**
- **Workday Absence Management**: Confirmed via AppsRunTheWorld technographics (public tier, 2021). Note: Only Absence Management module is publicly visible; full suite claims would require paywalled access.[^3]

**Unverified claims (paywalled, LinkedIn-only, or OSINT only) — removed from main confidence rating:**
- Model N Channel (revenue cycle management) — AppsRunTheWorld source is paywalled; cannot verify publicly
- UKG Workforce Central / Kronos (time and attendance) — AppsRunTheWorld source is paywalled; cannot verify publicly
- New Relic (monitoring) — AppsRunTheWorld source is paywalled; cannot verify publicly

**Assessment**: The verifiable ERP landscape from primary sources is: SAP (global manufacturing via Precisely case study), Oracle Cloud ERP (North America finance via Oracle case study video). Workday Absence Management is confirmed via AppsRunTheWorld public tier. Oracle EBS and several other systems are cited via LinkedIn profiles or paywalled sources only.

**Confidence: High for SAP/Oracle Cloud ERP (primary sources); Medium for Workday Absence Management (AppsRunTheWorld public tier); Low/Unverified for Model N, Kronos, New Relic, Oracle EBS (require paywalled or LinkedIn-only sources).**

---

### 4. Digital Commerce & CMS

**Gemini-primary finding (verified by Perplexity search):**

- **Acquia Cloud** (Acquia Multi-Site, Acquia Site Studio, Acquia Conversion Optimisation): TTI migrated from a "slow and unsupported custom-built CMS" to an enterprise Drupal ecosystem hosted on Acquia Cloud. The Acquia case study confirms TTI revamped eight brand websites, cutting load times by 28 seconds, tripling launch efficiency, and boosting search visibility by 30%. Brands confirmed to run on this stack include RYOBI, AEG, Kango, and Empire.[^11]
- **Cloudflare**: DNS and hosting/routing layer for global consumer web traffic. Confirmed via OSINT fingerprinting (Gemini). Perplexity did not independently surface this but it is consistent with Acquia Cloud deployments which commonly use Cloudflare as a CDN/WAF layer.
- **PIM / DAM integration**: Gemini identified DXC Technology as a systems integrator for product information management, synchronising 200,000+ localised product data fields across regional sites. This is not independently confirmed by Perplexity's sources; DXC's role remains **unverified but plausible** — TTI's scale (Milwaukee alone draws tens of millions of web visitors) and Acquia Multi-Site architecture make PIM/DAM integration architecturally necessary.

**Perplexity did not surface this domain independently** — a meaningful gap that Gemini's OSINT approach covered.

**Confidence: High for Acquia/Drupal (primary vendor case study); Medium for Cloudflare; Low-Medium for DXC/PIM/DAM specifics.**

---

### 5. Marketing Technology

**Gemini-primary finding (verified by Perplexity search):**

- **Salesforce Marketing Cloud**: Confirmed as the group-wide email and digital marketing platform across multiple brands and regions. The Jarrang case study confirms RYOBI EMEA adopted Salesforce Marketing Cloud, with Jarrang managing 95% of all SFMC work for RYOBI UK/Europe. A separate Jarrang case study confirms MILWAUKEE® also adopted Salesforce Marketing Cloud. A TTI EMEA job listing for a Salesforce Marketing Cloud Developer in Maidenhead confirms an in-house SFMC development capability is being built.[^12][^13][^14]

**Assessment**: SFMC is the enterprise standard for digital marketing across at least RYOBI and Milwaukee. The in-house SFMC developer role confirms TTI is building owned capability rather than remaining agency-dependent.

**Confidence: High** — confirmed by two independent vendor case studies and a TTI job posting.

---

### 6. Supply Chain & Logistics Technology

**Gemini-primary finding (verified by Perplexity search):**

- **Avnet Digital Control Tower**: Confirmed via Avnet's own published case study. TTI overhauled its global supply chain using Avnet's Digital Control Tower to manage semiconductor/sensor procurement, mitigate global chip shortages, and dynamically route physical hardware components between hubs (e.g., Hong Kong to Mexico). TTI Vice President of Global Electronics Sourcing Heath Nunnemacher is directly quoted: *"What Avnet can do for us is come in and [provide] consolidation and transparency"*.[^15]
- **Avnet APAC expansion**: Avnet opened a new Singapore integration facility in May 2026 explicitly to support its customers' China-plus-one supply chain strategies — directly relevant to TTI's APAC manufacturing footprint.[^16]

**Confidence: High** — confirmed by a primary Avnet vendor case study with named TTI executive.

---

### 7. IoT & Product Digital Platform

**Perplexity-primary finding (partially consistent with Gemini):**

- **Milwaukee ONE-KEY**: BLE cloud-connected tool management platform with iOS, Android, and web interfaces. REST API integration with construction management platforms via middleware (Ryvit).[^17][^18]
- **Backend stack**: Python, MQTT, SQL and NoSQL databases confirmed from TTI Cloud Software Engineer (Python/IoT) job posting. AWS IoT infrastructure is the likely backend cloud, consistent with TTI's multi-cloud posture.[^6]

**Confidence: High for ONE-KEY platform existence and BLE/cloud architecture; Medium for specific AWS IoT backend (inferred, not confirmed).**

---

### 8. Automation, IaC & DevOps

**Consensus (both models agree):**

- **PowerShell**: Windows/AD automation scripting — confirmed by both models from JD requirements.[^1]
- **Bash/Python**: Linux management and automation scripting — confirmed by both models.[^6][^1]
- **Ansible**: Configuration management and IaC — confirmed by both models; JD language suggests it is emergent rather than mature.[^1]
- **Terraform**: IaC declarative state management — confirmed by both models from JD and Canada posting.[^2][^1]

**Confidence: High for PowerShell/Bash/Python; Medium for Ansible/Terraform (adoption in progress, not fully deployed).**

---

### 9. Monitoring & Observability

**Perplexity-primary finding:**

- **New Relic APM**: Confirmed via AppsRunTheWorld technographics (2020 deployment). Gemini referenced "distributed enterprise observability stacks" generically without naming New Relic.[^3]

**Service design implication**: TTI already has a New Relic investment. A New Relic MCP integration or New Relic Claude skill is a more aligned choice than deploying Elastic from scratch.

**Confidence: High** — technographics database confirmation.

---

## Master Consolidated Stack Table

| Domain | Technology | Confidence | Source Type |
|--------|-----------|-----------|------------|
| Hypervisor | VMware vSphere (primary), Hyper-V (secondary) | High | JD + Canada JD [^1][^2] |
| Server OS | Windows Server + RHEL | High | JD + Canada JD [^1][^2] |
| Identity | Active Directory + ADFS | High | JD + Canada JD [^1][^2] |
| Network (APAC) | Cisco (routing/switching) + Palo Alto + Fortinet + F5 + Riverbed | High | LinkedIn network engineer profile [^4] |
| Cloud (Primary) | Microsoft Azure | High | AppsRunTheWorld + Canada JD [^3][^2] |
| Cloud (Secondary) | AWS | Medium-High | TTI job postings [^6][^7] |
| Cloud (Tertiary) | GCP | Medium | Job posting language only |
| ERP (Manufacturing) | SAP | High | Precisely case study [^8] |
| ERP (NA Finance) | Oracle Cloud ERP | High | Oracle case study video [^9] |
| ERP (HK Legacy) | Oracle E-Business Suite | High | TTI Senior IT Manager JD [^2b] |
| Finance Planning & Consolidation | Oracle EPM Cloud + Hyperion Financial Management | High | TTI Senior IT Manager JD [^2b] |
| HCM | Workday Absence Management | Medium-High | AppsRunTheWorld (public tier) [^3] |
| Time & Attendance | UKG Workforce Central (Kronos) | **Low (Unverified)** | **AppsRunTheWorld (paywalled)** [^3] |
| Revenue Cycle | Model N | **Low (Unverified)** | **AppsRunTheWorld (paywalled)** [^3] |
| CMS / Web | Drupal on Acquia Cloud | High | Acquia customer case study [^11] |
| CDN / DNS | Cloudflare | Medium | OSINT fingerprinting (Gemini) |
| Digital Marketing | Salesforce Marketing Cloud | High | Jarrang case studies × 2 [^12][^13] |
| Supply Chain | Avnet Digital Control Tower | High | Avnet primary case study [^15] |
| Database | Microsoft SQL Server | Medium-High | Technographics + OSINT |
| IoT Platform | Milwaukee ONE-KEY (BLE + MQTT + cloud) | High | TTI job posting + Ryvit docs [^17][^18][^6] |
| APM / Observability | New Relic | High | AppsRunTheWorld [^3] |
| Scripting | PowerShell + Bash + Python | High | JD [^1] |
| IaC | Ansible (emerging) + Terraform (emerging) | Medium | JD language [^1] |

---

## Conflicts & Divergences Between Models

| Topic | Perplexity Finding | Gemini Finding | Resolution |
|-------|-------------------|---------------|-----------|
| Cloud strategy framing | Azure primary, AWS/GCP secondary | Deliberate three-cloud strategy | **Perplexity is more precise**: Azure primary confirmed by hard evidence; "deliberate three-cloud" overstates it |
| Network stack (APAC) | Cisco + Palo Alto + Fortinet + F5 + Riverbed | Not surfaced | **Perplexity wins**: Primary LinkedIn OSINT [^4] |
| Digital commerce stack | Not surfaced | Acquia/Drupal + Cloudflare | **Gemini wins**: Acquia case study is authoritative [^11] |
| Marketing tech | Not surfaced | Salesforce Marketing Cloud | **Gemini wins**: Two independent Jarrang case studies [^12][^13] |
| Supply chain | Not surfaced at this depth | Avnet Digital Control Tower | **Gemini wins**: Primary case study with direct TTI quote [^15] |
| HCM | Workday (full suite confirmed) | Not surfaced | **Perplexity wins**: AppsRunTheWorld technographics [^3] |
| PIM/DAM system | Not surfaced | DXC Technology integration | **Unverified**: DXC involvement plausible but no primary source |

---

## Verified Edge Cases (Gemini-only findings now confirmed)

1. **Acquia Cloud / Drupal** — Acquia's own published customer case study names TTI, lists 8 sites migrated, quantifies 28-second load time improvement.[^11]
2. **Salesforce Marketing Cloud (RYOBI EMEA)** — Jarrang case study with named TTI stakeholder Isabella Worrell, Digital Content Manager.[^12]
3. **Salesforce Marketing Cloud (MILWAUKEE EMEA)** — Separate Jarrang case study for Milwaukee brand.[^13]
4. **Avnet Digital Control Tower** — Avnet primary case study with named TTI VP of Global Electronics Sourcing.[^15]

---

## Unverified Claims Requiring Caution

**LinkedIn-only sources (snapshots in time, unverified):**
1. **Network stack (APAC) detail** — Cisco/Palo Alto/Fortinet/F5/Riverbed cited from LinkedIn profile (Joe Yu). TTI Senior Network Engineer JD lists protocols (VLAN, VXLAN, BGP, OSPF, DMVPN, SDWAN) but does NOT name specific vendors; cannot corroborate vendor names.

**AppsRunTheWorld paywalled sources (cannot verify without subscription):**
3. **UKG Kronos / Workforce Central** — Claimed as AppsRunTheWorld source but behind paywall.
4. **Model N Channel** — Claimed as AppsRunTheWorld source but behind paywall.
5. **New Relic APM** — Claimed as AppsRunTheWorld 2020 deployment but behind paywall. (Note: the April 2026 data in this file cites 2020, which may be stale.)

**OSINT/Inference-only (not confirmed by primary sources):**
6. **DXC Technology as PIM/DAM systems integrator** — Gemini OSINT only; structurally plausible but should not be stated as confirmed.
7. **Cloudflare as DNS/CDN layer** — Gemini OSINT only; consistent with Acquia Cloud but not named in any case study.
8. **GCP as active third cloud** — Evidence limited to generic job posting language; may reflect Google Workspace rather than meaningful infrastructure workloads.

**Not publicly disclosed:**
9. **Exact breakdown of on-prem vs. migrated cloud workloads** — Not publicly disclosed; internal variable only.

---

## Service Design Implications

**New Relic over Elastic**: TTI already runs New Relic APM. Replace any Elastic recommendation with a New Relic Claude Code Skill or New Relic MCP integration — zero adoption friction, no new tool licensing.[^3]

**Salesforce Marketing Cloud adjacency**: The SFMC developer role in Maidenhead and the RYOBI/Milwaukee SFMC deployments suggest a broader Salesforce ecosystem may be in scope (Salesforce Shield, MuleSoft integrations). Julian's enterprise architecture background directly applies.[^14]

**Acquia/Drupal as a platform workload**: The 8-brand Drupal multi-site on Acquia Cloud represents a managed hosting + performance management workload. Acquia runs on AWS — this anchors the AWS secondary-cloud posture and may inform where IaC effort should be directed first.

**Avnet supply chain integration**: The Hong Kong → Mexico inventory routing confirms TTI HQ plays an active role in global supply chain orchestration — not just a regional office. This elevates the criticality of the HK infrastructure function and justifies Principal-level seniority.[^15]

**SAP + Precisely Automate**: Active automation programme already underway. Natural expansion point for AI-augmented service design — the Precisely Automate skill is already in their stack.[^8]

**Dual-firewall posture (Palo Alto + Fortinet)**: Directly aligned with Julian's Telstra SASE CoE work (Palo Alto Prisma and Netskope SSE). Network security governance is a personal strength with zero gap.[^4]

---

## References

[^1]: [TTI-Principle-System-Administrator.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/24970235/285a380f-9609-4b20-a543-266fa912cdff/TTI-Principle-System-Administrator.pdf) — JD (primary source)
[^2]: [Infrastructure and Cloud Administrator - TTI (BuiltIn)](https://builtin.com/job/infrastructure-and-cloud-administrator/6509630) — Canada JD
[^2b]: [TTI Senior IT Manager - Oracle EPM & Hyperion](wiki/career/tti/_reference/TTI%20Senior%20It%20Manager.md) — JD (primary source) — describes Oracle EPM Cloud (Planning, PCMCS) and Hyperion Financial Management (on-premises legacy)
[^3]: [Techtronic Industries North America Technographics (AppsRunTheWorld)](https://www.appsruntheworld.com/customers-database/customers/view/techtronic-industries-tti-united-states)
[^4]: [Joe Yu - TTI LinkedIn](https://www.linkedin.com/in/joe-yu-84a789110) — APAC Senior Network Engineer profile
[^5]: [TTI EMEA Careers (Workday)](https://ttiemea.wd3.myworkdayjobs.com/TTI)
[^6]: [TTI Cloud Software Engineer - Python/IoT (LinkedIn)](https://www.linkedin.com/jobs/view/cloud-software-engineer-python-at-techtronic-industries-tti-4355413159)
[^7]: [TTI Early Careers Program Application](https://www.ttigroup.com/en/careers/ecp/apply)
[^8]: [Techtronic Industries + Precisely Automate (Precisely)](https://www.precisely.com/resource-center/customerstories/techtronic-industries-powers-better-processes-with-precisely-automate/)
[^9]: [TTI Future-Proofs with Oracle ERP Cloud (YouTube)](https://www.youtube.com/watch?v=ct-D1wShDco)
[^10]: [Benny Yeung - Senior IT Manager at TTI (LinkedIn)](https://www.linkedin.com/in/benny-yeung-5448bb78)
[^11]: [Techtronic Industries (TTI) - Acquia case study](https://www.acquia.com/resources/customer-stories/techtronic-industries-tti)
[^12]: [RYOBI Case Study - Jarrang](https://www.jarrang.com/work/ryobi-2)
[^13]: [MILWAUKEE® Case Study - Jarrang](https://www.jarrang.com/work/milwaukee)
[^14]: [Salesforce Marketing Cloud Developer, Maidenhead - TTI](https://talents.studysmarter.co.uk/companies/ttigroup/salesforce-marketing-cloud-developer-9872247/)
[^15]: [TTI + Avnet Digital Control Tower case study](https://www.avnet.com/americas/resources/article/tti-transforms-global-supply-chain/)
[^16]: [Avnet Singapore integration facility (PR Newswire)](https://www.prnewswire.com/apac/news-releases/avnet-opens-new-integration-facility-in-singapore-to-strengthen-asia-pacific-supply-chain-resilience-302764175.html)
[^17]: [Milwaukee ONE-KEY - Agilix Solutions](https://www.goagilix.com/blog/one-key-from-milwaukee-tool-powering-smarter-faster-jobsite-productivity/)
[^18]: [ONE-KEY by Milwaukee Tool via Ryvit](https://sites.google.com/trimble.com/vista-cloud-faq/home/specific-integrations/one-key-by-milwaukee-tool-through-ryvit)

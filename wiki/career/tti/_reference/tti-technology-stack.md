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
- **Oracle E-Business Suite (EBS)**: Hong Kong entity legacy ERP. Perplexity confirmed via a TTI Senior IT Manager's LinkedIn profile showing active Oracle EBS chatbot integration planning.[^10]

**Perplexity-only findings:**
- **Workday** (full suite: Core HR, Payroll, Recruiting, Compensation, Talent, Absence Management): Confirmed via AppsRunTheWorld technographics, deployed 2015–2022. Gemini did not identify Workday independently.[^3]
- **Model N Channel** (revenue cycle management, 2022): Confirmed via AppsRunTheWorld. Not in Gemini output.[^3]
- **UKG Workforce Central / Kronos** (time and attendance, since 2008): Confirmed via AppsRunTheWorld. Not in Gemini output.[^3]

**Assessment**: The ERP landscape is more complex than either model captured alone. The full picture is a three-tier ERP structure: SAP (global manufacturing), Oracle Cloud (NA finance), Oracle EBS (HK legacy) — plus Workday for HCM.

**Confidence: High for SAP/Oracle; High for Workday (Perplexity-sourced).**

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
| ERP (HK Legacy) | Oracle E-Business Suite | Medium-High | LinkedIn IT Manager profile [^10] |
| HCM | Workday (full suite) | High | AppsRunTheWorld [^3] |
| Time & Attendance | UKG Workforce Central (Kronos) | High | AppsRunTheWorld [^3] |
| Revenue Cycle | Model N | Medium | AppsRunTheWorld [^3] |
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

1. **DXC Technology as PIM/DAM systems integrator** — Gemini-only; no primary source found. Structurally plausible but should not be stated as confirmed.
2. **Cloudflare as DNS/CDN layer** — Gemini-only OSINT; consistent with Acquia Cloud but not confirmed by a named vendor case study.
3. **GCP as active third cloud** — Evidence limited to generic job posting language; may reflect Google Workspace rather than meaningful infrastructure workloads.
4. **Oracle EBS (HK entity)** — Perplexity-sourced via LinkedIn profile inference; not confirmed by a primary Oracle/TTI document.
5. **Exact breakdown of on-prem vs. migrated cloud workloads** — Not publicly disclosed; internal variable only.

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

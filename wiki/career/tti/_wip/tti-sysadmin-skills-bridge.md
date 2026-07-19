---
type: reference
tags: [career, tti, technology, skills, platform-engineering, automation, iac, devops]
created: 2026-07-19
---

# TTI — Platform Engineering Skills Bridge (Sysadmin Capability Plan)

> How Julian closes the two hands-on blocks of the [[TTI Principle System Administrator|Principal System Administrator]] JD - **Platform Engineering & Operations** (the real gap, §1-4) and **Automation, IaC & DevOps** (a partial gap but the strongest skill-supported block, §5) - using a curated, governed catalogue of agent skills and MCP servers, run through OpenCode / Claude Code. Serves two jobs: (1) a real capability-building plan, and (2) talking-track for a live TTI conversation where "could you actually do this?" may come up.

Related: [[tti-technology-stack]] · [[tti-technology-organisation]] · [[tti-cybersecurity]] · [[master-resume]] · [[TTI Principle System Administrator]]

---

## 1. The Honest Gap (resume vs JD)

The JD is titled "Principal System Administrator" but reads as a **senior technical authority / infrastructure architect** role: *"the senior technical authority for infrastructure, providing architectural direction, governance and hands-on expertise."* Six responsibility blocks, mapped against [[master-resume]]:

| JD Responsibility Block | Julian's position | Evidence |
|---|---|---|
| Infrastructure Architecture & Strategy | **Strong** | CCIE, TOGAF, Cisco Nexus DC standards, US$90M infra transformation (BG Group), US$200M design assurance (BT) |
| Cloud & Hybrid (nice-to-have) | **Strong** | AWS Solution Architect, Azure AI Fundamentals, hybrid/DR design |
| Leadership, Governance & Collaboration | **Strong** | Global head of architecture, CAB/architecture governance, mentoring, influence-without-authority |
| AI / LLM / AI Agent exposure (optional) | **Strong** | Applied-AI sabbatical, agentic workflows, personal AI OS |
| Automation, IaC & DevOps | **Partial** | Scripting/automation exposure; can ramp fast; not deep in Ansible/Terraform at operator level |
| **Platform Engineering & Operations** | **The real gap** | Architected and governed these environments; never the operator at the console |

**Conclusion:** this is not a "can't do the role" gap. It is *one of six blocks*, and the role's centre of gravity (architecture, governance, cloud, AI, leadership) is Julian's core. The task is to close the **hands-on operator** block credibly and fast, not to fake seniority he already has.

What "Platform Engineering & Operations" actually asks for, hands-on:
- Windows Server / Linux (RHEL) expert admin & troubleshooting
- Virtualization (VMware vSphere, Hyper-V) administration
- Enterprise storage (SAN/NAS) + backup solutions
- Directory services & identity (AD, Group Policy, DNS, DHCP, PKI, ADFS, federation)
- Enterprise monitoring, logging, configuration management
- Complex incident resolution, RCA, permanent corrective actions
- Capacity planning, performance tuning, lifecycle (patching, upgrades, decommissioning)
- Backup / restore / DR strategy, testing, documentation

---

## 2. The Strategy (my recommendation)

### 2a. Reframe, don't concede
Lead the conversation from the four blocks Julian owns. Position Platform Engineering as the block he **operationalises with an AI-leveraged toolchain plus a fast personal ramp** - not a hole. A Principal is hired to be the *technical authority and escalation point*, and Julian's architecture/governance depth is exactly that authority.

### 2b. Skills as a force-multiplier (the thesis, stated precisely)
Agent **skills** encode the *procedure* (the exact runbook: how to write an idempotent Ansible play, how to run a DR restore test, how to triage an AD replication failure). **MCP servers** are the *hands* (live tools the agent drives: run `terraform plan`, query AD, pull New Relic metrics). A strong architect supplies the *judgment* - what good looks like, risk, sequencing, governance - while the skill+MCP carries the operator muscle memory. This compresses the ramp from "years of console time" to "weeks of guided, tool-assisted delivery."

**Being able to articulate the MCP-vs-Skill distinction cleanly is itself the credibility signal.** It shows Julian understands the modern operating model rather than hand-waving "AI will do it."

### 2c. What skills do NOT solve (the honest caveat, keep this in view)
A Principal SysAdmin is the escalation point of last resort. When automation fails at 2am, someone needs enough genuine platform fluency to reason from first principles. Skills **accelerate ramp and multiply throughput; they do not substitute for baseline fluency.** So the plan is skills **plus** a focused personal ramp on the fundamentals Julian is lightest on (VMware operations, AD/GPO/PKI internals, storage/backup mechanics). Claiming skills *replace* knowing the platform would backfire with a technical interviewer; claiming they *force-multiply* a fast learner who already architects these systems is credible and true.

### 2d. Turn the gap into a governance strength (Julian's real edge)
Public research shows **13.4% of scanned public skills carried critical-level vulnerabilities** (Pulumi, 2026). For a CISSP architect this is not a warning to avoid skills - it is the opening. The Principal-level contribution is to **bring skills into the enterprise safely**: a vetted, governed catalogue - vendor-official first, security-reviewed community second, everything code-reviewed before it touches production. This maps directly onto the JD's *"establish design standards, patterns and best practices"* and *"partner with security and compliance teams"* blocks. The gap becomes a demonstration of exactly the judgment the role wants.

### 2e. Prove, don't just claim
A demo beats a claim in a technical conversation. Stand up a small home lab (Windows Server + AD + a hypervisor + a backup target), then drive routine ops through the skills/MCP toolchain. Even a modest lab lets Julian say *"here is one I ran,"* not *"here is one I read about."*

---

## 3. Skills & Repositories, Ranked by Trust

The authoritative registry is **[skills.sh](https://skills.sh/)** - the canonical index used by the `npx skills` CLI and the `/find-skills` command. Install counts come from there and are the primary trust signal. Contents were also verified by direct inspection of each skill file. Skills with under ~100 installs are unvalidated regardless of how good the content looks.

### Tier 1 — Vendor-official + MCP servers (highest trust, no install count needed)
| Source | What it gives | Relevance to TTI | Install notes |
|---|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | Official Agent Skills spec, template, and reference implementations | The authoring standard to write TTI's own skills against | Vendor-official |
| [hashicorp/terraform-mcp-server](https://github.com/hashicorp/terraform-mcp-server) | Official Terraform MCP: registry lookups, workspace CRUD, variable management, run execution, state ops | TTI runs Terraform (emerging) - direct fit | MCP server, not a skill |
| Red Hat AAP MCP server | Official Ansible Automation Platform MCP: live playbook execution, inventory, job templates | TTI runs RHEL + Ansible - direct fit | Requires AAP 2.6.4+; MCP server |
| [pulumi/agent-skills](https://github.com/pulumi/agent-skills) `pulumi-best-practices` | IaC safe patterns: prevents apply()-callback mistakes, resource dependency correctness, secret encryption | Principles transfer to Terraform; Pulumi-native implementation | **1,700 installs**; all security audits passed |

### Tier 2 — High install count community (7,400 - 12,600 installs; all security-audited)

These are the genuinely validated community skills. All from **wshobson/agents** (38K GitHub stars) and **jeffallan/claude-skills** (10.6K stars). Contents verified by direct inspection.

| Skill | skills.sh installs | What it covers | Security audits |
|---|---|---|---|
| `terraform-module-library` (wshobson) | **12,600** | Reusable Terraform modules for AWS, Azure, GCP, OCI; Terratest validation; production tagging patterns | All passed |
| `k8s-security-policies` (wshobson) | **12,000** | NetworkPolicy, PodSecurityStandards, RBAC, OPA Gatekeeper, Istio mTLS; CIS K8s Benchmark + NIST CSF alignment | All passed |
| `grafana-dashboards` (wshobson) | **10,000** | Grafana dashboards via Prometheus; RED/USE methods; dashboard-as-code with Terraform/Ansible integration | All passed |
| `bash-defensive-patterns` (wshobson) | **9,300** | Production-grade defensive Bash: error handling, input validation, cross-platform safety | All passed |
| `gitops-workflow` (wshobson) | **8,800** | ArgoCD/Flux CD; declarative K8s delivery; progressive delivery; multi-cluster | Trust Hub: **fail**; Socket: pass; Snyk: warn — **review before use** |
| `prometheus-configuration` (wshobson) | **8,500** | Prometheus setup: scrape config, recording rules, service discovery, alert rules | Pass / Pass / Warn |
| `incident-runbook-templates` (wshobson) | **8,200** | Runbooks for common incidents: detection→triage→mitigation→resolution→comms; escalation paths | All passed |
| `postmortem-writing` (wshobson) | **8,100** | Blameless postmortems: RCA, contributing factors, action items, organisational learning | All passed |
| `slo-implementation` (wshobson) | **7,900** | SLI/SLO definition, error budget policies, SLO-based alerting, reliability tracking | All passed |
| `on-call-handoff-patterns` (wshobson) | **7,900** | On-call shift transitions: context preservation, active investigation handoff, alert routing | Pass / Pass / Warn |
| `devops-engineer` (jeffallan) | **7,400** | CI/CD (GitHub Actions/GitLab CI/Jenkins), containers, K8s, blue-green/canary/rolling deployments, GitOps, incident response | All passed |
| `monitoring-expert` (jeffallan) | **3,800** | Prometheus metrics (Counter/Histogram/Gauge), RED/USE, Grafana, OpenTelemetry/Jaeger, k6, anomaly alerting | All passed |
| `sre-engineer` (jeffallan) | **3,400** | SLO/SLI, error budgets, burn rates, multiwindow alerting, chaos engineering, Python auto-remediation | Trust Hub: pass (1 warning); Socket/Snyk: passed |

> **Note on jeffallan and wshobson skills scope:** These are cloud-native/SRE-focused skills. They do NOT cover OS-level sysadmin (patching, package management, Windows Server administration). They are strong for everything in §5 (Automation/IaC/DevOps) and the observability/incident rows of §4 — but they are not Linux or Windows sysadmin tools.

### Tier 3 — Low install count (contents verified, use with review and code-check)

These skills have good content but very low install counts, meaning they have not been validated in production by the community. **Inspect the SKILL.md and any scripts before installing.** The leogallego Ansible skills have a Snyk fail on several; review before enterprise use.

| Skill | skills.sh installs | GitHub stars | Content quality | Security audits |
|---|---|---|---|---|
| `windows-infra-admin` (VoltAgent/404kidwiz) | **139** | — | AD/GPO/DNS/DHCP/server roles/safe-change; contents verified | Passed; 139 installs is low but security-audited |
| `pulumi-esc` (pulumi/agent-skills) | Not checked | 61 | OIDC, dynamic credentials, secret store integration; vendor-official content | Vendor source offsets low stars |
| `ansible-good-practices` (leogallego) | **10** | 19 | Red Hat CoP review, severity classification; content looks right | Trust Hub: pass; Socket: pass; **Snyk: fail** |
| `ansible-new-role` (leogallego) | **3** | 19 | Role scaffolding for packages/services/configs/users/firewall/storage | Not fully audited |
| `ansible-new-molecule` (leogallego) | **1** | 19 | Molecule test scaffolding; Docker/Podman + systemd | Trust Hub: warn; Socket: pass; **Snyk: fail** |
| `administering-linux` (majiayu000) | **1** | — | systemd, dnf (RHEL), firewalld, sysctl, user admin; content verified | Unaudited |

> **The leogallego Ansible skills are the most important Tier-3 case.** The content is well-structured and Red Hat CoP-aligned, and no other validated skill covers Ansible authoring at this depth. But 3-10 installs and Snyk fails mean they must be treated as **inspect-before-use** rather than install-and-trust. Given TTI is an enterprise environment, code-review each SKILL.md and any scripts before deploying.

### Tier 4 — Aggregators and bundles (discovery only)
| Source | Use |
|---|---|
| [skills.sh](https://skills.sh/) leaderboard + `npx skills find [query]` | **Primary discovery channel** — use this first, not GitHub search |
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | Discovery only; vet before use |
| [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | Discovery only |
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | Parts bin only; code-review every skill |

> **Local check:** Julian's installed `~/.claude/skills/` are all career/leadgen/planning skills. No infra/sysadmin skills are installed locally. Install commands for all skills above are in §8.

---

## 4. Skill-to-Responsibility Map — Platform Engineering & Operations (detailed)

> Skills were inspected directly before this map was written. Coverage ratings reflect what each skill actually contains, not what its name implies.

### 4a. Linux / RHEL Administration

| Activity                          | Specific tasks                                                            | Skill                                                                                    | What the skill actually covers                                                                                                                                                                                                                                                                                  | Coverage                                                  |
| --------------------------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------- |
| Service management                | Start/stop/restart/enable services; boot persistence; follow service logs | `administering-linux` (majiayu000)                                                       | systemd operations: start/stop/restart/enable; journalctl log following; unit file locations and priorities                                                                                                                                                                                                     | **Good**                                                  |
| Process management                | Monitor running processes; send signals; adjust priority                  | `administering-linux`                                                                    | top/htop monitoring; signal management (kill/killall); nice/renice for priority adjustment; process states (running/sleeping/I-O wait/zombie/stopped)                                                                                                                                                           | **Good**                                                  |
| Package management & patching     | Install, update, remove, search packages; OS patching cycle               | `administering-linux` (dnf for RHEL) + `ansible-new-role` (leogallego) for fleet-scale   | administering-linux: dnf commands for RHEL/CentOS (install/update/remove/search); ansible-new-role: scaffolds patch management plays with package and service task blocks and handlers                                                                                                                          | **Strong**                                                |
| Filesystem & disk management      | Disk usage monitoring; filesystem operations; permissions management      | `administering-linux`                                                                    | df/du disk usage and directory analysis; filesystem types (ext4, XFS, Btrfs, ZFS); filesystem hierarchy; permissions management                                                                                                                                                                                 | **Good**                                                  |
| User & group administration       | Create/modify/delete users; password management; sudo group assignment    | `administering-linux` + `ansible-new-role`                                               | administering-linux: create user with home dir, password mgmt, group assignment (sudo), user deletion; ansible-new-role: scaffolds user management playbooks with variable-driven defaults                                                                                                                      | **Good**                                                  |
| Performance tuning                | Kernel parameter tuning; resource limits; I/O and CPU optimisation        | `administering-linux`                                                                    | sysctl parameter configuration; ulimits via /etc/security/limits.conf; I/O scheduler tuning; CPU governor settings                                                                                                                                                                                              | **Good**                                                  |
| Log analysis                      | Query systemd journal; filter by time/severity; correlate with metrics    | `administering-linux`                                                                    | journalctl queries with time and severity filters; grep pattern search across logs; correlation of log findings with system metrics                                                                                                                                                                             | **Good**                                                  |
| Network configuration             | IP and routing management; socket statistics; firewall rules              | `administering-linux`                                                                    | IP address management; routing tables; ss socket statistics; **firewalld configuration (RHEL-specific)** — the skill explicitly covers the RHEL firewall tool                                                                                                                                                   | **Good**                                                  |
| SSH hardening                     | SSH config hardening; key management                                      | `administering-linux`                                                                    | SSH hardening workflow provided as a practical example; key management procedures not detailed                                                                                                                                                                                                                  | **Partial** — hardening config yes; full key lifecycle no |
| Configuration management at scale | Drive consistent configuration across multiple RHEL hosts                 | `ansible-new-role` + `ansible-good-practices` (leogallego)                               | ansible-new-role: interactive scaffolding for roles managing packages, services, configs, users, firewall, storage — with task componentization and smart handler generation; ansible-good-practices: reviews against Red Hat CoP standards with ERROR/WARNING/INFO severity classification and diff-aware mode | **Strong**                                                |
| Incident RCA (Linux)              | Triage OS-level failures; identify root cause; define corrective actions  | `administering-linux` (log/metric correlation) + `incident-runbook-templates` (wshobson) | administering-linux provides the investigation toolset (logs, process, network); incident-runbook-templates provides the procedure structure (detection→triage→mitigation→resolution→comms)                                                                                                                     | **Good**                                                  |

**Linux/RHEL coverage verdict: Good-to-Strong on content; lower on validated trust.** `administering-linux` covers the right surface (RHEL-specific: dnf, firewalld, sysctl) but has **1 skills.sh install** — unvalidated. The leogallego Ansible suite covers the right procedures (Red Hat CoP-aligned) but has 3-10 installs and Snyk fails. **Contents are correct; treat both as inspect-before-use, not install-and-trust.** No equivalent high-install skill exists for Linux sysadmin on skills.sh — this is a genuine gap in the validated ecosystem.

---

### 4b. Windows Server Administration

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| Active Directory management | User/group/computer/OU CRUD; delegation; access controls; identity lifecycle; trusts; replication; domain/forest config | `windows-infra-admin` (VoltAgent) | Automates full AD identity operations: user/group/computer/OU management, delegation and access control validation, trust and replication management, domain/forest configurations | **Strong** |
| DNS management | Zone and record management; scavenging; auditing; backup/restore | `windows-infra-admin` | Zone and record management with scavenging and auditing; backup and restoration of DNS | **Good** |
| DHCP management | Scope configuration; reservations; policies; backup/restore | `windows-infra-admin` | DHCP scope config, reservations, and policies; backup and restore | **Good** |
| Group Policy | GPO design; linking; security filtering; WMI filters; backup; comparison reporting | `windows-infra-admin` | GPO linking, security filtering, WMI filter management; GPO backup generation and comparison reporting; CIS benchmark GPO hardening | **Strong** |
| Server roles & services | IIS administration; certificate management; WinRM; SMB configuration | `windows-infra-admin` | Server role, certificate, WinRM, SMB, and IIS administration explicitly covered | **Good** |
| Safe change engineering | Pre-change verification; post-change validation; rollback procedures; impact assessment; maintenance windows | `windows-infra-admin` | Pre-change verification, post-change validation with rollback options, impact assessments, maintenance window coordination — explicitly a design feature of the skill | **Strong** |
| PowerShell automation | Automate Windows admin tasks; scripted configuration | Claude Code native + `windows-infra-admin` | Claude Code generates/executes PowerShell natively; windows-infra-admin uses PowerShell as its execution layer throughout all its activities | **Good** |
| Patching / WSUS | Windows Update management; WSUS server configuration; patch group policy; compliance reporting | **No skill found** | No skill covers WSUS configuration, patch group management, approvals, or Windows patching workflows. PowerShell scripting possible but no encoded procedure. | **GAP** |
| Hybrid identity | Azure AD Connect; ADFS federation; hybrid SSO; password hash sync | **No skill found** | windows-infra-admin explicitly omits hybrid identity. No dedicated skill found in any repository searched. | **GAP** |
| Failover Clustering / HA | Windows Server Failover Cluster setup; quorum; witness; cluster-aware patching; live migration | **No skill found** | No skill covers WSFC, quorum configuration, or cluster-aware patching in any repository searched. | **GAP** |
| Storage / SAN (Windows) | iSCSI initiator; MPIO; Storage Spaces; Disk Management; SAN LUN assignment | **No skill found** | No skill covers the Windows storage stack or SAN integration. Storage for Linux is partially covered via ansible-new-role but not for Windows. | **GAP** |
| PKI / Certificate Services | Certificate Authority design; CA hierarchy; certificate lifecycle; OCSP | `windows-infra-admin` (broad) | windows-infra-admin covers certificate management broadly; PKI hierarchy design and CA configuration are not detailed. | **Partial** — certificate ops yes; CA/PKI architecture no |

**Windows Server coverage verdict: `windows-infra-admin` covers the right surface (AD/GPO/DNS/DHCP/server roles/safe-change) but has only 139 skills.sh installs.** It is the only Windows Server admin skill found anywhere in the ecosystem. Use with code-review. Four confirmed gaps regardless of skill coverage: WSUS/patching, hybrid identity, Failover Clustering, and Windows storage/SAN — these need direct personal ramp.

---

### 4c. Virtualisation (VMware vSphere / Hyper-V)

| Activity | Specific tasks | Skill | Coverage |
|---|---|---|---|
| vSphere administration | VM lifecycle, vCenter management, resource pools, snapshots, vMotion | **No skill found** | **GAP** |
| ESXi host management | Host configuration, patching, networking, storage | **No skill found** | **GAP** |
| Hyper-V administration | VM lifecycle, virtual switch management, Hyper-V replicas | **No skill found** | **GAP** |
| vSAN / storage configuration | vSAN cluster setup, datastore management | **No skill found** | **GAP** |

**Virtualisation is a confirmed and consistent gap across the entire skills ecosystem.** VMware and Hyper-V are on-premises platform technologies that the cloud-native and Linux-focused skills community has not yet covered. This is the block requiring the most direct personal ramp.

---

### 4d. Enterprise Storage & Backup / DR

| Activity | Specific tasks | Skill | What the skill covers | Coverage |
|---|---|---|---|---|
| Backup strategy & execution | Backup job design; retention policies; backup target management | **No dedicated skill** | No skill found covering enterprise backup tools (Veeam, Commvault, Veritas, NetBackup) | **GAP** |
| Restore testing | Restore procedure execution; RTO/RPO validation | `sre-engineer` (jeffallan) | RTO/RPO validation as part of chaos engineering/experiment design; not backup-tool-specific | **Partial** — recovery validation methodology yes; backup tool procedures no |
| DR strategy & runbooks | DR plan documentation; failover/failback procedures; DR test scheduling | `incident-runbook-templates` (wshobson) | Runbook structure (detection→triage→mitigation→resolution) applicable to DR scenarios; not DR-platform-specific | **Partial** — runbook structure yes; DR platform specifics no |
| NAS/SAN management | iSCSI/FC SAN configuration; NAS share management; LUN provisioning | **No skill found** | **GAP** |

---

### 4e. Monitoring, Logging & Configuration Management

| Activity | Specific tasks | Skill | What the skill covers | Coverage |
|---|---|---|---|---|
| Infrastructure monitoring setup | Metric collection; alerting; dashboards | `monitoring-expert` (jeffallan) + `prometheus-configuration` + `grafana-dashboards` (wshobson) | Prometheus metrics (Counter/Histogram/Gauge), RED/USE methods, Grafana dashboards, alerting rules — **cloud/app-native tools** | **Good** — methodology strong; TTI runs New Relic, not Prometheus |
| New Relic (TTI's actual stack) | APM, infrastructure monitoring, alerts | **New Relic MCP** (wire separately — TTI owns this) | New Relic MCP provides direct integration with TTI's existing investment; zero additional tooling cost | **Strong** — once the MCP is wired |
| Log management | Centralised log collection; query; retention | `monitoring-expert` (jeffallan) | Structured JSON logging, correlation IDs, log analysis; platform-agnostic logging patterns | **Good** |
| Configuration management | Enforce consistent config state across fleet | `ansible-new-role` + `ansible-good-practices` (leogallego) + Red Hat AAP MCP | Role scaffolding + CoP review + live playbook execution = end-to-end config management pipeline for the RHEL estate | **Strong** (for RHEL/Linux; Windows config mgmt has no Ansible equivalent in the skill set) |
| On-call handoff | Context preservation across shifts; alert routing | `on-call-handoff-patterns` (wshobson) | Context preservation and alert routing during on-call transitions | **Good** |

---

### 4f. Incident Resolution & RCA

| Activity | Specific tasks | Skill | What the skill covers | Coverage |
|---|---|---|---|---|
| Incident triage | Detection; severity classification; initial response | `incident-runbook-templates` (wshobson) | Runbooks for common incident scenarios with escalation paths; detection→triage→mitigation→resolution→comms structure | **Strong** |
| Root cause analysis | Systematic investigation; hypothesis testing; evidence gathering | `administering-linux` (log/metric correlation for Linux) + `sre-engineer` (jeffallan) | administering-linux provides the Linux investigation toolset; sre-engineer provides structured chaos experiment design and RCA validation | **Good** (Linux/SRE context; VMware/Windows-specific RCA has no dedicated skill) |
| Permanent corrective actions | Postmortem writing; action item definition; recurrence prevention | `postmortem-writing` (wshobson) + `sre-engineer` (jeffallan) | wshobson: RCA documentation and action items from incidents; jeffallan: blameless postmortem requirements | **Strong** |
| Capacity planning | Performance baseline; trend analysis; growth forecasting | `monitoring-expert` (jeffallan) | CPU/memory bottleneck identification; capacity forecasting and scaling guidance | **Good** |

---

### Consolidated Platform Engineering Gap Register

| Confirmed gap | Why it matters for TTI | Mitigation |
|---|---|---|
| VMware vSphere / Hyper-V operations | TTI's primary hypervisor platform — no skill exists | **Personal ramp essential**; foundational certification (VCP) recommended |
| Windows patching / WSUS | Required for Windows Server lifecycle management across TTI's estate | **Personal ramp** + PowerShell-native scripting for now |
| Hybrid identity (Azure AD Connect / ADFS federation) | TTI runs AD + ADFS + Azure; hybrid identity is live in their stack | **Personal ramp** — ADFS federation particularly important |
| Failover Clustering / HA | HA for critical Windows workloads | **Personal ramp** if relevant to TTI's estate |
| Windows storage / SAN | Storage provisioning for Windows workloads | **Personal ramp**; Linux-side covered via Ansible |
| Enterprise backup tools (Veeam/Commvault etc.) | DR strategy requires hands-on backup platform knowledge | **Personal ramp**; runbook structure supported by skills |
| PKI / CA hierarchy design | PKI architecture beyond certificate operations | Lower priority; `windows-infra-admin` covers certificate ops |

---

## 5. Automation, IaC & DevOps (dedicated block)

### 5a. The position — Partial gap, strongest skill support
This is a *separate* JD responsibility block from Platform Engineering & Operations, and Julian's position on it is different: **Partial, fast-learnable, and - importantly - the block where his adopted skill-tier is strongest.** The vendor-official Tier-1 skills (HashiCorp Terraform, Red Hat AAP/Ansible, Pulumi) map directly here, making this the *lowest-risk, highest-trust* part of the whole plan.

What the block asks for (JD):
- Drive automation of repetitive operational tasks via scripting (PowerShell, Python, Bash) and/or configuration-management tools
- Promote IaC practices where appropriate (Ansible, Terraform) to improve consistency and repeatability
- Collaborate with application, DevOps and security teams to streamline environment provisioning, configuration and deployment workflows

Honest resume read:
- **Have:** scripting/automation exposure; applied-AI sabbatical (agentic workflows, automation); a career setting design standards, ITIL change governance, and provisioning discipline; cloud provisioning familiarity (AWS SAA, Azure).
- **The third sub-point is a strength, not a gap:** *"collaborate with app/DevOps/security to streamline provisioning"* is cross-functional influence-without-authority plus governance - exactly Julian's track record.
- **Ramp target:** hands-on authoring of production Terraform modules / Ansible playbooks at operator depth, and CI/CD pipeline tooling hands-on.

### 5b. Skill-to-Responsibility Map — Automation, IaC & DevOps (detailed)

> Skills were inspected directly before this map was written. Coverage ratings reflect what each skill actually contains.

#### Scripting Automation

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| PowerShell automation | Automate Windows admin tasks; scheduled tasks; configuration scripts | Claude Code native + `windows-infra-admin` (VoltAgent) | Claude Code generates and executes PowerShell natively with no additional skill needed; windows-infra-admin uses PowerShell as its execution layer throughout AD/DNS/DHCP/GPO automation | **Good** |
| Bash scripting | Production-grade Bash for Linux/RHEL operations; operational scripts | `bash-defensive-patterns` (wshobson) | Defensive Bash programming techniques: error handling, input validation, safe patterns for production scripts — explicitly designed for production-grade shell work | **Strong** |
| Python automation | Operational automation scripts; auto-remediation; monitoring integrations | `sre-engineer` (jeffallan) | Python auto-remediation scripts (e.g. pod restart on error threshold breach); scriptable alerting responses with PromQL integration — SRE/cloud-native context | **Good** — cloud/SRE patterns; RHEL OS-level Python automation not explicitly covered |

---

#### Ansible / Configuration Management

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| Playbook authoring | Write idempotent plays for packages, services, config, users, firewall, storage | `ansible-new-role` (leogallego) | Interactive scaffolding: asks what the role manages (packages / services / configs / users / firewall / storage) and generates realistic variable defaults, tasks, handlers, and templates; includes task componentization and smart handler generation | **Strong** |
| Code quality & CoP review | Review playbooks against best practices; enforce Red Hat standards | `ansible-good-practices` (leogallego) | Reviews against Red Hat Communities of Practice standards; ERROR/WARNING/INFO severity classification; diff-aware mode for changed files only; category filtering and parallel review | **Strong** |
| Role testing | Test-driven development for Ansible roles before production | `ansible-new-molecule` (leogallego) | Molecule scaffolding with modern molecule.yml (no legacy driver blocks); self-contained create/destroy playbooks for Docker or Podman with systemd support; enables test-driven role development | **Strong** |
| Execution environment packaging | Package collections, Python, and system dependencies for consistent deployment | `ansible-new-ee` (leogallego) | Dependency introspection: auto-detects collections, roles, Python, and system dependencies; generates requirements.yml, requirements.txt, bindep.txt; isolates execution environments for consistent deployments across infrastructure | **Strong** |
| Documentation and Q&A | Answer Ansible questions grounded in official docs | `ansible-docs` (leogallego) | Q&A mode with citations from 6 official Ansible documentation sources; requires ansible-know MCP server | **Good** |
| Live playbook execution | Run plays against TTI's RHEL estate in real time | Red Hat AAP MCP server (Tier 1) | Live playbook execution via Ansible Automation Platform; job template triggering; inventory management — requires AAP 2.6.4+ | **Strong** |
| Collection development | Build custom Ansible modules for TTI-specific automation | `ansible-new-collection` (leogallego) | Creates collections using ansible-creator; generates plugin scaffolding for modules, filters, lookup, and action plugins; CI/CD pipeline and changelog setup | **Good** |
| Design principles | Enforce simplicity and maintainability across Ansible code | `ansible-zen` (leogallego) | Enforces 20 Zen of Ansible principles; Zen Score rating (1-10); review mode evaluates code for simplicity and readability | **Good** |

---

#### Terraform / IaC

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| Module authoring | Write reusable Terraform modules for Azure, AWS, GCP | `terraform-module-library` (wshobson) | Reusable modules for AWS, Azure, and GCP infrastructure — directly aligned with TTI's Azure-primary, AWS-secondary cloud posture | **Good** |
| State & workspace management | Workspace CRUD; variable management; run execution; HCP Terraform/Enterprise | `hashicorp/terraform-mcp-server` (Tier 1 — official HashiCorp) | Workspace create/update/delete; variable and tag management; run management and execution; HCP Terraform and Terraform Enterprise integration; state interactions; private registry access | **Strong** |
| Provider & module discovery | Find providers, modules, and policies from the Terraform registry | `hashicorp/terraform-mcp-server` (Tier 1) | Provider searching and detailed lookups; module discovery and analysis; policy information retrieval; private organisation registry access | **Strong** |
| IaC secrets & safe patterns | Secrets management; OIDC dynamic credentials; drift prevention; safe resource dependencies | `pulumi-esc` + `pulumi-best-practices` (pulumi/agent-skills — Tier 1 official) | ESC: secrets and config management with OIDC, dynamic credentials, and secret store integration; best-practices: prevents apply()-callback mistakes, enforces proper resource dependencies, ensures secret encryption | **Good** — Pulumi-native; principles are fully transferable to Terraform but the implementation detail is Pulumi-specific. For TTI's Terraform stack, HashiCorp MCP is the primary execution layer. |

---

#### CI/CD & Deployment

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| CI/CD pipeline design | GitHub Actions, GitLab CI, Jenkins pipeline creation; release automation | `devops-engineer` (jeffallan) | Pipeline creation for GitHub Actions, GitLab CI, Jenkins; artifact management; release automation with approval gates; rollback procedures with verification steps | **Strong** |
| Deployment strategies | Blue-green, canary, rolling deployments; minimising risk during releases | `devops-engineer` (jeffallan) | Blue-green, canary, and rolling deployment patterns with concrete implementation examples; rollback commands and verification steps for Kubernetes | **Strong** |
| GitOps workflows | ArgoCD/Flux CD; declarative cluster state; sync automation | `gitops-workflow` (wshobson) + `devops-engineer` (jeffallan) | gitops-workflow: ArgoCD and Flux CD deployment automation; devops-engineer: GitOps implementations as part of K8s deployment management | **Strong** |
| Container build & hardening | Multi-stage Dockerfiles; health checks; image scanning in CI | `devops-engineer` (jeffallan) | Multi-stage Dockerfiles with health checks; container scanning in CI/CD pipelines; resource limits enforcement; no "latest" tags in production | **Strong** |
| Kubernetes deployments | Production K8s; Helm charts; RBAC; network policies; pod security | `devops-engineer` (jeffallan) + `k8s-security-policies` (wshobson) | devops-engineer: K8s deployments, Helm, rollbacks, readiness probes; k8s-security-policies: NetworkPolicy, PodSecurityStandards, RBAC, admission control | **Strong** |
| Environment provisioning (cross-team) | Streamline provisioning across app, DevOps, and security teams | `devops-engineer` (jeffallan) + Julian's governance/influence strength | Internal developer platform construction; self-service infrastructure tooling — Julian's cross-functional influence-without-authority track record is the differentiator here | **Strong** — this is Julian's existing strength amplified by the toolchain |
| On-premises workload provisioning | Automate bare-metal or VMware-based environment setup | **Thin skill coverage** | devops-engineer and gitops-workflow are cloud/container-native; on-prem VMware provisioning automation has no dedicated skill | **Partial** — Ansible covers configuration; provisioning automation for VMware is a gap |

---

#### Observability, SRE & Incident Response

| Activity | Specific tasks | Skill | What the skill actually covers | Coverage |
|---|---|---|---|---|
| Monitoring setup | Metric collection; Prometheus scrape config; RED/USE method dashboards | `monitoring-expert` (jeffallan) + `prometheus-configuration` (wshobson) | Prometheus client libraries (Counter/Histogram/Gauge); RED method (Rate/Errors/Duration) and USE method (Utilization/Saturation/Errors); Grafana dashboards; DataDog also mentioned | **Strong** — methodology; TTI uses New Relic (wire MCP separately) |
| Distributed tracing | OpenTelemetry instrumentation; span tracking; Jaeger integration | `monitoring-expert` (jeffallan) | OpenTelemetry instrumentation; span creation and attribute tracking; Jaeger integration | **Good** |
| Alerting | Threshold and anomaly-based alerts; multiwindow burn rate alerts | `monitoring-expert` (jeffallan) + `sre-engineer` (jeffallan) | Prometheus alerting rules; anomaly detection; multiwindow burn rate alerts for fast and slow detection | **Strong** |
| SLO/SLI definition | Quantitative reliability targets; error budget policies; burn rate escalation | `sre-engineer` (jeffallan) + `slo-implementation` (wshobson) | Quantitative SLO/SLI definition; error budget calculation from targets; burn rate detection; release freeze policies when budgets deplete; PromQL queries for golden signals | **Strong** |
| Chaos engineering | Fault injection; resilience testing; RTO/RPO validation | `sre-engineer` (jeffallan) | Chaos experiment design and execution; graceful degradation testing; RTO/RPO validation before declaring experiments complete | **Good** |
| Incident runbooks | Standard procedures for common failures; escalation paths | `incident-runbook-templates` (wshobson) | Runbooks for common incident scenarios; detection→triage→mitigation→resolution→comms structure; escalation path definition | **Strong** |
| Postmortems & RCA | Blameless postmortem writing; action item definition | `postmortem-writing` (wshobson) + `sre-engineer` (jeffallan) | wshobson: RCA documentation and action items; jeffallan: blameless postmortem requirements and chaos experiment retrospectives | **Strong** |
| On-call handoff | Context preservation; alert routing during shift transitions | `on-call-handoff-patterns` (wshobson) | Context preservation and alert routing during on-call transitions; structured handoff procedures | **Good** |
| Performance testing | Load testing; benchmarking; capacity forecasting | `monitoring-expert` (jeffallan) | k6 load testing framework; Artillery referenced; benchmarking and threshold definition; CPU/memory bottleneck identification | **Good** |

---

**Coverage verdict: confirmed as the best-supported block in the plan — and the one with the strongest validated install counts.** wshobson skills (7,400-12,600 installs each, all security-audited) cover Terraform modules, CI/CD patterns, GitOps, observability, SLO, incident runbooks, and postmortems. jeffallan skills (3,400-7,400 installs) cover DevOps pipelines, SRE, and monitoring. HashiCorp MCP is vendor-official. The only low-install skills are the leogallego Ansible suite (3-10 installs) — inspect before use. Two bounded gaps regardless:

| Automation/IaC/DevOps gap | Nature | Mitigation |
|---|---|---|
| Windows patching automation (WSUS, Windows Update scripts) | No skill — consistent with the Windows sysadmin gap in §4 | PowerShell-native; personal ramp |
| On-premises VMware provisioning automation | Skills are cloud/container-native; VMware automation (PowerCLI, Terraform vSphere provider) not covered | Terraform vSphere provider exists; personal ramp |

### 5c. Talking-Track (Automation, IaC & DevOps)
1. **Strength-first:** *"This is where my toolchain is strongest - the automation and IaC skills I'd use are all vendor-official: HashiCorp for Terraform, Red Hat for Ansible, Pulumi for IaC discipline. Highest-trust tier, lowest adoption risk."*
2. **Fast ramp, honestly bounded:** *"I already have scripting and DevOps exposure. With those vendor skills the ramp to authoring production Terraform and Ansible is weeks, not months - and I'd govern it properly: state management, secrets, drift, review gates."*
3. **The collaboration win:** *"The part about streamlining provisioning across app, DevOps and security teams is squarely my strength - I've spent a career landing design standards and change governance across teams I don't manage."*
4. **Governance framing:** *"I bring IaC under standards rather than treating it as ad-hoc scripting - which is the 'design standards and best practices' line in the JD."*

### 5d. Honest holes / ramp

Coverage gaps identified from actual skill inspection:
- **Windows patching automation (WSUS)** — no skill exists; PowerShell-native scripting only. Consistent with the Windows gap in §4.
- **On-premises VMware provisioning automation (PowerCLI, Terraform vSphere provider)** — skills are cloud/container-native; this requires personal ramp. The Terraform vSphere provider exists and would be the right tooling path.
- **Pulumi-specific implementation detail** — `pulumi-esc` and `pulumi-best-practices` encode Pulumi-native patterns. For TTI's Terraform/Ansible stack the principles transfer but the specific implementation does not; HashiCorp MCP is the primary IaC execution layer for TTI.

Reps gaps (coverage exists, hands-on depth needs building):
- **Production Terraform module authoring** — `terraform-module-library` + HashiCorp MCP provide the procedure and live tooling; needs reps to make fluent.
- **CI/CD pipeline construction** — `devops-engineer` covers GitHub Actions/GitLab CI/Jenkins; needs reps on the tooling Julian hasn't used hands-on.

---

## 6. TTI-Specific Alignment (why these skills, not generic ones)

From [[tti-technology-stack]], TTI's confirmed stack lets Julian pick skills that map to *their* environment, not a generic one:
- **New Relic** - already in TTI's stack (since 2020). A New Relic MCP is zero-adoption-friction and lets Julian speak to *their* observability tool.
- **Ansible + Terraform** - both present but "emerging" per the JD and stack research. Julian arriving with vendor-official Terraform/AAP skills positions him to *mature* exactly the capability they are standing up.
- **VMware vSphere + Windows Server + RHEL + AD/ADFS** - the core operator surface; the personal-ramp target.
- **Azure primary + dual-firewall** - the APAC Senior Network Engineer LinkedIn profile names Palo Alto + Fortinet, aligning with Julian's Telstra SASE CoE work. Note: vendor names are unverified (LinkedIn-only; the TTI Senior Network Engineer JD lists protocols but not vendor names). The security-governance angle from §2d still holds regardless of specific vendor.

---

## 7. Conversation Talking-Track ("could you do it?")

1. **Reframe:** *"The role is a technical authority for infrastructure - architecture, governance, cloud, AI, leadership. That's four of the six blocks and it's my core. The hands-on platform-ops block is where I'd ramp."*
2. **Force-multiplier, precisely:** *"I run a curated toolchain of agent skills and MCP servers - skills carry the runbook, MCP servers drive the live tools. I supply the architecture and risk judgment; the toolchain carries the operator muscle. That compresses my ramp from years to weeks."*
3. **Governance edge:** *"13% of public skills ship with critical vulnerabilities. Bringing skills into an enterprise safely - vendor-official first, security-reviewed, code-reviewed before production - is a CISSP architect's job. That's design-standards and security-partnership work, which is in the JD."*
4. **Proof:** *"Here's a lab I stood up and the ops I ran through it,"* (once the lab exists).
5. **Honesty anchor:** *"Skills multiply a fast learner who already architects these systems. They don't replace knowing the platform, so I'm also ramping the fundamentals - VMware ops, AD/PKI internals - directly."*

---

## 8. Next Actions
- [ ] Adopt Tier-1 vendor-official skills/MCP first: HashiCorp Terraform MCP, Red Hat AAP/Ansible, Pulumi agent-skills, anthropics/skills template.
- [ ] Add Tier-2: obra/superpowers (`systematic-debugging`), wshobson/agents (`incident-runbook-templates`), jeffallan (`monitoring-expert`, `sre-engineer`).
- [ ] Wire a **New Relic MCP** (TTI already owns the platform).
- [ ] Stand up a minimal home lab: Windows Server + AD + a hypervisor + a backup target; drive routine ops through the toolchain.
- [ ] Build IaC reps in the lab: author one Terraform module + one Ansible role under proper state/secrets/review governance (§5).
- [ ] Close the two honest platform-ops holes with focused personal ramp: **VMware/Hyper-V operations** and **AD/GPO/DNS/DHCP/PKI internals**.
- [ ] Rehearse both talking-tracks (§7 platform-ops, §5c automation/IaC) before the TTI conversation.

---

## Key Takeaways
- The gap is real but **narrow**: one of six JD blocks (hands-on Platform Engineering & Operations). The role's centre of gravity is Julian's existing strength.
- **Skills + MCP servers = force-multiplier, not replacement.** Skills carry the procedure, MCP carries the tools, Julian carries the judgment. Articulating this distinction *is* the credibility.
- **Use skills.sh as the primary trust signal**, not GitHub search. Install count + security audit status (Gen Agent Trust Hub / Socket / Snyk) are the two criteria. Skills under ~100 installs are unvalidated regardless of content quality.
- **The gap becomes a governance strength:** 13% of public skills have critical vulnerabilities. Curating a vetted catalogue — install counts checked, security audits passed, code-reviewed before enterprise use — is exactly the design-standards + security-partnership work the JD asks for.
- **Automation/IaC/DevOps is the strongest block** (§5): wshobson skills (7,400-12,600 installs each) and jeffallan skills (3,400-7,400) cover Terraform, CI/CD, GitOps, observability, SLO, and incident response. HashiCorp MCP is vendor-official. Highest-validated tier across the whole plan.
- **Linux/RHEL content is right but trust is low** (§4a): `administering-linux` (1 install) and leogallego Ansible (3-10 installs, Snyk fails) cover the correct surface but are unvalidated. No high-install Linux sysadmin skill exists on skills.sh. Inspect before use; treat as best available, not production-validated.
- **Windows Server: one skill, low install count** (§4b): `windows-infra-admin` (139 installs) is the only option in the ecosystem. AD/GPO/DNS/DHCP/server roles/safe-change covered. Four hard gaps: **WSUS/patching, hybrid identity, Failover Clustering, Windows storage/SAN** — no skill exists; personal ramp required.
- **VMware/Hyper-V is a confirmed ecosystem gap** (§4c): no skill found anywhere in the registry or on GitHub. The most significant personal ramp requirement.
- **obra/superpowers `systematic-debugging` is a software development skill**, not infrastructure RCA. Do not cite it in infrastructure conversations.
- Map skills to **TTI's actual stack** (New Relic MCP, Ansible AAP MCP, HashiCorp Terraform MCP, RHEL, AD) so the pitch is about *their* environment, not a generic one.

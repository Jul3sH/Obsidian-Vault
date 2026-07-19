---
type: reference
tags: [career, tti, technology, skills, platform-engineering]
created: 2026-07-19
---

# TTI — Platform Engineering Skills Bridge (Sysadmin Capability Plan)

> How Julian closes the one genuine gap in the [[TTI Principle System Administrator|Principal System Administrator]] JD - hands-on **Platform Engineering & Operations** - using a curated, governed catalogue of agent skills and MCP servers, run through OpenCode / Claude Code. Serves two jobs: (1) a real capability-building plan, and (2) talking-track for a live TTI conversation where "could you actually do this?" may come up.

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

The right posture is **trust-tiered adoption**: vendor-official first, high-reputation community second, aggregators for discovery only, large bundles with caution.

### Tier 1 — Vendor-official (highest trust, adopt first)
| Source | What it gives | Relevance to TTI |
|---|---|---|
| [anthropics/skills](https://github.com/anthropics/skills) | The official Agent Skills spec, template, and reference skills | The standard to author TTI's own skills against |
| [hashicorp/terraform-mcp-server](https://github.com/hashicorp/terraform-mcp-server) | Official Terraform docs + plan/workspace operations via MCP | TTI runs Terraform (emerging) - direct fit |
| Red Hat AAP MCP server (Ansible Automation Platform 2.6.4+) | Official Ansible playbook execution via MCP | TTI runs RHEL + Ansible - direct fit |
| pulumi/agent-skills (`pulumi-esc`, `pulumi-best-practices`) | Official IaC secrets/config + safe-pattern skills | IaC discipline patterns transferable to Terraform/Ansible |

### Tier 2 — High-reputation community (battle-tested, some in Anthropic marketplace)
| Source | What it gives | Trust signal |
|---|---|---|
| [obra/superpowers](https://github.com/obra/superpowers) | `systematic-debugging` (RCA / hypothesis testing), TDD, collaboration patterns | ~94k stars; **accepted into the Anthropic skills marketplace** |
| [wshobson/agents](https://github.com/wshobson/agents) | `incident-runbook-templates` (detect→triage→mitigate→resolve→comms), `k8s-security-policies`, `gitops-workflow` | High-star, widely referenced |
| jeffallan/claude-skills | `monitoring-expert` (structured logging, metrics, tracing, alerting), `devops-engineer` (CI/CD, multi-cloud IaC), `sre-engineer` (SLO/SLI, error budgets, golden signals) | Referenced in Pulumi's DevOps skill roundup |

### Tier 3 — Curated aggregators (discovery only; vet before use)
| Source | Scale |
|---|---|
| [VoltAgent/awesome-agent-skills](https://github.com/VoltAgent/awesome-agent-skills) | 1000+ skills from official + community teams (Anthropic, Vercel, Stripe, Cloudflare, Trail of Bits, Sentry) |
| [ComposioHQ/awesome-claude-skills](https://github.com/ComposioHQ/awesome-claude-skills) | 1000+ production-ready skills, organised by category |
| [hesreallyhim/awesome-claude-code](https://github.com/hesreallyhim/awesome-claude-code) | 36.8k-star canonical hand-curated list |
| [travisvn/awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills) | Claude Code-focused curated list |

### Tier 4 — Large bundles (use with caution; code-review each skill)
| Source | Note |
|---|---|
| [alirezarezvani/claude-skills](https://github.com/alirezarezvani/claude-skills) | 345 skills / 30+ agents / 70+ commands - broad but unvetted; treat as a parts bin |

> **Local check:** Julian's installed `~/.claude/skills/` are all career/leadgen/planning skills (project-planner, define-task, linkedin-enrichment, llm-council, etc.). **No infra/sysadmin skills are installed locally** - which is exactly why external adoption is the path. A `find-skills` run confirms the same.

---

## 4. Skill-to-Responsibility Map (Platform Engineering & Operations)

| JD sub-domain | Skill / MCP to adopt | Source tier | Coverage maturity |
|---|---|---|---|
| Windows Server / Linux (RHEL) admin | `devops-engineer`, `sre-engineer` + native PowerShell/Bash via Claude Code | T2 | Good |
| Virtualization (VMware / Hyper-V) | Emerging MCP servers only; **thin skill coverage** | — | **Gap - needs personal ramp** |
| Storage & backup / DR | `incident-runbook-templates`, DR runbook patterns | T2 | Moderate |
| Directory services / identity (AD, GPO, DNS, DHCP, PKI, ADFS) | Scripting + MCP; **thin dedicated skill coverage** | — | **Gap - needs personal ramp** |
| Monitoring, logging, config mgmt | `monitoring-expert` + **New Relic MCP** (TTI already owns New Relic) | T2 / vendor | Good |
| Incident resolution / RCA | `systematic-debugging` (obra/superpowers), `incident-runbook-templates` | T2 | Strong |
| Capacity / patching / lifecycle | Red Hat AAP / Ansible skills | T1 | Good |
| Automation / IaC (Ansible, Terraform) | `hashicorp/terraform-mcp-server`, Red Hat AAP MCP, `pulumi-best-practices` | T1 | Strong |

**The two honest holes are VMware/Hyper-V operations and AD/PKI internals** - where the skill ecosystem is thinnest and where Julian therefore needs the most personal lab time. Everything else has credible skill/MCP support today.

---

## 5. TTI-Specific Alignment (why these skills, not generic ones)

From [[tti-technology-stack]], TTI's confirmed stack lets Julian pick skills that map to *their* environment, not a generic one:
- **New Relic** - already in TTI's stack (since 2020). A New Relic MCP is zero-adoption-friction and lets Julian speak to *their* observability tool.
- **Ansible + Terraform** - both present but "emerging" per the JD and stack research. Julian arriving with vendor-official Terraform/AAP skills positions him to *mature* exactly the capability they are standing up.
- **VMware vSphere + Windows Server + RHEL + AD/ADFS** - the core operator surface; the personal-ramp target.
- **Azure primary + dual-firewall (Palo Alto + Fortinet)** - already Julian's strength (Telstra SASE CoE), reinforcing the security-governance angle in §2d.

---

## 6. Conversation Talking-Track ("could you do it?")

1. **Reframe:** *"The role is a technical authority for infrastructure - architecture, governance, cloud, AI, leadership. That's four of the six blocks and it's my core. The hands-on platform-ops block is where I'd ramp."*
2. **Force-multiplier, precisely:** *"I run a curated toolchain of agent skills and MCP servers - skills carry the runbook, MCP servers drive the live tools. I supply the architecture and risk judgment; the toolchain carries the operator muscle. That compresses my ramp from years to weeks."*
3. **Governance edge:** *"13% of public skills ship with critical vulnerabilities. Bringing skills into an enterprise safely - vendor-official first, security-reviewed, code-reviewed before production - is a CISSP architect's job. That's design-standards and security-partnership work, which is in the JD."*
4. **Proof:** *"Here's a lab I stood up and the ops I ran through it,"* (once the lab exists).
5. **Honesty anchor:** *"Skills multiply a fast learner who already architects these systems. They don't replace knowing the platform, so I'm also ramping the fundamentals - VMware ops, AD/PKI internals - directly."*

---

## 7. Next Actions
- [ ] Adopt Tier-1 vendor-official skills/MCP first: HashiCorp Terraform MCP, Red Hat AAP/Ansible, Pulumi agent-skills, anthropics/skills template.
- [ ] Add Tier-2: obra/superpowers (`systematic-debugging`), wshobson/agents (`incident-runbook-templates`), jeffallan (`monitoring-expert`, `sre-engineer`).
- [ ] Wire a **New Relic MCP** (TTI already owns the platform).
- [ ] Stand up a minimal home lab: Windows Server + AD + a hypervisor + a backup target; drive routine ops through the toolchain.
- [ ] Close the two honest holes with focused personal ramp: **VMware/Hyper-V operations** and **AD/GPO/DNS/DHCP/PKI internals**.
- [ ] Rehearse the §6 talking-track before the TTI conversation.

---

## Key Takeaways
- The gap is real but **narrow**: one of six JD blocks (hands-on Platform Engineering & Operations). The role's centre of gravity is Julian's existing strength.
- **Skills + MCP servers = force-multiplier, not replacement.** Skills carry the procedure, MCP carries the tools, Julian carries the judgment. Articulating this distinction *is* the credibility.
- **Adopt by trust tier:** vendor-official (HashiCorp, Red Hat, Pulumi, Anthropic) first, high-reputation community (obra/superpowers, wshobson) second, aggregators for discovery, bundles with caution.
- **The gap becomes a governance strength:** curating and vetting a safe enterprise skill catalogue is exactly the design-standards + security-partnership work the JD asks for.
- **Two honest holes** (VMware ops, AD/PKI internals) have thin skill coverage and need personal lab time. Don't over-claim; ramp them directly.
- Map skills to **TTI's actual stack** (New Relic, Ansible, Terraform, VMware, RHEL, AD) so the pitch is about *their* environment, not a generic one.

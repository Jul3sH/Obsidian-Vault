---
type: reference
created: 2026-10-07
tags: [technical, claude, anthropic, sdlc, claude-code]
source: "The AI-Native SDLC Playbook (Anthropic Applied AI, Louis Claxton; PDF, 54 pp). Blog: https://claude.com/blog/the-ai-native-sdlc-playbook. Course: https://academy.claude.com/courses/ai-native-sdlc-playbook"
---

# The AI-Native SDLC Playbook

## Purpose

A working summary of Anthropic's *AI-Native SDLC Playbook*: how to rebuild the six stages of software delivery around Claude Code, play by play. It exists so an application build can be run against the playbook without rereading the 54-page PDF.

**Sections:** Key Takeaways · The core idea · The artifact chain · Adoption order · Stage 1 Plan · Stage 2 Design · Stage 3 Build · Stage 4 Test · Stage 5 Deploy · Stage 6 Maintain · Mapping to this vault · Source links

---

## Key Takeaways

- **Code is no longer the bottleneck.** Build collapses to hours; plan, review/test and deploy still run at human speed. Rebuild those, not just the coding step.
- **Every stage ends by committing an artifact the next stage reads:** `intent.md` → `spec.md` → `plan.md` → diff + tests → PR + review findings → incident record → new `intent.md`. The commit chain *is* the audit trail.
- **Nothing is built without an accepted plan.** Plan mode first; the approved plan is committed as `plan.md` and the PR review checks the diff against it.
- **Skills are advisory, hooks are deterministic.** "The skill makes violations rare and the hook makes them close to impossible." Any rule that must always hold needs a hook behind it.
- **Always give Claude a feedback loop** (one-command test/build/screenshot) and protect it: the agent fixing code must not be able to edit the tests.
- **The agent may act up to the production gate and cannot pass it.** Humans approve through branch protection and approval hooks.
- **Start by prompting each stage by hand.** Automate the handoffs (accepted artifact fires the next stage) only once each stage works manually.
- **Five entry-point plays need nothing first:** Capture intent, CLAUDE.md, Plan mode, Feedback loop, Hooks.

---

## The core idea

| Stage | Traditional | AI-native |
|---|---|---|
| Plan | Requirements by committee, workshops, sign-offs | Originator brainstorms with Claude; result captured as `intent.md` |
| Design | Analysts write spec, designers parse it | Requirements + design in one agent session, constrained by org skills |
| Build | Hand-written code and tests; docs after | AI-generated code and tests; knowledge in versioned `CLAUDE.md` and skills |
| Test | QA gates at stage boundaries | Continuous evals woven through implementation |
| Deploy | Humans review every line | Layered agentic review; humans for regulated/critical code; hooks as gates |
| Maintain | Humans watch production | Agents monitor; a breached control band becomes a new `intent.md` |

Humans stay "above the loop": instigating, directing, governing. Human attention concentrates at the gates, reviewing what the agent flagged rather than starting each stage from scratch.

## The artifact chain (what triggers what)

| Artifact | Committed at end of | Its acceptance triggers |
|---|---|---|
| `intent.md` | Plan | Requirements and design pass |
| `spec.md` | Design | Plan mode |
| `plan.md` | Build (before code) | Implementation |
| Diff + tests | Build / Test | PR |
| PR + review findings | Deploy | CI/CD pipeline |
| Incident record / breach | Maintain | Next `intent.md` |

**Legacy systems sidebar.** For every artifact, name **one** source of truth: (a) the repo is authoritative and Jira etc. reference commits; (b) the legacy tool is authoritative and markdown files are working copies, written back via MCP in the same session; or (c) as a minimum, *linkage*: every artifact carries the record ID and every record carries the commit SHA.

## Adoption order (dependency graph)

Columns are stages; arrows are adoption order, which is not the same thing.

| Play | Stage | Adopt after |
|---|---|---|
| **Capture intent** | Plan | Entry point |
| Requirements & design | Design | Capture intent, Skills (Plan mode is helped by it, not dependent) |
| **CLAUDE.md** | Build | Entry point |
| Skills | Build | CLAUDE.md |
| Subagents | Build | CLAUDE.md (Feedback loop helps) |
| **Plan mode** | Build | Entry point (CLAUDE.md and spec help) |
| **Feedback loop** | Test | Entry point |
| Evals | Test | CLAUDE.md, Feedback loop |
| PR review | Deploy | CLAUDE.md (Skills help) |
| **Hooks** | Deploy | Entry point |
| CI/CD | Deploy | PR review, Hooks |
| Closing the loop | Maintain | Capture intent, PR review, CI/CD, Hooks |

Every play is written in the same five parts: what changes, getting started (prerequisites, infrastructure), steps, governance, how to measure (leading and lagging indicator).

---

## Stage 1: Plan

### Capture as intent.md
Intent enters from an idea, a ticket, or an incident alert. The originator brainstorms with Claude and the result is a proto-spec in **the originator's own words**.

- **Infrastructure:** an agreed `intent.md` template (ideally a skill); a version-controlled home the product owner watches. Simplest: an `intent/` folder in the product repo.
- **Steps:** (1) describe the problem in plain words: what you can't do, who's affected, what better looks like, what's out of scope; (2) brainstorm until concrete, with Claude asking analyst questions (scope, users, constraints, success); (3) Claude writes `intent.md` from the template; (4) originator corrects it; (5) commit. Product owner picks it up.
- **Governance:** the product owner reviews and corrects before commit; accept/reject is recorded as the merge or closed review.
- **Measure:** time from first conversation to committed `intent.md` (weeks to hours); survival rate into Design; edits to `intent.md` after the first `spec.md`.

```markdown
# Intent: claims status self-service
Author: J. Ortiz (claims operations). Status: draft.

## Problem
Customers phone the contact center to ask where their claim is.
Handlers spend roughly a third of call time on status-only queries.

## Proposed outcome
Customers see claim status, next step and expected date in the portal.

## Affected users and systems
Claims handlers, portal team, claims-core API.

## Constraints
No new PII in the portal session. Existing authentication only.

## Open questions
Do third-party loss adjusters need access too?
```

## Stage 2: Design

### Requirements and design
Claude turns the accepted `intent.md` into one requirements-and-design spec, constrained by the organisation's skills (brand, security, compliance, UX), with **areas of concern flagged**. The product owner reviews it but does not write it. Front-end variant: mock up in Claude Design from `intent.md`, iterate, export to Claude Code.

- **Prerequisites:** `intent.md`; policies written as skills.
- **Steps:** (1) open a session with skills loaded, attach `intent.md`; (2) prompt (below). Run by hand first, then as a slash command, then as a non-interactive job fired by the `intent.md` merge that opens `spec.md` as a PR; (3) review: does it solve the stated problem, are open questions answered or carried forward?; (4) resolve flagged concerns with each policy owner first; (5) commit `spec.md` beside `intent.md`; (6) a human decides whether it goes to build (tech lead for higher risk).
- **Governance:** policy is applied while the spec is written, not found in review weeks later. Spec, prompt and skill versions are all versioned.
- **Measure:** time from `intent.md` commit to `spec.md` commit; `spec.md` commits after the first `plan.md` (requirements rework).

```text
Read the attached intent.md and produce a requirements and design spec for
integrating it into our existing codebase. Apply the skills available to you
so the plan conforms to our brand guidelines, security policies and UX
standards. Document the spec fully as spec.md, ready to hand to the
engineering team. Describe clearly any areas of concern, especially where you
cannot satisfy contradicting policies.
```

## Stage 3: Build

### Plan mode as the default starting point
- **Steps:** (1) start in plan mode; (2) give Claude `intent.md` + `spec.md`, ask for a plan naming files that change, order of work, and the tests that prove it; (3) interrogate: what could break, riskiest step, options rejected; (4) iterate until a stranger could implement from the plan alone; (5) commit as `plan.md`; (6) accept and let Claude implement (often one pass); (7) if implementation departs from the plan, update `plan.md` in the same commit (a hook can enforce this).
- **Governance:** design review happens before code, while changing course is still a document edit. Plan mode itself prevents edits until accepted.
- **Measure:** share of changes merging from the first pass; rework cycles; how often the merged diff still matches `plan.md`.

```markdown
# Plan: claims status self-service (from intent.md 2026-06-02)
## Files that change
portal/src/claims/StatusPanel.tsx (new), claims-api/routes/status.py,
claims-api/tests/test_status.py
## Order of work
1. Add the status endpoint behind existing auth.
2. Panel against the endpoint.
3. Wire into the portal nav.
## Risks
The claims-core API rate-limits at 50 rps; the panel must cache.
## Proof
test_status.py covers the four claim states; screenshot matches the
approved mock.
```

**Auto mode.** Once guardrails mature (tuned CLAUDE.md, policy skills, blocking hooks, a runnable test suite), auto-accept becomes the default for routine work: tight spec, small blast radius, code already covered by tests. Review shifts from watching edits to reviewing artifacts after longer autonomous runs.

### CLAUDE.md
- **Steps:** run `/init`; cut to what a new joiner needs on day one (build/test/lint commands, conventions, things Claude gets wrong); commit at repo root; **when Claude makes the same mistake twice, the correction goes into CLAUDE.md**; keep it under a page.
- **Measure:** repeated mistakes CLAUDE.md should have caught; time to first merged PR for a new joiner.

```markdown
# Payments service
## Commands
- Build: make build
- Test: make test (unit), make itest (integration, needs docker)
- Lint: make lint (runs in CI; fix before pushing)
## Conventions
- Java 21, Spring Boot 3. No new Lombok.
- Money is always BigDecimal, never double.
- Every endpoint needs an integration test in src/itest.
## Architecture
- api/ holds REST controllers, core/ holds domain logic,
  adapters/ talks to external systems.
- Kafka events are defined in schemas/; never edit generated classes.
## Things Claude gets wrong
- Do not bump dependency versions; the platform team owns them.
- The legacy v1/ package is frozen; changes go in v2/.
```

### Skills as institutional knowledge
Write a skill for knowledge that must be applied consistently; not for things that belong in CLAUDE.md or a prompt.
- **Steps:** pick one inconsistently enforced rule; write `SKILL.md` (frontmatter = when it triggers, body = what to do) from the policy owner's source; store in `.claude/skills/<name>/` or distribute via plugin; **test that it triggers** by asking for the task several ways; policy owner signs off changes.
- **Governance:** a skill is an *advisory* control. A must-hold policy needs a hook or PR review pass behind it.
- **Measure:** time from policy change to skill merge; PR findings citing the policy should fall towards zero (if not, the skill isn't triggering or has drifted).

```markdown
---
name: secure-api-review
description: Apply the API security standard. Use whenever creating or
  modifying an external-facing endpoint, reviewing API code, or
  generating an OpenAPI spec.
---
# Secure API review

When you create or change an API endpoint:
1. Authentication: every endpoint requires the gateway JWT;
   no anonymous routes outside /health.
2. Input validation: validate request bodies against the OpenAPI
   schema and reject unknown fields.
3. Audit: every state-changing endpoint emits an audit event with
   actor, action, entity and timestamp.
4. Data classification: fields tagged pii in the schema must never
   appear in logs or error messages.

Run scripts/check-endpoints.sh and include its output in your summary.
```

### Hooks as build-time guardrails
Block edits to protected paths; run formatter/linter after edits; keep credentials out of the diff. Keep them fast and scoped to the changed file; heavy checks (full test suite) belong at commit or PR. Approval-asking hooks belong in Deploy, not Build, or a human lands back on the critical path of every parallel session.

### Parallel sessions and subagents
A **parallel session** is a full Claude Code instance in its own git worktree (`claude --worktree feature-auth`); sessions know nothing of each other. A **subagent** is a scoped helper inside one session with its own context and tool limits, for recurring jobs.
- **Steps:** split work by files touched (shared-file tasks run sequentially in one session); one worktree per task; start with 2-3 sessions and add only while review keeps up; define repeated jobs in `.claude/agents/` (simplifier, verifier, researcher) and commit them.
- **Measure:** concurrent sessions per engineer while review quality holds; changes merged per week alongside rework rate.

```markdown
---
name: verifier
description: Runs the app and checks the change works before the session
  reports done
tools: Bash, Read
---
Start the app with make run. Exercise the changed behavior and the two
nearest neighboring flows. Report what you ran, what you saw, and any
behavior that does not match plan.md. Do not fix anything; report only.
```

## Stage 4: Test

### Give Claude a feedback loop
Distinct from the verifier subagent: the loop runs throughout the task; the verifier is a final fresh-context check so the verdict isn't coloured by the assumptions that produced the code.
- **Infrastructure:** test suite and build runnable with one command each; for UI, a browser or screenshot tool via MCP.
- **Steps:** (1) wrap checks in one target (`make test`, `npm test`) that exits non-zero on failure; (2) list commands with healthy output in CLAUDE.md; (3) state a quantifiable target ("all tests in test_status.py pass"); (4) **bug fixes: failing test first**, confirm it fails for the expected reason, commit it, then fix without editing it; (5) UI: implement, screenshot, compare to mock, adjust (2-3 rounds normal); (6) verification is part of "done": run tests and paste output; (7) **protect the loop**: hook blocking test-file edits during a fix, or reject test-touching diffs in review.
- **Measure:** first-pass CI success rate; review time per PR; change failure rate.

```markdown
## Verifying your work

- Build: make build (must finish with "Build succeeded")
- Test: make test (all green; never skip or delete a failing test)
- Lint: make lint (zero warnings)

Run all three before reporting any task complete, and paste the output.
If a test fails, fix the code, not the test.
```

### Continuous evals in CI
Evals regression-test the agent's *configuration* (CLAUDE.md, skills, hooks, model swaps). Treat as a live suite: retire cases that stop discriminating, add new ones from monitoring.
- **Steps:** collect 20-50 real recent tasks with accepted outcomes; write each as prompt + checks; run non-interactively in CI on a schedule and on any config change; gate config changes on pass rate; **every production incident becomes an eval**.
- **Measure:** pass rate over time; incident-to-eval time; regressions caught in CI vs production.

```yaml
name: Agent evals
on:
  pull_request:
    paths: ['CLAUDE.md', '.claude/**']
  schedule:
    - cron: '0 2 * * *'
jobs:
  evals:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install -g @anthropic-ai/claude-code
      - name: Run eval suite
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          for eval in evals/*.json; do
            claude -p "$(jq -r '.prompt' $eval)" \
              --allowedTools "Read,Edit,Bash(make test)" \
              --output-format json > result.json
            ./evals/check.sh "$eval" result.json
          done
```

## Stage 5: Deploy

### AI in the PR review loop
Claude reviews incoming PRs and addresses comments on its own. Humans judge intent and risk.
- **Infrastructure:** managed Code Review (research preview) or `claude-code-action` in your CI; branch protection requiring code-owner approval.
- **Steps:** enable review; tech lead writes `REVIEW.md` (passes, what counts as Important vs Nit, what to skip); findings never approve or block alone; `@claude` on a comment makes Claude fix and push; for Claude's own PRs, a slash command "babysits" until green and waiting only on code-owner approval; **a mistake flagged twice goes into CLAUDE.md**; monthly tuning of findings and nit cap.
- **Governance:** separation of duties: the agent that wrote the code cannot approve it.
- **Measure:** time to first review (minutes); comments resolved without a human touching the branch; defects caught pre-merge vs escaped.

```markdown
# Review instructions

## Passes
Run three passes and tag each finding with its pass:
- Bugs: logic errors, broken edge cases, subtle regressions
- Security: injection risks, authentication gaps, PII in logs
- Compliance: the change matches spec.md, plan.md and our design principles

## What Important means here
Reserve Important for findings that would break behavior, leak data
or breach a policy. Style and naming are nits.

## Cap the nits
Report at most five nits per review; summarize the rest as a count.

## Do not report
Generated files under src/gen/ and anything CI already enforces.
```

### Hooks as approval gates
A hook can allow, **ask**, or block. Leadership lists the human gates that must survive (change sign-off, release authorisation, protected paths); each becomes a hook; team hooks go in `.claude/settings.json`, non-negotiable ones in managed settings; a block must explain itself and the route to approval.

```json
{
  "hooks": {
    "PreToolUse": [
      {
        "matcher": "Bash",
        "hooks": [
          { "type": "command",
            "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/production-gate.sh" }
        ]
      }
    ]
  }
}
```

```bash
#!/bin/bash
# Production deploys require a named release authorization
cmd=$(jq -r '.tool_input.command' < /dev/stdin)
if [[ "$cmd" == *"deploy"* && "$cmd" == *"production"* ]]; then
  if [ -z "$RELEASE_APPROVAL" ]; then
    echo "Production deploys need a release authorization." >&2
    exit 2   # exit 2 blocks the action; the message goes to Claude
  fi
fi
exit 0
```

**Managed settings (regulated enterprise worked example).** Deny reads of `.env*`/secrets and network tools; allow the safe inner loop (`git`, `make build/test/lint`); disable bypass mode; managed rules/hooks/MCP only; OS-level sandbox with a domain allowlist and credential-file denial; approved plugin marketplace only; minimum version floor. The playbook stresses this is a starting point to tailor, not copy. Full key reference: code.claude.com/docs/en/settings.

- **Measure:** wait time per gate (from the OpenTelemetry export); gate violations reaching production before vs after.

### CI/CD integration and deployment
- **Prerequisites:** PR review and approval-gate hooks must exist first, "because the gates must exist before automation accelerates anything through them."
- **Steps:** (1) start read-only: `claude -p` to triage failed builds, summarise flaky tests, draft changelogs; (2) add write steps behind existing gates, always arriving as a PR, no route to main; (3) sandbox jobs in containers with short-lived scoped tokens, no standing prod credentials; (4) expose deploy/status/rollback as MCP tools scoped per environment; (5) tier autonomy: dev deploys freely, prod is prepared by the agent and authorised by a release manager; (6) **rollback is the most rehearsed path**, one command exercised in staging.
- **Measure:** pipeline failures triaged without paging a human; DORA metrics.

```yaml
- name: Triage failed build
  if: failure()
  run: >
    claude -p "Read the build log at out/build.log. Identify the most
    likely cause, say whether the failure looks flaky or real, and write a
    three-line summary for the PR thread." >> triage.md
```

## Stage 6: Maintain

### Closing the loop
A trigger (control-band breach, ticket, channel message, schedule) invokes Claude with no person in the path. Between headless stages sits an independent confidence gate (deterministic check or adversarial reviewing agent) that continues or escalates to a human.
- **Steps:** (1) pick one metric with a stable rolling baseline (CI failure rate, post-deploy 5xx, PR cycle time); (2) write a **deterministic, unit-tested** detection script (rolling mean/SD, Western Electric rules), no model involved; (3) tiers in `bands.yaml`: 1σ log, 2σ read-only diagnosis, 3σ act only via a PR or pre-approved runbook; (4) trigger via scheduled workflow, webhook or cron; Claude runs stateless (`claude -p` or Agent SDK); (5) agent writes its diagnosis as `intent.md`; (6) owner triages: fix, schedule or dismiss (dismissals tune the bands); (7) when a fix ships, add an eval.
- **Measure:** breach to `intent.md` in queue; share of findings becoming merged fixes; repeat incidents of the same class.

```yaml
metric: ci_test_failure_rate
baseline: rolling_30d
rules: western_electric
tiers:
  1sigma: { action: log }
  2sigma: { action: diagnose,
            tools: "Read,Grep,Bash(gh run view *)" }
  3sigma: { action: propose,
            routes: [pull_request, runbook:rollback-deploy] }
```

### Claude on call with Claude Tag
Claude Tag (public beta, Slack) makes Claude a channel member under its own identity: first responder to incidents, human authorises actions in-thread, post-mortem written to a versioned lessons file. Small bounded fixes arrive as PRs; larger work becomes `intent.md`. The channel is the audit trail.

---

## Mapping to this vault

Nearest existing equivalent for each playbook concept, so a build can reuse rather than duplicate. These are analogies, not identities.

| Playbook | Nearest equivalent here |
|---|---|
| `intent.md` in the originator's own words | The `## Prompt Zero` section of a deliverable ([[ai-os/skills/prompt-zero/SKILL\|prompt-zero]]) |
| `spec.md` before build | [[spec-driven-development]] |
| Skill (advisory) vs hook (deterministic) | [[mm-steering]], [[mm-rule-layering]], [[claude-code-skills]], [[claude-code-hooks]] |
| Verifier subagent, fresh-context check | [[mm-verification]], [[claude-code-subagents]] |
| Continuous evals | [[evals]] |
| CLAUDE.md, "mistake twice goes in" | [[claude-md-and-memory]] |
| Legacy source-of-truth sidebar | Wiki-wins rule in the Jira sync skills (repo as source of truth) |
| Agent acts up to the gate, not past it | [[mm-blast-radius]] |

## Source links

- Blog: https://claude.com/blog/the-ai-native-sdlc-playbook
- Free course (14 lessons): https://academy.claude.com/courses/ai-native-sdlc-playbook
- Docs the playbook lists for platform setup, in rollout order: admin-setup, settings, server-managed-settings, permissions, sandboxing, hooks-guide, hooks, skills, plugin-marketplaces, managed-mcp, third-party-integrations, network-config, monitoring-usage, analytics, security (all under code.claude.com/docs/en/), plus the Compliance API (platform.claude.com/docs/en/manage-claude/compliance-api).

## Document Log

| Date | Change |
|---|---|
| 2026-10-07 | Created from the PDF Julian supplied in session (54 pp, read in full). |

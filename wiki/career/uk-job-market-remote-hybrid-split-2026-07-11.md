---
type: reference
tags: [career, uk-relocation, job-market, remote, geography]
created: 2026-07-11
source: Adzuna GB Jobs API (live pull, 2026-07-11)
method: 80 count-queries across 6 role families x 8 geographic zones; 376 unique real-salary listings sampled; work-pattern and seniority inferred from listing text (directional)
confidence: counts high; salary bands medium; work-pattern/remote share low-to-medium (see Caveats)
supports-decision: uk-relocation-decision (London-direct vs Malvern-first sub-decision)
demand-addendum: 2026-07-14 (Q4 = time-to-fill proxy + salary momentum; supply-side only until LinkedIn applicant data lands)
---

# UK Job Market: Remote / Hybrid / On-site Split, Two-Base Pool Test (11 Jul 2026)

> **Purpose.** Deciding input for the HK to UK relocation sub-decision: **can Julian run his search from Malvern (Worcestershire) as well as from Wimbledon (SW London), and is a well-paid REMOTE senior role in his niche real or a mirage?** Live UK job-board counts and salaries from the [[target-role-profile|Target-Role Profile]] taxonomy, pulled from Adzuna on 11 Jul 2026. Feeds and corroborates the [[uk-150k-feasibility-report|£150k Feasibility Report]].
>
> **Companion spreadsheet:** [[uk-job-market-remote-hybrid-split-2026-07-11.xlsx]] - the same results as sortable/filterable tables (two-pool decision view, pool matrix, salary x work-pattern, well-paid skew, and all 376 raw listings). See **Data source and coverage** below for exactly where the listings come from.
>
> **⚠ UPDATE (11 Jul, supersedes the decision-framing below): the crash-pad interim changes the conclusion.** Julian's actual plan is not "live in Malvern" but a **crash-pad interim** - live in Malvern (Mum covers Sophia), take a London **hybrid** job, crash-pad Tue-Thu, then move to London full-time at the education-year boundary. Because hybrid (~2-3 days) is crash-pad-commutable, a Malvern base reaches far more than the ~15% resident-commute ratio in Q2. *Nuance (Fable red-team, [[fable-review-jobdata-2026-07-11]] §10.5):* ~40% of London roles mention hybrid, but only **~25% are genuinely crash-pad-compatible** once fixed-anchor-day and client-site roles are stripped (Julian's best-fit SI-presales lane is customer-facing, so this bites) - use **~25% as the planning figure**, still well above 15%. So the two-pool comparison is the wrong lens for the interim, and the "leans London-direct" decision-lean is **superseded**: the job axis no longer separates the options; the decision turns on money-risk (favours the interim) vs Sophia/Mum stability (favours London-direct). The Q1-Q3 findings below stand as **data**; their decision-framing is updated by [[fable-review-jobdata-2026-07-11|Fable's re-review]] (see also [[uk-move-financial-model]] §9a). *New numbers here (London hybrid split, crash-pad costs, time-to-fill proxy) are directional, pending independent verification.*

---

## Bottom line

Three findings, in the order they matter:

1. **A well-paid PERMANENT remote role in his niche is largely a mirage.** Remote-explicit postings are a tiny share of the national pool (roughly 1-3% per family). Remote *permanent* roles are the **lowest-paid** work-pattern (median base ~£70k vs ~£90k hybrid). The well-paid remote money that exists is almost entirely **contract day-rate** (which fails the net-of-benefits test) and skews to **globally-contested, offshore/AI-exposed product-config lanes** (AWS, Databricks, SAP, D365, ServiceNow, Salesforce, Zscaler config). The one structurally UK-protected remote lane is **SC/DV-cleared** defence/security, and that is clearance-gated and mostly contract.

2. **The Malvern commute pool is real but roughly one-seventh of the London pool** (~15% across families; best relative lane is Network at ~20%, but on tiny absolute numbers) - *for a Malvern **resident** commuting locally.* The well-paid *permanent* packages that meet his economic bar cluster in **London hybrid / on-site**: the **on-site-only** subset (~1/3 of London) is not reachable from Malvern, but the **hybrid** subset (~40%+) IS, via a crash-pad (see the update banner above). So this ~15% is the wrong denominator for the crash-pad interim.

3. **The "£150k+" band is 85% contract** (68 of 80 sampled high-salary roles). Permanent £120k+ architect roles are rare (~3% of the sample) and skew hard to London. This independently confirms the feasibility report: **£150k perm is top-decile, not the base case; the realistic perm band is ~£75-95k median, £85-130k reach.**

**Decision lean: the data points London-direct** for the stated goal (high-paid *permanent* role + medical/life benefits + team leadership). Malvern-first is only viable if Julian pivots into the **cleared defence-cyber** lane, but a dedicated assessment ([[cleared-defence-cyber-lane-assessment]]) shows this hedge is **weaker than it first looked**: he is **not near-term clearable** (SC needs ~5yr UK residency, DV ~10yr; he has ~13yr overseas in Hong Kong), the premium DV *contracts* actually cluster at **Basingstoke/Milton Keynes (London-commutable)**, and the Malvern/Cheltenham cluster is the **lower-paid permanent** end. So even the cleared pivot leans London/West-Corridor, not Malvern, and is a multi-year build via a permanent clearance-sponsored role rather than a landing spot on arrival.

> **Superseded (11 Jul):** this "leans London-direct" framing is overtaken by the crash-pad reframe in the update banner near the top. The job axis no longer decides between London-direct and the Malvern crash-pad interim; the decision turns on money-risk vs Sophia/Mum stability. See [[fable-review-jobdata-2026-07-11]]. The data below stands; only the decision-lean is updated.

---

## Q1 (THE HINGE) - Is well-paid remote real, or a mirage?

**Verdict: mirage for the goal as stated (well-paid PERMANENT + benefits). Real only as contract, or in clearance-gated defence.**

### (a) Remote is a small slice of the market
National count vs remote-keyword count per family (Adzuna keyword method under-counts remote, so read as a floor, but the gap is large):

| Family                     | UK-total count | Remote-explicit | Remote share |
| -------------------------- | -------------: | --------------: | -----------: |
| Solution Architect         |          3,103 |              54 |        ~1.7% |
| Network / Network-Security |            211 |               7 |        ~3.3% |
| Security / Cyber           |            895 |               6 |        ~0.7% |
| Cloud                      |            666 |               5 |        ~0.8% |
| Enterprise Architect       |            693 |              10 |        ~1.4% |

Even allowing a 3-5x undercount, remote-first is a minority of postings; hybrid dominates the modern architect market.

### (b) Remote is LOWER-paid and MORE JUNIOR
Permanent-only median base salary by inferred work-pattern (real, non-predicted salaries):

| Work pattern | Perm median base | Note |
|--------------|-----------------:|------|
| **Remote (perm)** | **£70,000** | n=27; lowest band |
| Hybrid (perm) | £90,000 | n=46; the paid middle |
| On-site (perm) | £70,000 | n=7 (small); high on-site money is contract, not perm |

Seniority mix (sampled): remote listings skew **mid, not senior/principal** (~76% mid, ~22% senior-titled). The senior/principal architect money is not sitting in the remote bucket.

### (c) The well-paid remote roles that DO exist are contract and/or contested
Of remote roles at £110k+ (annualised), nearly all are **contract day-rates**, and the stack tells the story: *AI Architect, AWS Solution Architect, Databricks, SAP Integration, D365/Power Platform, ServiceNow, Salesforce, Zscaler/Zero-Trust config*. These are exactly the **offshorable / globally-contested / AI-exposed** lanes (work-from-anywhere, EMEA-wide, younger global candidates). Adzuna annualises contract day-rates, so a "£156-182k remote" headline is a ~£600-700/day contract, not a package with benefits.

### (d) What is structurally protected
The UK-protected remote markers that appear: **SC / DV / "SC Cleared" / "eDV Cleared"** security and enterprise-architect roles. Clearance is a genuine moat (non-UK, non-resident candidates cannot hold it). But in this sample those are **contract**, and Julian is **clearable long-term via a permanent-sponsored path, not near-term for premium DV contract work** (SC needs ~5yr UK residency, DV ~10yr; he has ~13yr overseas). Clearance prevalence was ~20-24% across *all* zones, so it is a lane, not a Malvern-exclusive feature. Full analysis: [[cleared-defence-cyber-lane-assessment]].

**Which of his lanes are protected vs exposed:**

| Lane | Remote exposure | Verdict |
|------|-----------------|---------|
| Network / Network-Security (SASE/ZTA) | Scarce remote volume, but the scarcity itself is the moat; SI-presales is customer-facing (not pure-remote) | **Protected by scarcity, but low remote volume** |
| Security / Cyber, esp. **SC/DV-cleared** | Cleared roles cannot offshore | **Structurally protected** (but contract, clearance-gated) |
| Solution Architect (generic) | High remote contest, product-config offshorable | **Exposed** |
| Cloud (AWS/Azure config) | Global-remote, AI + offshore exposed | **Most exposed** |
| Enterprise Architect | Some remote, but perm skews London hybrid | Mixed |

---

## Q2 - Two-base pool comparison

**London base** = Remote + London + West-Corridor (Reading etc.), hybrid/on-site commutable from Wimbledon.
**Malvern base** = Remote + Cheltenham + Worcester + Birmingham + Bristol clusters.

| Family | London-base pool | Malvern-base pool | Malvern / London |
|--------|-----------------:|------------------:|-----------------:|
| Solution Architect | 1,475 | 230 | 16% |
| **Network / Network-Security** | 93 | 19 | **20% (best)** |
| Security / Cyber | 440 | 66 | 15% |
| Cloud | 313 | 53 | 17% |
| Enterprise Architect | 340 | 44 | 13% |
| BFSI security (financial services) | 1 | 0 | ~0% (thin everywhere) |
| **TOTAL** | **2,662** | **412** | **~15%** |

**Read:** the Malvern-commutable pool is roughly **one-seventh** the London pool. The defence/GCHQ cluster does show in Security (Cheltenham 8 + Birmingham 21 + Bristol 28 = 66) and Network is Malvern's *relatively* strongest lane (20%), consistent with the Cheltenham/QinetiQ/DSTL thesis, but the **absolute** numbers are small (19 network roles). Remote, the supposed equaliser, is small in absolute terms for both bases (~80 across families), so it does not rescue Malvern. BFSI-titled security roles are near-zero on the board in both bases; BFSI depth reads as sector experience inside broader roles, not a searchable title (matches the [[target-role-profile]] load-bearing assumption).

> **Crash-pad caveat (11 Jul):** this two-pool ratio measures the Malvern-**resident** commute pool. It is the **wrong denominator** for Julian's actual plan (a crash-pad interim). A crash-padder taking London **hybrid** roles (Tue-Thu) reaches Malvern-local + **all London hybrid** + **all remote** - roughly **2/3 of the London pool**, not ~15%. Only London **on-site-only** roles (~1/3) are genuinely lost. Do not cite the ~15% as the interim's constraint. See [[fable-review-jobdata-2026-07-11]] §9.1.

---

## Q2a - Solution Architect, broken down by domain (how applicable is it to Julian?)

"Solution Architect" is the largest and most generic family, so a raw count overstates relevance: many SA roles are **application-specific** (Salesforce, Workday, SAP, ServiceNow, Dynamics/D365, Oracle) and are **not Julian's profile**. His applicable SA roles are those anchored in **network, cloud, cyber-security, infrastructure**, with **GenAI as a differentiator**. This section filters the SA family to his lanes.

> **Method note.** This cut uses **exact-phrase** matching for "solution architect" (base = **2,096** national), a tighter, cleaner denominator than the headline report's word-match (3,103, which also catches "solution delivery architect" etc.). "Solution" and "solutions" phrase-match identically (Adzuna normalises the plural). Domain counts **overlap** (one role can mention both "cloud" and "security"), so they do not sum to the base; use the aggregate buckets for magnitudes.

### SA roles mentioning each domain (national, % of the 2,096 phrase base)

| Domain keyword | Count | % of SA base | Applicable to Julian? |
|----------------|------:|-------------:|-----------------------|
| Cloud | 1,381 | 66% | ✅ Applicable (secondary lane) |
| Security | 1,375 | 66% | ✅ Applicable |
| Infrastructure | 863 | 41% | ✅ Applicable |
| Network | 712 | 34% | ✅ Applicable (primary lane) |
| GenAI / generative | 450 | 21% | ✅ Differentiator |
| Cyber | 158 | 8% | ✅ Applicable |
| Network security (both words) | 92 | 4% | ✅ Strongest lane (rarest) |
| Firewall | 70 | 3% | ✅ Applicable |
| SASE | 12 | 1% | ✅ Applicable (very rare) |
| AI (any, incl. specialist ML) | 914 | 44% | ⚠️ Mixed (GenAI yes, specialist AI no) |
| Data | 1,445 | 69% | ⚠️ Ambiguous (data-centre yes, data-analytics no) |
| Dynamics / D365 | 360 | 17% | ❌ App-specific |
| Salesforce | 144 | 7% | ❌ App-specific |
| SAP | 135 | 6% | ❌ App-specific |
| Databricks | 117 | 6% | ❌ App-specific / specialist data |
| Oracle | 113 | 5% | ❌ App-specific |
| ServiceNow | 65 | 3% | ❌ App-specific |
| Workday | 34 | 2% | ❌ App-specific |

### Aggregate: applicable vs not (national, % of 2,096)

| Bucket | Count | % of SA base | Meaning |
|--------|------:|-------------:|---------|
| **Touches ≥1 of his core domains** (network / security / cyber / cloud / infra / SASE / firewall) | **1,850** | **88%** | The loose applicable ceiling |
| **Clean applicable** (core domain AND no app-specific product named) | **1,203** | **57%** | The strict, defensible "for Julian" set |
| Mentions ≥1 app-specific product | 749 | 36% | Overlaps with applicable (a cloud role can also say "Salesforce") |
| **Does not touch a core domain** (generic/other) | 246 | 12% | Ceiling on genuinely-not-for-him; of these ~102 are product-only, so the *true* "neither" is ~144 (~7%) |

**Read: Solution Architect is far more applicable to Julian than the raw family count implies.** Between **57% (strict) and 88% (loose)** of SA roles sit in his network/cloud/cyber/infrastructure wheelhouse; only **~12%** are clearly out of profile (pure application-specific). The generic "Solution Architect" glut is real, but the app-specific slice that genuinely excludes him is small.

### Applicable SA, two-pool (does filtering rescue Malvern? No)

| Bucket | London (d30) | Malvern cluster* | Malvern / London |
|--------|-------------:|-----------------:|-----------------:|
| Total SA (phrase) | 985 | 114 | 12% |
| **Clean applicable** | 578 | 62 | **11%** |
| App-specific | 343 | 38 | 11% |

*Malvern cluster = Cheltenham (d20) + Birmingham (d40) + Bristol (d15) + Worcester (d25).

**The applicability *share* is similar in both bases** (~59% London, ~54% Malvern are clean-applicable), so tailoring SA to Julian's profile does **not** change the two-base story: the Malvern applicable-SA pool is still only **~11% of London's**. Filtering to his lanes sharpens *relevance*, not *geography*.

---

## Q3 - Where do the well-paid roles cluster?

**£150k+ roles (annualised, unique sample of 80):**

| Cut | Split |
|-----|-------|
| By zone | London 43 · Malvern 14 · Remote 12 · UK-other 11 |
| By employment | **Contract 68 · Permanent 5 · unstated 7** |
| Cleared | 32 of 80 |

**Permanent £120k+ (only 12 in the whole 376-listing sample):** London 9 · Malvern 2 · Remote 1. The realistic perm reach band (£85-130k, 51 roles) is also London-weighted (23) and mostly **hybrid**.

**Conclusion:** the well-paid *permanent packages* skew **London hybrid / on-site**. The well-paid *remote and Malvern* numbers are almost all **contract day-rates** or **cleared on-site defence** (Cheltenham/Bristol). Perm median base sits at ~£75k (p75 ~£94.5k); contract median annualises to ~£143k, which is where every "£150k" headline lives.

---

## Q4 - Demand / competition (time-to-fill proxy) - added 14 Jul 2026

> **Why this section exists.** Everything above (Q1-Q3) is **supply**: how many roles exist. It says nothing about **demand**: how many people compete for them. "London has ~18x more roles than HK" is meaningless for *search difficulty* if London also has proportionally more applicants. The metric that actually drives **search duration** (the named decision hinge) is **applicants-per-role**.

> **The honest limit (verified 14 Jul).** The free Adzuna API has **no applicant field** - each listing was checked for `applicants / candidates / competition / views / clicks / fill` and none exist. Adzuna is an aggregator; applications happen on the employer ATS, so it cannot see them. **So applicants-per-role is not obtainable from this source.** What the API *does* return is each posting's `created` date, which supports a **time-to-fill proxy**.

**Method.** For each family x geography: pull live stock (`count`) and postings created in the last 30 / 7 days (`max_days_old`). **Persistence = 30 x (stock / 30-day inflow) = the average number of days a vacancy stays live.** Faster clearance (lower persistence) = the role is competed harder / candidate supply is deeper. Slower clearance (higher persistence) = candidate-scarce, the vacancy struggles to fill. *This is a market-clearing-speed proxy, not an applicant count: a role can persist long AND still draw many applicants if the employer is picky. Read it as directional.*

### Persistence - average days a vacancy stays live (lower = clears faster = more competition)

| Family | London | Birmingham | Cheltenham | Remote | UK national |
|--------|-------:|-----------:|-----------:|-------:|------------:|
| Solution Architect | 52.9 | 45.2 | 55.4 | **40.3** | 53.0 |
| Network Architect | 47.5 | 36.0\* | 0 roles | 30.0† | 44.3 |
| Security Architect | 46.6 | 51.0\* | 37.5\* | 36.0† | 47.0 |
| Cloud Architect | 48.0 | 40.6\* | 43.3\* | 30.0† | 47.2 |
| Enterprise Architect | 43.5 | 32.1\* | 0 roles | 30.0† | 43.9 |

\* Regional cells sit on thin stock (6-92 live roles) - **noisy, read as directional only.** † Remote stock is tiny (5-11 roles) and entirely <30 days old, which floors the 30-day proxy at exactly 30.0 - an artefact, not a real read. **Solution-Architect-remote (n=47) is the only robust remote cell.**

*Underlying live-stock counts (all / 30d / 7d): SA London 1281/726/249, Birmingham 92/61/30, Remote 47/35/11, national 2942/1664/649; Security London 354/228/105, national 827/528/269; Cloud London 296/185/88, national 666/423/228; Enterprise London 300/207/75, national 711/486/190; Network London 57/36/20, national 155/105/49.*

**Three findings:**

1. **Remote is the fastest-clearing = most-competed lane.** The one robust remote cell (Solution Architect, 40.3 days) clears clearly faster than London (52.9) and national (53.0). This is the **demand-side confirmation** of the Q1 "well-paid remote is a mirage" verdict: remote roles don't just pay less and skew junior, they also **clear the board fastest**, exactly what a global, offshore-exposed applicant pool swarming a scarce set of postings would produce.

2. **London does NOT clear faster than the regions - if anything it lingers.** London persistence sits at or above both Birmingham and national in every family. So London's far larger pool is **not** an illusion offset by proportionally more competition clearing it faster. The "London may have 18x roles but 100x applicants" worry is **not supported** by this proxy: London vacancies stay open at least as long as regional ones, consistent with robust, unmet employer demand for candidates rather than a saturated market. Mildly **reassuring** for a London-focused (crash-pad) search.

3. **The Malvern cluster is too thin to read.** Cheltenham returns **0** Network and **0** Enterprise Architect roles; Birmingham cells are single/low-double digits. Regional "competition" is not low - there is barely a market to compete in. Neutral for the crash-pad interim (which fishes London + remote), but another mark against a Malvern-**resident** search.

### Salary momentum (national, Jul 2025 → Jun 2026) - weak, directional only

A rising median implies employers bidding up for scarce talent (demand-favourable to candidates). **Caveat: this is a two-point read on a noisy monthly series that bounces ±£8k month to month - treat as drift, not trend.**

| Family | Jul 2025 | Jun 2026 | Drift |
|--------|---------:|---------:|-------|
| Cloud Architect | £84.4k | £102.8k | ↑ rising |
| Solution Architect | £83.6k | £92.6k | ↑ rising |
| Enterprise Architect | £95.0k | £96.7k | → flat |
| Network Architect | £99.2k | £88.5k | ↓ falling |
| Security Architect | £109.4k | £94.2k | ↓ falling |

No clean demand story - the month-to-month volatility is large enough that this should not be leaned on.

### What this section CANNOT answer (awaiting LinkedIn)

- **Applicants-per-role** - the actual head-to-head demand number. Not in any free Adzuna endpoint; only LinkedIn ("X applicants" per posting) exposes it.
- **UK vs Hong Kong** - the free Adzuna API is **GB-only**, so the cross-market comparison Julian asked for cannot be built here. LinkedIn is global and covers HK, so it will carry both the applicant count and the UK-vs-HK cut.

> **Update pending:** a LinkedIn pull (UK + HK, role x geography, capturing the applicant band and posting age per listing) will replace this proxy with real demand counts. When it lands, this section extends into a full supply-**and**-demand view. Collection brief drafted 14 Jul.

**Net:** the demand proxy **reinforces the existing picture and removes one worry** - remote is the tightest, most-competed lane (bad for a remote strategy, already dropped), and London's big pool is genuine rather than competition-inflated. It does not, on its own, move the London-direct vs crash-pad-interim decision.

---

## Decision framing

For the stated goal - a **high-paid permanent role with medical + life insurance + a team-leadership dimension** - the data leans **London-direct**. A well-paid *permanent* remote role in his niche is scarce, lower-paid, and mid-skewed; the robust remote money is either **contract** (fails the net-of-benefits test per the [[uk-150k-feasibility-report|feasibility report]]) or **clearance-gated defence**. Because the perm packages that meet his economic bar cluster in London hybrid/on-site (uncommutable from Malvern), **Malvern-first risks being "a cheap place to die a slow death"** for a perm-with-benefits seeker: he would be fishing a pool ~15% the size, minus the London hybrid roles that hold the money.

**The one honest Malvern-viable path:** pivot into the **SC/DV-cleared defence-cyber cluster** (Cheltenham GCHQ, QinetiQ/DSTL Malvern, Bristol). It is UK-protected, pays well, and Julian is clearable - but it is **contract**, needs clearance he does not yet hold, and forgoes the perm benefits package. That is a deliberate, narrower bet, not the default "run my search remotely from a cheaper base."

This sharpens the income/geography arm of the pre-agreed reopen condition; it does not by itself reopen the [[uk-relocation-decision|relocation decision]] (see [[commitment-lock-protocol]]). Current reading: London is where his *stated* target role concentrates; Malvern is viable only if he changes the target (cleared contract).

---

## Data source and coverage

**What the listings are and where they come from.** Every number in this report and the companion workbook is derived from the **Adzuna GB Jobs API** (adzuna.co.uk), a job-search **aggregator**, pulled live on **11 Jul 2026**. Adzuna is not a survey or a language model: it is a search engine for jobs that continuously indexes and de-duplicates real, currently-advertised postings from across the UK market. Its listings are gathered from:

> **Is Adzuna a credible source?** Yes, for what this report does. The UK **Office for National Statistics uses Adzuna** to power its official real-time weekly vacancy index, and academic groups use it as a *primary* UK labour-market dataset (~350M archived adverts). It is validated for **trends and relative comparisons** (movement over time, region/occupation differences) and treated as an **indicator, not a census**, for absolute counts. **This report only makes relative claims** (pool ratios, remote-vs-on-site salary, contract-share) - Adzuna's validated strength - so the source posture is sound. Full reliability/coverage profile: [[adzuna-uk-job-market-data-source|Adzuna as a UK Job-Market Data Source]].


| Source type | What it contributes |
|-------------|--------------------|
| **Employer / company career sites** (and their ATS feeds) | Direct-hire permanent roles posted by the hiring company |
| **Recruitment and staffing agencies** | A large share of the architect **contract** roles and many perm roles (agencies dominate senior-architect advertising) |
| **Other job boards and partner feeds** that syndicate to aggregators | Broad volume across the general market |
| **Direct employer submissions to Adzuna** | Additional employer-posted roles |

**What each listing record gave me (the fields used):** job title, employer, location (town + region), `salary_min` / `salary_max`, a flag for whether the salary is **employer-stated or Adzuna-predicted** (I used **only employer-stated, non-predicted** salaries for every median in this report), `contract_type` (permanent vs contract), full/part-time, category, and the **description text** (from which I inferred work-pattern and SC/DV clearance). Counts come from Adzuna's `count` field (the total matching a query); salary samples are up to 50 listings per query, de-duplicated to **376 unique real-salary listings**.

**Coverage gaps (what is NOT in this data):**
- **LinkedIn is excluded** - it keeps postings behind authentication and does not syndicate to aggregators. This is the single biggest under-count, and it hides a slice of senior/hybrid roles. Treat all counts as a **floor**, not a census.
- **Single-board niche roles** advertised only on a specialist board that does not syndicate.
- **Unadvertised / recruiter-network / word-of-mouth roles**, which are common at senior-architect level.
- **No "remote" field exists** in Adzuna, so the remote/hybrid/on-site split is inferred from description text (directional), and **contract salaries are annualised day-rates**, not packages.

Net: **counts and employer-stated salaries are hard data from live postings**; the work-pattern split and remote-share are directional inferences on top of that data. See Caveats for the full confidence breakdown.

---

## Caveats

- **Adzuna under-represents LinkedIn** and specialist boards; treat counts as directional, not a census. Title strings overlap across families, so summed family counts double-count somewhat.
- **No remote flag exists in Adzuna.** Remote share is a keyword floor (listings containing "remote"); work-pattern per listing is inferred from truncated description text - **directional, low-to-medium confidence.**
- **Contract day-rates are annualised** by Adzuna into salary_min/max, inflating apparent "£150k+" figures. A £156k+ contract line is ~£600-700/day, not a package. Compare net-of-benefits, never gross day-rate vs gross salary ([[target-role-profile]] employment-mode rule).
- **Seniority is inferred from title keywords** (senior/principal/lead vs junior/graduate) - noisy on small samples.
- **Clearance roles need SC/DV;** Julian is clearable but not currently cleared, so cleared roles are a future-state option, not an immediate pool.
- Salary sample n=376 unique real-salary listings; per-zone salary sub-samples are modest.
- **Demand data is a proxy, not a count (Q4).** The free API has no applicant field, so competition is inferred from vacancy clearing-speed (time-to-fill), not measured directly; a slow-filling role can still be heavily applied to. GB-only, so no HK comparison. Real applicants-per-role and the UK-vs-HK cut await the LinkedIn pull.

---

## Key Takeaways

- **Well-paid permanent remote in his niche is a mirage.** Remote is ~1-3% of postings, is the lowest-paid perm work-pattern (~£70k median base), skews mid-level, and the well-paid remote roles are contract day-rates in offshorable/AI-exposed product-config stacks.
- **Only two remote lanes are structurally protected:** scarce network-security (low volume) and SC/DV-cleared defence/security (contract, clearance-gated). Cloud and generic Solution Architect are the most exposed to global remote competition.
- **Malvern's commute pool is ~15% of London's** (best lane Network at 20%, on tiny absolute numbers). The defence-cyber cluster is real but concentrated and largely cleared/contract.
- **The "£150k" band is 85% contract;** permanent £120k+ is ~3% of the market and London-weighted. Realistic perm base ~£75-95k, reach £85-130k - corroborating the [[uk-150k-feasibility-report|feasibility report]].
- **Lean London-direct** for the perm-plus-benefits goal. Malvern-first only makes sense as a deliberate pivot into cleared defence-cyber contract, which changes the whole employment-mode and benefits equation.
- **Demand-side (Q4, time-to-fill proxy):** remote is the fastest-clearing = most-competed lane (confirms the mirage); London does **not** clear faster than the regions, so its bigger pool is real, not competition-inflated; the Malvern cluster is too thin to compete in. Real applicants-per-role and the UK-vs-HK comparison still await the LinkedIn pull (the free Adzuna API has no applicant data and is GB-only).

---

## Related

- [[target-role-profile|Career Target-Role Profile]] - the taxonomy and positioning this pull was run against
- [[uk-150k-feasibility-report|UK £150k Feasibility Report]] - corroborated and extended by this geography/remote layer (linked from its Competition section)
- [[uk-relocation-decision|UK Relocation Decision]] - the project this informs (London-direct vs Malvern-first sub-decision)
- [[uk-vs-hk-earning-comparison|UK vs HK Earning Comparison]] - the income head-to-head
- [[master-resume|Master Resume]] - credential stack (CCIE + CISSP + TOGAF + AWS SA + SASE + presales + leadership)
- [[commitment-lock-protocol|Commitment-Lock Protocol]] - governs whether this evidence reopens the locked decision
</content>
</invoke>

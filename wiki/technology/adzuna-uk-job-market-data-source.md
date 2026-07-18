---
type: reference
tags: [technology, data-source, job-market, career, research]
created: 2026-07-11
source-of-truth: this-file
subject: Adzuna as a UK job-market data source (coverage, reliability, limitations)
---

# Adzuna as a UK Job-Market Data Source

> **What this is.** A reliability and coverage profile of **Adzuna** as a source for UK job-market analysis, compiled from independent research (Julian, 11 Jul 2026). It answers: how good is Adzuna's coverage, how do official statistics bodies and academics treat it, what are its blind spots, and what can you safely conclude from it. Use this whenever an Adzuna pull is used as evidence (e.g. [[uk-job-market-remote-hybrid-split-2026-07-11|the UK remote/hybrid job-market report]]).

## Key Takeaways

- **Adzuna is a serious, high-coverage UK online-vacancy source, not a hobby feed.** The UK **Office for National Statistics (ONS) uses Adzuna data** to power its official real-time weekly vacancy index, and academic groups (e.g. Glasgow's Urban Big Data Centre, ~350M archived UK adverts 2016-2025) use it as a *primary* labour-market dataset.
- **It is an aggregator, not a single board.** It crawls and partners across "thousands" of sites: major national job boards, niche/local boards, and employer career pages (100+ partners). It does **not publish a canonical, enumerated partner list**, so you cannot reweight by contributing board.
- **Reliable for what we actually use it for: trends and RELATIVE comparisons.** ONS and academics treat it as excellent for movement over time and relative differences across regions/occupations, and as an *indicator* (not a census) for absolute levels.
- **Its blind spots are exactly the caveats already in our report:** online-only frame (misses offline/word-of-mouth/internal hiring), partner-board dependence, imperfect dedup, and estimated salaries where the ad omits pay. **LinkedIn is excluded** (login-walled, doesn't syndicate).
- **Net for our use:** for "the state of the UK *online* job-advert market," Adzuna is among the best available sources. Our report uses it for relative pool ratios and remote-vs-on-site comparisons - its validated strength - not for absolute census counts.

## What Adzuna aggregates

Adzuna is a job-search **aggregator**: it pulls postings from "large job boards, specialized job portals and employer websites" into one deduplicated database, rather than only hosting its own ads. Its own marketing says it searches "thousands of job sites."

- No canonical public partner list exists, but third-party tooling gives hints at the *kinds* of partners: multi-board scrapers group Adzuna alongside Reed, Totaljobs, CV-Library, CWJobs and Indeed as one of the "big boards/aggregators"; an ATS integration (Ceipal) describes Adzuna as sourcing from "100+ national, local, and niche partners."
- Practical model: **a meta-search engine aggregating the main commercial UK boards plus many smaller sites and employer career pages** - but not a transparent, source-attributed feed.
- **Per-listing provenance is masked.** In the API, each listing's `redirect_url` routes through `adzuna.co.uk/jobs/land/ad/{id}`; there is no origin-board field. The closest provenance signal is the `company` (advertiser) field, which in our niche skews ~38% recruitment agencies / ~62% direct employers.

## Coverage and scale (UK)

- Glasgow / Urban Big Data Centre (UBDC): Adzuna is "one of the UK's most popular vacancy search engines"; their research dataset holds **~350 million job adverts** from weekly snapshots of adzuna.co.uk, 2016-2025. Sustained, large-scale capture.
- Independent comparisons describe Adzuna's coverage as **strongest in the UK and Western Europe**, used by "researchers, government statistics bureaus."
- If the unit of analysis is "UK **online** job advertisements," Adzuna has both depth (hundreds of millions of historical ads) and breadth (thousands of sites).

## How official statistics and academics treat it

- **ONS adoption is the strongest reliability signal.** ONS methodology on "using Adzuna data to derive an indicator of weekly vacancies" states Adzuna has **"a high coverage of all job adverts in the UK,"** while noting it is limited to online vacancies. ONS and Adzuna publicly partnered so Adzuna data "exclusively power[s] a real-time national job vacancy index" in ONS "faster indicators" (index built by analysing 36M+ adverts, 2018-2020).
- ONS "comparison of labour market data sources" frames online-vacancy data (incl. Adzuna) as strong on **timeliness and granularity** but sample-frame-biased toward online-advertised roles.
- **Academic use:** UBDC's Adzuna dataset has spawned derived panels by local authority / Travel-to-Work-Area, teaching-sector slices, and hourly-pay vacancy counts; Zenodo-published studies use Adzuna counts for subregional high-frequency analysis. In most cases Adzuna is the *primary* online-vacancy source, consistent with high perceived coverage.

**Methodological posture (ONS-style):** a large, high-frequency, **non-probability** source, excellent for *movement over time* and *relative comparisons*, not a perfect census of all UK jobs (offline/informal/internal hiring is out of frame).

## Known limitations and biases

1. **Online-only frame** - misses roles filled by word-of-mouth, internal moves, or channels that never post online. Smaller bias in highly-advertised sectors (tech, professional services), larger in small business, some trades, parts of the public sector.
2. **Partner-board dependence** - coverage is only as good as the sites Adzuna crawls/partners with; the full list is not public, so you cannot precisely reweight by source. Validate against external benchmarks where absolute levels matter.
3. **Dedup and metadata quality** - as an aggregator it must dedupe cross-posted ads and normalise titles/salaries; missed duplicates or over-merges add micro-level noise. **Salaries may be estimated** where the ad omits pay (we use only non-predicted salaries).
4. **Time-series/taxonomy changes** - UBDC notes the production method changed over time (two dataset versions); long time-series need break checks. Adzuna's Intelligence API taxonomy evolves, implying occasional reclassification.
5. **Geographical/sectoral skew** - like most online-vacancy data, strongest in larger labour markets and digital-recruitment-heavy sectors.

These shape *what you can safely claim*: trends and relative differences yes; precise population-level counts no.

## Reliability verdict for our use case

- **For trends, relative comparisons, and online-vacancy dynamics:** widely accepted as reliable; ONS + academic precedent is strong.
- **For level estimates of *all* UK vacancies:** treat as an indicator, not a census.
- If the snapshot is explicitly "the UK **online** job-advert market," Adzuna is one of the best available sources on timeliness and coverage. To approximate the whole labour market you would calibrate against ONS survey vacancy data or restrict claims to relative patterns.

## Practical robustness steps (for future pulls)

1. **Use Adzuna's Intelligence/Historical API aggregations** (postings over time, new postings, posting duration, time-to-fill, mean/median salary, distribution by region/occupation) instead of hand-rolling aggregations from raw listings - fewer errors, aligned with other researchers.
2. **Cross-check against ONS** online-vacancy index and survey counts to confirm trend consistency and spot divergent sectors/regions.
3. **Document ONS-style:** state that data are online advertised vacancies, list bias sources, cite ONS/academic precedent.
4. **Watch for structural breaks** if using history back to 2016 (dataset version 1 vs 2).

## Impact on the current report

**None on the findings.** The [[uk-job-market-remote-hybrid-split-2026-07-11|remote/hybrid report]] makes **relative** claims (Malvern pool ~15% of London's; remote vs on-site salary; £150k-band contract share) - exactly Adzuna's validated strength - and never claims an absolute census. This research **strengthens the report's credibility footing** (ONS + academic adoption) and **confirms its existing caveats** (online-only frame, partner-board dependence, dedup/salary-estimation, LinkedIn excluded). No number or verdict changes.

## References

- [University of Glasgow / UBDC - Adzuna research dataset (2016-2025)](https://researchdata.gla.ac.uk/2047/)
- [ONS - Using Adzuna data to derive an indicator of weekly vacancies](https://www.ons.gov.uk/peoplepopulationandcommunity/healthandsocialcare/conditionsanddiseases/methodologies/usingadzunadatatoderiveanindicatorofweeklyvacanciesexperimentalstatistics)
- [ONS / Adzuna - real-time job vacancy index launch](https://www.adzuna.co.uk/blog/ons-and-adzuna-launch-real-time-job-vacancy-index-to-help-get-britain-back-to-work/)
- [ONS - Comparison of labour market data sources](https://cy.ons.gov.uk/employmentandlabourmarket/peopleinwork/employmentandemployeetypes/methodologies/comparisonoflabourmarketdatasources)
- [UBDC - Labour Market data theme](https://www.ubdc.ac.uk/data-theme/labour-market)
- [Zenodo - Adzuna-based entry-level vacancy dataset](https://zenodo.org/records/14771706)
- [Ceipal - Adzuna integration (100+ partners)](https://www.ceipal.com/integrations/adzuna-job-board)
- [Apify - Adzuna multi-board scraper (board grouping)](https://apify.com/thirdwatch/adzuna-jobs-scraper/api)
- [Adzuna Developer API](https://developer.adzuna.com/)
- [Adzuna - Wikipedia](https://en.wikipedia.org/wiki/Adzuna)

## Related

- [[uk-job-market-remote-hybrid-split-2026-07-11|UK Job Market: Remote/Hybrid Split (11 Jul 2026)]] - the report this source underpins
- [[uk-150k-feasibility-report|UK £150k Feasibility Report]] - also draws on Adzuna tightness proxies
- [[technology/_index|Technology index]]
</content>

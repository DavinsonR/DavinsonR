## Davirson Novoa Ramírez

*[Leer en español](README.es.md)*

**Economist and FP&A consultant who builds the data infrastructure himself.
I read a P&L and I build the pipeline that feeds it.**

Three years inside corporate finance — treasury, billing and FP&A — supporting
operations across 15+ countries in the Americas. MSc Economics at Pontificia
Universidad Javeriana: thesis filed August 2026, graduation expected November 2026.

Bogotá · GMT-5 · full overlap with US hours · open to remote roles

**[proyecto-davirson-git.vercel.app](https://proyecto-davirson-git.vercel.app)**

---

### Financial inclusion and regional growth in Colombia
[`financial-inclusion-colombia`](https://github.com/DavinsonR/financial-inclusion-colombia) · [open the atlas](https://proyecto-davirson-git.vercel.app/en/research/fintech-inclusion)

I asked whether financial inclusion predicts departmental growth in Colombia.

**It does not** — β = 0.0007, p = 0.90, with entity and time fixed effects across
33 departments, 2019 to 2025, N = 228. Wild cluster bootstrap p = 0.89,
permutation placebo p = 0.68. Without time effects the same coefficient is
+0.024 with p < 0.001, and that distance is exactly what the national trend was
worth.

I published the result with its specification, its N, its clusters and its
tests. I also published what went wrong: sampling adequacy came to KMO 0.314 for
access and 0.404 for use, below the 0.5 a factor model needs, so the planned PCA
was dropped. Forcing it produced negative implicit weights on microcredit — an
index that says more credit is less inclusion.

Nineteen public sources with a sha256 manifest · every series resolved to
municipal codes, 100% coverage across the 34 quarterly cuts · an index by
dimension with frozen, published weights · two annual panels · an atlas of all
1,123 municipalities · a full battery against spurious correlation (CIPS, CCE,
permutation placebo, shift-share, event study, Moran, SAR/SDM).

`Python` `dbt` `DuckDB` `linearmodels` `Quarto` `BigQuery`

---

### Market data platform
[`market-data-medallion`](https://github.com/DavinsonR/market-data-medallion) · [open the lab](https://proyecto-davirson-git.vercel.app/en/projects/trading-sim)

Public APIs into a PostgreSQL medallion warehouse with dbt, an honest
backtesting engine on top, and a daily refresh on GitHub Actions that keeps
itself alive without a server. 48 assets, 58,000+ daily candles, zero budget.

**Of 1,392 strategy variants evaluated, barely one in eight of the in-sample
winners survived out-of-sample validation.** I published every one that did not.
The 42 variants combining five signals at once won zero times: more degrees of
freedom is not more signal, it is more room to fit noise.

A signal computed at day *t*'s close executes at day *t+1*'s open — never at the
close that produced it, and a regression test asserts that truncating the future
does not change past signals. Fees and slippage are always on, and buy-and-hold
pays the same. 89 dbt data-quality tests and 171 Python unit tests run before a
single figure is published.

`Python` `dbt` `PostgreSQL` `pandera` `GitHub Actions` `Power BI`

---

### JARVIS — daily tracking
[public demo, no account](https://jarvis-app-psi-sable.vercel.app/demo) · private repository

A full day — habits, body, sleep, food, spending — logged in under ninety
seconds with one hand, and handed back read rather than raw.

Half the people who start a tracking app abandon it in the first month, so the
design targets specific failure modes: a gap is not a failure, a mastered habit
graduates instead of counting as churn, nothing is interpolated, and no progress
bar points at a target weight. A personal-finance data model plus health
tracking on Postgres with RLS: 35 tables, 22 views, ~370 tests and an RLS smoke
test in CI.

`Next.js` `TypeScript` `Supabase` `RLS` `PWA`

---

### How I work

- **I publish what did not work.** The null result, the KMO below the threshold,
  the data leak I found in my own app. The engineering log records 28 defects
  found and fixed, numbered one by one. A portfolio that only shows wins says
  nothing.
- **Every figure traces to a test.** If a number appears in a document, it comes
  from a test, a row of the verification ledger, or a dbt test.
- **Decisions are written before the code.** Sixteen decision records in the
  research repository, each with the assumption that kills it if it fails.

### What I am looking for

Remote Finance Data Analyst, Analytics Engineer and FP&A automation roles —
where financial judgement and data engineering are paid as one capability, not
two halves. Consulting too. I answer in English and Spanish.

[LinkedIn](https://linkedin.com/in/davirson-novoa-ramirez-2721641b5) · davinsonnovoaramirez@gmail.com

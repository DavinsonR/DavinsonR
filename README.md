## Davirson Novoa Ramírez

*[Leer en español](README.es.md)*

**Economist who builds machine learning that survives an audit.
I read a P&L, I build the pipeline that feeds it, and I write the control that
blocks my own model when it does not comply.**

Three years inside corporate finance — treasury, billing and FP&A — supporting
operations across 15+ countries in the Americas. MSc Economics at Pontificia
Universidad Javeriana: thesis filed August 2026, graduation expected November 2026.

Bogotá · GMT-5 · full overlap with US hours · open to remote roles

**[proyecto-davirson-git.vercel.app](https://proyecto-davirson-git.vercel.app)**

---

### Credit risk with model governance
[`credit-risk-mlops`](https://github.com/DavinsonR/credit-risk-mlops)

A credit decisioning system on real US public data — 1.96M SBA 7(a) loans and
62.4M HMDA applications. The model is not the point. The point is that it
survives an audit, and that I ran the audit against myself first.

**My first honest number was a deleted one.** The signal check returned AUC
0.9461, which is not a credit model, it is a leak: `TermInMonths` is overwritten
when a loan is liquidated, so the field carried the outcome. Removing it drops
the ablation to 0.6621. Production sits at **0.7005**, +0.0311 over an
interpretable WoE scorecard, with calibration error 0.0107.

**Ten promotion gates, and one of them blocks my own model.** The access model
scores a disparate impact ratio of **0.7639** against a 0.80 threshold, so it is
not promoted — and I did not move the threshold. Every threshold has its
derivation written next to it, and two of the gates exist because the governance
documents lied: the model card listed 7 gates of 8, omitting the only one the
model fails, while the validation report printed PASS for that same gate in one
section and "promotion blocked" in another.

**Declining the riskiest 10% would have avoided $276.3M** in charge-offs, 2.15x
what declining at random achieves, and $942.1M of the period's realized loss was
absorbed by the taxpayer through the guarantee. It also forgoes **$1.99B in good
lending volume** — 7.2x the loss avoided — and both numbers ship in the same
payload. A headline that shows only the numerator is not a headline.

**A charge-off takes a median of 51 months to appear**, so performance monitoring
on young cohorts is arithmetic, not measurement, and the project refuses to fake
it. What it monitors instead found something: the SBA changed the `business_age`
category scheme between FY2018 and FY2021, and today **84% of its values fall
into categories the model never saw**. Serving maps them to "unknown", so the
model does not degrade — it loses a top-three variable entirely and keeps
answering with the same confidence.

**On the causal side I published a non-identification, not an effect.** The
guarantee percentage is the one lever the SBA actually controls, and it is
administratively determined: R² 0.9145 against processing-method × loan-size
cells, so there is no overlap left to exploit. At the $150,000 statutory
threshold, 83.1% of the ±$5k window sits at exactly $150,000 — the density is
destroyed, and with it the regression discontinuity. Conditioning on size removes
38% of the raw gradient and leaves a residual whose sign is what adverse
selection predicts. An estimator applied where its assumptions fail produces a
number, not an estimate.

Out-of-time validation across the COVID shock · under a 2007-style regime the
same model falls to AUC 0.5456 and underestimates risk eightfold, which is a
deliverable and not a caveat · 13 architecture decision records · `make
reproduce` asserts the published metrics are identical after a retrain · CI was
red for eight consecutive commits before I caught it, and the fix was a script
that reproduces CI locally before pushing.

`Python` `LightGBM` `PyTorch` `DuckDB` `PySpark` `MLflow` `ONNX` `FastAPI` `Power BI`

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

### How I work

- **I publish what did not work.** The null result, the KMO below the threshold,
  the data leak I found in my own app. The engineering log records 28 defects
  found and fixed, numbered one by one, and the credit-risk repository keeps its
  own ledger — including two published numbers I had to retract because they did
  not replicate on a second machine, and one claim I repeated four times before
  measuring it and finding it false. A portfolio that only shows wins says
  nothing.
- **Every figure traces to a test.** If a number appears in a document, it comes
  from a test, a row of the verification ledger, or a dbt test. In the credit-risk
  repository the gate does not trust the artifact either: it recomputes the
  published metrics from the saved predictions before letting anything be
  promoted.
- **Decisions are written before the code.** Sixteen decision records in the
  research repository and thirteen in the credit-risk one, each with the
  assumption that kills it if it fails.
- **A control that cannot fail is not a control.** Three of the defects I found in
  my own tooling reported success while doing nothing: a compliance check that
  matched nothing, a hook that accepted what it was built to reject, and a
  pipeline that printed "approved" after the training step had crashed. Each one
  now has a test that fails in the environment where it silently passed.

### What I am looking for

Remote Finance Data Analyst, Analytics Engineer and FP&A automation roles —
where financial judgement and data engineering are paid as one capability, not
two halves. Consulting too. I answer in English and Spanish.

[LinkedIn](https://linkedin.com/in/davirson-novoa-ramirez-2721641b5) · davinsonnovoaramirez@gmail.com

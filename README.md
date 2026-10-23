# CDP Scores and Emission Cuts

**Author:** Godfrey M. Kanotunga
**Affiliation:** MS Applied Data Science, Reh School of Business, Clarkson University
**Supervisor:** Professor Santosh Mahapatra
**Data:** CDP Climate Change public responses 2018–2021 and CDP investor scores 2018–2020

**Live dashboard:** https://godfreykanotunga.github.io/cdp-esg-command-center/

---

## Question

Do companies with higher CDP climate scores actually cut their emissions — and does a high score come **before** the cuts, or just describe firms that were already cutting?

## Key finding

- **Same period** (the year the firm was being scored): each grade higher goes with about **0.6 percentage points** more cut in Scope 1+2 emissions (p = 0.031, sector and year controls).
- **After the score** (the year after it was released): **−0.2 points** per grade (p = 0.61, 95% CI −1.0 to +0.6).
- **Reading:** high scorers were already cutting a bit more, but there is no clear evidence of extra cuts after the score is published. The after-score sample is smaller (840 company-years), so a small effect cannot be ruled out. This is an association, not a causal effect.

## Why timing matters

A CDP score for year *t* is based on the questionnaire answered in *t*, which reports the previous year's data. Most firms in the 2019 file (68.5%) report a year that ends in 2018. So comparing a 2018 score with the change in the 2019 report measures the **same period** the firm was scored on. The **after-score** test compares the 2018 score with the change in the 2020 report (2019 vs 2018), and the 2019 score with the 2021 report, keeping only rows where the measured year starts after the scores were released.

## Method

- Emissions change is read **inside one report**: reporting year vs "Past year 1" (C6.1 Scope 1 + C6.3 Scope 2 location-based). This avoids bias from later restatements (39% of Scope 1 figures change by more than 1% in a later file).
- Kept only when the two periods end 335–395 days apart and both totals are above zero.
- Change = log(current / previous), shown as a percentage; trimmed at the 1st and 99th percentile.
- Score bands: A / A-, B / B-, C / D (incl. C-, D-). Grade step: A = 8 … D- = 1.
- Models: OLS with sector and year controls, standard errors clustered by company; median regression with sector and year controls.
- Robustness: Scope 1 only, and reporting-year totals compared across two reports.
- Every number was recomputed by a second, independent script from the original files.

## Limits

- Association only; firms planning cuts may also score well.
- Only firms reporting two back-to-back years in one report are included, which leans toward larger, well-organised reporters.
- Changes can reflect acquisitions or divestments, not real cuts.
- 2019→2020 changes include COVID effects; the 2018 score year is the cleanest test.
- Scope 3 is not used.

## Files

| File | Description |
|---|---|
| `index.html` | Interactive dashboard (self-contained; loads d3 and Google Fonts from CDNs) |

The CDP source files are not included in this repository.

---

Academic research for educational purposes only. Not investment advice.

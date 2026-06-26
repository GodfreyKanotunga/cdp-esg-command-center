# CDP ESG Command Center

**Author:** Godfrey M. Kanotunga  
**Role:** Graduate Research Assistant, Clarkson University  
**Supervisor:** Professor Santosh Mahapatra, Reh School of Business  
**Data:** CDP Climate Change Public Disclosure, 2018–2021  

---

## Overview

The CDP ESG Command Center is an institutional climate disclosure analytics dashboard built on a four-year longitudinal panel dataset. It synthesises statistical modelling, machine learning classification, and emissions analysis into a single, self-contained HTML dashboard designed for academic research and ESG portfolio applications.

The central research question addressed is whether corporate governance practices or emissions scale better explain the quality of CDP climate disclosure scores. The answer, supported by multiple methods, is governance.

---

## Dataset

| Attribute | Detail |
|---|---|
| Source | CDP Climate Change Public Questionnaire |
| Years covered | 2018, 2019, 2020, 2021 |
| Total firm-years | 16,957 |
| Countries | 108 |
| Sectors | 61 |
| Join key | account_id |
| Scored firm-years | 8,331 (49.1% of panel) |

The master analytical file (`CDP_2018_2021_Master_v2.xlsx`) was constructed through a full ETL pipeline: multi-year flat file extraction, column-intersection harmonisation across question naming conventions, and panel assembly via account_id.

---

## Key Finding

> **Governance practices explain 31% of variation in CDP disclosure scores. Emissions size does not.**

OLS regression with HC3 heteroskedasticity-robust standard errors across 8,331 scored firm-years:

- R² = 0.31
- Seven binary governance indicators included as predictors
- Log Scope 1 emissions: β = −0.004, p = 0.614 (statistically insignificant once governance is controlled)
- Strongest predictor: Reduction Initiatives (β = 1.40, adoption rate 93.9%)

This finding is consistent with stakeholder and legitimacy theory - large emitters invest in disclosure quality under investor and regulatory pressure, but the governance structure, not emissions volume, drives score variation.

---

## Methods

### OLS Regression - Governance Transmission Model
Seven binary governance indicators regressed against CDP disclosure score. HC3 robust standard errors used throughout to account for heteroskedasticity. Results presented as β coefficients with adoption rates per indicator.

| Governance Practice | Adoption Rate | β Coefficient |
|---|---|---|
| Reduction Initiatives | 93.9% | 1.40 |
| Emissions Target | 86.1% | 1.14 |
| Board Oversight | 96.4% | 0.90 |
| Value Chain Engagement | 31.6% | 0.78 |
| Climate Risks | 87.3% | 0.50 |
| Climate Opportunities | 98.6% | 0.43 |
| Internal Carbon Price | 24.2% | 0.40 |

### Random Forest Classification
- 200 trees, max depth 8
- 5-fold cross-validation, 3-class target (Low / Mid / High scorer)
- Accuracy: 54.9% vs. 33.3% naive baseline

### CART Decision Tree
- Max depth 5
- Accuracy: 54.4%

### Scope 1 Emissions ANOVA
- Inverted-U pattern across emissions quartiles (Q1: 5.35, Q2: 5.78, Q3 peak: 5.94, Q4: 5.74)
- F = 33.4, p < 0.001
- Consistent with selection effect: mid-range emitters face highest scrutiny

---

## Dashboard Sections

The dashboard is a single self-contained HTML file with no external dependencies beyond Chart.js (loaded via CDN) and Google Fonts.

- **ESG Risk Scorecard** - mean CDP score by year (2018–2021), trend, governance adoption rates, bivariate correlation, RF classification accuracy
- **Governance Transmission Model** - OLS β coefficients per governance practice with adoption rate bars
- **Score Distribution and Panel Stats** - modal score, mean score, scored vs. total firm-years
- **Top Countries by Mean CDP Score** - ranked list with score bars
- **Predictive Model Results** - RF, CART, and naive baseline accuracy comparison
- **Adopter vs. Non-Adopter Score Gap** - mean score differential between governance adopters and non-adopters
- **Emissions Profile Scope 1** - sector-level median tCO2e, top emitting sectors
- **Score by Scope 1 Quartile** - inverted-U pattern visualisation
- **ESG Transmission Framework** - network diagram mapping governance practices to CDP score through legitimacy and stakeholder theory pathways

---

## Limitations

- OLS applied to an ordinal outcome (ordered logit recommended for robustness)
- 50.9% of panel unscored - rates computed on scored subsample only
- Cross-sectional design within years - causality not established
- Bivariate correlation (+0.13) explained by stakeholder scrutiny of large emitters, not scale driving quality

---

## How to Use

Open `CDP_ESG_Command_Center_v3.html` in any modern browser. No installation or dependencies required. The file is fully self-contained.

---

## Files

| File | Description |
|---|---|
| `CDP_ESG_Command_Center_v3.html` | Interactive analytics dashboard |

The master analytical file (`CDP_2018_2021_Master_v2.xlsx`) is not included in this repository. The dataset was constructed from CDP Climate Change public disclosures and is available on request.

---

## Disclaimer

Academic research for educational and portfolio purposes only. Data sourced from CDP public disclosures. Not investment advice. Sources: CDP, IMF, World Bank, Bloomberg.

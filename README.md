# Retail Credit Risk Scorecard
## Overview

This repository contains an **end-to-end implementation of a retail credit risk scorecard** using **logistic regression and Weight of Evidence (WOE) binning**, following **industry-standard scorecard methodology** commonly used in banks and financial institutions.

The project covers:

* Data preparation and variable selection
* WOE binning and Information Value (IV) analysis
* Logistic regression model development
* Scorecard scaling and score generation
* Risk grade (A/B/C/D) construction
* Model validation (KS, AUC, Gini)
* Management-ready PowerPoint reporting (via VBA)

---

## Dataset Description

The dataset consists of **10,499 accepted credit card applications** with post-approval default outcomes.

| Variable | Description                             |
| -------- | --------------------------------------- |
| CARDHLDR | 1 if credit card application accepted   |
| DEFAULT  | 1 if defaulted, 0 otherwise             |
| AGE      | Age in years                            |
| ACADMOS  | Months at current address               |
| ADEPCNT  | 1 + number of dependents                |
| MAJORDRG | Number of major derogatory reports      |
| MINORDRG | Number of minor derogatory reports      |
| OWNRENT  | 1 = owns home, 0 = rents                |
| INCOME   | Monthly income (scaled)                 |
| SELFEMPL | 1 if self-employed                      |
| INCPER   | Income per dependent                    |
| EXP_INC  | Credit card expenditure to income ratio |
| SPENDING | Avg monthly spending (cardholders only) |
| LOGSPEND | Log of spending                         |

📌 **Target Variable:** `DEFAULT`
📌 **Portfolio Bad Rate:** ~9.5%

---

## Variable Selection

* Variables were evaluated using **Information Value (IV)**, predictive power, and stability.
* **WOE binning with monotonicity enforcement** was applied.
* The following variables were retained in the final model:

  * `AGE`
  * `INCOME`
  * `INCPER`
  * `OWNRENT`

### Removed Variable

* **ACADMOS** was removed due to **low IV and weak marginal contribution** to model performance.

This resulted in a **parsimonious and stable scorecard**, consistent with regulatory expectations.

---

## Model Methodology

* **Model Type:** Logistic Regression
* **Transformations:** Weight of Evidence (WOE)
* **Binning:** `scorecardpy.woebin` with manual review
* **Score Scaling:**

  * Points-to-Double-Odds (PDO): 20
  * Base Score: ~300–480 (portfolio-calibrated)

---

## Scorecard & Grades

Scores were mapped into **risk grades** based on observed default rates:

| Grade | Population (%) | Bad Rate (%) | Score Range |
| ----- | -------------- | ------------ | ----------- |
| A     | ~10%           | ~4%          | 389–405     |
| B     | ~20%           | ~5%          | 377–388     |
| C     | ~40%           | ~8%          | 360–377     |
| D     | ~30%           | ~16%         | 324–359     |

Bad rates increase monotonically from **Grade A → D**.

---

## Model Performance

| Metric | Value |
| ------ | ----- |
| KS     | ~0.23 |
| AUC    | ~0.66 |
| Gini   | ~0.31 |

* Performance is consistent with **retail unsecured credit scorecards**
* Grade-level and score-level validation performed
* No grade-level risk reversals observed

---

## Repository Structure

```
├── retail_credit_scorecard_python.ipynb   # Main notebook (WOE, model, scoring)
├── credit_scorecard_report.pptx           # Management presentation (generated)
├── README.md                              # Project documentation
```

---

## PowerPoint Reporting (VBA)

A **6-slide management-ready PowerPoint deck** is generated using **native PowerPoint VBA**, covering:

1. Model overview
2. Data & variable selection
3. WOE binning insights
4. Scorecard & grades
5. Model performance
6. Conclusions & next steps

This allows deployment in **corporate environments without Python**.

---

## Tools & Libraries

* Python 3
* pandas
* numpy
* scikit-learn
* scorecardpy
* PowerPoint VBA (for reporting)

---

## Key Takeaways

* Fully explainable, regulator-friendly scorecard
* Strong risk segmentation with limited variables
* Suitable for **approval, limit assignment, and pricing strategies**
* Easily extensible for:

  * Out-of-time (OOT) validation
  * Population Stability Index (PSI)
  * Excel or system deployment

---

## Disclaimer

This project is for **educational and demonstration purposes**.
Thresholds, cutoffs, and performance metrics should be recalibrated before production use.

---

## Author

Developed as part of a **retail credit risk modeling and scorecarding exercise**, aligned with industry standards used by banks and financial institutions.

# Retail Credit Scorecard

## Model Overview
The scorecard processes 10,499 observations with a 9.5% baseline default rate (996 bads, 9,503 goods). Selected variables like `ACADMOS` (IV=0.0138) and `SELFEMPL` (IV=0.0014) drive scoring after binning and WOE calculation.

## Performance Metrics
Key metrics indicate acceptable separation for internal risk management.

| Metric | Value  |
|--------|--------|
| KS Statistic | 0.226 |
| AUC      | 0.345 |
| Gini     | 0.310 |

## Grade Band Analysis
Population segments into A-D grades by score, showing monotonic bad rates from 3.9% (A) to 15.9% (D).

| Grade | Population (%) | Bads (%) | Bad Rate (%) | Score Range |
|-------|----------------|----------|--------------|-------------|
| A     | 9.7            | 4.0      | 3.92         | 389-405     |
| B     | 20.2           | 11.2     | 5.29         | 377-388     |
| C     | 40.0           | 34.2     | 8.11         | 360-377     |
| D     | 30.1           | 50.5     | 15.93        | 324-359     |

## Recommendations
Refine by adding higher-IV variables or calibrating for production use in credit risk workflows. Export to Excel for dashboard integration per user preferences in quantitative modeling.

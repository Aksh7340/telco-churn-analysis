# Week 2 Journal — Telco Customer Churn Analysis

## Week Objective

Complete the Exploratory Data Analysis phase, identify the most important churn-related patterns, convert validated patterns into analytical features, and quantify the current recurring revenue exposure associated with active customers who match the defined at-risk criteria.

---

# Day 5 — Phase 2: Exploratory Data Analysis

**Phase:** Phase 2 — Exploratory Data Analysis

## What I Did

- Loaded the cleaned dataset produced during Phase 1.
- Confirmed the analytical grain remained one row per customer.
- Established the EDA structure:
  - Business question
  - Analysis
  - Visualization
  - Insight
- Calculated the overall churn baseline.
- Investigated churn across:
  - Contract
  - Tenure
  - InternetService
  - PaymentMethod
  - MonthlyCharges
- Created temporary analytical tenure and charge bands where useful.
- Reviewed numeric relationships and correlation.
- Created a correlation heatmap.
- Documented analytical limitations and non-causal interpretations.

## Findings

- Total customers: **7,043**
- Churned customers: **1,869**
- Overall churn rate: **26.54%**

### Contract

| Contract | Churn Rate |
|---|---:|
| Month-to-month | 42.71% |
| One year | 11.27% |
| Two year | 2.83% |

### Tenure

Customers in the earlier stages of the customer lifecycle showed substantially higher observed churn than customers with longer tenure.

### Internet Service

| Internet Service | Churn Rate |
|---|---:|
| Fiber optic | 41.89% |
| DSL | 18.96% |
| No internet service | 7.40% |

### Payment Method

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | 45.29% |
| Mailed check | 19.11% |
| Bank transfer (automatic) | 16.71% |
| Credit card (automatic) | 15.24% |

### Monthly Charges

| Charge Band | Churn Rate |
|---|---:|
| 0–50 | 15.70% |
| 50–100 | 32.67% |
| 100+ | 28.05% |

The relationship between monthly charges and churn was not strictly monotonic.

## Analytical Interpretation

Contract type, tenure, internet service, payment method, and monthly charges showed meaningful differences in observed churn.

These findings were used to determine which characteristics warranted deeper analysis during Phase 3.

## Limitations

- Observed differences represent associations and do not establish causation.
- Customer characteristics may overlap with one another.
- Analytical bands are created for segmentation and do not necessarily represent official business categories.
- Individual-variable analysis does not establish the independent effect of a variable.

---

# Day 6 — Phase 2: Deeper Relationship Analysis

**Phase:** Phase 2 — Exploratory Data Analysis

## What I Did

- Compared numeric-variable distributions across churn status.
- Examined:
  - `tenure`
  - `MonthlyCharges`
  - `TotalCharges`
- Created a Contract × InternetService cross-tabulation.
- Examined relationships among numeric variables.
- Created a correlation matrix and heatmap.
- Reviewed the overlap between high-churn characteristics.

## Findings

- Churned customers were more concentrated at lower tenure values.
- Churned customers showed greater concentration at elevated monthly charges.
- `TotalCharges` was concentrated at lower values among churned customers, which is closely related to shorter tenure.
- Fiber-optic customers were more concentrated in month-to-month contracts than in longer-term contracts.

### Numeric Correlations

| Variables | Correlation |
|---|---:|
| `tenure` ↔ `TotalCharges` | 0.83 |
| `MonthlyCharges` ↔ `TotalCharges` | 0.65 |
| `tenure` ↔ `MonthlyCharges` | 0.25 |

## Analytical Interpretation

The Contract × InternetService analysis showed compositional overlap between two characteristics associated with higher observed churn.

The strong `tenure`–`TotalCharges` relationship is structurally expected because `TotalCharges` accumulates over the customer's relationship with the company.

## Limitations

Correlation measures linear association and does not establish causation.

The overlap between contract type and internet service does not establish an independent effect of either variable on churn.

---

# Day 7 — Phase 2 Completion and Transition to Feature Analysis

**Phase:** Phase 2 — Exploratory Data Analysis

## What I Did

- Consolidated the EDA findings.
- Reviewed the highest-priority churn characteristics.
- Confirmed the EDA visualizations and written insights.
- Documented analytical limitations.
- Removed temporary EDA grouping columns where appropriate.
- Finalized the Phase 2 analytical conclusion.
- Used the EDA findings to determine the focus of Phase 3.

## Key EDA Findings

The strongest observed churn concentrations included:

- **0–12 months tenure:** 47.44%
- **Electronic check:** 45.29%
- **Month-to-month contract:** 42.71%
- **Fiber optic:** 41.89%

These findings did not establish causation. They were used to identify characteristics suitable for further segmentation and feature analysis.

## Phase 2 Outcome

**Phase 2 — Exploratory Data Analysis: Completed**

The analysis established the main churn patterns and provided the evidence needed to begin feature engineering.

---

# Day 8 — Phase 3: Feature Analysis — Tenure Band

**Phase:** Phase 3 — Feature Analysis

## What I Did

- Loaded the Phase 1 cleaned dataset.
- Created the `tenure_band` feature.
- Used fixed 10-month intervals with a final `50+` category.
- Validated category coverage and customer counts.
- Calculated churn rates across the tenure bands.
- Documented the feature definition, rationale, and limitations.

## Tenure Band Definition

| Tenure Band | Definition |
|---|---|
| `0-10` | 0 ≤ tenure < 10 |
| `10-20` | 10 ≤ tenure < 20 |
| `20-30` | 20 ≤ tenure < 30 |
| `30-40` | 30 ≤ tenure < 40 |
| `40-50` | 40 ≤ tenure < 50 |
| `50+` | tenure ≥ 50 |

## Findings

| Tenure Band | Customers | Churn Rate |
|---|---:|---:|
| 0-10 | 1,854 | 49.78% |
| 10-20 | 953 | 32.53% |
| 20-30 | 762 | 23.10% |
| 30-40 | 653 | 22.05% |
| 40-50 | 648 | 18.21% |
| 50+ | 2,173 | 9.11% |

The difference between the 0–10 and 50+ groups is **40.67 percentage points**.

## Validation

- 7,043 customers classified.
- 6 unique tenure bands.
- 0 null values.
- No customers left outside the defined intervals.
- Customer-level grain preserved.

## Interpretation

The earliest tenure group showed substantially higher observed churn than the longest-tenure group.

## Limitation

The tenure bands are analytical groupings and do not establish that tenure itself causes churn.

---

# Day 8 — Phase 3: Feature Analysis — Spend Tier

**Phase:** Phase 3 — Feature Analysis

## What I Did

- Reviewed the distribution of `MonthlyCharges`.
- Defined fixed spending ranges.
- Created the `spend_tier` feature.
- Validated category boundaries.
- Compared churn across spending tiers.
- Documented the feature definition and limitations.

## Spend Tier Definition

| Spend Tier | Definition |
|---|---|
| `10-30` | 10 ≤ MonthlyCharges < 30 |
| `30-50` | 30 ≤ MonthlyCharges < 50 |
| `50-70` | 50 ≤ MonthlyCharges < 70 |
| `70-90` | 70 ≤ MonthlyCharges < 90 |
| `90+` | MonthlyCharges ≥ 90 |

## Findings

| Spend Tier | Customers | Churn Rate |
|---|---:|---:|
| 10-30 | 1,653 | 9.80% |
| 30-50 | 641 | 31.05% |
| 50-70 | 1,158 | 20.21% |
| 70-90 | 1,847 | 37.95% |
| 90+ | 1,744 | 32.86% |

The 70–90 tier had the highest observed churn rate at **37.95%**.

## Interpretation

The relationship between monthly spending and churn was not strictly monotonic across the defined spending tiers.

## Limitation

The spending tiers are analytical groupings rather than official business pricing categories. The observed differences do not establish that higher monthly charges directly cause churn.

---

# Day 9 — Phase 3: Historical Risk Segment Validation

**Phase:** Phase 3 — Feature Analysis

## What I Did

- Combined the highest-priority churn characteristics identified during EDA.
- Created a separate `historical_risk_segment` for validation.
- Kept `Churn` out of the segment definition so that the historical churn rate could be measured.
- Calculated the segment's historical churn rate.
- Compared the segment with the overall and remaining customer populations.
- Used the result to support the criteria for the final active-customer `is_at_risk` feature.

## Historical Risk Segment Definition

The segment was defined using:

- Month-to-month contract
- Tenure ≤ 12 months
- Fiber optic internet
- Electronic check payment
- `MonthlyCharges` between 50 and 100 inclusive

## Findings

| Metric | Result |
|---|---:|
| Matching customers | 596 |
| Churned customers | 422 |
| Observed churn rate | 70.81% |
| Customer population | 8.46% |

### Comparison with Overall Population

Overall observed churn rate: **26.54%**

Historical risk segment churn rate: **70.81%**

The historical risk segment therefore had an observed churn rate approximately **2.7×** the overall customer churn rate.

### Comparison with Remaining Customers

| Group | Customers | Churn Rate |
|---|---:|---:|
| Remaining customers | 6,447 | 22.44% |
| Historical risk segment | 596 | 70.81% |

The historical risk segment had an observed churn rate approximately **3.2×** the remaining customer population.

The absolute difference was **48.37 percentage points**.

## Interpretation

The selected combination of characteristics identified a relatively small historical customer segment with substantially higher observed churn than the rest of the customer base.

This result was used to support the criteria for the final active-customer risk feature.

## Limitation

`historical_risk_segment` is an analytical validation segment, not a predictive model. The result demonstrates an observed association within this dataset and does not establish causation or guarantee future churn.

---

# Day 9 — Phase 3: Final Active At-Risk Feature

**Phase:** Phase 3 — Feature Analysis

## What I Did

- Created the final `is_at_risk` feature.
- Added `Churn = No` to the risk definition.
- Recalculated the at-risk customer population.
- Validated that every customer classified as `is_at_risk = 1` was active.
- Separated current active risk identification from historical risk validation.

## Final `is_at_risk` Definition

A customer is classified as `is_at_risk = 1` only when all of the following conditions are satisfied:

- Month-to-month contract
- Tenure ≤ 12 months
- Fiber optic internet
- Electronic check payment
- `MonthlyCharges` between 50 and 100 inclusive
- `Churn = No`

## Final Result

| `is_at_risk` | Customers | Active Customers |
|---:|---:|---:|
| 0 | 6,869 | 5,000 |
| 1 | 174 | 174 |

The final active at-risk segment contains **174 customers** and represents approximately **2.47%** of the total customer population.

## Interpretation

The final `is_at_risk` feature converts the validated historical characteristics into a current retention-oriented segment by excluding customers who have already churned.

This allows the analysis to focus on customers who are still active and may represent future retention opportunities.

## Limitation

`is_at_risk` is an analytical segmentation feature, not a predictive model. It does not estimate an individual customer's probability of churn and does not guarantee future churn.

`is_at_risk = 0` means only that the customer does not meet the complete defined criteria; it does not mean that the customer is safe from churn.

---

# Day 9 — Phase 3: Revenue at Risk

**Phase:** Phase 3 — Feature Analysis

## What I Did

- Defined `revenue_at_risk` using current recurring monthly charges.
- Restricted the calculation to `is_at_risk = 1` customers.
- Used `MonthlyCharges` rather than cumulative `TotalCharges`.
- Calculated the total current monthly recurring revenue exposure.
- Distinguished current revenue exposure from historical revenue associated with customers who have already churned.

## Definition

`revenue_at_risk` represents the current monthly recurring revenue exposure associated with active customers classified as `is_at_risk = 1`.

At customer level:

```text
revenue_at_risk = MonthlyCharges
```

for `is_at_risk = 1`.

For customers outside the at-risk segment:

```text
revenue_at_risk = 0
```

## Result

The 174 active at-risk customers collectively represent:

**13,933.80 in current monthly recurring revenue exposure.**

## Interpretation

The 13,933.80 figure represents current monthly recurring revenue that could potentially be exposed if the identified active at-risk customers churn.

It is not:

- revenue already lost;
- guaranteed future revenue loss; or
- an estimate of the probability of churn.

## Limitation

The metric assumes current `MonthlyCharges` represent the relevant recurring revenue exposure. It does not account for future pricing changes, upgrades, downgrades, cancellations, or the actual probability that each customer will churn.

---

# Week 2 Summary

## Completed

### Phase 2 — Exploratory Data Analysis

- Overall churn analysis.
- Contract-level churn analysis.
- Tenure-level churn analysis.
- Internet-service churn analysis.
- Payment-method churn analysis.
- Monthly-charge churn analysis.
- Numeric distribution analysis.
- Contract × InternetService cross-tabulation.
- Numeric correlation analysis.
- Correlation heatmap.
- EDA findings documentation.
- Analytical limitations documentation.
- EDA conclusion.
- Temporary EDA columns removed where appropriate.

### Phase 3 — Feature Analysis

- `tenure_band`
- `spend_tier`
- `historical_risk_segment`
- `is_at_risk`
- `revenue_at_risk`

## Key Findings

The strongest observed churn concentrations identified during EDA were:

- **0–12 months tenure:** 47.44%
- **Electronic check:** 45.29%
- **Month-to-month contract:** 42.71%
- **Fiber optic:** 41.89%

The historical risk segment containing the selected combination of characteristics had:

- **596 customers**
- **70.81% observed churn**
- **2.7× the overall churn rate**

After restricting the final risk feature to currently active customers:

- **174 active at-risk customers**
- **2.47% of the customer base**
- **13,933.80 current monthly recurring revenue exposure**

## Important Analytical Distinction

The project deliberately separates three concepts:

```text
Historical risk validation

596 customers
70.81% observed churn

        ↓

Supports selection of risk criteria

        ↓

Final active at-risk customers

174 customers
Churn = No

        ↓

Current recurring revenue exposure

13,933.80 per month
```

`historical_risk_segment` is therefore supporting analytical validation, while `is_at_risk` is the final current-customer feature.

## Key Analytical Principle

> EDA identifies patterns and associations in the data. These patterns should not be interpreted as causal relationships without further analysis.

Similarly, `is_at_risk` is a segmentation rule rather than a predictive model, and `revenue_at_risk` represents potential current revenue exposure rather than guaranteed future revenue loss.

## Week 2 Outcome

**Phase 2 — Exploratory Data Analysis: Completed**

**Phase 3 — Feature Analysis: Analytically Completed**

The analytical work for Phase 3 is complete. The remaining work is final output/export and documentation consistency verification.

## Final Phase 3 Feature Set

| Feature | Status |
|---|---|
| `tenure_band` | Completed |
| `spend_tier` | Completed |
| `is_at_risk` | Completed |
| `revenue_at_risk` | Completed |

`historical_risk_segment` is supporting validation logic and is not treated as a final feature in the feature dataset.

## Final Outputs

- `data/processed/telco_features.csv` — complete customer-level feature dataset.
- `outputs/exports/at_risk_customers.csv` — filtered business output containing the 174 active at-risk customers.

## Next

- Complete the final `telco_features.csv` export if not already completed.
- Perform final Phase 3 consistency checks.
- Ensure the Data Dictionary, Assumptions Log, Insights Log, notebook, and exported datasets use the same definitions.
- Commit the completed Phase 3 work.
- Begin the next project phase only after the documentation and outputs are synchronized.

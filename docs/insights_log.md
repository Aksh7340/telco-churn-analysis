# Insights Log — Telco Customer Churn Analysis

| Date | Phase | Tool | Finding | Business Significance |
|---|---|---|---|---|
| 2026-08-14 | Phase 1 — Data Cleaning | Python | 11 `TotalCharges` records contained whitespace-only values; all affected records had `tenure = 0`. | Required treatment before reliable monetary analysis. |

---

# Phase 2 — Exploratory Data Analysis (2026-08-18)

## Overall Churn

**Finding:** The dataset contains 7,043 customers, of whom 1,869 have churned.

- Churned customers: 1,869
- Retained customers: 5,174
- Overall churn rate: **26.54%**

**Interpretation:**

Approximately one in four customers in the dataset has churned. The retained-to-churned distribution is approximately 3:1 and should be considered when interpreting segment-level churn comparisons.

**Business Relevance:**

The overall churn rate provides the baseline against which customer segments can be compared.

---

## Contract Type

**Finding:** Churn varies substantially across contract types.

| Contract Type | Churn Rate |
|---|---:|
| Month-to-month | **42.71%** |
| One year | **11.27%** |
| Two year | **2.83%** |

The difference between month-to-month and two-year customers is **39.88 percentage points**.

**Interpretation:**

Contract structure shows one of the strongest observed associations with churn in the dataset.

**Business Relevance:**

Contract type should be examined further in combination with tenure, service type, and monthly charges to determine whether specific customer profiles represent higher-risk segments.

**Caution:**

This finding represents an observed association and does not establish that contract type causes churn.

---

## Tenure

**Finding:** Churn decreases substantially across tenure bands.

| Tenure Band | Churn Rate |
|---|---:|
| 0–12 months | **47.44%** |
| 13–24 months | **28.71%** |
| 25–48 months | **20.39%** |
| 49–72 months | **9.51%** |

The difference between the 0–12 month and 49–72 month groups is **37.93 percentage points**.

**Interpretation:**

The observed churn rate decreases monotonically across the tenure bands.

**Business Relevance:**

The early customer lifecycle represents a priority segment for further retention analysis.

**Caution:**

The tenure bands were created as temporary exploratory groupings and are not final engineered business segments.

---

## Internet Service

**Finding:** Churn varies substantially across internet service types.

| Internet Service | Churn Rate |
|---|---:|
| Fiber optic | **41.89%** |
| DSL | **18.96%** |
| No internet service | **7.40%** |

The difference between fiber-optic and no-internet customers is **34.49 percentage points**.

**Interpretation:**

Fiber-optic customers show a substantially higher observed churn rate than DSL and no-internet customers.

**Business Relevance:**

The fiber-optic segment warrants further investigation alongside contract type, tenure, and other service characteristics.

**Caution:**

The observed difference does not establish that internet service type causes churn.

---

## Payment Method

**Finding:** Electronic-check customers show substantially higher churn than the other payment groups.

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | **45.29%** |
| Mailed check | **19.11%** |
| Bank transfer (automatic) | **16.71%** |
| Credit card (automatic) | **15.24%** |

Electronic-check customers have a churn rate approximately **26 percentage points higher** than the other payment methods.

**Interpretation:**

Payment method is strongly associated with churn in the observed dataset.

**Business Relevance:**

The relationship should be investigated alongside contract type, tenure, and other customer characteristics before attributing the difference directly to payment method.

**Caution:**

Payment method may represent differences in customer composition rather than being a direct driver of churn.

---

## Monthly Charges

**Finding:** Churn varies across monthly-charge bands, but the relationship is not strictly monotonic.

| Monthly Charge Band | Churn Rate |
|---|---:|
| 0–50 | **15.70%** |
| 50–100 | **32.67%** |
| 100+ | **28.05%** |

The 50–100 group has the highest observed churn rate.

**Interpretation:**

The 50–100 charge band has a higher churn rate than both the lower and higher charge bands. Therefore, the relationship between monthly charges and churn cannot be described simply as "higher charges result in higher churn."

**Business Relevance:**

Monthly charges should be examined together with contract type, internet service, tenure, and other customer characteristics.

**Caution:**

The charge bands are exploratory groupings and are not final business segments.

---

## Contract × Internet Service

**Finding:** The cross-tabulation shows an overlap between contract type and internet service.

Fiber-optic customers are more concentrated in month-to-month contracts than in longer-term contracts.

**Interpretation:**

Two characteristics with high observed churn rates overlap within the customer population.

**Business Relevance:**

Phase 3 should investigate whether the elevated churn associated with fiber-optic service persists after accounting for contract type.

**Caution:**

The cross-tabulation identifies compositional overlap and does not establish causation or an independent effect.

---

## Numeric Variable Relationships

### Tenure × TotalCharges

**Correlation:** **0.83**

There is a strong positive correlation between `tenure` and `TotalCharges`.

**Interpretation:**

This relationship is structurally expected because `TotalCharges` accumulates over the customer's relationship with the company.

Therefore, the relationship should not be interpreted as an independent churn signal.

---

### MonthlyCharges × TotalCharges

**Correlation:** **0.65**

There is a moderate positive correlation between `MonthlyCharges` and `TotalCharges`.

**Interpretation:**

Customers with higher monthly charges tend to have higher cumulative charges.

---

### Tenure × MonthlyCharges

**Correlation:** **0.25**

There is a relatively weak positive linear relationship between `tenure` and `MonthlyCharges`.

**Interpretation:**

Longer-tenure customers do not necessarily have substantially higher monthly charges.

---

# Phase 2 Key Findings

The strongest observed churn concentrations identified during EDA are:

| Segment | Churn Rate |
|---|---:|
| 0–12 months tenure | **47.44%** |
| Electronic check | **45.29%** |
| Month-to-month contract | **42.71%** |
| Fiber optic | **41.89%** |

These findings identify several areas for deeper segment-level investigation.

---

# Analytical Caveat

All findings in this log represent observed associations within the dataset.

They should not be interpreted as causal relationships.

The next phase investigated combinations of customer characteristics to determine whether specific customer profiles represented meaningful high-risk segments.

---

# Phase 3 — Feature Analysis Insights (2026-08-19 to 2026-08-20)

## 1. Tenure and Churn

### Finding

Observed churn decreases substantially across the defined tenure bands.

| Tenure Band | Customers | Churn Rate |
|---|---:|---:|
| 0-10 | 1,854 | 49.78% |
| 10-20 | 953 | 32.53% |
| 20-30 | 762 | 23.10% |
| 30-40 | 653 | 22.05% |
| 40-50 | 648 | 18.21% |
| 50+ | 2,173 | 9.11% |

The difference between the 0–10 and 50+ groups is **40.67 percentage points**.

### Interpretation

Customers in the earliest tenure segment show substantially higher observed churn than customers with longer tenure.

### Limitation

The tenure bands represent analytical groupings and do not establish that tenure itself causes churn.

---

## 2. Monthly Charges and Churn

### Finding

Observed churn differs substantially across the defined spending tiers.

| Spend Tier | Customers | Churn Rate |
|---|---:|---:|
| 10-30 | 1,653 | 9.80% |
| 30-50 | 641 | 31.05% |
| 50-70 | 1,158 | 20.21% |
| 70-90 | 1,847 | 37.95% |
| 90+ | 1,744 | 32.86% |

The 70–90 tier has the highest observed churn rate at **37.95%**, while the 10–30 tier has the lowest at **9.80%**.

### Interpretation

The relationship between monthly charges and churn is not strictly monotonic across the defined spending tiers.

### Limitation

The spending tiers are analytical groupings rather than official business pricing categories. The observed differences should not be interpreted as evidence that higher monthly charges directly cause churn.

---

## 3. Historical Risk Segment Validation

### Finding

A historical risk segment was defined using:

- Month-to-month contract
- Tenure ≤ 12 months
- Fiber optic internet
- Electronic check payment
- `MonthlyCharges` between 50 and 100 inclusive

This segment was used to evaluate whether the selected combination of characteristics was associated with elevated historical churn.

The segment contains **596 customers**.

Of these customers:

- 422 have churned.
- Observed churn rate = **70.81%**.
- Segment size = **8.46%** of the customer population.

### Comparison with Overall Population

Overall observed churn rate:

**26.54%**

Historical risk segment observed churn rate:

**70.81%**

The historical risk segment therefore has an observed churn rate approximately **2.7×** the overall customer churn rate.

### Comparison with the Remaining Customer Population

| Group | Customers | Churn Rate |
|---|---:|---:|
| Remaining customers | 6,447 | 22.44% |
| Historical risk segment | 596 | 70.81% |

The historical risk segment has an observed churn rate approximately **3.2×** the remaining customer population.

The absolute difference between the two groups is **48.37 percentage points**.

### Interpretation

The selected combination of customer characteristics identifies a relatively small historical customer segment with substantially higher observed churn than the rest of the customer base.

This result was used to support the selection of the criteria for the final active-customer `is_at_risk` feature.

### Limitation

`historical_risk_segment` is an analytical validation segment, not a predictive model. The result demonstrates an observed association within this dataset and does not establish causation or guarantee future churn.

---

## 4. Active At-Risk Customer Segment

### Finding

The final `is_at_risk` feature identifies currently active customers who meet all of the following conditions:

- Month-to-month contract
- Tenure ≤ 12 months
- Fiber optic internet
- Electronic check payment
- `MonthlyCharges` between 50 and 100 inclusive
- `Churn = No`

The final segment contains **174 currently active customers**.

| `is_at_risk` | Customers | Active Customers |
|---:|---:|---:|
| 0 | 6,869 | 5,000 |
| 1 | 174 | 174 |

The active at-risk segment represents approximately **2.47%** of the total customer population.

### Interpretation

The final `is_at_risk` feature converts the historical risk characteristics into a current retention-oriented customer segment by excluding customers who have already churned.

This allows the analysis to focus on customers who are still generating revenue and may represent future retention opportunities.

### Limitation

`is_at_risk` is an analytical segmentation feature, not a predictive model. It identifies currently active customers matching the defined criteria but does not estimate an individual customer's probability of churn.

`is_at_risk = 0` should not be interpreted as meaning that a customer is safe or has zero churn risk.

---

## 5. Revenue at Risk

### Finding

`revenue_at_risk` represents the current monthly recurring revenue exposure associated with customers where `is_at_risk = 1`.

The 174 active at-risk customers collectively represent:

**13,933.80 in current monthly recurring revenue exposure.**

The calculation uses `MonthlyCharges` rather than `TotalCharges`.

### Interpretation

The 13,933.80 figure represents the current monthly recurring revenue exposure that could potentially be affected if the identified active at-risk customers churn.

It is therefore a measure of **potential revenue exposure**, not revenue already lost and not guaranteed future revenue loss.

### Limitation

The metric is based on the dataset's `MonthlyCharges` field. It does not account for future changes in pricing, upgrades, downgrades, cancellations before the next billing period, or the actual probability that each active at-risk customer will churn.

Revenue associated with customers who have already churned is treated as a separate historical churn metric and is not included in `revenue_at_risk`.

---

# Phase 3 Feature Status

| Feature / Analysis | Status |
|---|---|
| `tenure_band` | Completed |
| `spend_tier` | Completed |
| `historical_risk_segment` | Completed — historical validation |
| `is_at_risk` | Completed — final active-customer feature |
| `revenue_at_risk` | Completed |

## Phase 3 Status

**Phase 3 — Feature Analysis: Complete**

The final Phase 3 customer-level features are:

- `tenure_band`
- `spend_tier`
- `is_at_risk`
- `revenue_at_risk`

`historical_risk_segment` is supporting analytical validation and should not be treated as a final feature in the feature dataset.

---

# Phase 3 Output Datasets

## `telco_features.csv`

The complete customer-level Phase 3 feature dataset.

Expected contents:

- Full customer population
- `tenure_band`
- `spend_tier`
- `is_at_risk`
- `revenue_at_risk`

## `at_risk_customers.csv`

A derived business output containing only the **174 currently active customers** where:

```text
is_at_risk = 1
```

The exported segment preserves the final current-risk definition and represents **13,933.80 in total current monthly recurring revenue exposure**.

The file is a retention-focused output and is not a replacement for the complete `telco_features.csv` dataset.

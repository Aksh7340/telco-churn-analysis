# Data Dictionary — Telco Customer Churn Analysis

---

# 1. Dataset Overview

| Attribute | Value |
|---|---|
| Dataset | IBM Telco Customer Churn Dataset |
| Dataset Grain | One row represents one customer |
| Number of Rows | 7,043 |
| Number of Columns | 21 raw columns |
| Target Variable | `Churn` |
| Data Level | Customer-level |
| Raw Dataset | `data/raw/WA_Fn-UseC_-Telco-Customer-Churn.csv` |
| Cleaned Dataset | `data/processed/telco_cleaned.csv` |
| Final Feature Dataset | `data/processed/telco_features.csv` |
| At-Risk Customer Export | `outputs/exports/at_risk_customers.csv` |

---

# 2. Data Quality Profile

The raw dataset was profiled before analytical transformations.

| Check | Result |
|---|---:|
| Rows | 7,043 |
| Columns | 21 |
| Duplicate Rows | 0 |
| Standard Null Values | 0 |
| Empty / Whitespace-only Values | 11 in `TotalCharges` |
| Raw Dataset Modified | No |

## Important Data Quality Finding

The initial null-value check returned zero missing values because the 11 affected
`TotalCharges` records contain whitespace characters rather than standard
missing-value representations.

A whitespace check identified 11 records where `TotalCharges` contains an
empty/whitespace-only value.

All 11 affected records have:

- `tenure = 0`
- `Churn = No`
- Valid `MonthlyCharges` values

During Phase 1 data cleaning:

- All 11 whitespace-only `TotalCharges` values were treated as `0` for this analysis.
- `TotalCharges` was converted from `object` to `float64`.
- No raw customer records were removed.

---

# 3. Raw Data Dictionary

| Column Name | Data Type | Business Definition | Nulls | Values / Range |
|---|---|---|---:|---|
| `customerID` | object | Unique identifier assigned to each customer. | 0 | Unique alphanumeric customer IDs |
| `gender` | object | Customer's reported gender. | 0 | Male, Female |
| `SeniorCitizen` | int64 | Indicates whether the customer is a senior citizen. | 0 | 0 = No, 1 = Yes |
| `Partner` | object | Indicates whether the customer has a partner. | 0 | Yes, No |
| `Dependents` | object | Indicates whether the customer has dependents. | 0 | Yes, No |
| `tenure` | int64 | Number of months the customer has remained with the company. | 0 | 0–72 months |
| `PhoneService` | object | Indicates whether the customer has phone service. | 0 | Yes, No |
| `MultipleLines` | object | Indicates whether the customer has multiple phone lines. | 0 | Yes, No, No phone service |
| `InternetService` | object | Type of internet service subscribed to by the customer. | 0 | DSL, Fiber optic, No |
| `OnlineSecurity` | object | Indicates whether the customer subscribes to online security service. | 0 | Yes, No, No internet service |
| `OnlineBackup` | object | Indicates whether the customer subscribes to online backup service. | 0 | Yes, No, No internet service |
| `DeviceProtection` | object | Indicates whether the customer subscribes to device protection service. | 0 | Yes, No, No internet service |
| `TechSupport` | object | Indicates whether the customer subscribes to technical support service. | 0 | Yes, No, No internet service |
| `StreamingTV` | object | Indicates whether the customer subscribes to streaming TV service. | 0 | Yes, No, No internet service |
| `StreamingMovies` | object | Indicates whether the customer subscribes to streaming movie service. | 0 | Yes, No, No internet service |
| `Contract` | object | Type and duration of the customer's service contract. | 0 | Month-to-month, One year, Two year |
| `PaperlessBilling` | object | Indicates whether the customer uses paperless billing. | 0 | Yes, No |
| `PaymentMethod` | object | Payment method used by the customer. | 0 | Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic) |
| `MonthlyCharges` | float64 | Amount charged to the customer per month. | 0 | Observed range: 18.25–118.75 |
| `TotalCharges` | object | Total amount charged to the customer over their relationship with the company. | 0 | Numeric-looking values stored as text; 11 whitespace-only values identified |
| `Churn` | object | Indicates whether the customer has left the company. | 0 | Yes, No |

---

# 4. Column Groups

## Customer Demographics

- `customerID`
- `gender`
- `SeniorCitizen`
- `Partner`
- `Dependents`

## Customer Lifecycle

- `tenure`
- `Contract`

## Phone Services

- `PhoneService`
- `MultipleLines`

## Internet Services

- `InternetService`
- `OnlineSecurity`
- `OnlineBackup`
- `DeviceProtection`
- `TechSupport`
- `StreamingTV`
- `StreamingMovies`

## Billing and Payment

- `PaperlessBilling`
- `PaymentMethod`
- `MonthlyCharges`
- `TotalCharges`

## Target Variable

- `Churn`

---

# 5. Target Variable

The primary target variable for this project is `Churn`.

| Value | Meaning |
|---|---|
| `Yes` | Customer has churned / left the company |
| `No` | Customer has not churned |

`Churn` is used to evaluate historical churn differences across customer
segments and engineered features.

For the final `is_at_risk` feature, `Churn = No` is explicitly required because
the feature identifies currently active customers who may represent future
churn and current revenue exposure.

---

# 6. Important Data Notes

## `customerID`

This column uniquely identifies customers and should not be treated as an
analytical measure.

---

## `SeniorCitizen`

The raw dataset stores this field numerically:

- `0` = Customer is not a senior citizen
- `1` = Customer is a senior citizen

No transformation was required during Phase 1.

---

## `tenure`

`tenure` represents the number of months a customer has remained with the
company.

It is a customer lifecycle variable and was used during Phase 3 to create the
analytical `tenure_band` feature.

---

## `MonthlyCharges`

`MonthlyCharges` represents the customer's current monthly service charge.

It was used during Phase 2 spending analysis and during Phase 3 to:

- create `spend_tier`;
- identify the monthly-charge component of the risk criteria; and
- calculate `revenue_at_risk` for active at-risk customers.

The source dataset does not specify the currency of the monetary fields.
Therefore, this project does not label these values as INR/₹ or any other
specific currency.

---

## `TotalCharges`

`TotalCharges` represents the total amount charged to a customer over their
relationship with the company.

In the raw dataset, this column was stored as `object` even though its values
represent monetary amounts.

Initial profiling identified 11 whitespace-only values. All 11 affected records
had `tenure = 0`.

During Phase 1 data cleaning:

- The 11 whitespace-only values were treated as `0` for this analysis.
- `TotalCharges` was converted from `object` to `float64`.
- The cleaned column was validated after transformation.

The source dataset does not specify a currency for this field.

---

## `Churn`

`Churn` is the project's target variable and represents whether the customer
has left the company.

It is used to evaluate historical churn differences across customer segments
and engineered features.

For the final `is_at_risk` feature, `Churn = No` is explicitly required because
the feature identifies currently active customers who may represent future
churn and current revenue exposure.

---

# 7. Data Grain

The analytical grain of the raw dataset is:

> **One row = one customer.**

Customer-level analysis should preserve this grain unless a different analytical
grain is explicitly defined.

All Phase 3 engineered features preserve the customer-level grain.

Both final output datasets are derived from the same customer-level grain:

- `data/processed/telco_features.csv`
- `outputs/exports/at_risk_customers.csv`

---

# 8. Engineered Features

The following fields are not part of the raw dataset. They were created during
**Phase 3 — Feature Analysis**.

## Final customer-level features

1. `tenure_band`
2. `spend_tier`
3. `is_at_risk`
4. `revenue_at_risk`

## Supporting analytical logic

`historical_risk_segment` is a validation segment used to test the selected
risk criteria against historical churn.

It is **not** treated as a final feature and is not required in
`telco_features.csv`.

---

# 8.1 `tenure_band`

`tenure_band` converts the continuous `tenure` variable into fixed analytical
lifecycle segments.

## Definition

| Band | Definition |
|---|---|
| `0-10` | 0 ≤ tenure < 10 |
| `10-20` | 10 ≤ tenure < 20 |
| `20-30` | 20 ≤ tenure < 30 |
| `30-40` | 30 ≤ tenure < 40 |
| `40-50` | 40 ≤ tenure < 50 |
| `50+` | tenure ≥ 50 |

The feature uses fixed 10-month intervals with a final `50+` group.

## Validation

- 7,043 customers classified
- 6 unique categories
- 0 null values
- No customers left unclassified
- Customer-level grain preserved

## Observed Churn

| Tenure Band | Customers | Churn Rate |
|---|---:|---:|
| `0-10` | 1,854 | 49.78% |
| `10-20` | 953 | 32.53% |
| `20-30` | 762 | 23.10% |
| `30-40` | 653 | 22.05% |
| `40-50` | 648 | 18.21% |
| `50+` | 2,173 | 9.11% |

The difference between the `0-10` and `50+` groups is **40.67 percentage
points**.

## Interpretation

Customers in the earliest tenure segment show substantially higher observed
churn than customers with longer tenure.

## Limitation

The tenure bands are analytical groupings and do not establish that tenure
itself causes churn.

Customers close to a band boundary may also be grouped separately despite
having similar tenure values.

---

# 8.2 `spend_tier`

`spend_tier` converts `MonthlyCharges` into interpretable spending segments.

## Definition

| Tier | Definition |
|---|---|
| `10-30` | 10 ≤ MonthlyCharges < 30 |
| `30-50` | 30 ≤ MonthlyCharges < 50 |
| `50-70` | 50 ≤ MonthlyCharges < 70 |
| `70-90` | 70 ≤ MonthlyCharges < 90 |
| `90+` | MonthlyCharges ≥ 90 |

The observed minimum `MonthlyCharges` is **18.25**.

## Validation

- 7,043 customers classified
- 5 unique categories
- No unclassified customers
- All observed values fall within the intended ranges
- Customer-level grain preserved

## Observed Churn

| Spend Tier | Customers | Churn Rate |
|---|---:|---:|
| `10-30` | 1,653 | 9.80% |
| `30-50` | 641 | 31.05% |
| `50-70` | 1,158 | 20.21% |
| `70-90` | 1,847 | 37.95% |
| `90+` | 1,744 | 32.86% |

The `70-90` tier has the highest observed churn rate at **37.95%**.

## Interpretation

The relationship between monthly charges and churn is not strictly monotonic
across the defined spending tiers.

## Limitation

The spending tiers are analytical groupings rather than official business
pricing categories.

The observed differences should not be interpreted as evidence that higher
monthly charges directly cause churn.

---

# 8.3 `historical_risk_segment`

`historical_risk_segment` is a temporary analytical segment used to validate the
selected at-risk criteria against the historical `Churn` outcome.

It is **not a final feature** and is not used to calculate `revenue_at_risk`.

## Definition

The segment is defined using all of the following:

- `Contract = Month-to-month`
- `tenure <= 12`
- `InternetService = Fiber optic`
- `PaymentMethod = Electronic check`
- `MonthlyCharges` between 50 and 100, inclusive

Unlike the final `is_at_risk` feature, `historical_risk_segment` does **not**
require `Churn = No`.

## Historical Validation Result

| Metric | Result |
|---|---:|
| Matching customers | 596 |
| Churned customers | 422 |
| Observed churn rate | 70.81% |
| Customer population | 8.46% |

Overall observed churn rate:

**26.54%**

Historical risk segment observed churn rate:

**70.81%**

Observed risk lift:

**Approximately 2.67× the overall churn rate.**

## Comparison with Remaining Customers

| Group | Customers | Churn Rate |
|---|---:|---:|
| Remaining customers | 6,447 | 22.44% |
| Historical risk segment | 596 | 70.81% |

The historical risk segment has an observed churn rate approximately **3.2×**
the remaining customer population.

The absolute difference is **48.37 percentage points**.

## Interpretation

The selected combination of characteristics identifies a relatively small
historical customer segment with substantially higher observed churn than the
rest of the customer base.

This result supports the criteria used to construct the final active-customer
`is_at_risk` feature.

## Limitation

`historical_risk_segment` is an analytical validation segment, not a predictive
model.

The result demonstrates an observed association within this dataset and does
not establish causation or guarantee future churn.

---

# 8.4 `is_at_risk`

`is_at_risk` is a binary customer-level analytical segmentation feature designed
to identify **currently active customers** who match the selected
characteristics associated with elevated historical churn.

## Definition

A customer is classified as `is_at_risk = 1` only when **all** conditions are
satisfied:

- `Contract = Month-to-month`
- `tenure <= 12`
- `InternetService = Fiber optic`
- `PaymentMethod = Electronic check`
- `MonthlyCharges` between 50 and 100, inclusive
- `Churn = No`

## Values

| Value | Meaning |
|---:|---|
| `0` | Customer does not meet all defined active at-risk criteria |
| `1` | Customer is active and meets all defined active at-risk criteria |

## Final Active At-Risk Population

| `is_at_risk` | Customers | Active Customers |
|---:|---:|---:|
| `0` | 6,869 | 5,000 |
| `1` | 174 | 174 |

The final `is_at_risk = 1` segment contains **174 currently active customers**,
representing approximately **2.47% of the total customer population**.

## Interpretation

The final `is_at_risk` feature converts the historically validated risk
characteristics into a current retention-oriented customer segment by
excluding customers who have already churned.

This allows the analysis to focus on customers who are still active and may
represent future retention opportunities.

## Limitation

`is_at_risk` is an analytical segmentation feature, not a predictive model.

It identifies currently active customers who match the defined criteria but
does not estimate an individual customer's probability of churn and does not
guarantee future churn.

Because `Churn = No` is part of the feature definition, churn rate is not used
as a validation metric for the final feature.

Historical churn validation is performed separately through
`historical_risk_segment`.

---

# 8.5 `revenue_at_risk`

`revenue_at_risk` represents the **current monthly recurring revenue exposure**
associated with active customers classified as `is_at_risk = 1`.

It is a customer-level feature derived from `MonthlyCharges`.

## Customer-Level Logic

For customers where:

```text
is_at_risk = 1
```

the value is:

```text
revenue_at_risk = MonthlyCharges
```

For all other customers:

```text
revenue_at_risk = 0
```

## Final Result

The 174 active at-risk customers collectively represent:

**13,933.80 in current monthly recurring revenue exposure.**

This is calculated as:

```text
SUM(revenue_at_risk)
```

across the full customer-level feature dataset.

## Business Interpretation

The value represents the current monthly recurring charge exposure associated
with customers identified as active and at risk.

It represents **potential future revenue exposure if those customers churn**.

It is not:

- revenue already lost;
- realized historical revenue loss; or
- guaranteed future revenue loss.

## Distinction from Churned Revenue

Revenue associated with customers who have already churned is a separate
historical measure and is **not included** in `revenue_at_risk`.

The sum of `MonthlyCharges` for customers where:

```text
Churn = Yes
```

represents the monthly charge base associated with customers who have already
churned. It should not be interpreted as current revenue at risk.

## Limitation

`revenue_at_risk` is based on the dataset's `MonthlyCharges` field and therefore
represents the current monthly charge exposure captured by this dataset.

It does not account for:

- future changes in customer charges;
- upgrades;
- downgrades;
- cancellations before the next billing period; or
- the actual probability that an individual customer will churn.

The source dataset does not specify a currency for `MonthlyCharges`, so the
project intentionally reports the value without a currency symbol.

---

# 9. Phase 1 Cleaning Transformation Summary

| Column | Raw Data Type | Final Data Type | Issue Identified | Transformation |
|---|---|---|---|---|
| `TotalCharges` | object | float64 | 11 whitespace-only values and numeric values stored as text | Replaced 11 whitespace-only values with 0 and converted the column to numeric |

## Validation

- Row count remained 7,043.
- Column count remained 21.
- `TotalCharges` became `float64`.
- No standard null values remained.
- No blank `TotalCharges` values remained.
- No duplicate rows were present after cleaning.
- No duplicate customer IDs were present after cleaning.
- No customer records were removed during Phase 1.

---

# 10. Raw vs Cleaned State

| Attribute | Raw Dataset | Cleaned Dataset |
|---|---:|---:|
| Rows | 7,043 | 7,043 |
| Columns | 21 | 21 |
| `TotalCharges` dtype | object | float64 |
| Blank `TotalCharges` values | 11 | 0 |
| Standard null values | 0 | 0 |
| Duplicate rows | 0 | 0 |
| Duplicate customer IDs | 0 | 0 |

---

# 11. Phase 1 Data Quality Validation

| Validation Check | Result |
|---|---:|
| Rows | 7,043 |
| Columns | 21 |
| Standard Null Values | 0 |
| Blank `TotalCharges` Values | 0 |
| Duplicate Rows | 0 |
| Duplicate Customer IDs | 0 |
| Logical Inconsistencies | 0 identified |
| Invalid Numeric Values | 0 |

The cleaned dataset was exported to:

```text
data/processed/telco_cleaned.csv
```

The exported dataset was reloaded and verified to confirm that the cleaned
output retained the expected structure and data quality.

---

# 12. Phase 3 Feature Status

| Feature / Analysis | Status | Role |
|---|---|---|
| `tenure_band` | ✅ Completed | Final feature |
| `spend_tier` | ✅ Completed | Final feature |
| `historical_risk_segment` | ✅ Completed | Supporting historical validation |
| `is_at_risk` | ✅ Completed | Final active-customer risk feature |
| `revenue_at_risk` | ✅ Completed | Final revenue-exposure feature |

## Phase 3 Status

**Phase 3 — Feature Analysis: Complete**

The final customer-level features are:

- `tenure_band`
- `spend_tier`
- `is_at_risk`
- `revenue_at_risk`

`historical_risk_segment` is supporting analytical validation and is not treated
as a final production feature.

---

# 13. Final Output Datasets

## `telco_features.csv`

**Location**

```text
data/processed/telco_features.csv
```

**Purpose**

Complete customer-level feature dataset for downstream analytical work.

The dataset preserves the customer-level analytical grain and contains the
final Phase 3 engineered features.

Expected final feature columns:

```text
customerID
tenure_band
spend_tier
is_at_risk
revenue_at_risk
```

The full customer population remains represented in this dataset.

---

## `at_risk_customers.csv`

**Location**

```text
outputs/exports/at_risk_customers.csv
```

**Purpose**

Filtered business output containing only customers where:

```text
is_at_risk = 1
```

The export represents the **current active at-risk customer population**.

### Current Output

| Metric | Result |
|---|---:|
| Active at-risk customers | 174 |
| Share of total customer population | 2.47% |
| Current monthly recurring revenue exposure | 13,933.80 |

The export contains the customer-level attributes required for retention
analysis.

It is a derived business output and **not a replacement for**
`telco_features.csv`.

The historical 596-customer `historical_risk_segment` is **not** exported as
the current at-risk customer list.

---

# 14. Historical Risk vs Current At-Risk Definition

The project deliberately separates historical validation from current
customer-risk identification.

```text
Historical Risk Validation
        ↓
historical_risk_segment
596 customers
70.81% observed churn
        ↓
Supports selected risk criteria
        ↓
Add Churn = No
        ↓
is_at_risk
174 active customers
        ↓
MonthlyCharges
        ↓
revenue_at_risk
13,933.80 monthly exposure
```

This distinction prevents customers who have already churned from being
included in the current revenue-at-risk calculation.

---

# 15. Final Feature Definition Summary

| Feature | Definition | Business Purpose |
|---|---|---|
| `tenure_band` | Fixed analytical tenure intervals | Customer lifecycle segmentation |
| `spend_tier` | Fixed monthly-charge intervals | Customer spending segmentation |
| `is_at_risk` | Active customers satisfying all selected risk criteria | Identify current retention opportunities |
| `revenue_at_risk` | `MonthlyCharges` for active at-risk customers; otherwise 0 | Quantify current monthly recurring revenue exposure |

---

# 16. Data Dictionary Maintenance

This document should be updated when:

- new analytical fields are introduced;
- an existing feature definition changes;
- the final feature dataset structure changes; or
- important assumptions introduced during later analytical phases materially
  affect the interpretation of existing fields.

The Data Dictionary should remain synchronized with:

- `notebooks/01_data_cleaning.ipynb`
- `notebooks/02_eda.ipynb`
- `notebooks/03_feature_analysis.ipynb`
- `data/processed/telco_cleaned.csv`
- `data/processed/telco_features.csv`
- `outputs/exports/at_risk_customers.csv`
- `docs/assumptions_log.md`
- `docs/insights_log.md`
- `docs/journal/week2.md`

The raw dataset remains unchanged and is preserved separately from the
processed datasets.

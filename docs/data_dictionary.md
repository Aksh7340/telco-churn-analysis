# Data Dictionary — Telco Customer Churn Analysis

## 1. Dataset Overview

| Attribute | Value |
|---|---|
| Dataset | IBM Telco Customer Churn Dataset |
| Dataset Grain | One row represents one customer |
| Number of Rows | 7,043 |
| Number of Columns | 21 |
| Target Variable | `Churn` |
| Data Level | Customer-level |
| Raw Dataset | `data/raw/WA_Fn-UseC_-Telco-Customer-Churn.csv` |

---

## 2. Data Quality Profile

The raw dataset was profiled before analytical transformations.

| Check | Result |
|---|---:|
| Rows | 7,043 |
| Columns | 21 |
| Duplicate Rows | 0 |
| Null Values | 0 |
| Empty / Whitespace-only Values | 11 in `TotalCharges` |
| Raw Dataset Modified | No |

### Important Data Quality Finding

The initial null-value check returned zero missing values because the 11 affected
`TotalCharges` records contain whitespace characters rather than standard
missing-value representations.

A whitespace check identified 11 records where `TotalCharges` contains an
empty/whitespace-only value.

All 11 affected records have:

- `tenure = 0`
- `Churn = No`
- Valid `MonthlyCharges` values

These records were handled during the Phase 1 data-cleaning process.

All 11 whitespace-only `TotalCharges` values were treated as 0 for this
analysis, and `TotalCharges` was converted from `object` to `float64`.

---

## 3. Raw Data Dictionary

| Column Name | Data Type | Business Definition | Nulls | Values / Range |
|---|---|---|---:|---|
| `customerID` | object | Unique identifier assigned to each customer. | 0 | Unique alphanumeric customer IDs |
| `gender` | object | Customer's reported gender. | 0 | `Male`, `Female` |
| `SeniorCitizen` | int64 | Indicates whether the customer is a senior citizen. | 0 | `0` = No, `1` = Yes |
| `Partner` | object | Indicates whether the customer has a partner. | 0 | `Yes`, `No` |
| `Dependents` | object | Indicates whether the customer has dependents. | 0 | `Yes`, `No` |
| `tenure` | int64 | Number of months the customer has remained with the company. | 0 | `0–72` months |
| `PhoneService` | object | Indicates whether the customer has phone service. | 0 | `Yes`, `No` |
| `MultipleLines` | object | Indicates whether the customer has multiple phone lines. | 0 | `Yes`, `No`, `No phone service` |
| `InternetService` | object | Type of internet service subscribed to by the customer. | 0 | `DSL`, `Fiber optic`, `No` |
| `OnlineSecurity` | object | Indicates whether the customer subscribes to online security service. | 0 | `Yes`, `No`, `No internet service` |
| `OnlineBackup` | object | Indicates whether the customer subscribes to online backup service. | 0 | `Yes`, `No`, `No internet service` |
| `DeviceProtection` | object | Indicates whether the customer subscribes to device protection service. | 0 | `Yes`, `No`, `No internet service` |
| `TechSupport` | object | Indicates whether the customer subscribes to technical support service. | 0 | `Yes`, `No`, `No internet service` |
| `StreamingTV` | object | Indicates whether the customer subscribes to streaming TV service. | 0 | `Yes`, `No`, `No internet service` |
| `StreamingMovies` | object | Indicates whether the customer subscribes to streaming movie service. | 0 | `Yes`, `No`, `No internet service` |
| `Contract` | object | Type and duration of the customer's service contract. | 0 | `Month-to-month`, `One year`, `Two year` |
| `PaperlessBilling` | object | Indicates whether the customer uses paperless billing. | 0 | `Yes`, `No` |
| `PaymentMethod` | object | Payment method used by the customer. | 0 | `Electronic check`, `Mailed check`, `Bank transfer (automatic)`, `Credit card (automatic)` |
| `MonthlyCharges` | float64 | Amount charged to the customer per month. | 0 | Observed range: `18.25–118.75` |
| `TotalCharges` | object | Total amount charged to the customer over their relationship with the company. | 0 | Numeric-looking values stored as text; 11 whitespace-only values identified |
| `Churn` | object | Indicates whether the customer has left the company. | 0 | `Yes`, `No` |

---

## 4. Column Groups

### Customer Demographics

- `customerID`
- `gender`
- `SeniorCitizen`
- `Partner`
- `Dependents`

### Customer Lifecycle

- `tenure`
- `Contract`

### Phone Services

- `PhoneService`
- `MultipleLines`

### Internet Services

- `InternetService`
- `OnlineSecurity`
- `OnlineBackup`
- `DeviceProtection`
- `TechSupport`
- `StreamingTV`
- `StreamingMovies`

### Billing and Payment

- `PaperlessBilling`
- `PaymentMethod`
- `MonthlyCharges`
- `TotalCharges`

### Target Variable

- `Churn`

---

## 5. Target Variable

The primary target variable for this project is `Churn`.

| Value | Meaning |
|---|---|
| `Yes` | Customer has churned / left the company |
| `No` | Customer has not churned |

---

## 6. Important Data Notes

### `customerID`

This column uniquely identifies customers.

It is used as the customer-level identifier and should not be treated as an
analytical measure.

---

### `SeniorCitizen`

The raw dataset stores this field numerically:

- `0` = Customer is not a senior citizen
- `1` = Customer is a senior citizen

No transformation was required during Phase 1.

---

### `tenure`

`tenure` represents the number of months a customer has remained with the
company.

It is a customer lifecycle variable and may later be used to create analytical
tenure groups during feature engineering.

---

### `MonthlyCharges`

`MonthlyCharges` represents the customer's current monthly service charge.

It will be used for spending analysis and for estimating recurring revenue
exposure.

The source dataset does not specify the currency of the monetary fields.
Therefore, this project will not label these values as INR/₹.

---

### `TotalCharges`

`TotalCharges` represents the total amount charged to a customer over their
relationship with the company.

In the raw dataset, this column was stored as `object` even though its values
represent monetary amounts.

Initial profiling identified 11 whitespace-only values.

All 11 affected records had `tenure = 0`.

During Phase 1 data cleaning:

- The 11 whitespace-only values were treated as 0 for this analysis.
- `TotalCharges` was converted from `object` to `float64`.
- The cleaned column was validated after transformation.

The source dataset does not specify a currency for this field.

---

### `Churn`

`Churn` is the project's target variable and represents whether the customer
has left the company.

---

## 7. Data Grain

The analytical grain of the raw dataset is:

> One row = one customer.

Customer-level analysis should therefore preserve this grain unless a
different analytical grain is explicitly defined.

---

## 8. Engineered Features

The following fields are **not part of the raw dataset**.

They will be created later during the feature-analysis phase:

- `tenure_band`
- `spend_tier`
- `is_at_risk`
- `revenue_at_risk`

Their definitions and calculation logic will be documented after they are
created and validated.

---

## 9. Data Dictionary Status

**Status:** Raw dataset dictionary completed and updated with Phase 1 cleaning
information.

The dictionary documents:

- The original 21 columns in the raw dataset.
- The raw data types and observed values/ranges.
- The identified `TotalCharges` data-quality issue.
- The Phase 1 transformation applied to `TotalCharges`.
- The validated raw-versus-cleaned state.

Engineered features such as `tenure_band`, `spend_tier`, `is_at_risk`, and
`revenue_at_risk` will be documented after they are created and validated.

---

## 10. Phase 1 Cleaning Transformation Summary

The raw dataset was profiled before transformation. The following cleaning
decision was applied during Phase 1.

| Column | Raw Data Type | Final Data Type | Issue Identified | Transformation |
|---|---|---|---|---|
| `TotalCharges` | object | float64 | 11 whitespace-only values and numeric values stored as text | Replaced 11 whitespace-only values with 0 and converted the column to numeric |

### Validation

After transformation:

- Row count remained 7,043.
- Column count remained 21.
- `TotalCharges` data type became `float64`.
- No null values remained.
- No blank `TotalCharges` values remained.
- No duplicate rows were present after cleaning.
- No duplicate customer IDs were present after cleaning.
- No customer records were removed during Phase 1.

### Raw vs Cleaned State

| Attribute | Raw Dataset | Cleaned Dataset |
|---|---:|---:|
| Rows | 7,043 | 7,043 |
| Columns | 21 | 21 |
| `TotalCharges` dtype | object | float64 |
| Blank `TotalCharges` values | 11 | 0 |
| Null values | 0 | 0 |
| Duplicate rows | 0 | 0 |
| Duplicate customer IDs | 0 | 0 |

---

## 11. Phase 1 Data Quality Validation

The cleaned dataset was independently validated after transformation.

| Validation Check | Result |
|---|---:|
| Rows | 7,043 |
| Columns | 21 |
| Null Values | 0 |
| Blank `TotalCharges` Values | 0 |
| Duplicate Rows | 0 |
| Duplicate Customer IDs | 0 |
| Logical Inconsistencies | 0 identified |
| Invalid Numeric Values | 0 |

The cleaned dataset was exported to:

`data/processed/telco_cleaned.csv`

The exported dataset was then reloaded and verified to confirm that the
cleaned output retained the expected structure and data quality.

---

## 12. Data Dictionary Maintenance

This document will be updated when new analytical fields are introduced.

Future updates will include:

- Feature-engineered fields created during Phase 3.
- Definitions and calculation logic for engineered features.
- Any additional transformations that materially affect the analytical
  dataset.
- Important assumptions introduced during later analytical phases.

The raw dataset remains unchanged and is preserved separately from the
processed dataset.
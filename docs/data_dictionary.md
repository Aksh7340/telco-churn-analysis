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

These records will be handled during the data-cleaning phase.

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
| `MonthlyCharges` | float64 | Amount charged to the customer per month. | 0 | Approximately `18.25–118.75` |
| `TotalCharges` | object | Total amount charged to the customer over their relationship with the company. | 0 | Numeric values stored as text; 11 whitespace-only values identified |
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

Any transformation of this representation will be documented in the
assumptions log.

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

In the raw dataset, this column is stored as `object` even though its values
represent monetary amounts.

Initial profiling identified 11 whitespace-only values.

All 11 affected records have `tenure = 0`.

The handling of these values will be documented in the assumptions log and
implemented during the data-cleaning phase.

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

**Status:** Raw dataset dictionary completed and updated after initial
data-quality profiling.

The dictionary currently documents the original 21 columns before cleaning
transformations.

It will be updated again after the cleaned dataset and engineered features
are created.

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
- No duplicate rows were introduced.
- No duplicate customer IDs were introduced.

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

No customer records were removed during Phase 1.
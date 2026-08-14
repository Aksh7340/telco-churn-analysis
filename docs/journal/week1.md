# Week 1 Journal — Telco Customer Churn Analysis

---

## Day 1 — August 11, 2026

**Phase:** Phase 0 — Project Setup

### ✅ What I Did

- Created the complete project folder structure.
- Created the root project files:
  - `requirements.txt`
  - `.gitignore`
- Initialized the Git repository.
- Created and connected the GitHub repository.
- Completed the initial project setup and repository push.
- Created the documentation structure inside `docs/`.
- Created:
  - `project_charter.md`
  - `data_dictionary.md`
  - `assumptions_log.md`
  - `insights_log.md`
  - `journal/week1.md`

### 🔍 Findings

- The project will analyze customer churn in a telecommunications business.
- The raw dataset contains 7,043 rows and 21 columns.
- `Churn` is the target variable.
- The dataset has a customer-level grain: one row represents one customer.
- Monetary fields such as `MonthlyCharges` and `TotalCharges` do not have a specified currency in the source dataset.

### ⚠️ Problems Faced

- No major technical problem was encountered during the initial project setup.

### 💡 Resolution

- Project structure and documentation files were created successfully.
- The raw dataset was kept separate from processed data.

### ⚡ Decisions

- The raw dataset will remain untouched.
- Monetary values will be treated as currency with an unspecified currency.
- INR/₹ will not be assigned to the dataset unless explicitly justified later.
- Project documentation will be maintained throughout the analysis.

### 🔎 Validation

- Git repository and project structure were created successfully.
- Raw dataset was placed in the designated raw-data directory.

### 🎯 Next

- Continue Phase 0 by understanding and documenting the raw dataset.
- Complete the Data Dictionary using the actual dataset.

---

## Day 2 — August 12, 2026

**Phase:** Phase 0 — Raw Data Understanding

### ✅ What I Did

- Created the Jupyter Notebook:
  - `01_data_cleaning.ipynb`
- Loaded the raw Telco Customer Churn dataset into Python.
- Began profiling the dataset before performing any transformations.
- Checked the dataset structure and column information.
- Reviewed the data types of the columns.

### 🔍 Findings

- The dataset contains 21 columns.
- The dataset contains 7,043 customer records.
- `TotalCharges` is stored as an `object` data type in the raw dataset.
- The dataset was examined before making any cleaning transformations.

### ⚠️ Problems Faced

- No immediate data-quality issue was identified during the initial profiling.

### 💡 Resolution

- No transformation was applied simply because a transformation had been suggested beforehand.
- Further profiling was performed before deciding whether cleaning was actually necessary.

### ⚡ Decisions

- Data cleaning decisions will be based on the actual dataset rather than assumptions about the dataset.
- The raw dataset will not be modified during profiling.

### 🔎 Validation

- Dataset structure and data types were inspected using Python.
- The raw dataset was successfully loaded into the notebook.

### 🎯 Next

- Complete the remaining raw-data quality checks.
- Use the profiling results to complete the Data Dictionary.

---

## Day 3 — August 13, 2026

**Phase:** Phase 0 — Data Profiling & Documentation

### ✅ What I Did

- Continued profiling the raw dataset in `01_data_cleaning.ipynb`.
- Checked for duplicate records.
- Checked for null values.
- Checked for empty strings.
- Reviewed categorical values.
- Reviewed numeric values and ranges.
- Investigated the raw `TotalCharges` data type.
- Used the profiling results to complete the Data Dictionary.

### 🔍 Findings

- No duplicate rows were identified.
- No null values were identified.
- No empty strings were identified.
- No unusual categorical values were identified during the initial review.
- No immediate data-quality anomalies were identified during the initial profiling.
- `TotalCharges` is stored as `object` in the raw dataset.

### ⚠️ Problems Faced

- `TotalCharges` is represented as an `object` despite representing a monetary amount.

### 💡 Resolution

- The column was not changed during profiling.
- The issue was documented for evaluation during the data-cleaning phase.

### ⚡ Decisions

- No unnecessary transformations will be performed.
- A transformation will only be made when the data and analytical requirements justify it.

### 🔎 Validation

- Duplicate, null, empty-string, categorical, and numeric checks were performed.
- Results were used to document the raw dataset accurately.

### 🎯 Next

- Complete the Project Charter.
- Finalize Phase 0 documentation.

---

## Day 4 — August 14, 2026

**Phase:** Phase 0 — Project Documentation

### ✅ What I Did

- Completed `project_charter.md`.
- Completed `data_dictionary.md`.
- Defined the business problem and project objective.
- Documented the project stakeholders.
- Defined the business questions the analysis will investigate.
- Defined core KPIs and supporting metrics.
- Defined the analytical scope and out-of-scope areas.
- Documented the purpose of Python, SQL, Excel, and Power BI within the project.
- Documented the analytical approach and project success criteria.
- Documented the raw dataset's 21 columns in the Data Dictionary.
- Documented the raw dataset's initial data-quality profile.

### 🔍 Findings

- The raw dataset contains 7,043 customers and 21 columns.
- The dataset has no duplicate rows based on the completed profiling.
- No null values were identified.
- No empty strings were identified.
- `TotalCharges` is stored as `object` in the raw dataset.
- No immediate data-quality anomalies were identified during initial profiling.
- The source dataset does not specify the currency for monetary fields.

### ⚠️ Problems Faced

- Needed to distinguish between the original dataset fields and future engineered features.
- Needed to avoid assuming that monetary values were in INR.

### 💡 Resolution

- The Data Dictionary currently documents only the original 21 columns.
- Future fields such as `tenure_band`, `spend_tier`, `is_at_risk`, and `revenue_at_risk` will be documented when they are actually engineered.
- Monetary values will remain currency-neutral throughout the project unless a justified conversion is introduced later.

### ⚡ Decisions

- `tenure_band`, `spend_tier`, `is_at_risk`, and `revenue_at_risk` are not part of the raw Data Dictionary.
- Engineered features will be documented after their definitions and calculation logic are finalized.
- The project will distinguish association from causation.
- Important analytical metrics will be cross-validated before being reported.
- Business findings will be based on evidence from the dataset.

### 🔎 Validation

- `project_charter.md` completed.
- `data_dictionary.md` completed for the original 21 columns.
- Raw dataset profiling completed.
- `TotalCharges` confirmed as `object` in the notebook.
- No duplicates, nulls, or empty strings identified during profiling.

### 🎯 Next

- Begin Phase 1 — Data Cleaning.
- Evaluate whether any transformations are actually required based on the profiling results.
- Continue documenting non-obvious decisions in `assumptions_log.md`.

---

# Week 1 Summary

## Completed

- Project repository and folder structure
- Git/GitHub setup
- Raw dataset setup
- Project Charter
- Raw Data Dictionary
- Initial raw-data profiling
- Jupyter cleaning notebook setup
- Initial data-quality assessment

## Key Principle Established

> **The data determines the cleaning and analysis decisions; transformations will not be performed simply because they were expected in the roadmap.**

## Current Project Status

**Phase 0 — Project Setup & Documentation: Completed**

**Next Phase: Phase 1 — Data Cleaning**
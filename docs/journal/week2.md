# Week 2 Journal — Telco Customer Churn Analysis

---

## Day 6 — Phase 2 Setup

**Phase:** Phase 2 — Exploratory Data Analysis

### ✅ What I Did

- Started Phase 2 — Exploratory Data Analysis.
- Loaded the cleaned dataset produced during Phase 1.
- Established the analytical objective for EDA.
- Confirmed the analytical grain remained one row per customer.
- Reviewed the cleaned dataset before beginning exploratory analysis.
- Established a consistent EDA structure:
  - Business question
  - Analysis
  - Visualization
  - Insight

### 🔍 Findings

- Dataset contains 7,043 customers and 21 columns.
- `Churn` remains the target variable.
- The cleaned dataset was used as the starting point for EDA.

### ⚡ Decisions

- EDA would focus on meaningful business questions rather than generating
  charts for every available column.
- Churn rates would be prioritized over raw churn counts when comparing
  customer segments.
- Findings would be treated as observed associations rather than causal
  relationships.

### 🎯 Next

- Establish the overall churn baseline.
- Analyze churn across major customer characteristics.

---

## Day 7 — Churn Distribution & Customer Segments

**Phase:** Phase 2 — Exploratory Data Analysis

### ✅ What I Did

- Calculated the overall churn rate.
- Analyzed churn by contract type.
- Analyzed churn by tenure.
- Created temporary tenure bands for exploratory comparison.
- Visualized churn rates across contract and tenure groups.

### 🔍 Findings

- Overall churn rate: **26.54%**.
- 1,869 customers churned out of 7,043.
- Month-to-month customers showed a **42.71%** churn rate.
- One-year customers showed an **11.27%** churn rate.
- Two-year customers showed a **2.83%** churn rate.
- Customers with 0–12 months of tenure showed a **47.44%** churn rate.
- Customers with 49–72 months of tenure showed a **9.51%** churn rate.

### 💡 Analytical Interpretation

Contract type and tenure showed some of the largest observed differences in
churn.

The early customer lifecycle emerged as an important area for further
investigation.

### ⚠️ Caution

These differences represent associations within the dataset and do not
establish that contract type or tenure causes churn.

### 🎯 Next

- Investigate churn across service and payment characteristics.
- Examine whether high-churn characteristics overlap.

---

## Day 8 — Service, Payment & Spending Analysis

**Phase:** Phase 2 — Exploratory Data Analysis

### ✅ What I Did

- Analyzed churn by internet service.
- Analyzed churn by payment method.
- Analyzed churn across monthly-charge bands.
- Created a horizontal bar chart for payment-method comparison.
- Created temporary monthly-charge bands for exploratory analysis.

### 🔍 Findings

#### Internet Service

- Fiber optic: **41.89%**
- DSL: **18.96%**
- No internet: **7.40%**

#### Payment Method

- Electronic check: **45.29%**
- Mailed check: **19.11%**
- Bank transfer: **16.71%**
- Credit card: **15.24%**

#### Monthly Charges

- 0–50: **15.70%**
- 50–100: **32.67%**
- 100+: **28.05%**

### 💡 Analytical Interpretation

Fiber-optic customers and electronic-check customers showed substantially
higher observed churn rates.

Monthly charges showed a non-monotonic relationship with churn because the
50–100 group had a higher churn rate than the 100+ group.

### ⚠️ Caution

Payment method and internet service may overlap with other customer
characteristics. These relationships should not be interpreted as direct
causal effects.

### 🎯 Next

- Examine numeric-variable distributions.
- Investigate overlap between high-churn customer characteristics.
- Analyze correlations among numeric variables.

---

## Day 9 — Deeper EDA & Relationship Analysis

**Phase:** Phase 2 — Exploratory Data Analysis

### ✅ What I Did

- Compared distributions of:
  - `tenure`
  - `MonthlyCharges`
  - `TotalCharges`
  across churn status.
- Created a Contract × Internet Service cross-tabulation.
- Visualized the service distribution across contract types.
- Created a correlation matrix for:
  - `tenure`
  - `MonthlyCharges`
  - `TotalCharges`
- Created a correlation heatmap.
- Removed temporary EDA grouping columns after analysis.

### 🔍 Findings

- Churned customers are concentrated more heavily at lower tenure values.
- Churned customers show greater concentration at elevated monthly charges.
- TotalCharges is concentrated at lower values among churned customers, which
  is closely related to their shorter tenure.
- Fiber-optic customers are more concentrated in month-to-month contracts than
  in longer-term contracts.
- `tenure` and `TotalCharges` have a correlation of **0.83**.
- `MonthlyCharges` and `TotalCharges` have a correlation of **0.65**.
- `tenure` and `MonthlyCharges` have a correlation of **0.25**.

### 💡 Analytical Interpretation

The cross-tabulation revealed compositional overlap between two high-churn
characteristics: fiber-optic service and month-to-month contracts.

The strong `tenure`–`TotalCharges` correlation is structurally expected because
TotalCharges accumulates over the customer's relationship with the company.

### ⚠️ Caution

Correlation measures linear association and does not establish causation.

The overlap between contract type and internet service does not establish an
independent effect of either variable on churn.

### 🎯 Next

- Consolidate and document the validated EDA findings.
- Complete Phase 2 validation.
- Prepare the Phase 2 Git commit.
- Begin Phase 3 — Feature Analysis after documentation is complete.

---

# Week 2 Summary

## Half Completed

- Overall churn analysis
- Contract-level churn analysis
- Tenure-level churn analysis
- Temporary tenure-band analysis
- Internet-service churn analysis
- Payment-method churn analysis
- Monthly-charge churn analysis
- Numeric distribution analysis
- Contract × Internet Service cross-tabulation
- Numeric correlation analysis
- EDA findings documentation
- Analytical limitations documentation
- EDA conclusion
- Temporary EDA columns removed

## Remaining 
Phase 3

## Key Findings

The strongest observed churn concentrations were:

- 0–12 months tenure: **47.44%**
- Electronic check: **45.29%**
- Month-to-month contract: **42.71%**
- Fiber optic: **41.89%**

## Key Analytical Principle

> EDA identifies patterns and associations in the data. These patterns should
> not be interpreted as causal relationships without further analysis.

## Phase Status

**Phase 2 — Exploratory Data Analysis: Completed**

**Next Phase: Phase 3 — Feature Analysis**
# Assumptions Log

| Date | Column / Area | Decision | Reasoning |
|---|---|---|---|
| 2026-08-14 | `TotalCharges` | Treat 11 whitespace-only values as zero during cleaning | The 11 affected records were investigated and all had `tenure = 0`. Since `TotalCharges` represents cumulative charges, the whitespace-only values were treated as zero for analytical purposes. |
| 2026-08-14 | `TotalCharges` | Convert `TotalCharges` from `object` to `float64` | The column represents numeric monetary amounts but was stored as text in the raw dataset. Numeric storage is required for reliable aggregation, comparison, and financial analysis. |
| 2026-08-14 | Raw Dataset | Do not remove duplicate rows | The dataset contained 0 duplicate rows, so no duplicate records required removal. |
| 2026-08-14 | `customerID` | Do not remove or consolidate customer records | No duplicate `customerID` values were identified. Each row represents a unique customer in the dataset. |
| 2026-08-14 | Categorical Variables | Do not modify categorical values | All observed categorical values matched the expected categories in the dataset. Values such as `No internet service` and `No phone service` were retained because they represent valid service states. |
| 2026-08-14 | Numeric Variables | Do not modify numeric values other than `TotalCharges` | `SeniorCitizen`, `tenure`, `MonthlyCharges`, and the cleaned `TotalCharges` values were within the expected observed ranges. No additional numeric corrections were required. |
| 2026-08-14 | Service Variables | Retain existing service-status categories | Logical consistency checks showed no identified inconsistencies between `InternetService` and internet-dependent service columns. |
| 2026-08-14 | Monetary Fields | Do not assign INR/₹ to monetary values | The source dataset does not specify a currency. Monetary values will therefore remain currency-neutral throughout the project. |
| 2026-08-18 | Tenure EDA | Use temporary tenure bands of `0–12`, `13–24`, `25–48`, and `49–72` months | The bands were created only to make churn-rate differences easier to compare during exploratory analysis. They are not treated as final engineered business segments. |
| 2026-08-18 | Monthly Charges EDA | Use temporary charge bands of `0–50`, `50–100`, and `100+` | The bands were created only for exploratory comparison of churn rates. They are not treated as final engineered spending segments. |
| 2026-08-18 | EDA Interpretation | Treat observed relationships as associations rather than causal effects | Exploratory analysis identifies patterns and differences within the dataset but does not establish causation. |
| 2026-08-18 | Contract × Internet Service | Treat overlap between contract type and internet service as compositional overlap | The cross-tabulation identifies how customer characteristics are distributed across groups but does not establish an independent effect on churn. |
| 2026-08-18 | Correlation Analysis | Interpret correlation as linear association rather than causation | Correlation measures the strength and direction of linear association between numeric variables and does not establish a causal relationship. |
| 2026-08-18 | EDA Scope | Prioritize contract, tenure, internet service, payment method, monthly charges, and numeric relationships | These variables were prioritized because they produced meaningful churn-rate differences or relationships relevant to the project's business questions. Other variables remain available for later analysis if justified. |

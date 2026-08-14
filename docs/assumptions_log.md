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
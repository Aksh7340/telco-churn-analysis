# Assumptions Log

| Date | Column / Area | Decision | Reasoning |
|---|---|---|---|
| 2026-08-14 | TotalCharges | Treat 11 whitespace-only values as zero during cleaning and convert the column to numeric | The 11 affected records have `tenure = 0`. Since `TotalCharges` represents cumulative charges and these customers have no recorded tenure, the whitespace-only values will be treated as zero for analytical purposes. |
| 2026-08-14 | TotalCharges | Convert `TotalCharges` from `object` to numeric after handling whitespace-only values | The column represents monetary amounts but is stored as text in the raw dataset. Numeric storage is required for reliable aggregation, comparison, and financial analysis. |
| 2026-08-14 | Monetary Fields | Do not assign INR/₹ to monetary values | The source dataset does not specify a currency. Monetary values will therefore remain currency-neutral throughout the project unless a justified conversion is introduced later. |
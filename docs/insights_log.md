| Date | Phase | Tool | Finding | Business Significance |
|---|---|---|---|---|
| 2026-08-14 | Phase 1 — Data Cleaning | Python | 11 `TotalCharges` records contained whitespace-only values; all affected records had tenure = 0. | Required treatment before reliable monetary analysis. |

## Phase 2 — Exploratory Data Analysis (2026-08-18)

### Overall Churn

**Finding:** The dataset contains 7,043 customers, of whom 1,869 have churned.

- Churned customers: 1,869
- Retained customers: 5,174
- Overall churn rate: **26.54%**

**Interpretation:**

Approximately one in four customers in the dataset has churned. The
retained-to-churned distribution is approximately 3:1 and should be considered
when interpreting segment-level churn comparisons.

**Business Relevance:**

The overall churn rate provides the baseline against which customer segments
can be compared.

---

## Contract Type

**Finding:** Churn varies substantially across contract types.

| Contract Type | Churn Rate |
|---|---:|
| Month-to-month | **42.71%** |
| One year | **11.27%** |
| Two year | **2.83%** |

The difference between month-to-month and two-year customers is
**39.88 percentage points**.

**Interpretation:**

Contract structure shows one of the strongest observed associations with churn
in the dataset.

**Business Relevance:**

Contract type should be examined further in combination with tenure, service
type, and monthly charges to determine whether specific customer profiles
represent higher-risk segments.

**Caution:**

This finding represents an observed association and does not establish that
contract type causes churn.

---

## Tenure

**Finding:** Churn decreases substantially across tenure bands.

| Tenure Band | Churn Rate |
|---|---:|
| 0–12 months | **47.44%** |
| 13–24 months | **28.71%** |
| 25–48 months | **20.39%** |
| 49–72 months | **9.51%** |

The difference between the 0–12 month and 49–72 month groups is
**37.93 percentage points**.

**Interpretation:**

The observed churn rate decreases monotonically across the tenure bands.

**Business Relevance:**

The early customer lifecycle represents a priority segment for further
retention analysis.

**Caution:**

The tenure bands were created as temporary exploratory groupings and are not
final engineered business segments.

---

## Internet Service

**Finding:** Churn varies substantially across internet service types.

| Internet Service | Churn Rate |
|---|---:|
| Fiber optic | **41.89%** |
| DSL | **18.96%** |
| No internet service | **7.40%** |

The difference between fiber-optic and no-internet customers is
**34.49 percentage points**.

**Interpretation:**

Fiber-optic customers show a substantially higher observed churn rate than
DSL and no-internet customers.

**Business Relevance:**

The fiber-optic segment warrants further investigation alongside contract
type, tenure, and other service characteristics.

**Caution:**

The observed difference does not establish that internet service type causes
churn.

---

## Payment Method

**Finding:** Electronic-check customers show substantially higher churn than
the other payment groups.

| Payment Method | Churn Rate |
|---|---:|
| Electronic check | **45.29%** |
| Mailed check | **19.11%** |
| Bank transfer (automatic) | **16.71%** |
| Credit card (automatic) | **15.24%** |

Electronic-check customers have a churn rate approximately **26 percentage
points higher** than the other payment methods.

**Interpretation:**

Payment method is strongly associated with churn in the observed dataset.

**Business Relevance:**

The relationship should be investigated alongside contract type, tenure, and
other customer characteristics before attributing the difference directly to
payment method.

**Caution:**

Payment method may represent differences in customer composition rather than
being a direct driver of churn.

---

## Monthly Charges

**Finding:** Churn varies across monthly-charge bands, but the relationship is
not strictly monotonic.

| Monthly Charge Band | Churn Rate |
|---|---:|
| 0–50 | **15.70%** |
| 50–100 | **32.67%** |
| 100+ | **28.05%** |

The 50–100 group has the highest observed churn rate.

**Interpretation:**

The 50–100 charge band has a higher churn rate than both the lower and higher
charge bands. Therefore, the relationship between monthly charges and churn
cannot be described simply as "higher charges result in higher churn."

**Business Relevance:**

Monthly charges should be examined together with contract type, internet
service, tenure, and other customer characteristics.

**Caution:**

The charge bands are exploratory groupings and are not final business
segments.

---

## Contract × Internet Service

**Finding:** The cross-tabulation shows an overlap between contract type and
internet service.

Fiber-optic customers are more concentrated in month-to-month contracts than
in longer-term contracts.

**Interpretation:**

Two characteristics with high observed churn rates overlap within the customer
population.

**Business Relevance:**

Phase 3 should investigate whether the elevated churn associated with
fiber-optic service persists after accounting for contract type.

**Caution:**

The cross-tabulation identifies compositional overlap and does not establish
causation or an independent effect.

---

## Numeric Variable Relationships

### Tenure × TotalCharges

**Correlation:** **0.83**

There is a strong positive correlation between `tenure` and `TotalCharges`.

**Interpretation:**

This relationship is structurally expected because `TotalCharges` accumulates
over the customer's relationship with the company.

Therefore, the relationship should not be interpreted as an independent churn
signal.

---

### MonthlyCharges × TotalCharges

**Correlation:** **0.65**

There is a moderate positive correlation between `MonthlyCharges` and
`TotalCharges`.

**Interpretation:**

Customers with higher monthly charges tend to have higher cumulative charges.

---

### Tenure × MonthlyCharges

**Correlation:** **0.25**

There is a relatively weak positive linear relationship between `tenure` and
`MonthlyCharges`.

**Interpretation:**

Longer-tenure customers do not necessarily have substantially higher monthly
charges.

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

The next phase will investigate combinations of customer characteristics to
determine whether specific customer profiles represent meaningful high-risk
segments.
# Project Charter — Telco Customer Churn Analysis

## 1. Project Overview

### Project Name

Telco Customer Churn Analysis

### Project Type

End-to-End Business Analytics Project

### Dataset

IBM Telco Customer Churn Dataset

### Project Objective

Analyze customer churn to understand where churn is concentrated, identify customer segments that may require retention attention, and quantify the potential recurring revenue exposure associated with customer attrition.

The project will transform raw customer data into validated business insights and actionable recommendations using Python, SQL, Excel, and Power BI.

---

## 2. Business Problem

Customer churn directly affects the stability of a subscription-based telecommunications business. When customers leave, the company loses recurring revenue and may need to spend additional resources replacing those customers.

The business needs to understand where churn is concentrated, which customer segments appear most vulnerable, and which areas may represent meaningful retention opportunities.

---

## 3. Stakeholders

| Stakeholder                   | Information / Decision Needed                                                          |
| ----------------------------- | -------------------------------------------------------------------------------------- |
| Executive Management          | Understand the overall scale of churn and potential financial exposure                 |
| Customer Retention Team       | Identify customer segments that may require retention intervention                     |
| Marketing / Customer Strategy | Understand customer characteristics and service relationships associated with churn    |
| Finance                       | Understand the potential recurring revenue exposure associated with customer attrition |

---

## 4. Business Questions

The project will investigate the following questions:

1. What is the overall customer churn rate?
2. How many customers have churned?
3. Which customer segments have the highest churn rates?
4. How does customer tenure relate to churn?
5. How does contract type relate to churn?
6. How do internet and other subscribed services relate to churn?
7. How does customer spending relate to churn?
8. Which combinations of customer characteristics represent potentially high-risk segments?
9. What is the estimated monthly revenue exposure associated with churn?
10. Which customer segments should be prioritized for further retention investigation?

These questions may be refined during the analysis if the data reveals important analytical limitations or opportunities.

---

## 5. Key Performance Indicators

### Core KPIs

| KPI                               | Definition                                                  | Business Purpose                               |
| --------------------------------- | ----------------------------------------------------------- | ---------------------------------------------- |
| Churn Rate                        | Churned customers ÷ total customers                         | Measures overall customer attrition            |
| Churned Customer Count            | Number of customers who churned                             | Quantifies customer loss                       |
| Estimated Monthly Revenue at Risk | Sum of MonthlyCharges for the defined churn/risk population | Estimates potential recurring revenue exposure |

### Supporting Metrics

| Metric                 | Definition                                                               | Business Purpose                                      |
| ---------------------- | ------------------------------------------------------------------------ | ----------------------------------------------------- |
| Average Tenure         | Average number of months customers have remained with the company        | Provides customer lifecycle context                   |
| At-Risk Customer Count | Number of customers meeting the project's defined risk criteria          | Quantifies the potentially actionable risk population |
| Segment Churn Rate     | Churned customers within a segment ÷ total customers within that segment | Compares churn across customer groups                 |

Additional analytical metrics may be created during the analysis where they directly support a business question.

---

## 6. Analytical Scope

### In Scope

* Customer churn
* Customer tenure
* Contract characteristics
* Customer services
* Payment characteristics
* Monthly charges
* Total charges
* Customer segmentation
* Churn patterns
* Estimated recurring revenue exposure
* Identification of potentially high-risk customer segments
* Business recommendations supported by the analysis

### Out of Scope

* Customer acquisition cost
* Customer lifetime value
* Competitor analysis
* Marketing campaign effectiveness
* Call-center interactions
* Customer sentiment analysis
* External economic factors
* Predictive churn modeling

The project will not claim to establish causal relationships that cannot be supported by the available observational data.

---

## 7. Tools and Their Purpose

| Tool         | Purpose                                                                         |
| ------------ | ------------------------------------------------------------------------------- |
| Python       | Data cleaning, exploratory data analysis, and feature engineering               |
| SQL          | Business analysis, segmentation, aggregation, and independent validation        |
| Excel        | Executive summary reporting, pivot analysis, and stakeholder-friendly reporting |
| Power BI     | Interactive dashboard development and business communication                    |
| Git / GitHub | Version control, reproducibility, and portfolio documentation                   |

---

## 8. Analytical Approach

The project will follow this sequence:

1. Understand and document the raw dataset
2. Clean and validate the data using Python
3. Perform exploratory data analysis
4. Engineer analytical features where justified
5. Analyze business questions using SQL
6. Cross-validate important results between Python and SQL
7. Build an executive Excel report
8. Develop an interactive Power BI dashboard
9. Consolidate findings and recommendations
10. Document limitations and lessons learned

---

## 9. Success Criteria

The project will be considered complete when:

* The raw dataset remains untouched and the analytical workflow is reproducible.
* Data-cleaning decisions are documented.
* The processed dataset can be reproduced from the raw dataset.
* Each major business question has an evidence-based answer.
* Important analytical results are cross-validated.
* Key assumptions and analytical decisions are documented.
* Excel reporting is understandable to a non-technical stakeholder.
* Power BI provides an interactive view of the major findings.
* Recommendations are directly connected to analytical evidence.
* Project limitations are explicitly documented.
* The complete analytical workflow is documented in GitHub.
* The analyst can explain the methodology, findings, and business implications without relying on notes.

---

## 10. Project Deliverables

### Python

* Data-cleaning notebook
* EDA notebook
* Feature-analysis notebook
* Cleaned dataset
* Feature-engineered dataset

### SQL

* Database/schema setup
* Churn analysis
* Segment analysis
* Tenure analysis
* At-risk customer analysis
* Revenue-impact analysis

### Excel

* KPI summary
* Contract × tenure analysis
* Service analysis
* At-risk customer analysis

### Power BI

* Executive overview
* Segment deep-dive
* At-risk action view

### Documentation

* Data dictionary
* Assumptions log
* Insights log
* Daily project journal
* Final report
* README

---

## 11. Project Governance Principles

The following principles will be maintained throughout the project.

### Evidence Before Conclusion

Findings will be based on the actual data rather than predetermined assumptions.

### Validation Before Reporting

Important metrics will be independently checked before being used in business recommendations.

### Business Context Before Visualization

Charts will be created to answer business questions rather than simply display available columns.

### Document Important Decisions

Non-obvious data and analytical decisions will be recorded in the assumptions log.

### Distinguish Association From Causation

Observed relationships between customer characteristics and churn will not automatically be interpreted as causal relationships.

### Reproducibility

All major transformations and analytical results should be reproducible from the documented workflow.


# DEGO Project - Team 11
# # Team Members
-[ Miguel Teixeira]
-[ Leonardo Cantù]
-[ Kaltoum El Glaoui Hamdellah]
-[ Catarina Cardoso]
## Project Description
Credit scoring bias analysis for DEGO course .
## Structure
- ‘ data /‘ - Dataset files
- ‘ notebooks /‘ - Jupyter analysis notebooks
- ‘ src /‘ - Python source code
- ‘ reports /‘ - Final deliverables

## Executive Summary: Data Engineering & Quality Audit
As the **Data Engineer**, I established the repository structure and developed a data pipeline to transform raw, nested JSON applications into an analysis-ready dataset.

### 1. Key Data Quality Findings
I performed an audit across 6 categories (Completeness, Consistency, Validity, Accuracy, Integrity, and Timeliness):
* **Completeness:** Identified and removed 10 records with missing critical identifiers (5 SSNs, 5 Annual Incomes).
* **Consistency:** Standardized gender coding (standardizing 'M'/'F' to 'Male'/'Female') to ensure accurate Bias Analysis.
* **Validity:** Detected and removed 2 records with impossible negative credit history months.
* **Data Types:** Converted `annual_income` from string to numeric to allow for financial calculations.

### 2. Remediation Outcome
The final dataset, `cleaned_credit_data.csv`, contains **492 high-quality records**. This file is now ready for Bias Detection and Fairness analysis.

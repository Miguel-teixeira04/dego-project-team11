
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

As the **Data Engineer**, I established the repository structure and developed a robust data pipeline to transform raw, nested JSON applications into an analysis-ready dataset. 

### 1. Key Data Quality Findings
I performed a comprehensive audit across core Data Quality Dimensions, drastically improving upon our initial scan:

* **Uniqueness:** Identified 4 duplicate records (across 2 groups). We applied a strict deduplication rule to keep the first occurrence, leaving a clean base of 500 unique records.
* **Completeness:** Identified ~20 records missing critical fields such as email, SSN, DOB, and income. Instead of dropping them, we applied a quarantine flag (`dq_flag_missing`) to maintain a strict governance audit trail.
* **Consistency:** * Standardized gender coding by mapping 111 messy inputs ('M'/'F') to canonical 'Male'/'Female' categories.
  * Unified 4 disparate date-of-birth formats into strict ISO-8601 datetimes.
* **Validity & Accuracy:** * Converted `annual_income` from string to numeric for 8 records.
  * Flagged and nullified 2 records with negative `credit_history_months` and 1 record with a negative `savings_balance`.
  * Flagged 1 impossible Debt-to-Income (DTI) ratio (> 1.0) and 4 invalid email formats via Regex matching.

### 2. Remediation Outcome
The final dataset, `clean_credit_applications.csv`, contains exactly **500 high-quality records** across 26 columns. All impossible values were safely nullified and flagged rather than deleted. This pristine file is now fully prepared for the Data Scientist's Bias Detection and Fairness analysis.
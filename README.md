
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

## Executive Summary: Bias Detection & Fairness Analysis

As the **Data Scientist**, I conducted a structured fairness audit on the cleaned dataset, testing for discriminatory patterns across gender, age, and geography using the four-fifths rule, statistical significance tests, and interaction analysis.

### 1. Key Bias Findings

* **Gender Disparate Impact:** Female applicants are approved at 50.6% vs. 66.0% for males, producing a **DI ratio of 0.767**  below the 0.8 threshold that triggers the four-fifths rule (29 CFR § 1607.4D). A χ² test confirms this is not due to chance (χ² = 11.51, **p = 0.0007**). This is a statistically significant and legally material finding.

* **Age-Based Discrimination:** The 18–29 cohort is approved at just 41.7% vs. 61.8% for the peak 30–39 cohort, yielding a **DI ratio of 0.676**. A point-biserial correlation confirms a significant positive relationship between age and approval (r = 0.124,
  **p = 0.006**).

* **Interaction Effect:** Young women (18–29) face compound disadvantage. A **22.6 percentage point gender gap** (31.1% vs. 53.7% for young men), far exceeding the gap in any other age band. This finding is invisible in marginal DI ratios alone.

* **Geographic Proxy:** NYC (100xx) applicants are approved at 64.5% vs. 51.7% for LA (902xx), a significant 12.8pp gap (χ² p = 0.006). Critically, a Mann-Whitney U test shows **no significant income difference** between the clusters (p = 0.285), ruling out financial justification and raising a redlining risk.

* **Sensitive Spending Categories:** `Gambling` and `Alcohol` spending are present in the feature pipeline. Regardless of their current directional effect on outcomes, lifestyle behavioural data can proxy for religion, health status, and cultural background protected characteristics under the EU AI Act 2025.

* **Interest Rate Disparity:** Male borrowers receive a median rate of 4.70% vs. 4.40% for females. This 0.30% gap is not statistically significant (Mann-Whitney p = 0.326) but warrants ongoing monitoring given its potential real-money impact at scale.

### 2. Regulatory Exposure

Under the **EU AI Act 2025** , credit scoring is a **high-risk AI application**. Based on our findings, NovaCred's current system would fail conformity assessment on Article 9 (risk management), Article 10 (data governance — discriminatory training patterns), and Article 13 (transparency — 82% of rejections cite only `algorithm_risk_score` with no human-interpretable basis).

## **Video Presentation:** https://youtu.be/dYcer2oJD4I

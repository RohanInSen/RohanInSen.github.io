\# Loan Approval Risk Scoring



\*\*Objective\*\*  

Predict loan sanction decisions from applicant and loan attributes to improve decision speed and consistency while controlling default risk.



\*\*Business Context\*\*  

Underwriting needs a ranked risk signal to triage applications. Goal: reduce manual review on low-risk cases, focus analyst time on borderline/high-risk, and give product teams clear threshold options based on approval targets and loss appetite.



\*\*Data / Fields (examples)\*\*

\- Demographics \& employment: Gender, Married, Dependents, Education, Self\_Employed

\- Financials: ApplicantIncome, CoapplicantIncome, LoanAmount, Loan\_Amount\_Term, Credit\_History

\- Geography: Property\_Area (Urban, Rural, Semiurban)

\- Target: \*\*Loan\_Status\*\* (Y/N)



\## Solution Overview

\- Built a binary classifier to estimate \*\*P(Approve)\*\* per application.

\- Feature prep: one-hot encodes for categorical fields; numeric scaling kept simple for tree-friendly models; missing values handled prior to training.

\- Candidate models: regularised logistic as baseline; tree-based model as primary (handles non-linearities and mixed data well).

\- Probability calibration for threshold-based decisions (align to approval-rate or expected-loss constraints).

\- Monitoring views: approval rate, precision/recall at operational thresholds, PSI/feature drift checks.



\## Example Operating Policies (choose per business target)

\- \*\*High-throughput\*\*: auto-approve if P(Approve) ≥ τ₁ (e.g., top 50%), send the rest to manual.

\- \*\*Conservative\*\*: auto-approve top 30%; manual review 30–60%; auto-decline bottom 40%.

\- Publish a monthly scorecard with approval rate, overturn rate (manual vs model), and bad-rate tracking.



\## Technical Summary

\- \*\*Target\*\*: `Loan\_Status` mapped to 1/0.

\- \*\*Categoricals encoded\*\*: Gender\_Male, Married\_Yes, Dependents\_{1,2,3+}, Education\_Not Graduate, Self\_Employed\_Yes, Property\_Area\_{Semiurban,Urban}.

\- \*\*Numerics\*\*: ApplicantIncome, CoapplicantIncome, LoanAmount, Loan\_Amount\_Term, Credit\_History.

\- \*\*Missingness (train)\*\*: Credit\_History (~8%), Self\_Employed (~5%), LoanAmount (~3.6%), Dependents (~2.4%), Term (~2.3%), Gender (~2.1%).  

&nbsp; Simple, defensible approach: median/mode imputation; optionally add missing indicators for Credit\_History and LoanAmount.

\- \*\*Class balance\*\*: ~69% approved, ~31% declined (train). Use stratified CV and class weighting to avoid optimistic metrics.

\- \*\*Metrics to report\*\*: ROC-AUC, PR-AUC; precision/recall at business thresholds; approval-rate vs bad-rate curve; lift by decile.

\- \*\*Explainability\*\*: permutation or SHAP to surface drivers (Credit\_History, LoanAmount/Term, incomes, Property\_Area, Dependents).

\- \*\*Governance\*\*: versioned data snapshot; fixed random seed; threshold change log; challenger model rotation each quarter.



\## Artifacts

\- \*\*Data\*\*: train/test CSVs + processed matrix (one-hot).

\- \*\*Notebook\*\*: model training and evaluation (Colab/GitHub). Add links below once committed.

\- \*\*Score export\*\*: CSV with Application ID, P(Approve), auto-decision at current threshold.



\## Next Steps

\- Add reject-inference or post-approval performance labels if available.

\- Add affordability features (debt-to-income, EMI/income), delinquency history, and bureau-derived scores if compliant.

\- Deploy as a batch job or simple API; log decisions and features for audit.




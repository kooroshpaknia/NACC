# Multimodal Clinical and Neuroimaging Data Analysis: Predictors of Cognitive Capability (MoCA)

**Project Overview**
This repository contains the data quality audit, statistical preprocessing, and exploratory data analysis for a multimodal dataset ($N=1237$) combining clinical records and structural MRI metrics. 

**Primary Research Question**
"In the NACC clinical cohort, how are demographic characteristics (NACCAGE, SEX, EDUC), vascular and clinical risk factors (HYPERTEN, DIABETES, NACCBMI, NACCGDS, smoking history), and medial temporal lobe MRI biomarkers (bilateral Entorhinal and Parahippocampal cortical volumes and thickness) associated with general cognitive capability (MOCATOTS)? Furthermore, does a multimodal model integrating structural MRI improve explanatory power over a clinical UDS-only model, and how do these metrics vary between men and women?"

**Analytical Strategy**
To address the research question, the analysis is structured into three modeling phases:
1. **Clinical Baseline Model:** Evaluating the independent associations of demographics and vascular/clinical risk factors with `MOCATOTS`.
2. **Multimodal Integration:** Comparing the baseline clinical model against a combined model incorporating the 8 structural MRI biomarkers to quantify improvements in explanatory power (e.g., via adjusted $R^2$ or likelihood ratio tests).
3. **Sex-Stratified Analysis:** Investigating interaction effects and stratified descriptive statistics to determine how these cognitive associations differ between male and female cohorts.

**Data Provenance & Linkage**
* `udslong_imputed.csv`: Pre-imputed clinical data from the Uniform Data Set (UDS).
* `mriscanclean.csv`: Structural neuroimaging measurements (cortical volume and thickness).
* `multimodal_merged_dataset.csv`: The final linked cohort matched on `NACCID`, representing a 100% sample overlap.

**Feature Scope**
The analysis focuses on 24 primary variables:
* **Target Variable:** `MOCATOTS` (Montreal Cognitive Assessment Total Score).
* **Clinical Predictors (15):** Includes demographics (`NACCAGE`, `SEX`, `EDUC`), vascular/clinical risk factors (`HYPERTEN`, `DIABETES`, `NACCBMI`, `NACCGDS`, `SMOKYRS`), and baseline diagnostics.
* **Structural MRI Biomarkers (8):** Includes volumetric (`GVOL`) and average thickness (`AVGTH`) measurements for the Entorhinal and Parahippocampal cortices.

**Data Quality & Preprocessing**
A strict data quality protocol was applied to the merged cohort via Python/pandas:
* Explicit mapping of NACC special codes (e.g., 88, 99, -4) to `NaN`.
* Enforcement of physiological bounds (e.g., `NACCBMI` between 10-100, MRI metrics > 0, `MOCATOTS` between 0-30).
* Exclusion of features exceeding 30% missingness post-audit (e.g., `DIABTYPE`).
* Resolution of imputation artifacts (fractional decimals in binary/categorical variables).

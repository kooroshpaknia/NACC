# Investigating the Impact of Demographic, Clinical, and Structural Brain Indices (MRI) on Dementia Severity and Cognitive Decline in a Clinical Sample

## 1. Main Statistical Question
“In the NACC clinical cohort, how are demographic characteristics (NACCAGE,
SEX, EDUC), vascular and clinical risk factors (HYPERTEN, DIABETES, NACCBMI,
NACCGDS, smoking history), and medial temporal lobe MRI biomarkers (bilateral Entorhinal and Parahippocampal cortical volumes and thickness) associated with general cognitive capability (MOCATOTS)? Furthermore, does a multimodal model integrating structural MRI improve explanatory power over a
clinical UDS-only model, and how do these metrics vary between men and
women?”

## 2. Dataset and Subset Selection
For detailed information regarding the official data source, required files, acquisition date, and the dataset reconstruction pipeline, please refer to the [`data/README.md`](data/README.md) documentation.

* **Target Subset / Cohort:** The analysis utilizes the entire available clinical sample to model continuous disease trajectories across the full spectrum of cognitive statuses (from normal cognition to severe dementia), rather than restricting the sample to a specific etiologic diagnosis.

## 3. Key Variables (Preliminary Scope)

### A. Identifiers
* `NACCID` (Participant ID)

### B. Primary Response (Dependent) Variable
* `CDRSUM` (Clinical Dementia Rating - Sum of Boxes)

### C. Cognitive & Clinical Status
* `NACCUDSD` (Cognitive Diagnosis)
* `CDRGLOB` (Global CDR Score)
* `NACCGDS` (Geriatric Depression Scale)

### D. Demographics & Baseline Characteristics
* `SEX`
* `NACCAGE`
* `EDUC` (Years of Education)
* `NACCBMI` (Body Mass Index)

### E. Medical History, Risk Factors & Genetics
* `NACCAPOE` (APOE Genotype)
* `HYPERTEN` (Hypertension History)
* `DIABETES` (Diabetes Status)
* `DIABTYPE` (Diabetes Type)
* `CBSTROKE` (Stroke History)
* `SMOKYRS` (Years of Smoking)
* `TOBAC100` (Smoked >= 100 cigarettes in lifetime)

### F. Neuroimaging (MRI) Predictors
* **Entorhinal Cortex (Volume & Thickness):**
  * `LH_ENTORHINAL_GVOL` (Left)
  * `RH_ENTORHINAL_GVOL` (Right)
  * `LH_ENTORHINAL_AVGTH` (Left)
  * `RH_ENTORHINAL_AVGTH` (Right)
* **Parahippocampal Gyrus (Volume & Thickness):**
  * `LH_PARAHIPPOCAMPAL_GVOL` (Left)
  * `RH_PARAHIPPOCAMPAL_GVOL` (Right)
  * `LH_PARAHIPPOCAMPAL_AVGTH` (Left)
  * `RH_PARAHIPPOCAMPAL_AVGTH` (Right)

## 4. Unit of Observation and Target Population
* **Unit of Observation:** Each row represents a single **patient/participant**.
* **Target Population:** Findings are applicable to **patients attending specialized memory clinics and research centers (ADRCs)**. Due to clinical sampling, results cannot be generalized to the broader general population.

## 5. Main Variables and Measurement Scales
* **Identifier:** `NACCID`
* **Continuous Quantitative:** `CDRSUM` (Primary Response), `NACCAGE`, `NACCBMI`, `LH_ENTORHINAL_GVOL`, `RH_ENTORHINAL_GVOL`, `LH_PARAHIPPOCAMPAL_GVOL`, `RH_PARAHIPPOCAMPAL_GVOL`, `LH_ENTORHINAL_AVGTH`, `RH_ENTORHINAL_AVGTH`, `LH_PARAHIPPOCAMPAL_AVGTH`, `RH_PARAHIPPOCAMPAL_AVGTH`.
* **Discrete Quantitative:** `EDUC`, `NACCGDS`, `SMOKYRS`.
* **Ordinal:** `NACCUDSD`, `CDRGLOB`.
* **Nominal:** `NACCAPOE`, `HYPERTEN`, `DIABETES`, `DIABTYPE`, `CBSTROKE`.
* **Binary / Dichotomous:** `SEX`, `TOBAC100`.

## 6. Role of Variables in the Research Question
Since the research question is both relational (assessing impact) and comparative (assessing gender differences), the variables are assigned specific modeling roles:

* **Primary Response (Dependent) Variable:** `CDRSUM` (acting as the quantitative measure of dementia severity).
* **Explanatory (Independent/Predictor) Variables:** 
  * *Continuous Predictors:* `NACCAGE`, `NACCBMI`, `SMOKYRS`, and all neuroimaging metrics (`*_GVOL`, `*_AVGTH`).
  * *Categorical Predictors (Secondary Grouping Variables):* `HYPERTEN`, `DIABETES`, `DIABTYPE`, `CBSTROKE`, `NACCGDS`, `TOBAC100`, `NACCAPOE`. These act as covariates in regression models and grouping variables during Exploratory Data Analysis (EDA).
* **Primary Grouping / Comparative Variables:** 
  * `SEX`: The explicit grouping variable to evaluate statistical differences in dementia severity between males and females.
  * `NACCUDSD`: Used to stratify the cohort across the clinical cognitive spectrum (Normal to Dementia).

## 7. Type of Statistical Question
The primary research question is a hybrid of **Relational** and **Comparative** types:

* **Relational:** It investigates the association and statistical impact of various explanatory variables (structural MRI metrics, age, clinical history) on the continuous response variable (`CDRSUM`).
* **Comparative:** It explicitly compares the severity of functional decline across different categorical groups, primarily evaluating significant differences between males and females (`SEX`).

## 8. Initial Scientific Hypotheses
The preliminary scientific expectations guiding this study are:

1. **Neuroimaging Effect:** Reduced cortical volume and thickness in the entorhinal and parahippocampal regions are significantly associated with higher dementia severity (an increase in the `CDRSUM` score).
2. **Clinical Risk Factors:** The presence of vascular risk factors (such as a history of hypertension, diabetes, or stroke) exacerbates functional and cognitive decline.
3. **Gender Disparities:** There is a discernible difference in the average baseline dementia severity between males and females within this clinical cohort.

## 9. Initial Limitations
1. **Lack of Etiological Specificity:** By modeling "all-cause dementia" across the cognitive spectrum, the study does not isolate specific underlying pathologies (e.g., Alzheimer's disease, Parkinson's disease, or Lewy Body dementia). Consequently, the model cannot distinguish if the observed structural MRI impacts or clinical risk factors vary between specific disease mechanisms.
2. **Sampling Bias (Non-Random Sample):** The NACC dataset comprises data from specialized Alzheimer’s Disease Research Centers (ADRCs). This represents a clinical case series rather than a randomized, population-based sample, meaning the findings cannot be directly generalized to estimate dementia trends in the broader general public.
3. **Missing Data & Imputation Uncertainty:** Clinical and longitudinal neuroimaging datasets inherently suffer from missing observations. Utilizing a pre-imputed dataset (`udslong_imputed.csv`) allows for robust multivariate modeling but introduces a degree of statistical uncertainty compared to completely observed raw data.

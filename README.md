PIMA  diabetes dataset

# Localized Nigerian EMR Vitals & Chronic Disease Risk Dataset

## Context
This dataset addresses the critical challenge of ethical and institutional clearance delays in local healthcare research by repurposing and localizing open-source medical records into a 3-tier multi-risk stratification matrix. It specifically targets the early clinical identification of Hypertension and Type-2 Diabetes comorbidity risk clusters within a Nigerian electronic medical record (EMR) context.

## Data Localization & Feature Engineering
The raw features were engineered and transformed to align with standard sub-Saharan African clinical intake workflows:
1. **Blood Glucose Metric Normalization:** Converted from US standard units (mg/dL) to the Nigerian clinical standard (mmol/L) using the established enzymatic conversion rule: `Glucose_mmol = Glucose_mgdl / 18.018`.
2. **Cardiovascular Metric Expansion:** Diastolic pressure attributes were augmented with calculated Systolic Blood Pressure metrics (`Systolic_BP = Diastolic_BP + 40`) to facilitate Stage-2 Hypertension mapping.
3. **Unisex Demographics:** Synthesized balanced gender vectors (`0 = Female`, `1 = Male`) to build a globally applicable inference matrix for EMR form inputs.

## The 3-Tier Multi-Risk Target Coding Rules
Every patient row is scored using an additive clinical point rubric:
* **Fasting Glucose:** $\geq$ 7.0 mmol/L (+2 points) | 5.6 to 6.9 mmol/L (+1 point)
* **Blood Pressure:** Diastolic $\geq$ 90 mmHg (+2 points) | 80 to 89 mmHg (+1 point)
* **Obesity (BMI):** $\geq$ 30.0 (+1 point)
* **Genetics (Pedigree):** $\geq$ 0.50 (+1 point)

### Risk Class Definitions:
* **Class 0 (Low Risk):** Cumulative score of 0 points. Pristine baseline vitals.
* **Class 1 (Moderate Risk):** Cumulative score of 1 or 2 points. Borderline markers requiring monitoring.
* **Class 2 (High Chronic Risk):** Cumulative score $\geq$ 3 points. Acute comorbidity risk or active disease presentation.

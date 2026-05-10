# 🏥 Population Health Readmission Risk

> A full-stack population health analytics project demonstrating readmission risk modelling, health equity stratification, SDOH analysis, and interactive surveillance dashboards.

**Author:** Taiwo Tobi Omoyeni · Health Data Analyst & Population Health Informaticist  
**Stack:** Python · SQL · scikit-learn · Chart.js · ICD-10 · SDOH Framework

---

## 📊 Live Dashboard

**[https://taiwotimman.github.io/pop-health-folder](https://taiwotimman.github.io/pop-health-folder)**


### Dashboard Sections:
| Tab | Contents |
|-----|----------|
| **Overview** | KPI strip, risk tier distribution, readmission by ICD-10 diagnosis, medication counselling impact, top odds ratios |
| **Health Equity** | Race/ethnicity stratification, insurance-type analysis, race × insurance disparity matrix |
| **SDOH Analysis** | SDOH burden gradient (0–4 factors), factor prevalence, SDOH × insurance grouped analysis |
| **Predictive Model** | ROC curve, feature importance (odds ratios), model metrics, methodology |

---

## 🗂 Project Structure

```
population-health-dashboard/
├── data/
│   ├── generate_data.py        # Synthetic EHR dataset generator (n=2,000)
│   ├── analysis.py             # Logistic regression + equity analysis
│   ├── population_health_data.csv
│   ├── model_results.json      # Model performance + feature importances
│   ├── equity_report.json      # Stratified disparity analysis
│   └── summary_stats.json      # Dashboard KPIs
├── sql/
│   └── population_health_queries.sql  # 8 production-grade analytics queries
├── dashboard/
│   └── index.html              # Interactive surveillance dashboard
└── README.md
```

---

## 🔬 Key Findings

### Readmission Landscape
- **22.9%** overall 30-day readmission rate across 2,000 discharge records
- **628 patients** (31.4%) classified as High or Critical risk
- **37.2%** of patients discharged without medication counselling — highest modifiable gap

### Health Equity Signals
- Black/African American patients: **28.6%** readmission rate vs 19.2% for Asian patients — a **9.4pp disparity**
- Uninsured patients: **29.2%** readmission rate vs 18.9% for Medicare beneficiaries
- Black + Uninsured intersection: estimated **34.8%** readmission rate — highest observed subgroup

### SDOH Burden Gradient
| SDOH Score | N | Readmission Rate |
|------------|---|-----------------|
| 0 factors  | 415 | 16.9% |
| 1 factor   | 810 | 19.6% |
| 2 factors  | 561 | 27.5% |
| 3 factors  | 184 | 32.6% |
| 4 factors  | 30  | **53.3%** |

SDOH burden is a **3.2× multiplier** on readmission risk from lowest to highest burden.

### Predictive Model Performance
| Metric | Value |
|--------|-------|
| ROC-AUC | 0.772 |
| 5-fold CV AUC | 0.751 ± 0.023 |
| Sensitivity | 71.7% |
| Specificity | 68.8% |
| Brier Score | 0.196 |

**Top independent risk factors** (adjusted odds ratios):
1. Prior admissions (12m): OR = 1.68
2. Age: OR = 1.60
3. Number of comorbidities: OR = 1.45
4. Length of stay: OR = 1.39
5. Medicaid insurance: OR = 1.26

---

## ⚙️ Reproducing the Analysis

### Requirements
```bash
pip install pandas numpy scikit-learn
```

### Run
```bash
# Step 1 — Generate dataset
cd data/
python generate_data.py

# Step 2 — Run full analysis (logistic regression + equity + KPIs)
python analysis.py

# Step 3 — Open dashboard
open ../dashboard/index.html
```

---

## 🗃 SQL Analytics Queries

Eight production-grade SQL queries in `sql/population_health_queries.sql`:

1. **KPI Summary** — Top-level surveillance metrics
2. **Readmission by ICD-10** — Diagnosis burden with rolling average comparison
3. **Health Equity Matrix** — Race × insurance disparity analysis with rate ratios
4. **SDOH Burden Impact** — Window function analysis of cumulative SDOH risk
5. **Medication Counselling Gap** — Protocol failure analysis by diagnosis
6. **High-Risk Patient Registry** — CTE + window function to generate intervention list
7. **Geographic Hotspot Detection** — Zip code clustering with NTILE quartile ranking
8. **Cohort Before/After Protocol** — Simulated pre/post discharge protocol comparison

All queries use CTEs and window functions; compatible with PostgreSQL / BigQuery / Snowflake.

---

## 🎯 Relevance to Population Health Informatics

This project directly demonstrates:

- ✅ **Population-level health data analysis** — 2,000-record EHR cohort with realistic distributions
- ✅ **Health equity & disparity quantification** — race × insurance stratification with reference group comparison
- ✅ **SDOH integration** — 4-factor burden scoring linked to readmission risk gradient
- ✅ **ICD-10 classification** — diagnosis-level risk attribution across 8 major categories
- ✅ **Dashboard design & reporting frameworks** — interactive multi-tab surveillance tool
- ✅ **Predictive modelling** — logistic regression with cross-validation and calibration (Brier score)
- ✅ **Data annotation readiness** — structured risk tier labelling suitable for downstream ML training
- ✅ **SQL analytics pipelines** — 8 advanced queries with CTEs and window functions
- ✅ **Actionable insight communication** — KPI cards, insight callouts, intervention flags

---

## 📄 Disclaimer

All data is **entirely synthetic**, generated programmatically for portfolio and research demonstration purposes. No real patient data is used. The readmission outcomes are derived from a logistic data-generating process, not real clinical events.

---

*Built as a portfolio demonstration for Population Health Informatics and AI training evaluation roles.*

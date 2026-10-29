# Python & Power BI Portfolio — Model Risk Analytics

---

## What this repository is

This repository contains **two end-to-end analytical projects** — one in **Python**, one in **Power BI** — built around a common theme: **model risk analytics**.

The Python projects demonstrate the full model development and validation pipeline: data loading, cleaning, leakage detection, model training, independent validation, fairness testing, calibration assessment, cross-population validation, and regulatory mapping. The Power BI projects demonstrate the **consumption layer** — how the pipeline's outputs become executive dashboards, fairness panels, and scenario views for decision-makers.

**The two projects are linked by a common pipeline.** The Fannie Mae IFRS 9 ECL Demonstration produces Power BI exports as its final stage. The Lending Club Credit Default Model produces its own Power BI exports for the governance report. **The Python work is the analysis; the Power BI work is the communication.**

---

## The two projects at a glance

### Lending Club — Credit Default Model

| | |
|---|---|
| **What it does** | Predicts which current loans are most likely to default, for collections prioritization |
| **Dataset** | 10,000 Lending Club public loans |
| **Python pipeline** | 5 notebooks: EDA, model development, independent validation, governance, cross-validation |
| **Power BI dashboard** | Model performance, fairness panel, findings register, compliance scorecard |
| **Verdict** | **HIGH / REJECT** (fairness-driven: region-level DI 0.5414) |
| **What it demonstrates** | Model validation, leakage detection, fairness testing, verdict-ownership chain |

### Fannie Mae — IFRS 9 ECL Demonstration

| | |
|---|---|
| **What it does** | Demonstrates IFRS 9 parameterization (PD/LGD/EAD, staging, probability-weighted ECL) on historical mortgage data |
| **Dataset** | 100,000 Fannie Mae single-family mortgages |
| **Python pipeline** | 6 notebooks: data prep, EDA, calibration, stress & fairness, compliance, Power BI export |
| **Power BI dashboard** | ECL by stage, scenario analysis, capital coverage, data quality |
| **Verdict** | **Accepted as a demonstration** (documented limitations, register guards fire as designed) |
| **What it demonstrates** | Methodology validation, parameter defensibility, register guards, regulatory mapping |

**The single-sentence distinction:**

> *Lending Club asks "is this model fit to be deployed?" and the answer is no (fairness-driven REJECT). Fannie Mae asks "is this methodology fit to be cited?" and the answer is yes, with documented limitations.*

---

## What a reader should look at first

1. [Lending Club Credit Risk Model Validation](https://github.com/MiltonGreat/credit-risk-model-validation.git)

2. [Fannie Mae IFRS 9 ECL Framework](https://github.com/MiltonGreat/fannie-mae-ifrs9-portfolio.git)

3. [IFRS 9 Stress Testing Dashboard](https://github.com/MiltonGreat/Stress-Testing-Dashboard-.git)

---

## How each folder is used

| Folder | Purpose | Key contents |
|---|---|---|
| **`lending-club/`** | Full Lending Club project | 5 notebooks, 12 MAP deliverables, trained models, artifacts |
| **`fannie-mae/`** | Full Fannie Mae project | 6 notebooks, 12 MAP deliverables, parameters, Power BI exports |
| **`powerbi/`** | Power BI dashboards | Two `.pbix` files, screenshots, data dictionary |
| **`supporting/`** | Cross-project artifacts | AI Interaction Record, Reproducibility Record |
| **`governance/`** | Enterprise governance artifacts | AI Governance Policy, Regulatory Gap Analysis, Vendor Review Template |

**Each project folder is self-contained.** A reader can clone `lending-club/` alone and have the full project. The `powerbi/` folder references both projects' exports. The `supporting/` and `governance/` folders are shared context.

---

## The technologies

**Python:**
- `pandas`, `numpy` — data handling
- `scikit-learn`, `xgboost`, `lightgbm` — models
- `fairlearn` — fairness metrics
- `shap` — explainability
- `matplotlib`, `seaborn` — visualization
- `joblib` — model serialization

**Power BI:**
- Power BI Desktop (`.pbix` files)
- Data sources: CSV exports from the Python pipelines
- Visuals: KPI cards, scenario comparisons, fairness panels, stage distributions, coverage diagnostics

**The integration:**
- Python exports CSVs to `fannie-mae/powerbi_exports/` and `lending-club/artifacts/`
- Power BI reads those CSVs
- No live connection — the export is a **snapshot** with provenance (`run_id`, `notebook_version`)

---

## What each project demonstrates

### Lending Club — Python

**The story:** a model built with leakage, caught by validation, corrected, and re-validated. The verdict is REJECT because of fairness. **The Python pipeline demonstrates the full model risk lifecycle.**

**The skills:**
- Data loading, inspection, cleaning
- Leakage detection via pre-registered list
- Four model classes compared
- Independent validation (recompute, not trust)
- Fairness testing (FD-05 compliant)
- Calibration assessment (HL + degeneracy check)
- Verdict-ownership chain (developer → validator → governance → committee)

### Lending Club — Power BI

**The story:** the fairness panel that supports the REJECT verdict. **The dashboard demonstrates how a fairness finding is communicated to a Model Risk Committee.**

**The visuals:**
- Performance panel (AUC by model)
- Fairness panel (DI by region, with SEVERE threshold)
- Findings register (11 findings by severity)
- Compliance scorecard (OSFI E-23, SR 11-7, ECOA, IFRS 9)

### Fannie Mae — Python

**The story:** a methodology demonstration with 0 critical findings and 10 documented limitations. **The Python pipeline demonstrates the full IFRS 9 parameterization lifecycle.**

**The skills:**
- Parameter construction with frozen formulas
- IFRS 9 staging (with documented SICR proxy)
- Probability-weighted ECL across four scenarios
- Register guards (AP-02, AP-03, AP-04)
- Claim-authorization (the pipeline produces evidence; the analyst authors the verdict)
- Power BI export (staging-then-promotion)

### Fannie Mae — Power BI

**The story:** the scenario analysis and ECL distribution for IFRS 9. **The dashboard demonstrates how IFRS 9 outputs are communicated to a modelling team.**

**The visuals:**
- ECL by stage (Stage 1/2/3 distribution)
- Scenario analysis (baseline, adverse, severely adverse, tail risk)
- Coverage panel (ECL % of assets)
- Data quality panel (missingness, leakage, macro gap)

---

## How the two projects are related

**They share:**
- The same audit discipline (`run_id` on every artifact)
- The same reproducibility requirements (seed 42, content hash)
- The same regulatory framing (OSFI E-23, SR 11-7)
- The same MAP deliverable structure (12 deliverables per project)

**They differ:**
- **Lending Club validates a model** — the verdict is in the pipeline (NB03), and the Power BI dashboard communicates it.
- **Fannie Mae validates a methodology** — the verdict is in the MAP document, and the Power BI dashboard is the final output of the pipeline.

**The portfolio-level insight:**

> *A model needs to be corrected; a methodology needs to be scoped. The Lending Club project shows the correction path (REJECT → 8 remediation actions → re-validation). The Fannie Mae project shows the scoping path (10 limitations documented → accepted as a demonstration). Both are necessary; both are demonstrated here.*

---

## Reproducibility

**Every artifact carries provenance.** The `run_id` and `notebook_version` are recorded in the JSON contracts, the CSV exports, and the audit logs. **A reviewer can trace any number back to the notebook run that produced it.**

**Every notebook uses seed 42.** Re-running a notebook with the same inputs produces the same outputs. **The content hash in `data_quality_summary.json` is the fingerprint.**

**The Power BI dashboards are not live-connected.** They read CSV exports, which are snapshots. **A dashboard reader sees the data as of the export run** — not a live feed. This is deliberate: an audit-ready dashboard should show the same numbers as the audit trail, not numbers that have drifted.

---

## How to navigate the repository

**If you have 5 minutes:** read this README, then open the Lending Club Validation Opinion.

**If you have 30 minutes:** read this README, the Lending Club Validation Opinion, the Fannie Mae Methodology Document, and the Power BI Fairness Dashboard.

**If you have 2 hours:** read the EXECUTIVE_SUMMARY.md, both Validation Opinions, both Findings Registers, and skim the decision criteria registers.

**If you're reviewing the code:** open `lending-club/notebooks/NB03_independent_validation.ipynb` and `fannie-mae/notebooks/NB03_calibration.ipynb`. These are the two "core" notebooks.

**If you're reviewing the Power BI:** open `powerbi/lending-club/README.md` and `powerbi/fannie-mae/README.md`. Each links to the `.pbix` files and the screenshots.

---

## Status

| Project | Status | Next milestone |
|---|---|---|
| **Lending Club** | Validation Opinion signed (REJECT) | MRC decision; remediation plan approval |
| **Fannie Mae** | Methodology documented and accepted | MAP Validation Opinion sign-off |
| **Power BI dashboards** | Built and exported | Awaiting final stakeholder review |

**Nothing here is production-ready.** The Lending Club model is REJECTed. The Fannie Mae methodology is accepted as a demonstration, not for production use. **Both are portfolio demonstrations, not deployed systems.**

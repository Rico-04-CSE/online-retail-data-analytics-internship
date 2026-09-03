# End-to-End Data Analytics Internship Project — UCI Online Retail

## Project Overview

This repository contains my complete five-week Data Analytics Strategist internship project, developed as one continuous analytics lifecycle using the **UCI Online Retail** dataset.

The project progresses from strategic planning and data preparation to exploratory analysis, predictive analytics, statistical impact evaluation, optimization, and analytics delivery.

### Five-Week Analytics Lifecycle

```text
WEEK 1
Strategic Analytics Plan
│
├── Strategic KPI baseline
├── Business opportunities
├── Analytics lifecycle
└── 18-month Horizon roadmap
        ↓
WEEK 2
Data Collection & Cleaning
│
├── Data profiling
├── Missing-value analysis
├── Duplicate detection
├── CustomerID / GUEST treatment
├── Cancellation handling
├── Outlier detection
└── Data-quality validation
        ↓
WEEK 3
Exploratory Data Analysis
│
├── Revenue analysis
├── Country analysis
├── Product analysis
├── Distribution analysis
├── Correlation analysis
├── Statistical visualization
└── Interactive Plotly analysis
        ↓
WEEK 4
Predictive Analytics
│
├── Baseline forecasting
├── Random Forest
├── XGBoost
├── LightGBM
├── Statsmodels
├── Prophet benchmark
├── Walk-forward / time-aware validation
└── SHAP explainability
        ↓
WEEK 5
Impact Evaluation & Optimization
│
├── Baseline vs model comparison
├── MAPE / MAE / RMSE
├── Paired statistical testing
├── Bootstrap confidence interval
├── Prescriptive optimization
└── Scenario analysis
        ↓
ANALYTICS DELIVERY
│
├── SQLAlchemy / SQLite
├── API acquisition demonstration
├── FastAPI KPI endpoint
├── Airflow orchestration design
├── Excel KPI formulas
├── Power BI DAX measures
└── R/RStudio demonstration
```

---

## Dataset

### UCI Online Retail

The project uses the official **Online Retail** dataset from the UCI Machine Learning Repository.

Official source:

https://archive.ics.uci.edu/dataset/352/online-retail

The dataset contains **541,909 transaction records** for a UK-based online retailer and covers transactions from **1 December 2010 through 9 December 2011**. The dataset includes fields such as InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID and Country.

UCI also documents that an InvoiceNo beginning with `C` represents a cancellation.

### Dataset citation

Chen, D. (2015). *Online Retail* [Dataset]. UCI Machine Learning Repository.  
https://doi.org/10.24432/C5BW33

The dataset is licensed under **Creative Commons Attribution 4.0 International (CC BY 4.0)**. Appropriate attribution is included in `DATA_LICENSE.txt`.

---

## Repository Structure

```text
Online_Retail_Internship/
│
├── Internship_Project.ipynb
│
├── data/
│   └── Online_Retail.csv
│
├── scripts/
│   ├── 00_master_pipeline.py
│   ├── 01_week1_strategy.py
│   ├── 02_week2_cleaning.py
│   ├── 03_week3_eda.py
│   ├── 04_week4_predictive.py
│   ├── 05_week5_impact_optimization.py
│   └── 06_requests_api_demo.py
│
├── validation/
│   ├── pandera_validation.py
│   └── great_expectations_optional.py
│
├── sql/
│   └── sqlalchemy_demo.py
│
├── api/
│   └── app.py
│
├── airflow/
│   └── dags/
│       └── online_retail_pipeline.py
│
├── r/
│   └── online_retail_eda.R
│
├── excel/
│   └── formulas.txt
│
├── powerbi/
│   └── dax_measures.txt
│
├── outputs/
│   ├── week1/
│   ├── week2/
│   ├── week3/
│   ├── week4/
│   └── week5/
│
├── requirements.txt
├── requirements-optional.txt
├── environment.yml
├── SOFTWARE_MAP.txt
├── RUN_GUIDE.md
├── DATA_DICTIONARY.md
├── DATA_LICENSE.txt
└── .gitignore
```

---

## Main Notebook

The primary evaluator-facing file is:

**`Internship_Project.ipynb`**

It contains the connected Week 1–5 analytical workflow and can be opened directly in:

- Jupyter Notebook
- JupyterLab
- VS Code
- Google Colab after uploading the repository

The standalone scripts in `scripts/` provide reproducible versions of the same analytical stages.

---

## How to Run the Project

### Option 1 — Jupyter Notebook

Open:

```text
Internship_Project.ipynb
```

Select the Python environment/kernel and run the cells in order.

Recommended execution:

```text
Week 1 → Week 2 → Week 3 → Week 4 → Week 5
```

### Option 2 — Run the complete Python pipeline

From the repository root:

```bash
python scripts/00_master_pipeline.py
```

The pipeline writes evidence and results into:

```text
outputs/week1/
outputs/week2/
outputs/week3/
outputs/week4/
outputs/week5/
```

---

## Installation

Create a dedicated environment:

```bash
conda create -n retail_internship python=3.11 -y
conda activate retail_internship
```

Install the main analysis stack:

```bash
pip install -r requirements.txt
```

The optional technologies in `requirements-optional.txt` include:

- Prophet
- SHAP
- TensorFlow
- Great Expectations
- Airflow

These are kept separate because they are not all required to execute the core five-week analysis on Windows.

---

# Week 1 — Strategic Analytics Plan

### Objective

Develop a practical analytics strategy for improving data-driven decision making and establishing measurable business outcomes.

### Implemented evidence

The code calculates:

- Raw transaction count
- Unique invoices
- Unique customers
- Unique products
- Countries
- Revenue baseline
- Monthly revenue
- Geographic revenue
- Strategic KPI baseline

### Horizon 3 roadmap

The strategic plan uses three explicit gates:

| Period | Focus |
|---|---|
| Months 10–12 | Optimization pilot |
| Months 13–15 | Scenario planning and expansion |
| Months 16–18 | Analytics Center of Excellence, reusable models and quantified impact |

The code exports this roadmap into `outputs/week1/horizon3_timeline.csv`.

---

# Week 2 — Data Collection & Cleaning

The cleaning workflow follows the six-stage methodology:

1. Profile
2. Standardize
3. Deduplicate
4. Handle missing values
5. Handle outliers
6. Validate

### Major cleaning decisions

- Exact duplicates are removed.
- Missing `Description` records are removed because product-level analytics requires a valid description.
- Missing `CustomerID` values are retained and represented as `GUEST`.
- Cancellation invoices are separated from sales.
- Non-positive UnitPrice values in the sales dataset are removed.
- IQR is used to flag UnitPrice outliers rather than automatically deleting every extreme observation.
- Data types are explicitly standardized.
- Pandera validation is available as an executable data-quality check.

### Output

```text
outputs/week2/
```

contains the quality audit, before/after profiles, cleaned sales data, returns data and data dictionary.

---

# Week 3 — Exploratory Data Analysis

The project generates:

- Revenue KPIs
- Monthly revenue trend
- Top-country analysis
- Top-product analysis
- Revenue distribution
- Quantity distribution
- Quantity vs UnitPrice scatter plot
- Correlation matrix
- Correlation heatmap
- Day-of-week revenue analysis
- Interactive Plotly revenue visualization

All charts are generated from the cleaned dataset rather than from fabricated example values.

---

# Week 4 — Predictive Analytics

The target variable is **weekly revenue**.

### Features

- Calendar features
- Trend
- Lagged revenue
- Rolling averages

### Models

- Four-week moving-average baseline
- Random Forest
- HistGradientBoosting
- XGBoost
- LightGBM
- Statsmodels Exponential Smoothing
- Optional Prophet
- Optional TensorFlow LSTM
- SHAP explainability

### Evaluation metrics

- MAE
- RMSE
- MAPE

The final eight weeks are used as a held-out test period, while TimeSeriesSplit is also provided for time-aware validation.

### Important analytical rule

The most accurate model is selected based on measured validation performance. The project does not force an advanced machine-learning model to win simply because it is more complex.

Because the source dataset covers approximately one year, a 52-week lag is not used in the primary model; doing so would leave insufficient training observations. Longer historical data should be used to properly test year-over-year seasonality.

---

# Week 5 — Impact Evaluation & Optimization

The evaluation compares the business baseline with the best advanced forecasting model.

It includes:

- Baseline MAPE
- Advanced-model MAPE
- Relative error improvement
- Paired t-test
- Wilcoxon sensitivity test
- Bootstrap 95% confidence interval

The project then demonstrates prescriptive allocation using:

- SciPy optimization
- PuLP

### Scenario-analysis disclaimer

The UCI dataset does not contain the organization's actual:

- inventory carrying cost
- warehouse capacity
- product margin
- procurement cost
- service-level target

Therefore, optimization outputs are explicitly treated as **scenario estimates based on stated assumptions**, not as claims of actual company savings.

---

# Additional Technology Demonstrations

## SQLAlchemy / SQLite

The cleaned sales table can be loaded into SQLite and queried with SQL.

## Requests

A small API-acquisition demonstration is included to show Python API ingestion.

## FastAPI

`api/app.py` exposes a KPI endpoint for the cleaned retail dataset.

Run from the repository root:

```bash
python -m uvicorn api.app:app --reload
```

Then open:

```text
http://127.0.0.1:8000
http://127.0.0.1:8000/docs
http://127.0.0.1:8000/kpis
```

## Airflow

The repository contains an Airflow DAG showing orchestration of the Week 1–5 pipeline.

The DAG is an orchestration/deployment component and should not be executed as an ordinary Python script. A suitable Airflow environment should be configured separately.

## R / RStudio

`r/online_retail_eda.R` demonstrates the same cleaned retail data workflow using R, tidyverse, ggplot2 and corrplot.

## Excel

`excel/formulas.txt` contains KPI and forecast-evaluation formulas.

## Power BI

`powerbi/dax_measures.txt` contains DAX measures for an executive analytics dashboard.

---

# Data Quality and Reproducibility

The project is designed so that:

```text
Raw Data
   ↓
Cleaning
   ↓
Validated Data
   ↓
EDA
   ↓
Forecasting
   ↓
Statistical Evaluation
   ↓
Optimization
```

Every major stage creates evidence files under `outputs/`.

The project avoids presenting illustrative numbers as observed business results. Calculated model metrics must come from the actual execution of the notebook/scripts.

---

# Key Deliverables for Evaluation

An evaluator can inspect:

1. `Internship_Project.ipynb` — end-to-end notebook
2. `scripts/` — reproducible Python implementations
3. `outputs/` — generated analytical evidence
4. `validation/` — data-quality validation
5. `sql/` — SQL/database implementation
6. `api/` — FastAPI implementation
7. `airflow/` — orchestration design
8. `r/` — R implementation
9. `excel/` — spreadsheet analytics
10. `powerbi/` — business intelligence measures

---

# Author

**Pritam Dey**

Data Analytics Internship Project  
Data Analytics Strategist Track

---

## Note to Evaluators

This repository is intended to demonstrate the practical progression from strategic analytics planning to reproducible data preparation, exploratory analysis, predictive modelling, statistical evaluation and optimization using a real public dataset.

The project emphasizes transparent measurement: model performance, statistical results and analytical findings are generated from the actual UCI Online Retail data rather than from hypothetical company figures.

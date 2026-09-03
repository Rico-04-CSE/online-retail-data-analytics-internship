# Internship Project — UCI Online Retail Data Analytics

## Project Overview

This repository contains my complete **Data Analytics Internship Project** implemented in Python using the **UCI Online Retail dataset**.

The project is presented as a single Jupyter Notebook:

**`Internship_Project.ipynb`**

The notebook follows a continuous analytical workflow from strategic baseline analysis, through data collection and cleaning, exploratory data analysis, predictive analytics, impact evaluation, prescriptive analysis, SQL implementation, and data-quality validation.

The project is designed to demonstrate how raw transactional data can be transformed into useful analytical evidence and then used for forecasting, evaluation, and decision support.

---

# Dataset Used

## UCI Online Retail Dataset

The project uses the **UCI Online Retail** dataset.

Official UCI source:

https://archive.ics.uci.edu/dataset/352/online-retail

Dataset citation:

> Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33

The dataset contains transaction-level retail information including:

- `InvoiceNo`
- `StockCode`
- `Description`
- `Quantity`
- `InvoiceDate`
- `UnitPrice`
- `CustomerID`
- `Country`

The notebook works directly with the CSV version of the UCI dataset.

---

# Main Project Notebook

The primary file for evaluation is:

```text
Internship_Project.ipynb
```

The notebook was developed using:

```text
Python 3.11
Jupyter Notebook
Python - Retail Internship kernel
```

The notebook is organized into the following sections.

---

# WEEK 1 — Strategic Baseline

The first section establishes the business and analytical baseline from the actual retail transaction data.

### Work performed

- Load the Online Retail dataset
- Convert `InvoiceDate`, `Quantity`, and `UnitPrice` into appropriate data types
- Create the derived `Revenue` metric
- Measure the number of:
  - Rows
  - Columns
  - Unique invoices
  - Unique customers
  - Unique products
  - Countries
- Calculate:
  - Total revenue
  - Total orders
  - Total customers
  - Total products
  - Total countries
  - Total units sold
  - Average Order Value (AOV)
- Calculate monthly revenue
- Visualize the monthly revenue trend
- Create a Horizon 3 implementation roadmap

### Strategic evidence

The Week 1 section is intended to provide actual data-driven baseline evidence for the strategic plan instead of relying only on illustrative business figures.

### Horizon 3 roadmap

The notebook defines:

| Period | Strategic Focus |
|---|---|
| Months 10–12 | Optimization Pilot |
| Months 13–15 | Scenario Planning and Expansion |
| Months 16–18 | Analytics Center of Excellence |

---

# WEEK 2 — Data Collection and Cleaning

The Week 2 section follows the data-cleaning framework described in the internship report.

The methodology is:

```text
Profile
   ↓
Standardize
   ↓
Deduplicate
   ↓
Handle Missing Values
   ↓
Handle Outliers
   ↓
Validate
```

## 1. Initial Data Profile

The notebook examines:

- Data types
- Missing values
- Missing-value percentages
- Duplicate records
- Negative quantities
- Non-positive UnitPrice values
- Cancellation invoices

## 2. Standardization

The following fields are standardized:

- Column names
- Description text
- Country text
- InvoiceNo
- StockCode
- InvoiceDate
- Quantity
- UnitPrice

## 3. Deduplication

Exact duplicate transaction rows are identified and removed.

The analysis records the number of duplicate records before and after cleaning.

## 4. Missing Description

Records with missing `Description` values are removed because product-level analysis requires a valid product description.

## 5. CustomerID

Missing customer identifiers are not simply discarded.

A flag is created:

```text
CustomerID_was_missing
```

and missing customer identifiers are represented as:

```text
GUEST
```

This preserves the records for revenue and volume analysis while making the missingness explicit.

## 6. Cancellation Handling

The notebook identifies cancellation invoices using the InvoiceNo convention and creates:

```text
IsCancellation
```

The transaction data are separated into:

```text
Sales
Returns / Cancellations
```

## 7. Revenue Creation

Revenue is calculated as:

```python
Revenue = Quantity * UnitPrice
```

## 8. Outlier Detection

The notebook uses the Interquartile Range (IQR) method on `UnitPrice`.

The analysis creates:

```text
Price_Outlier
```

as an outlier flag.

The objective is to identify unusual observations rather than automatically deleting every statistical extreme.

## 9. Final Validation

The notebook checks:

- Final sales row count
- Remaining duplicates
- Missing descriptions
- Missing customer identifiers
- Invalid prices
- Guest-customer percentage

## 10. Before/After Quality Summary

A summary table compares the raw dataset with the cleaned sales dataset.

## 11. Clean Dataset Export

The notebook exports:

```text
outputs/online_retail_sales_clean.csv
outputs/online_retail_returns.csv
```

---

# WEEK 3 — Exploratory Data Analysis

The Week 3 section analyzes the cleaned retail dataset to identify trends, patterns, distributions, relationships, and business opportunities.

## KPI Analysis

The notebook calculates:

- Revenue
- Orders
- Customers
- Products
- Countries
- Units
- Average Order Value

## Monthly Revenue

A monthly revenue time series is calculated and visualized.

## Country Analysis

The notebook calculates revenue by country and identifies the top countries by revenue.

## Product Analysis

Revenue is aggregated by:

```text
StockCode
Description
```

to identify the highest-revenue products.

## Revenue Distribution

A revenue distribution is created to study the shape and spread of transaction revenue.

The visualization applies a 99th-percentile cap **for visualization only**, so that extreme observations do not compress the main body of the chart.

## Quantity Boxplot

A boxplot is used to examine the distribution of purchased quantities.

## Quantity vs Unit Price

A scatter plot is used to investigate the relationship between quantity and unit price.

## Correlation Analysis

The notebook calculates correlations between:

```text
Quantity
UnitPrice
Revenue
```

and presents the result using a correlation heatmap.

## Day-of-Week Analysis

Revenue is aggregated by:

```text
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
```

to identify weekly patterns.

## Interactive Visualization

Plotly is used to create an interactive monthly revenue visualization.

The interactive chart can be exported as:

```text
outputs/interactive_monthly_revenue.html
```

---

# WEEK 4 — Predictive Analysis

The Week 4 section develops a weekly revenue forecasting workflow.

## Forecast Target

The target variable is:

```text
Weekly Revenue
```

The transaction-level revenue is aggregated into weekly revenue.

## Time Features

The notebook creates:

- Week of year
- Month
- Quarter
- Year
- Trend

## Lag Features

Historical revenue features are created using:

```text
Lag 1
Lag 2
Lag 3
Lag 4
Lag 8
Lag 12
```

## Rolling Features

Rolling historical averages are created using:

```text
4-week rolling mean
8-week rolling mean
12-week rolling mean
```

The rolling features are shifted so that future information is not directly used as a predictor.

## Train/Test Split

The final **8 weeks** are held out as the test period.

The remaining observations are used for model training.

## Baseline Forecast

A:

```text
4-Week Moving Average
```

is used as the baseline forecasting method.

## Machine-Learning Models

The notebook evaluates:

### Random Forest

Implemented using:

```python
RandomForestRegressor
```

### XGBoost

Implemented using:

```python
XGBRegressor
```

### LightGBM

Implemented using:

```python
LGBMRegressor
```

## Statistical Forecasting Benchmark

An Exponential Smoothing model from `statsmodels` is also evaluated.

## Model Metrics

Each forecasting approach is evaluated using:

- MAE — Mean Absolute Error
- RMSE — Root Mean Squared Error
- MAPE — Mean Absolute Percentage Error

## Model Comparison

All tested models are combined into a comparison table and the best-performing model is identified according to MAPE.

## Forecast Visualization

Actual values are compared against:

- Baseline
- XGBoost predictions

on the eight-week holdout period.

## XGBoost Feature Importance

The notebook extracts feature importance from the XGBoost model and visualizes the most influential variables.

## Walk-Forward Validation

`TimeSeriesSplit` is included to provide time-aware model validation rather than random cross-validation.

## SHAP Explainability

SHAP is used to explain the contribution of the XGBoost features to model predictions.

## Prophet Benchmark

Prophet is included as an additional time-series forecasting benchmark.

---

# WEEK 5 — Impactful Evaluation

The Week 5 section evaluates whether the predictive approach provides an improvement relative to the baseline.

## Baseline vs XGBoost

The notebook compares:

```text
4-Week Moving Average Baseline
vs
XGBoost
```

using absolute percentage error.

## Forecast Improvement

Relative forecast improvement is calculated as:

```text
(Baseline MAPE - Model MAPE)
--------------------------------
Baseline MAPE
```

The result may be positive or negative. The project does not force an advanced model to outperform the baseline.

## Paired Statistical Test

A paired t-test is performed on the baseline and advanced-model absolute percentage errors.

## Wilcoxon Test

A Wilcoxon signed-rank test is included as a non-parametric sensitivity analysis.

## Bootstrap Confidence Interval

5,000 bootstrap samples are used to estimate a 95% confidence interval for the difference in forecast errors.

## Week 5 Evaluation Table

The notebook brings together:

- Baseline MAPE
- XGBoost MAPE
- Relative improvement
- Paired t-test p-value
- Wilcoxon p-value
- Bootstrap confidence interval

---

# WEEK 5 — Prescriptive Analysis

The second Week 5 section demonstrates a resource-allocation optimization scenario.

## Product Scenario

The analysis selects the top products from the most recent 56 days according to revenue and calculates:

- Revenue
- Units
- Orders

## Scenario Margin Assumption

Because the UCI Online Retail dataset does not contain actual product margins, an assumed margin-rate range is used for demonstration.

The margin assumptions must therefore be interpreted as:

```text
Scenario assumptions
```

and not as actual company financial data.

## Contribution Calculation

The notebook estimates:

```text
Average Price
Contribution Per Unit
```

## Resource Capacity

A scenario capacity is defined as a proportion of recent product units.

## SciPy Optimization

`scipy.optimize.linprog` is used to determine a recommended allocation under the capacity constraint.

## Optimization Output

The result contains:

- Product
- Units
- Assumed margin
- Recommended allocation
- Expected contribution

This is a **prescriptive scenario analysis**, not a claim of actual company savings.

---

# SQLAlchemy

A separate SQL section demonstrates how the cleaned sales dataset can be loaded into SQLite.

The table is:

```text
sales
```

A SQL query is used to calculate the top countries by revenue and number of orders.

The implementation demonstrates:

```text
pandas
+
SQLAlchemy
+
SQLite
+
SQL
```

---

# Pandera — Data Quality Validation

The notebook contains a Pandera schema for the cleaned sales data.

The validation checks fields including:

- InvoiceNo
- StockCode
- Description
- Quantity
- UnitPrice
- CustomerID
- Country
- Revenue

The schema checks include non-null requirements and a positive `UnitPrice`.

This provides an executable data-quality gate after the cleaning stage.

---

# Python Libraries Used in the Notebook

The notebook uses the following libraries:

| Library | Purpose |
|---|---|
| pandas | Data loading, transformation and analysis |
| NumPy | Numerical calculations |
| matplotlib | Static charts |
| seaborn | Statistical visualization |
| Plotly | Interactive visualization |
| SciPy | Statistical testing and optimization |
| scikit-learn | Metrics, Random Forest and time-series validation |
| XGBoost | Predictive modelling |
| LightGBM | Predictive modelling |
| statsmodels | Exponential Smoothing |
| Prophet | Forecasting benchmark |
| SHAP | Model explainability |
| PuLP / SciPy optimization concepts | Prescriptive optimization |
| SQLAlchemy | Database / SQL implementation |
| Pandera | Data-quality validation |

---

# Project Outputs

When the notebook is executed, the major output files are organized under:

```text
outputs/
```

Important files include:

```text
outputs/
│
├── week1/
│   └── strategic_kpis.csv
│
├── week2/
│   ├── quality_summary.csv
│   ├── online_retail_sales_clean.csv
│   └── online_retail_returns.csv
│
├── week3/
│   └── analysis outputs and charts
│
├── week4/
│   ├── model_comparison.csv
│   └── forecast_predictions.csv
│
└── week5/
    ├── impact_evaluation.csv
    └── optimization_results.csv
```

Additional interactive visualizations and analysis files are also generated by the notebook.

---

# How to Run

## 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd YOUR_REPOSITORY_NAME
```

## 2. Create the Python environment

```bash
conda create -n retail_internship python=3.11 -y
conda activate retail_internship
```

## 3. Install the core packages

```bash
pip install pandas numpy openpyxl scipy matplotlib seaborn plotly scikit-learn statsmodels xgboost lightgbm shap sqlalchemy pandera
```

For the optional forecasting benchmark:

```bash
pip install prophet
```

## 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
Internship_Project.ipynb
```

Select the:

```text
Python - Retail Internship
```

kernel.

## 5. Execute the notebook from top to bottom

The recommended execution order is:

```text
Week 1
↓
Week 2
↓
Week 3
↓
Week 4
↓
Week 5
↓
SQLAlchemy
↓
Pandera validation
```

---

# Project Objective

The overall objective is to demonstrate a complete analytics workflow using a real-world transactional dataset:

```text
Raw Retail Data
      ↓
Strategic Baseline
      ↓
Data Cleaning
      ↓
Exploratory Analysis
      ↓
Predictive Forecasting
      ↓
Statistical Impact Evaluation
      ↓
Prescriptive Optimization
      ↓
SQL / Data Quality Validation
```

The project emphasizes reproducibility and evidence-based conclusions.

Model performance is reported based on the actual results generated from the UCI Online Retail dataset. Illustrative values from the original strategic planning document are not treated as observed company results.

---

# Limitations

The UCI Online Retail dataset is a public historical transaction dataset and does not provide all information that would be required for a production enterprise analytics system.

In particular, it does not provide:

- Actual inventory carrying costs
- Warehouse capacity
- Product cost
- Actual product margin
- Procurement lead times
- Service-level targets
- Future operational data

Therefore, the predictive and optimization results should be interpreted as an analytical internship demonstration and scenario study rather than as actual recommendations issued to the original retailer.

The forecasting dataset also covers approximately one year, which limits reliable estimation of longer-term year-over-year seasonality.

---

# Internship Deliverable Mapping

| Internship Week | Notebook Section |
|---|---|
| Week 1 | Strategic baseline and Horizon 3 roadmap |
| Week 2 | Data collection, cleaning, missing values, cancellations, outliers and validation |
| Week 3 | Exploratory Data Analysis and visualization |
| Week 4 | Predictive analysis, model comparison, validation, SHAP and Prophet |
| Week 5 | Impact evaluation, statistical testing, bootstrap CI and prescriptive optimization |

---

# Author

**Pritam Dey**

Data Analytics Internship Project

Data Analytics Strategist Track

---

# Repository Notes

The main evaluator-facing artifact is:

```text
Internship_Project.ipynb
```

The supporting Python and validation files are included to make the workflow reproducible and easier to inspect.

The dataset should be attributed to the UCI Machine Learning Repository according to its published dataset terms.

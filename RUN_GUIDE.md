# RUN GUIDE — Evaluator / User

## 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
cd Online_Retail_Internship
```

## 2. Create environment

```bash
conda create -n retail_internship python=3.11 -y
conda activate retail_internship
pip install -r requirements.txt
```

## 3. Launch Jupyter

```bash
jupyter notebook
```

Open:

```text
Internship_Project.ipynb
```

Choose the `retail_internship` kernel.

## 4. Execute in order

```text
Week 1 → Week 2 → Week 3 → Week 4 → Week 5
```

## 5. Or run the complete pipeline

```bash
python scripts/00_master_pipeline.py
```

Outputs are created under:

```text
outputs/week1
outputs/week2
outputs/week3
outputs/week4
outputs/week5
```

## 6. FastAPI demonstration

From the repository root:

```bash
python -m uvicorn api.app:app --reload
```

Open:

- http://127.0.0.1:8000
- http://127.0.0.1:8000/docs
- http://127.0.0.1:8000/kpis

## 7. Optional tools

Prophet, SHAP, TensorFlow, Great Expectations and Airflow are documented as
optional/advanced components. Install them with:

```bash
pip install -r requirements-optional.txt
```

Airflow should be run in a dedicated supported Airflow environment rather
than by executing the DAG file directly.

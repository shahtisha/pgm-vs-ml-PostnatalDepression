# Bayesian Networks vs. Machine Learning for Postnatal Depression Prediction

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1oWtHCQScPKuGxC1X4JYpEW-f0VUGZAmA?usp=sharing)
![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![pgmpy](https://img.shields.io/badge/pgmpy-1.1.2-green)

---

## What is this?

A comparative study evaluating **Bayesian network structure-learning methods** against **standard machine learning classifiers** for predicting anxiety in postnatal depression screening — with a focus on how each model handles **missing data**, which is a realistic and common problem in clinical questionnaire datasets.

---

## Models Used

**PGM side:**
- Chow-Liu Tree Search
- Hill-Climbing Search
- PC Algorithm
- Naive Bayes

**ML side:**
- Logistic Regression
- Random Forest
- XGBoost

---

## Dataset

Questionnaire responses from mothers at a medical hospital (n=1,503), covering postnatal depression symptoms and demographic indicators. Target variable: **Feeling anxious** (Yes/No).

---

## How to Run

Click **Open in Colab** above — no setup needed, just run the notebook.

If running locally:
```bash
pip install pgmpy xgboost scikit-learn pandas numpy matplotlib
```

---

## Paper

Full write-up included as `research_paper.pdf` in this repo.

---

*This project was built as part of a research study on probabilistic graphical models applied to mental health data.*

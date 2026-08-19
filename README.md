# Comparative Study of Bayesian Networks and ML Models for Postnatal Depression Prediction Under Missing Data

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1oWtHCQScPKuGxC1X4JYpEW-f0VUGZAmA?usp=sharing)
![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python)
![pgmpy](https://img.shields.io/badge/pgmpy-1.1.2-green)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## Overview

This project presents a controlled, comparative study evaluating **four Bayesian network structure-learning methods** against **three standard machine learning classifiers** for predicting anxiety in postnatal depression screening — with a specific focus on **missing-data robustness**, a property rarely tested directly in prior work.

### Models Compared

| Model | Type |
|---|---|
| Chow-Liu Tree Search | PGM (Bayesian Network) |
| Hill-Climbing Search | PGM (Bayesian Network) |
| PC Algorithm | PGM (Bayesian Network) |
| Naive Bayes | PGM (Bayesian Network) |
| Logistic Regression | Machine Learning |
| Random Forest | Machine Learning |
| XGBoost | Machine Learning |

---

## Key Findings

- **PC Algorithm** achieved the highest accuracy (up to **97.12%**) but produced the densest, least interpretable structure — confirming a quantifiable **accuracy vs. interpretability trade-off** among Bayesian network variants.
- Under increasing artificial test-set missingness (10–40%, MCAR), **all four Bayesian network variants degraded far more gracefully** than the machine learning classifiers.
- **XGBoost's native missing-value handling** did not prevent a sharp accuracy drop: **89.91% → 61.67%** at 40% missingness — contrary to a common assumption in applied ML.
- **Age** was independently identified as the weakest predictor by three different methods (Hill-Climbing excluded it entirely from the learned structure; Random Forest and XGBoost both ranked it last in feature importance).
- The relative ordering of model robustness was consistent across **two independently constructed dataset baselines**, confirming the findings are not an artifact of a single data-cleaning choice.

---

## Dataset

The dataset consists of **1,503 questionnaire responses** collected from mothers at a medical hospital, covering postnatal depression symptoms and demographic information.

| Variable | Description |
|---|---|
| Age | Age group of respondent |
| Feeling sad or Tearful | Sadness/tearfulness frequency |
| Irritable towards baby & partner | Irritability reported |
| Trouble sleeping at night | Sleep difficulty |
| Problems concentrating or making decision | Concentration issues |
| Overeating or loss of appetite | Eating habit changes |
| **Feeling anxious** | **Target variable (Yes/No)** |
| Feeling of guilt | Reported guilt |
| Problems of bonding with baby | Bonding difficulty |
| Suicide attempt | History of suicide attempt |

**Target class balance:** 64.92% anxious / 35.08% not anxious (Baseline 1)

---

## Methodology

### Two Baseline Dataset Variants
- **Baseline 1 (n=1,491):** Real-world missing values retained in `Suicide attempt` (22.5% missing)
- **Baseline 2 (n=1,156):** Fully complete, zero missing values

### Missing-Data Robustness Experiment
Each model was trained **once** on clean data, then evaluated against test sets with progressively increasing artificial missingness (10%, 20%, 30%, 40% MCAR), **without retraining** — isolating inference-time robustness from structure-learning requirements.

### Missing-Data Handling Per Model Type
| Model | Strategy |
|---|---|
| Bayesian Networks | Variable elimination with partial evidence (native) |
| Logistic Regression, Random Forest | Mode imputation before inference |
| XGBoost | Native sparsity-aware split routing |

---

## Results Summary

| Model | Type | Baseline 1 Acc | Baseline 2 Acc | Acc @ 40% Missing |
|---|---|---|---|---|
| PC Algorithm | PGM | 95.88% | 97.12% | 89.63% |
| Hill Climb Search | PGM | 85.00% | 87.03% | 81.27% |
| Naive Bayes | PGM | 80.00% | 83.57% | 79.83% |
| Tree Search | PGM | 77.35% | 80.40% | 76.08% |
| Random Forest | ML | 86.83% | 91.93% | 79.83% |
| XGBoost | ML | 88.84% | 89.91% | **61.67%** |
| Logistic Regression | ML | 83.04% | 80.98% | 76.66% |

---

## Repository Structure

```
PPD-/
├── PGM_vs_ML_project.ipynb     ← Full Colab notebook (code + outputs)
├── post natal data.csv          ← Raw dataset
├── research_paper.pdf           ← Full research paper
└── README.md
```

---

## How to Run

Click the **Open in Colab** badge above to open the notebook directly — no local setup needed.

If running locally:

```bash
pip install pgmpy xgboost scikit-learn pandas numpy matplotlib
```

Then run the notebook top to bottom. The dataset (`post natal data.csv`) must be in the same directory or update the file path in the first cell.

---

## Paper

The full research paper is included as `research_paper.pdf`.

**Title:** Robustness Versus Accuracy: Comparing Bayesian Networks and Machine Learning for Postnatal Depression Prediction with Incomplete Data

**Authors:** Tisha Shah, Pooja Vartak, Kanchan Dabre

---

## Requirements

```
Python       3.10+
pgmpy        1.1.2
xgboost      ≥1.7
scikit-learn ≥1.2
pandas       ≥1.5
numpy        ≥1.23
matplotlib   ≥3.6
```

---

## License

This project is licensed under the MIT License.

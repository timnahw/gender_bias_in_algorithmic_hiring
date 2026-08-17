# Gender Bias in Algorithmic Hiring: A Systematic Literature-Based Synthetic Data Generating Process for Studying Algorithmic Discrimination

**Type:** Bachelor's Thesis

**Author:** Timnah Weckner

**1st Examiner:** Prof. Dr. Stefan Lessmann

**2nd Examiner:** Prof. Dr. Jan Mendling

## Table of Content

- [Summary](#summary)
- [Working with the repo](#working-with-the-repo)
    - [Dependencies](#dependencies)
    - [Setup](#setup)
- [Reproducing results](#reproducing-results)
    - [Training code](#training-code)
    - [Evaluation code](#evaluation-code)
- [Project structure](#project-structure)

## Summary

This thesis investigates gender bias in AI-supported hiring by developing a systematic, literature-based synthetic data generating process (DGP) for the hiring context. Building on a systematic review of the empirical literature on gender differences in job applications and algorithmic discrimination, the DGP produces fair and unfair applicant-hiring datasets with a continuously variable degree of direct discrimination, enabling controlled experiments on gender bias in algorithmic hiring decisions. Using this framework, a Logistic Regression baseline classifier is trained across an 11-point discrimination sweep, and one bias-correction method from each family (pre-, in-, and post-processing) is applied. They are being compared using standard fairness metrics (Disparate Impact, Equal Opportunity Difference) alongside predictive accuracy. The results quantify how far algorithmic correction can reduce measured discrimination toward zero, and where the limits of correctability lie.

**Keywords**: gender bias, algorithmic hiring, algorithmic discrimination, synthetic data generation, bias correction, algorithmic fairness

## Working with the repo

### Dependencies

- All required libraries are listed in [`requirements.txt`](requirements.txt)

### Setup

1. Clone this repository
```bash
git clone https://github.com/timnahw/gender_bias_in_algorithmic_hiring
cd gender_bias_in_algorithmic_hiring
```

2. Create a virtual environment and activate it
```bash
python -m venv venv
source venv/bin/activate
```

3. Install requirements
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

## Reproducing results

All results are produced by a single notebook, [`DGP_and_Experiment.ipynb`](DGP_and_Experiment.ipynb), which implements both the DGP (thesis Chapter 3) and the bias-correction experiment (thesis Chapter 4).

1. Activate the environment set up above and launch Jupyter:
```bash
jupyter notebook DGP_and_Experiment.ipynb
```
2. Run the notebook **top to bottom, in one session**.
3. All 11 sweep datasets are generated fresh from fixed, explicit seeds, so results are exactly reproducible without needing to download any external data.

**Runtime:** roughly 1.5–2 hours end to end on a standard laptop, dominated by the GridSearch cells (Sections 12 and 12a, ~50 min and ~25–40 min respectively). GridSearch checkpoints its progress after every dataset, so an interruption does not lose completed work.

### Training code

Sections 10–13 of the notebook train the baseline Logistic Regression classifier and apply the three bias-correction methods (Reweighing, GridSearch, ThresholdOptimizer) across the discrimination sweep, using 25 repeated train/test splits per dataset.

### Evaluation code

Fairness metrics (Disparate Impact Ratio, Equal Opportunity Difference) and predictive accuracy are computed inline in Sections 10–15 of the notebook and combined into a single comparison table in Section 14.

## Project structure

```bash
├── README.md
├── requirements.txt
├── .gitignore
├── DGP_and_Experiment.ipynb
```
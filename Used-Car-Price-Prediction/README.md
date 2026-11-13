# Used-Car Price Analysis — Data Science Portfolio

**Student:** Dorian Nowacki (C00288163)  
**Repository:** https://github.com/onlydoryy/Data-Science  
**Project:** Data Science & Machine Learning continuous assessment, 2026

## Overview

The Jupyter notebook `Automobile_Price_Analysis.ipynb` studies 30,824 used-vehicle listings in `public_cars.csv`. It contains:

1. Data exploration, cleaning and analysis of car-price patterns.
2. **Linear Regression** and **Random Forest Regression** for predicting listed prices in USD.
3. **Logistic Regression** for classifying listings as **below $15,000** or **$15,000 and above**.
4. **K-Means Clustering** on model year, mileage and engine capacity, with post-hoc comparisons of prices.
5. Evaluation graphs, appropriate metrics, conclusions, limitations and references.

The notebook is the main assessed technical portfolio. The weekly work diary must be included at submission.

## How to run

1. Download or clone this repository.
2. Open a terminal in the `Used-Car-Price-Prediction` folder.
3. Ensure Python 3.10+ is available; ideally use a virtual environment.
4. Install packages: `python -m pip install -r requirements.txt`
5. Run `jupyter notebook` or `jupyter lab` (if JupyterLab is installed).
6. Open `Automobile_Price_Analysis.ipynb`.
7. Choose **Kernel → Restart Kernel and Run All Cells**, verify no exceptions, and save the notebook.

The CSV is read by relative filename, so **the notebook and `public_cars.csv` must remain in the same folder**. A fresh run trains the models and generates the plots; no external API is needed. Execution speed depends on hardware.

## Method summary

- Regression task: 80/20 train/test split with random state 42; numeric imputation and scaling plus categorical one-hot encoding; report MAE, RMSE and R².
- Classification task: fixed $15k boundary; **stratified** 80/20 train/test split; report baseline accuracy, accuracy, balanced accuracy, class-1 precision/recall/F1, ROC AUC and confusion matrix.
- Clustering task: standardised year/mileage/engine size (price excluded); compare k = 2...6 using a sampled silhouette score and inertia; profile clusters afterwards by median listing price.
- Models are for an academic demonstration; neither the listing prices nor trained models are a reliable third-party vehicle valuation.

## Source note

The source file provided with the project is `public_cars.csv`. A [public Kaggle listing with matching schema](https://www.kaggle.com/datasets/sivaakhilnukala/used-cars-price) was located, but the original download provenance **must be confirmed by the student** before asserting that this Kaggle page is the exact source. Library documentation is cited in the notebook.

## Required final checks

- Confirm the original dataset source and any lecturer-approved scope changes.
- Populate and submit the real work diary (see `WORK_DIARY_TEMPLATE.md`).
- Restart/run every Jupyter cell, save updated outputs, check all plots and explain every model choice.
- Submit the notebook, CSV, code, references and relevant notes before the published deadline.
- Prepare and deliver the mandatory portfolio presentation.

**Final portfolio:** Friday **27 November 2026, 17:00** (updated brief). **Presentation:** week of 30 November 2026. The brief contains conflicting historical years in body text; follow the deliverables section and Moodle announcements.

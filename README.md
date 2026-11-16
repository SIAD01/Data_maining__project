<div align="center">

# 🏁 F1: Why Does a Driver Win or Lose?

**Driver, car or starting grid: what really decides a Formula 1 win?**

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-data%20cleaning-150458?logo=pandas&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-modelling-F7931E?logo=scikitlearn&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-interactive%20page-F7DF1E?logo=javascript&logoColor=black)
![License](https://img.shields.io/badge/License-MIT-green)

[Overview](#-overview) · [Structure](#-project-structure) · [Method](#-methodology) · [Results](#-key-results) · [Demo](#-interactive-page) · [Run it](#-how-to-run)

<!-- Add a screenshot of the page here:
![Interactive page](docs/screenshot.png)
-->

</div>

---

## 📌 Overview

This project asks a simple question: **why does a Formula 1 driver win or lose a race?**

Three factors compete to explain a result: the **driver’s skill**, the **car’s quality**, and the **starting position**. Using every race from **2003 to 2024**, I cleaned and merged the official F1 data, explored it, and built statistical models to measure how much each factor matters.

The final model powers an **interactive web page** where anyone can pick a driver, a car, a season and a grid slot, and see the **win probability** and the **main reason** for the result.

## 📁 Project structure

```
f1-win-lose-cause/
├── README.md                              # problem, method, results, how to run
├── requirements.txt
├── LICENSE                                # MIT
├── .gitignore
├── data/
│   ├── README.md                          # source + description of the data
│   ├── raw/archive.zip                    # original 14 CSV files
│   └── processed/                         # f1_cleaned.csv is created here by the notebook
├── notebooks/
│   └── 01_cleaning_eda_modelling.ipynb    # cleaning + EDA + models
└── app/
    └── index.html                         # interactive page (standalone)
```

## 🔬 Methodology

| Step | What was done |
|---|---|
| **1. Cleaning** | Merged 7 tables (`results`, `races`, `drivers`, `constructors`, `circuits`, `status`, `qualifying`) with a check that no row was duplicated. Renamed columns, kept seasons ≥ 2003, parsed dates and lap times, computed driver age, created the targets `win`, `podium`, `DNF`, handled pit-lane starts, removed duplicates and missing values. |
| **2. EDA** | Podium rate by team and grid slot, class balance (wins ≈ 5 % of starts), distributions, box plots, grid vs finishing position, correlation heatmap. |
| **3. Variance decomposition** | OLS regressions (adjusted R²): unique share of the finishing order explained by driver, car and circuit. |
| **4. Prediction** | Logistic regression with cross-validation grouped by race (AUC) for each factor. |
| **5. Driver vs teammate** | Same car, same race: removes the car effect and shows who really outperforms. |
| **6. Final model** | Logistic regression (driver + team + grid + year) embedded in the web page. |

## 📊 Key results

| Factor | Finishing order explained (R²) | Win prediction (AUC) |
|---|:---:|:---:|
| 🏎️ Car alone | **40 %** | 0.91 |
| 🚦 Starting grid alone | 36 % | **0.94** (grid + qualifying) |
| 🧑‍✈️ Driver alone | 26 % | 0.86 |
| 🏟️ Circuit alone | 0 % | 0.50 (no better than chance) |

**Conclusions**
1. The **car** matters more than the driver alone.
2. The **starting grid** is the best single predictor because it already reflects both car and driver.
3. The **circuit** has almost no effect on who wins.
4. The best drivers (Verstappen, Alonso, Norris, Gasly, Hamilton…) still beat their teammates: skill matters, but it is limited by the car.

## 🖥️ Interactive page

Open [`app/index.html`](app/index.html) in any browser, with no install needed.

- Choose a **driver**, a **car**, a **season** and a **starting position**
- See the **win probability** on a gauge and the **main reason** for the result
- See how much the **grid, car and driver** each contribute
- Try the **“what if”** table (for example, the same driver in an average car)
- The page checks its own predictions against scikit-learn on **5 real races**

<!-- Live demo (after enabling GitHub Pages): https://<your-username>.github.io/f1-win-lose-cause/app/ -->

## ▶️ How to run

```bash
git clone https://github.com/<your-username>/f1-win-lose-cause.git
cd f1-win-lose-cause
python -m venv .venv
source .venv/bin/activate          # Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook notebooks/01_cleaning_eda_modelling.ipynb
```

The notebook extracts `data/raw/archive.zip` and creates `data/processed/f1_cleaned.csv` by itself.

## ⚠️ Limitations

- Results show **correlation, not strict causality**: the best drivers tend to drive the best cars.
- Wins are rare (≈ 5 %), so predictions for unusual combinations are less reliable.
- Rare drivers and teams are grouped as “other” in the final model.

## 🧰 Tech stack

Python · pandas · NumPy · matplotlib · seaborn · statsmodels · scikit-learn · HTML / CSS / JavaScript

## 📄 License

Code under the [MIT License](LICENSE). Data © the authors of the original Formula 1 dataset (see [`data/README.md`](data/README.md)).

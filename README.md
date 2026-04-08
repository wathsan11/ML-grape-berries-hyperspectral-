# 🍇 Grape Berries Sugar Content Prediction using Hyperspectral Imaging

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/wathsan11/ML-grape-berries-hyperspectral-/blob/main/GrapeBerriesHyperspectral.ipynb)

## Overview

This project applies machine learning to predict the **sugar content (g/l)** of grape berries using **hyperspectral imaging data**. By capturing light reflectance across 204 spectral wavelength bands (approximately 397 nm to 1003 nm), the goal is to enable non-destructive, fast sugar estimation — a key quality indicator in viticulture and winemaking.

---

## Dataset

The dataset (`grapes.csv`) contains hyperspectral reflectance measurements of grape berries across three varieties:

| Feature | Description |
|---|---|
| `Variety` | Grape variety: `SYRAH`, `MAUZAC`, `FER` |
| `Sugar content (g/l)` | Target variable — sugar concentration |
| `x.397.32` → `x.1003.5` | 204 spectral reflectance bands (wavelength in nm) |

- **Total features:** 207 columns (including index and metadata)
- **Spectral range:** ~397 nm to ~1003 nm
- **Task type:** Supervised regression

---

## Project Structure

```
ML-grape-berries-hyperspectral/
│
├── GrapeBerriesHyperspectral.ipynb   # Main Jupyter notebook
├── grapes.csv                        # Dataset (add to Google Drive)
└── README.md
```

---

## Methodology

### 1. Exploratory Data Analysis (EDA)
- Distribution of sugar content across grape varieties (SYRAH, MAUZAC, FER)
- Variety balance visualized via pie chart
- Spectral signature plots (wavelength vs. intensity) for individual samples and variety groups
- Correlation between specific wavelength bands and sugar content

### 2. Data Preprocessing
- Target: `Sugar content (g/l)`
- Features: All spectral bands + one-hot encoded `Variety`
- Train / Validation / Test split: **60% / 20% / 20%**
- Feature scaling with `StandardScaler`

### 3. Models Trained

#### Linear Regression
- Baseline model trained on scaled features
- Overfitting observed on raw high-dimensional features
- Polynomial features (degrees 1–3) explored; RAM constraints limited higher degrees
- PCA + Polynomial feature engineering pipeline tested at various component counts

#### Random Forest Regressor
- Hyperparameter tuning via manual grid search:
  - `min_samples_split`: [2, 10, 15, 20, 25, 30, 40, 50, 100]
  - `max_depth`: [2, 4, 5, 6, 7, 8, 10, 12, 14, 16, 18, 20, 24, 32, None]
  - `n_estimators`: [10, 20, 50, 60, 70, 75, 80, 90, 100, 120, 125, 150, 200, 250, 300]
- Best configuration: `n_estimators=150`, `max_depth=10`, `min_samples_split=30`

---

## Results

### Linear Regressionr (Best Model)

| Split | MSE |
|---|---|
| Training | 148.15 |
| Cross-Validation | 102.56 |
| Test | 235.98 |

| Metric | Value |
|---|---|
| Test RMSE | 15.36 |
| Test R² | 0.73 |

### Random Forest Regressor 

| Split | MSE |
|---|---|
| Training | 142.49 |
| Cross-Validation | 149.01 |
| Test | 355.94 |

| Metric | Value |
|---|---|
| Test RMSE | 18.87 |
| Test R² | 0.59 |

---

## Technologies Used

- **Python 3**
- **NumPy**, **Pandas** — data manipulation
- **Matplotlib**, **Seaborn** — visualization
- **Scikit-learn** — PCA, StandardScaler, LinearRegression, RandomForestRegressor, train_test_split, metrics
- **Google Colab** — development environment

---

## How to Run

1. Clone this repository:
   ```bash
   git clone https://github.com/wathsan11/ML-grape-berries-hyperspectral-.git
   ```

2. Upload `grapes.csv` to your Google Drive under:
   ```
   My Drive/Machine Learning/grapes.csv
   ```

3. Open `GrapeBerriesHyperspectral.ipynb` in [Google Colab](https://colab.research.google.com/) and run all cells.

> **Note:** Polynomial feature engineering beyond degree 3 may cause RAM issues in the free Colab tier.

---

## Real-World Application

Hyperspectral-based sugar prediction can support:
- **Smart harvesting** — determine optimal ripeness without physical sampling
- **Quality control** — non-destructive testing at scale
- **Precision viticulture** — variety-specific monitoring across a vineyard

---

## License

This project is open-source and available under the [MIT License](LICENSE).

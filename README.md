<div align="center">

### Exoplanet KOI Classifier

</div>

<div align="center">

[![Python](https://img.shields.io/badge/Python-3776AB?logo=python&logoColor=fff)](#) [![Scikit-learn](https://img.shields.io/badge/-scikit--learn-%23F7931E?logo=scikit-learn&logoColor=white)](#) [![Pandas](https://img.shields.io/badge/Pandas-150458?logo=pandas&logoColor=fff)](#) [![Matplotlib](https://custom-icon-badges.demolab.com/badge/Matplotlib-71D291?logo=matplotlib&logoColor=fff)](#) [![Seaborn](https://img.shields.io/badge/Seaborn-4EAEAA?logo=python&logoColor=fff)](#) [![Jupyter](https://img.shields.io/badge/Jupyter-ffffff?logo=Jupyter)](#)

</div>

---

### Overview

A machine learning classifier that separates real exoplanets (`CONFIRMED`), unresolved signals (`CANDIDATE`), and non-planetary artifacts (`FALSE POSITIVE`) using NASA Kepler Objects of Interest (KOI) data. Built for the India High School Exoplanet Data Challenge, the project uses transit photometry features to train XGBoost and Random Forest models, achieving 85.9% accuracy with proper feature engineering and leakage prevention.

---

### Results

| Model | Accuracy | Precision (macro) | Recall (macro) | F1 (macro) |
|-------|----------|-------------------|----------------|------------|
| Random Forest | 84.2% | 0.811 | 0.819 | 0.814 |
| **XGBoost (selected)** | **85.9%** | **0.829** | **0.835** | **0.832** |

---

### Usage

Install dependencies and run the notebook:

```bash
pip install -r requirements.txt
jupyter notebook exoplanet_classification.ipynb
```

Or execute the entire notebook non-interactively:

```bash
jupyter nbconvert --to notebook --execute --inplace exoplanet_classification.ipynb
```

---

### Project Structure

```
exoplanet-koi-classifier/
├── exoplanet_classification.ipynb  # Full ML pipeline (EDA → model → evaluation)
├── data/
│   └── KOI_Cumulative_clean.csv    # NASA Kepler KOI dataset
├── requirements.txt                 # Python dependencies
└── README.md                        # This file
```

---

### Tech Stack

- **Core ML:** scikit-learn, XGBoost
- **Data Processing:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Environment:** Jupyter Notebook

---

### Key Design Decisions

- **Leakage prevention:** Dropped `koi_pdisposition` and `koi_fpflag_*` columns (NASA's vetting pipeline outputs) to ensure the model learns from physical transit signals, not the answer key
- **Class imbalance:** Handled via `class_weight='balanced'` (Random Forest) and balanced sample weights (XGBoost) rather than resampling, given moderate ~2.4:1 imbalance
- **Feature engineering:** Derived `snr_per_transit`, `depth_to_radius_ratio`, and `duration_period_ratio` to capture transit-geometry consistency — the same checks astronomers use to validate candidates

---

### Data Source

NASA Exoplanet Science Institute at IPAC, Caltech. Kepler Objects of Interest, Cumulative Table. DOI: [10.26133/NEA4](https://doi.org/10.26133/NEA4).

---

<div align="center">

Built by [Shaurya Chopra](https://shauryachopra.dev/)

</div>

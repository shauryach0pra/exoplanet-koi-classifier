# Exoplanet Candidate Classification — NASA Kepler KOI Data

A machine learning model that classifies NASA Kepler Objects of Interest (KOI) into
`CONFIRMED`, `CANDIDATE`, or `FALSE POSITIVE` using real transit and stellar
photometry data from the Kepler Space Telescope.

## Results

| Model | Accuracy | Precision (macro) | Recall (macro) | F1 (macro) |
|---|---|---|---|---|
| Random Forest | 84.2% | 0.811 | 0.819 | 0.814 |
| **XGBoost (selected)** | **85.9%** | **0.829** | **0.835** | **0.832** |

## Contents

- [`exoplanet_classification.ipynb`](exoplanet_classification.ipynb) — full pipeline:
  EDA → data cleaning → feature engineering → model training → evaluation → explainability,
  plus the written summary required by the challenge (embedded in the final markdown cell).
- [`data/KOI_Cumulative_clean.csv`](data/KOI_Cumulative_clean.csv) — the challenge's
  starter dataset (NASA Exoplanet Archive, Cumulative KOI table, DOI: 10.26133/NEA4).

## Key design decisions

- **Leakage prevention:** `koi_pdisposition` and the four `koi_fpflag_*` columns are
  outputs of NASA's own vetting pipeline and correlate almost perfectly with the
  target — they were dropped to keep the model learning from physical transit signal,
  not the answer key.
- **Class imbalance:** handled via `class_weight='balanced'` (Random Forest) and
  balanced sample weights (XGBoost) rather than resampling, since the imbalance is
  moderate (~2.4:1).
- **Feature engineering:** derived `snr_per_transit`, `depth_to_radius_ratio`, and
  `duration_period_ratio` to capture transit-geometry consistency — the same checks
  an astronomer would use to sanity-check a candidate.

## Reproducing

```bash
pip install -r requirements.txt
jupyter nbconvert --to notebook --execute --inplace exoplanet_classification.ipynb
```

## Data source

NASA Exoplanet Science Institute at IPAC, Caltech. Kepler Objects of Interest,
Cumulative Table. DOI: [10.26133/NEA4](https://doi.org/10.26133/NEA4).

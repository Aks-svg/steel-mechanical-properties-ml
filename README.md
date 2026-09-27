# Steel Mechanical Properties ML

Machine-learning study for predicting **Yield Strength (YS)**, **Ultimate Tensile Strength (UTS)**, and **Elongation (EL)** from 17 composition/process features in a 435-sample steel dataset.

## Project contents

- `notebooks/steel_mechanical_properties_ML.ipynb` — complete Colab/Jupyter workflow
- `data/steel_mechanical_properties_435.csv` — processed 435-row dataset
- `figures/` — final SHAP and prediction/residual figures
- `SUMMARY.md` — project results, discussion, and conclusion
- `requirements.txt` — Python dependencies

## Workflow

1. Data loading and quality checks
2. Descriptive statistics and target distributions
3. SciPy Shapiro-Wilk normality testing
4. Feature distribution and rare-level analysis
5. IQR-based outlier screening without deleting observations
6. Pearson/Spearman correlation analysis
7. VIF and multicollinearity analysis
8. Train/test split
9. Leakage-safe scaling and feature-selection workflow
10. Ridge, SVR, Random Forest, Extra Trees, Gradient Boosting, XGBoost, LightGBM and stacking comparison
11. Mutual-information feature selection
12. Repeated 5-fold cross-validation
13. Final held-out test evaluation
14. SHAP interpretation
15. Actual-vs-predicted and residual analysis

## Final model

The strongest overall configuration was **Random Forest with target-specific mutual-information feature selection**.

| Target | Selected features | Repeated-CV R² | Test R² |
|---|---|---:|---:|
| YS | Al, AlS, C, Cr, Mn, N, Nb, Ni, P, S, Si, Ti | 0.437 ± 0.140 | 0.141 |
| UTS | Al, AlS, C, Cr, Mn, N, Nb, Ni, P, S, Si, Ti | 0.566 ± 0.138 | 0.234 |
| EL | Al, AlS, C, Cr, Mn, N, Ni, P | 0.390 ± 0.111 | 0.549 |

## Important result

The available dataset does **not** support claiming an 85–95% held-out R². The project therefore reports leakage-safe cross-validation and untouched-test results rather than tuning against the test set to obtain an inflated score.

## Methodology reference

The supplied reference paper was used as a methodological guide for preprocessing, feature selection, nonlinear ML modeling, and R²/RMSE/MAE evaluation. Its dataset and performance values are not treated as results from this 435-sample dataset.

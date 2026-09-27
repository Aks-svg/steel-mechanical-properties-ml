# Project Summary

## Results and Discussion

The supplementary dataset contained **435 samples**, with 17 numerical input variables and three mechanical-property targets: **yield strength (YS), ultimate tensile strength (UTS), and elongation (EL)**. No missing values or duplicate records were identified. The data were divided into 80% training and 20% testing subsets. Model preprocessing and feature selection were performed within the training/CV workflow to avoid information leakage.

Several regression approaches were evaluated, including Ridge regression, SVR, Random Forest, Extra Trees, Gradient Boosting, XGBoost, LightGBM, and a stacking ensemble. Both standardized and min-max-scaled versions were considered for scale-sensitive models. Tree-based models did not require scaling.

Feature redundancy was evident between **Al and AlS**, with an approximately 0.999 Pearson correlation and very high VIF values. Mutual-information analysis was subsequently used for nonlinear feature screening.

The Random Forest model combined with target-specific mutual-information feature selection provided the strongest overall cross-validation performance.

### Selected features

- **YS:** Al, AlS, C, Cr, Mn, N, Nb, Ni, P, S, Si, Ti
- **UTS:** Al, AlS, C, Cr, Mn, N, Nb, Ni, P, S, Si, Ti
- **EL:** Al, AlS, C, Cr, Mn, N, Ni, P

### Repeated 5-fold cross-validation

| Target | R² | RMSE | MAE |
|---|---:|---:|---:|
| YS | **0.437 ± 0.140** | 13.15 | 9.40 |
| UTS | **0.566 ± 0.138** | 9.00 | 6.34 |
| EL | **0.390 ± 0.111** | 1.80 | 1.31 |

### Held-out test set

| Target | Test R² | Test RMSE | Test MAE |
|---|---:|---:|---:|
| YS | 0.141 | 15.14 | 10.51 |
| UTS | 0.234 | 9.40 | 6.44 |
| EL | **0.549** | 1.69 | 1.09 |

### SHAP interpretation

For **YS**, Cr was the most influential feature, followed by C and Mn. For **UTS**, C was the dominant feature, followed by N, Cr and Mn. For **EL**, Cr was the dominant feature, with Al, N, AlS, P and C also showing appreciable contributions. The SHAP distributions indicate nonlinear and non-monotonic effects that are not fully captured by simple Pearson correlation.

### Conclusion

Machine-learning models were developed to predict YS, UTS and EL from chemical-composition and process-related parameters. Multiple regression, tree-based, boosting and ensemble approaches were compared, with mutual-information-based feature selection and leakage-safe cross-validation. Random Forest with target-specific feature selection provided the strongest overall cross-validation performance. The available 435-sample dataset did **not** support an honest 0.85–0.95 held-out R² with the available 17 predictors; further tuning toward that number would risk overfitting. The results nevertheless demonstrate useful nonlinear relationships between composition/process variables and steel mechanical properties.

> **Important:** The reference paper used for methodology describes a larger dataset and should not be treated as the source of the performance numbers reported here.

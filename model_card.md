# Model Card: Multi-Function Predictive Models

## Overview

**Name:** Function Predictor Ensemble  
**Type:** Supervised regression / predictive modeling  
**Version:** 1.0  

This approach evaluates multiple regression models (Gaussian Processes, Tree Ensembles, K-Nearest Neighbors, Support Vector Regression, and Polynomial Linear Regression) across eight benchmark functions. The strategy is iterative: new data points are added safely, models are refitted, and predictions are compared using Leave-One-Out Cross-Validation (LOO-CV).

---

## Intended Use

### Primary Use Cases:

1. Predicting outputs for the eight benchmark functions based on input features.  
2. Supporting exploration and optimization via GP-based uncertainty (UCB) strategies.  
3. Incremental dataset updates for active learning or iterative optimization.  

### Recommended Models per Function:

| Function   | Observed Best Model(s)            | Notes |
|------------|----------------------------------|-------|
| Function 1 | GradientBoosting                 | Low RMSE/MAE; GP also strong. |
| Function 2 | GradientBoosting                 | Handles moderate non-linearity well. |
| Function 3 | GradientBoosting / RandomForest  | Tree ensembles capture local patterns. |
| Function 4 | Poly2_Linear / GP_Matern         | Polynomial trend; GP captures uncertainty. |
| Function 5 | GP_RBF / KNN                     | Handles large output variations; KNN effective locally. |
| Function 6 | Poly2_Linear / SVR               | Lower MAE; smooth trends captured. |
| Function 7 | SVR / KNN                        | Local neighborhood modeling effective; GP reasonable. |
| Function 8 | Poly2_Linear                     | Near-perfect fit with linear approximation; complex models not necessary. |

### Use Cases to Avoid:

- Extrapolation outside the training input ranges.  
- High-noise scenarios that violate GP assumptions.  
- Real-time, high-dimensional tasks without further optimization.  

---

## Details

- **Strategy:** Ten rounds of iterative data collection and model evaluation.  
- **Techniques Used:** Gaussian Processes (RBF and Matern kernels), Random Forest, Gradient Boosting, K-Nearest Neighbors, Support Vector Regression, Polynomial Linear Regression.  

### Workflow Evolution:

1. Initial datasets loaded per function (ranging from 10–40 datapoints).  
2. New points safely appended with safe_append.  
3. LOO-CV used to evaluate predictive accuracy.  
4. UCB-based GP selection used to suggest promising next points.  
5. Model comparison informs which model is best for each function.  

---

## Performance

LOO-CV metrics for all functions (RMSE and MAE):

### Function 1

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.000850 | 0.000380 |
| GP_Matern | 0.000850 | 0.000380 |
| RandomForest | 0.000915 | 0.000405 |
| GradientBoosting | 0.000827 | 0.000190 |
| KNN | 0.000955 | 0.000380 |
| SVR | 0.001877 | 0.001551 |
| Poly2_Linear | 0.000940 | 0.000557 |

### Function 2

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.221384 | 0.191486 |
| GP_Matern | 0.221384 | 0.191486 |
| RandomForest | 0.226732 | 0.186339 |
| GradientBoosting | 0.196533 | 0.157056 |
| KNN | 0.235702 | 0.199716 |
| SVR | 0.258362 | 0.202288 |
| Poly2_Linear | 0.281385 | 0.242595 |

### Function 3

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.077732 | 0.050260 |
| GP_Matern | 0.076815 | 0.047531 |
| RandomForest | 0.069859 | 0.040270 |
| GradientBoosting | 0.065738 | 0.033938 |
| KNN | 0.076302 | 0.050121 |
| SVR | 0.078528 | 0.056193 |
| Poly2_Linear | 0.089065 | 0.063063 |

### Function 4

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 4.679869 | 3.384646 |
| GP_Matern | 2.406792 | 1.665393 |
| RandomForest | 4.411253 | 3.168035 |
| GradientBoosting | 4.581905 | 3.356138 |
| KNN | 6.011942 | 4.354563 |
| SVR | 6.436734 | 5.136865 |
| Poly2_Linear | 2.035102 | 1.596206 |

### Function 5

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 137.951777 | 93.955912 |
| GP_Matern | 270.019393 | 173.354532 |
| RandomForest | 154.777769 | 100.748073 |
| GradientBoosting | 178.321883 | 92.971635 |
| KNN | 152.155275 | 91.066622 |
| SVR | 278.946550 | 140.165641 |
| Poly2_Linear | 180.680425 | 144.974140 |

### Function 6

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.273998 | 0.219426 |
| GP_Matern | 0.251774 | 0.199046 |
| RandomForest | 0.373881 | 0.290958 |
| GradientBoosting | 0.405479 | 0.317113 |
| KNN | 0.391291 | 0.285984 |
| SVR | 0.218367 | 0.163974 |
| Poly2_Linear | 0.204206 | 0.143211 |

### Function 7

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.309233 | 0.255213 |
| GP_Matern | 0.359393 | 0.280002 |
| RandomForest | 0.322555 | 0.246359 |
| GradientBoosting | 0.339748 | 0.251972 |
| KNN | 0.285741 | 0.203861 |
| SVR | 0.230503 | 0.149042 |
| Poly2_Linear | 0.475079 | 0.377647 |

### Function 8

| Model | RMSE | MAE |
|-------|------|------|
| GP_RBF | 0.280784 | 0.203945 |
| GP_Matern | 0.249230 | 0.172055 |
| RandomForest | 0.474052 | 0.355090 |
| GradientBoosting | 0.401282 | 0.307143 |
| KNN | 0.584574 | 0.419853 |
| SVR | 0.431597 | 0.332594 |
| Poly2_Linear | 0.000000 | 0.000000 |

---

## Assumptions and Limitations

- Assumes smooth functional relationships for GP and Polynomial models.  
- Tree ensembles assume local patterns dominate; may overfit if sampling is sparse.  
- KNN assumes dense sampling of the input space to be effective.  
- SVR assumes stationarity and limited noise; hyperparameters can influence performance heavily.  
- Models are unreliable for extrapolation outside observed input ranges.  
- GP-based UCB selection works best with low observation noise.  
- High-dimensional input spaces may require more candidates for robust UCB search.  
- Performance varies by function; per-function model selection is recommended.  

---

## Ethical Considerations

- **Transparency:** Complete documentation of dataset, model evaluation, and selection criteria supports reproducibility.  
- **Reproducibility:** Code and LOO-CV results allow independent verification of predictive performance.  
- **Limitations Disclosure:** Clearly communicates model constraints to avoid misuse.  
- **Responsible Use:** Intended for benchmark function prediction, active learning, and optimization experiments; not for high-risk real-world decision-making without further validation.

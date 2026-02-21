# Imperial College London – ML/AI Capstone BBO Project

## Overview

This repository contains the work developed for the **Imperial College London Machine Learning / AI Capstone Project** focused on **Black-Box Optimization (BBO)**.

The project investigates surrogate modelling approaches for approximating unknown real-valued benchmark functions and using those models to guide iterative exploration. In particular, it evaluates multiple regression techniques across eight benchmark functions of varying dimensionality (2–8 dimensions), comparing predictive performance and uncertainty-aware optimization strategies.

The core themes of this repository include:

- Function approximation in low-to-moderate dimensional spaces  
- Model comparison using Leave-One-Out Cross-Validation (LOO-CV)  
- Surrogate modelling for optimization  
- Exploration vs. exploitation trade-offs using acquisition strategies such as Upper Confidence Bound (UCB)  
- Incremental dataset expansion and active learning  

---

## Repository Structure

This repository includes:

- **Datasheet for the 8-Function Dataset**  
- **Model Card for the Multi-Function Predictive Models**  
- Implementation code for regression models and evaluation  
- Stored `.npy` datasets for each benchmark function  
- **Still a work in progress**

---

## About the Dataset (Datasheet)

The datasheet provides detailed documentation of the eight-function dataset, including:

- **Motivation**  
  - Purpose of the dataset (function approximation and Bayesian optimization)
  - Intended research and experimentation use cases  

- **Composition**  
  - Number of functions (8)  
  - Input dimensionality (2–8 dimensions)  
  - Initial sampling sizes and incremental additions  
  - Total datapoints per function  
  - Data format (NumPy arrays)  

- **Collection Process**  
  - Uniform random sampling in \([0,1]^D\)  
  - Incremental weekly submissions  
  - Model-guided candidate selection (e.g., GP-based UCB)  

- **Preprocessing and Usage Guidelines**  
  - No scaling or normalization of outputs  
  - Duplicate handling policy  
  - Appropriate and inappropriate use cases  

- **Distribution and Maintenance**  
  - Storage format (.npy files)  
  - Update process  
  - Terms of use  

The datasheet ensures transparency, reproducibility, and responsible usage of the benchmark dataset.

---

## About the Models (Model Card)

The model card documents the predictive modelling approach applied to the dataset.

It includes:

- **Model Overview**  
  - Ensemble comparison of:
    - K-Nearest Neighbors (KNN)
    - Decision Trees (DT)
    - Random Forest (RF)
    - Gradient Boosting (GB)
    - Gaussian Processes (RBF and Matern kernels)
    - Support Vector Regression (SVR)
    - Polynomial Linear Regression  

- **Intended Use**  
  - Surrogate modelling  
  - Iterative optimization  
  - Uncertainty-aware exploration (UCB strategies)  

- **Performance Evaluation**  
  - Leave-One-Out Cross-Validation (LOO-CV)  
  - RMSE and MAE metrics per function  
  - Function-specific best model recommendations  

- **Assumptions and Limitations**  
  - Smoothness assumptions (GP, polynomial models)  
  - Local pattern assumptions (tree ensembles)  
  - Limitations in extrapolation  
  - Sensitivity to sampling density and noise  

- **Ethical Considerations**  
  - Transparency and reproducibility  
  - Clear communication of limitations  
  - Not intended for safety-critical real-world decisions  

The model card ensures that model performance, constraints, and appropriate use cases are clearly documented.

---

## Project Goals

This capstone project aims to:

1. Compare surrogate models across multiple benchmark functions  
2. Evaluate predictive accuracy under small-sample regimes  
3. Study the impact of model choice on exploration strategies  
4. Demonstrate responsible ML documentation practices (Datasheets & Model Cards)  

---

## Intended Audience

- Machine Learning and AI students  
- Researchers in surrogate modelling and Bayesian optimization  
- Practitioners exploring black-box optimization workflows  

---

## Responsible Use

This repository is intended for educational and research purposes.  
It is not designed for high-stakes, safety-critical, or real-world deployment without further validation.

---

## Acknowledgement

Developed as part of the Imperial College London ML/AI Capstone Project on Black-Box Optimization.

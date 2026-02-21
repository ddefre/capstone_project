# Datasheet for the 8-Function Dataset

## 1. Motivation

### Purpose:

This dataset was created to support function approximation, regression modelling, and Bayesian optimization tasks. It is intended for testing and comparing different machine learning models (KNN, Decision Trees, Random Forests, Gradient Boosting, Gaussian Processes, SVR, and Polynomial Regression) in low-to-moderate dimensional spaces (2–8 dimensions).

### Use Case:

- Modelling real-valued functions where analytical expressions may be unknown.  
- Testing surrogate models for active learning / Bayesian optimization with uncertainty-aware acquisition strategies such as Upper Confidence Bound (UCB).  
- Supporting research and experimentation in regression accuracy, model selection, and exploration vs. exploitation trade-offs.  

### Intended Users:

- Data scientists, ML researchers, and students exploring function approximation, surrogate modelling, or automated optimization.  

---

## 2. Composition

### Overview:

| Function   | Input Dim | Initial Points | New Points Added | Total Points | Output Type |
|------------|----------|---------------|------------------|--------------|------------|
| Function 1 | 2 | 10 | 9 | 19 | Real-valued |
| Function 2 | 2 | 10 | 9 | 19 | Real-valued |
| Function 3 | 3 | 15 | 9 | 24 | Real-valued |
| Function 4 | 4 | 30 | 9 | 39 | Real-valued |
| Function 5 | 4 | 20 | 9 | 29 | Real-valued |
| Function 6 | 5 | 20 | 9 | 29 | Real-valued |
| Function 7 | 6 | 30 | 9 | 39 | Real-valued |
| Function 8 | 8 | 40 | 9 | 49 | Real-valued |

### Format and Structure:

- Inputs: Numpy arrays of shape (N, D), where N = number of points, D = input dimensions.  
- Outputs: Corresponding 1D numpy arrays (N,) of real-valued function evaluations.  
- Data Integrity: Each point is unique; duplicate points are updated rather than repeated.  
- Gaps / Missing Data: None—every input point has a corresponding output.  

---

## 3. Collection Process

### Generation of Queries / Input Points:

- Initial points were sampled uniformly at random in the domain [0, 1]^D.  
- Subsequent points were generated through incremental submission, either as part of experimentation or exploration guided by model suggestions (e.g., UCB for GP-based acquisition).  

### Time Frame:

- The dataset was collected in batches, with initial points and subsequent submissions per week for each function (currently a total of 9).  

### Strategy Notes:

- Designed to cover input space efficiently while allowing model-driven exploration.  
- Candidate points for UCB evaluation were randomly generated and evaluated using GP predictive mean and variance.  

---

## 4. Preprocessing and Uses

### Transformations Applied:

- None of the original function outputs were scaled or normalized.  
- Duplicate input points are detected via numerical tolerance (np.isclose) and their outputs updated.  

### Intended Uses:

- Regression analysis and model comparison.  
- Surrogate modelling for optimization.  
- Active learning experiments (e.g. using UCB or other acquisition functions).  

### Inappropriate Uses:

- Classification tasks — all outputs are continuous.  
- Extrapolation far outside [0,1]^D without further validation.  
- Any safety-critical or high-stakes predictions without further testing.  

---

## 5. Distribution and Maintenance

### Availability:

- Currently stored locally as numpy .npy files per function.  

### Terms of Use:

- Open for educational and research purposes.  
- Users must acknowledge the source if used in publications or shared analyses.  

### Maintenance:

- Maintained by the dataset creator (Imperial College London).  
- New points can be appended safely without duplicating previous entries after receiving the results of your weekly submission into the Imperial Capstone Emeritus website.  

### Future Plans:

- May expand with additional submissions, higher-resolution sampling, or alternative model-driven explorations.  

---

## 6. Reflections / Decisions

- Input dimensionality varies across functions (2–8) to test scalability of surrogate models.  
- GP models are used to quantify uncertainty and guide exploration.  
- Decision to add 9 submissions per function ensures incremental learning without overwhelming the original data distribution.  
- Leave-One-Out CV was selected for model evaluation due to small dataset sizes.  
- Candidate models include KNN, DT, RF, GB, GP, SVR, and polynomial regression pipelines, providing a diverse benchmark suite.  

# Lab 3 — Simple Linear Regression

**Course:** Machine Learning Lab
**Dataset:** Student Awareness Survey (`Student_Awareness_Survey.csv`)
**Language:** Python 3

---

## Objective

Build and evaluate Simple Linear Regression models to predict a student's GPA using CIA percentage and Attendance percentage as independent variables. The lab covers end-to-end ML workflow — preprocessing, modelling via Scikit-learn, manual OLS derivation, and model serialization.

---

## Dataset

| Column | Cleaned As | Role |
|---|---|---|
| Your CIA % of last semester | `CIA_pct` | Independent (Exp 1) |
| Your maximum attendance % till last semester | `Attendance_pct` | Independent (Exp 2) |
| Your GPA of last semester | `GPA` | Dependent (target) |

- **Raw size:** 50 observations, 15 attributes
- **After cleaning:** 49 rows (dropped nulls in key columns + 1 GPA outlier > 5)
- **Duplicates:** None found

---

## Structure

### Part A — EDA & Preprocessing
- Load dataset and inspect shape, dtypes, null counts
- Drop rows with nulls in key columns
- Parse mixed-format strings (e.g. `"72%"`, `"72 %"`) using regex-based `clean_numeric()`
- Remove GPA outlier (entry > 5.0)
- Generate statistical summary for `CIA_pct`, `Attendance_pct`, `GPA`
- Visualizations:
  - Histograms — feature distributions
- Save cleaned data to `Student_Survey_Cleaned.csv`

### Part B — Simple Linear Regression (Scikit-learn)
Two experiments using `LinearRegression` from `sklearn`:

| | Experiment 1 | Experiment 2 |
|---|---|---|
| X | `CIA_pct` | `Attendance_pct` |
| y | `GPA` | `GPA` |
| Train/Test split | 80/20, `random_state=42` | 80/20, `random_state=42` |

Outputs per experiment: slope, intercept, regression equation, MSE, RMSE, R².
- Visualization
  - Scatter plots — CIA % vs GPA, Attendance % vs GPA

### Part C — Manual OLS
Manually derive slope and intercept using the OLS formulas:

$$b_1 = \frac{\sum(x_i - \bar{x})(y_i - \bar{y})}{\sum(x_i - \bar{x})^2}, \quad b_0 = \bar{y} - b_1\bar{x}$$

Compare manual predictions against Scikit-learn predictions — both produce identical results (difference < 1e-10), confirming correctness.

### Part D — Model Serialization (Pickle)
- Save slope and intercept for both experiments to `linear_regression_weights.pkl`
- Reload and use loaded parameters for inference
- Verify predictions match original model output

---

## Results Summary

| Experiment | Slope | Intercept | R² | RMSE |
|---|---|---|---|---|
| CIA % → GPA | 0.012800 | 2.4834 | 0.177 | 0.26 |
| Attendance % → GPA | 0.024410 | 1.1407 | — (negative) | 0.30 |

- CIA % shows a weak positive correlation with GPA (~17.7% variance explained)
- Attendance % shows a weak negative correlation — low variance in X (most students cluster at 94–96%) limits predictive power
- Manual OLS and Scikit-learn produce numerically identical results

---

## Files

```
lab3.ipynb                      # Main notebook
Student_Awareness_Survey.csv    # Raw dataset
Student_Survey_Cleaned.csv      # Cleaned dataset (generated)
linear_regression_weights.pkl   # Saved model parameters (generated)
```

---

## Dependencies

```bash
pip install pandas numpy matplotlib scikit-learn
```

| Library | Usage |
|---|---|
| `pandas` | Data loading, cleaning, DataFrames |
| `numpy` | Numerical operations, OLS computation |
| `matplotlib` | Histograms, scatter plots, boxplots |
| `scikit-learn` | `LinearRegression`, `train_test_split`, metrics |
| `pickle` | Model parameter serialization |
| `re` | Parsing mixed-format percentage strings |
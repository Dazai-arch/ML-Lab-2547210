# Linear Regression via Gradient Descent — Student Performance Dataset

A from-scratch (NumPy-only) implementation of **Linear Regression trained with Batch Gradient Descent**, applied to the UCI **Student Performance (Portuguese course)** dataset to predict students' final grade (`G3`).

## Files

| File | Description |
|---|---|
| `student_performance_gd_linear_regression.ipynb` | Main notebook (fully executed, with outputs) |
| `student-por.csv` | Input dataset (semicolon-separated) |

## Dataset

- **Source:** UCI Machine Learning Repository — Student Performance Dataset (Portuguese language course)
- **Rows / columns:** 649 students × 33 attributes
- **Target:** `G3` — final grade (0–20)
- **Features:** demographic info (age, sex, address, family), school-related attributes (study time, failures, support), social/lifestyle factors (free time, going out, alcohol consumption, health), and the earlier-period grades `G1`, `G2`
- **Missing values:** none found — no imputation required

## Pipeline

1. **Load data** — read the semicolon-delimited CSV with pandas.
2. **Preprocessing**
   - Checked for missing values (none present).
   - **Binary categorical columns** (`school`, `sex`, `address`, `famsize`, `Pstatus`, and the yes/no support/activity columns) → label-encoded to 0/1.
   - **Multi-category nominal columns** (`Mjob`, `Fjob`, `reason`, `guardian`) → one-hot encoded (`drop_first=True`), expanding the feature set from 32 to 41 predictors.
   - **Feature scaling** — standardized (zero mean, unit variance) using statistics computed only on the training set, then applied to the test set to avoid data leakage.
3. **Feature/target selection** — `X` = all 41 encoded predictor columns, `y` = `G3`.
4. **Train/test split** — 80/20 (519 training rows, 130 test rows), `random_state=42`.
5. **Gradient Descent Linear Regression (from scratch)**
   - Hypothesis: `ŷ = Xw + b`
   - Cost function: Mean Squared Error, `J(w,b) = (1/2m) Σ(ŷ⁽ⁱ⁾ − y⁽ⁱ⁾)²`
   - Batch gradient updates for `w` and `b` computed manually with NumPy (no `sklearn` model used for fitting).
6. **Learning rate experiments** — trained with `lr ∈ {0.001, 0.01, 0.05, 0.1, 0.5}` for 1000 iterations each, plotting cost vs. iterations for all five on one chart (log scale).
7. **Loss vs. iterations plot** — final model retrained with the best learning rate for 3000 iterations.
8. **Evaluation** — MAE, MSE, RMSE, and R² computed on the held-out test set.
9. **Interpretation** — discussion of convergence behavior and prediction quality.

## Learning Rate Experiment Results

| Learning Rate | Final Cost (1000 iters) | Behavior |
|---|---|---|
| 0.001 | 10.4588 | Too slow — hasn't converged yet |
| 0.01  | 0.7551  | Converges, slightly behind optimum |
| 0.05  | 0.7456  | Converges well |
| **0.1** | **0.7456** | **Converges well — selected as best** |
| 0.5   | ~7.7 × 10⁶⁰ | **Diverges** — cost explodes exponentially |

At `lr = 0.5` (and more dramatically at `lr = 1`, tested separately), the update step overshoots the minimum on every iteration. The error compounds geometrically each step, and within a few hundred iterations the cost overflows 64-bit floating-point range entirely (`inf`), after which the arithmetic hits an indeterminate operation and the values degrade to `nan`. This is a clean illustration of *why* an appropriately small-but-not-too-small learning rate matters for gradient descent stability.

**Selected learning rate: `0.1`**, retrained for 3000 iterations to ensure full convergence (final training cost ≈ 0.7456).

## Model Evaluation (Test Set)

| Metric | Value |
|---|---|
| MAE  | 0.7651 |
| MSE  | 1.4759 |
| RMSE | 1.2149 |
| R²   | 0.8487 |

## Key Takeaways

- **Feature scaling is essential** for gradient descent — without standardization, features on very different scales (e.g., `age` vs. `absences` vs. `G1`) would require very different learning rates and hurt convergence.
- **Learning rate is the most critical hyperparameter**: too small wastes iterations without reaching the minimum; too large causes oscillation, then exponential divergence, then floating-point overflow (`inf` → `nan`).
- The model achieves a strong **R² ≈ 0.85** on unseen data, driven largely by the inclusion of `G1` and `G2` (prior-period grades), which are highly correlated with the final grade `G3`.
- Average prediction error (MAE) is under 1 grade point on a 0–20 scale, indicating good real-world usefulness for early academic-performance forecasting.

## How to Run

```bash
pip install numpy pandas matplotlib scikit-learn
jupyter notebook student_performance_gd_linear_regression.ipynb
```

Run all cells top to bottom. The notebook is self-contained aside from requiring `student-por.csv` to be in the same directory.
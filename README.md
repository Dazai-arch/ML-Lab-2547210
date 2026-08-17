# Lab 4: K-Nearest Neighbors (KNN) Classification with Heuristic K Selection & PCA Visualization

## Aim
To build a KNN classifier for breast cancer diagnosis, select the optimal K using both a heuristic rule and cross-validation, visualize decision boundaries via PCA, and compare classification metrics against a regression baseline from Lab 3.

## Dataset
| Dataset | File | Description |
|---|---|---|
| Breast Cancer Wisconsin (Diagnostic) | `brca.csv` | Numeric tumor features (e.g., `area_mean`, `smoothness_mean`, etc.) with a binary diagnosis label `y` (`B` = Benign, `M` = Malignant) |

## Notebook
- `lab4.ipynb`

## Steps / Tasks Covered

| Task | Description |
|---|---|
| **Task 1: Data Preparation** | Load `brca.csv`, drop the redundant index column, check for missing values/duplicates (none found), encode target (`B`→0, `M`→1), and apply `StandardScaler` — justified because KNN is distance-based and unscaled features (e.g. `area_mean` up to 2500 vs `smoothness_mean` ~0.05–0.2) would dominate the distance metric |
| **Task 2: Train-Test Split Analysis** | Compare 80:20, 70:30, and 90:10 splits; evaluate how split ratio affects model stability and generalization |
| **Task 3: KNN with Heuristic K Selection** | 3.1 Compute a baseline K using the heuristic **K = √n** (n = training samples)<br>3.2 Train KNN across K±5 nearby values, plot accuracy vs. K to find the optimal K<br>3.3 Explain Euclidean vs. Manhattan distance metrics and plot 2D decision boundaries (via PCA) for K = 1, 5, 10, 20 to visualize the bias-variance trade-off |
| **Task 4: Cross-Validation** | Apply 5-fold and 10-fold cross-validation across K values; compare CV accuracy stability against the single train-test split; select the final K using both heuristic and CV results |
| **Task 5: Classification Evaluation** | Evaluate the final KNN model with Accuracy, Precision, Recall, F1 Score, Confusion Matrix, and ROC Curve/AUC |
| **Task 6: Comparative Study with Regression (Lab 3 Integration)** | Train a `LinearRegression` model on the same features and contrast error-based regression metrics (MAE, MSE, RMSE, R²) against decision-based classification metrics |
| **Task 7: Analytical Questions** | Short-answer discussion: why KNN is a "lazy learner", why feature scaling matters, the √n heuristic, why cross-validation is more reliable than a single split, and how K affects the bias-variance trade-off |
| **Conclusion** | Summary comparing heuristic, split-validated, and CV-selected K, and interpreting recall vs. precision trade-offs in a medical diagnosis context |

## Key Techniques Used
- `StandardScaler` for feature scaling
- `train_test_split` with multiple split ratios
- `KNeighborsClassifier` with heuristic (`K = √n`) and empirically tuned K
- `PCA` (2 components) for 2D decision boundary visualization
- `KFold` / `cross_val_score` for 5-fold and 10-fold cross-validation
- Classification metrics: accuracy, precision, recall, F1, confusion matrix, ROC/AUC
- `LinearRegression` for a regression-vs-classification metric comparison

## Key Findings
- All three split ratios (80:20, 70:30, 90:10) produced similar accuracy at K=5, validating the **√n heuristic** as a good starting point, backed up by cross-validation.
- Decision boundaries get **smoother as K increases**: K=1 overfits (jagged, high variance), K=20 oversmooths (high bias).
- 10-fold cross-validation gave more stable accuracy estimates across K values than a single train-test split.
- The final model scored high on **Accuracy, Precision, F1, and AUC**, but had **noticeably lower Recall** — several malignant cases were misclassified as benign (false negatives), which is the costliest error type in cancer diagnosis.
- Unlike Lab 3's error-based regression metrics (MAE/MSE/R²), this classification task must weight **Recall and ROC-AUC** heavily since false negatives carry a much higher real-world cost than false alarms.

## How to Run
1. Place `brca.csv` in the same directory as the notebook.
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib scikit-learn
   ```
3. Open `lab4.ipynb` and run all cells in order.

## Relation to Other Labs
Task 6 directly reuses the regression approach from **lab3** (branch `lab3`) to contrast regression vs. classification evaluation on related data.
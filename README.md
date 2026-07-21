# Lab 6 — Breast Cancer Wisconsin (Diagnostic) Classification

## Aim
To implement Logistic Regression and K-Nearest Neighbors (KNN) classifiers on the Breast Cancer Wisconsin (Diagnostic) dataset and compare their performance using standard classification evaluation metrics.

## Objectives
1. Preprocess the dataset for classification.
2. Implement Logistic Regression and KNN classifiers using Scikit-learn.
3. Evaluate both models using standard performance metrics.
4. Compare the performance of Logistic Regression and KNN and identify the better classifier.

## Files
| File | Description |
|---|---|
| `lab6.ipynb` | Main Jupyter notebook with full implementation, outputs, and inference |
| `wdbc.data` | Raw dataset (569 samples, 32 columns) — local fallback source |
| `wdbc.names` | Official UCI documentation describing the dataset and its columns |

## Dataset
**Source:** UCI Machine Learning Repository — Wisconsin Diagnostic Breast Cancer (WDBC), donated by Dr. William H. Wolberg, W. Nick Street, and Olvi L. Mangasarian, University of Wisconsin (1995).

- 569 samples, 30 numeric features + `id` + `diagnosis` (target)
- Features are computed from digitized images of fine needle aspirates (FNA) of breast masses, describing characteristics of cell nuclei (radius, texture, perimeter, area, smoothness, compactness, concavity, concave points, symmetry, fractal dimension — each as mean, standard error, and worst value)
- Target: `M` = Malignant, `B` = Benign (encoded as 1 / 0 respectively)

## Workflow (Notebook Sections)
1. **Load Data** — download from UCI, with fallback to local `wdbc.data`, then to sklearn's built-in copy
2. **EDA** — shape, dtypes, class balance, summary statistics, correlation heatmap
3. **Missing Value Check** — confirmed no missing values
4. **Preprocessing** — target encoding, 80/20 stratified train/test split, feature scaling with `StandardScaler` (fit on train only)
5. **Logistic Regression** — trained on scaled features
6. **KNN** — trained on scaled features (k=5), with a k=1–20 sweep to justify neighbor count
7. **Evaluation** — Accuracy, Precision, Recall, F1-score, and Confusion Matrix for both models
8. **Comparison Table & Chart** — side-by-side metric comparison
9. **Interpretation** — written discussion of which model performs better and why

## Results Summary

| Model | Accuracy | Precision | Recall | F1 Score |
|---|---|---|---|---|
| Logistic Regression | 0.9649 | 0.9750 | 0.9286 | 0.9512 |
| K-Nearest Neighbors (k=5) | 0.9561 | 0.9744 | 0.9048 | 0.9383 |

## Conclusion
Logistic Regression outperformed KNN across every metric — accuracy, precision, recall, and F1-score — and caught more true malignant cases (higher recall), making it the better-suited classifier for this dataset, both in overall performance and in minimizing missed cancer diagnoses.

## How to Run
1. Ensure `wdbc.data` and `wdbc.names` are in the same folder as `lab6.ipynb`.
2. Install dependencies: `pip install pandas numpy scikit-learn matplotlib seaborn`
3. Open and run all cells: `jupyter notebook lab6.ipynb`
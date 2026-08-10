# Lab 9 — SVM & PCA

Support Vector Machine (SVM) classification on the Breast Cancer Wisconsin dataset, and Principal Component Analysis (PCA) / Linear Discriminant Analysis (LDA) on the Wine dataset.

## Files

```
├── lab9.ipynb          # Main notebook
└── data/
    ├── wdbc.data        # Breast Cancer Wisconsin (Diagnostic) dataset
    └── wine.data         # Wine dataset
```

## Requirements

```
pip install pandas numpy matplotlib seaborn scikit-learn
```

## How to Run

1. Keep `lab9.ipynb` and the `data/` folder (with `wdbc.data` and `wine.data`) in the same directory.
2. Open the notebook with Jupyter:
   ```
   jupyter notebook lab9.ipynb
   ```
3. Run all cells (Kernel → Restart & Run All).

## Contents

**Part A — SVM (Breast Cancer dataset)**
- Preprocessing and 80:20 train-test split
- Linear kernel SVM + hyperparameter tuning (GridSearchCV)
- Evaluation: Accuracy, Precision, Recall, F1 Score, Confusion Matrix
- Kernel comparison (linear, RBF, poly, sigmoid)

**Part B — PCA (Wine dataset)**
- Feature standardization
- PCA reduction from 13 → 2 components
- Explained variance ratio, cumulative variance, scree plot
- 2D scatter plot of transformed data
- Component interpretation

**Extra Credit — LDA vs PCA**
- LDA projection to 2 components
- Side-by-side comparison of PCA vs LDA separability

Every task includes a short interpretation of the results, with a final overall interpretation at the end.

## Dataset Sources

- Breast Cancer Wisconsin (Diagnostic): https://archive.ics.uci.edu/dataset/17/breast+cancer+wisconsin+diagnostic
- Wine: https://archive.ics.uci.edu/dataset/109/wine
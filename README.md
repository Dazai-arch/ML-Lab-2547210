# Decision Tree Classifier on the Iris Dataset

A lab activity exploring Decision Tree classification using the classic Iris dataset — covering data exploration, model training, visualization, hyperparameter effects, and tuning with GridSearchCV.

## Dataset

- **Source:** `sklearn.datasets.load_iris`
- **Samples:** 150 (50 each of *setosa*, *versicolor*, *virginica*)
- **Features:** 4 — sepal length, sepal width, petal length, petal width (cm)
- **Split:** 80% train / 20% test (`train_test_split`, `random_state=42`, stratified)

## Requirements

```
numpy
pandas
matplotlib
scikit-learn
```

Install with:
```bash
pip install numpy pandas matplotlib scikit-learn
```

## Contents / Tasks

| Task | Description |
|------|-------------|
| 1 | Dataset exploration — shape, features, class balance |
| 2 | Train/test split (80/20, stratified) |
| 3 | Baseline Decision Tree with default parameters |
| 4 | Visualizing the tree (`plot_tree`) with `min_samples_split=40` |
| 5 | Inspecting root split, internal nodes, leaves, and max depth |
| 6 | Effect of `max_depth` (1, 2, 3, 4, None) on decision boundaries & over/underfitting |
| 7 | Effect of `min_samples_split` on tree complexity |
| 8 | Effect of `min_samples_leaf` on tree complexity |
| 9 | Hyperparameter tuning using `GridSearchCV` |
| 10 | Final analysis & recommended model |

## Key Results

**Baseline model (default parameters):**
- Test Accuracy: **93.33%**
- Root split: `petal length (cm) <= 2.45`
- Tree depth: 5, Leaf nodes: 8

**Effect of `max_depth`:**

| Max Depth | Train Acc | Test Acc | Tree Depth |
|-----------|-----------|----------|------------|
| 1 | 0.667 | 0.667 | 1 |
| 2 | 0.967 | 0.933 | 2 |
| 3 | 0.983 | 0.967 | 3 |
| 4 | 0.983 | 0.933 | 4 |
| None | 0.992 | 0.933 | 5 |

- Underfitting: `max_depth=1`
- Best generalization: `max_depth=3`
- Overfitting risk: `max_depth=None`

**GridSearchCV (best hyperparameters found):**
```
criterion='gini', max_depth=4, min_samples_leaf=1, min_samples_split=2
Best CV score (train): 0.9500
Test accuracy (tuned): 0.9333
Test accuracy (default): 0.9333
```

## Conclusion

Decision trees achieve high accuracy (93–97%) on the Iris dataset with minimal tuning. `max_depth` has the strongest effect on model complexity and generalization, while `min_samples_split`, `min_samples_leaf`, and `criterion` (gini vs. entropy) have a smaller, fine-tuning effect. GridSearchCV improved cross-validation score but not test accuracy, since the default model was already near-optimal for this simple, well-separated dataset. A shallow, interpretable tree (`max_depth=3`) is recommended as the best balance of accuracy and generalization.

## How to Run

1. Open `lab_activity.ipynb` in Jupyter Notebook / JupyterLab.
2. Run all cells sequentially (**Kernel → Restart & Run All** recommended to avoid stale-variable issues).
3. Plots and metrics will render inline after each relevant task.
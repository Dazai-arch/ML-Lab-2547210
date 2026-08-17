# ML-Lab-2547210
# Machine Learning & Deep Learning Lab Exercises

This repository contains the lab exercises completed as part of the Machine Learning / Deep Learning coursework. Each lab is developed on its **own branch**, so this `main` branch acts purely as an index — it contains no code of its own.

> **Note:** The branch `Lab_Activity` contains the same code as `lab7` (Decision Tree Classifier on the Iris dataset).

## How to Access a Lab

```bash
git clone <repo-url>
cd <repo-name>
git checkout <branch-name>     # e.g. git checkout lab7
```

Each branch contains a single Jupyter notebook (`.ipynb`) with the complete implementation for that lab, along with the dataset (where applicable) and any supporting files.

## Branch Index

| Branch | Lab Title | Dataset(s) | Key Concepts |
|---|---|---|---|
| `Lab1` | Data Preprocessing & EDA — Part 1 | Air Quality (`city_day.csv`), Crop Production | Handling missing values, merging datasets with inconsistent keys, distribution analysis, IQR-based outlier treatment |
| `Lab2` | Data Preprocessing & EDA — Part 2 | Air Quality (`city_day.csv`), Crop Production | Yearly/seasonal AQI trend analysis, state-wise aggregation, insights & conclusions, optional visualization tasks |
| `lab3` | Simple & Multiple Linear Regression | Custom dataset (50 obs, 15 attributes) | Missing value handling, dtype conversion, deduplication, regression modeling, evaluation via MSE/R²/MAE |
| `lab4` | K-Nearest Neighbors (KNN) with PCA | Breast Cancer Wisconsin (via `sklearn.datasets`) | Feature scaling, PCA for visualization, KNN decision boundary, K-Fold cross-validation |
| `lab5` | Linear Regression from Scratch (Gradient Descent) | Student Performance dataset | Preprocessing & encoding, gradient descent implementation, learning rate experiments, convergence analysis |
| `lab6` | Logistic Regression | Breast Cancer Wisconsin (Diagnostic) | EDA & preprocessing, Pipeline + StandardScaler, Stratified K-Fold cross-validation, performance metrics |
| `lab7` | Decision Tree Classifier | Iris dataset | Dataset exploration, train/test split, hyperparameter tuning with GridSearchCV, tree visualization, confusion matrix |
| `lab8` | Naive Bayes vs. Other Classifiers | Play Tennis dataset | Label encoding, CategoricalNB, cross-validation, comparison with Logistic Regression / SVM / Decision Tree |
| `lab9` | SVM, PCA & LDA | Breast Cancer Wisconsin, Wine dataset | SVM with hyperparameter tuning (GridSearchCV), PCA dimensionality reduction & explained variance, LDA |
| `Lab10` | MLP for XOR (Keras & TensorFlow) | XOR truth table | MLP with ReLU hidden layer, Keras high-level API vs. TensorFlow low-level API (`GradientTape`), decision boundary visualization |
| `Lab_Activity` | Decision Tree Classifier *(same as `lab7`)* | Iris dataset | Identical content to `lab7` |

## Tech Stack
- Python 3
- Jupyter Notebook
- pandas, NumPy, Matplotlib, Seaborn
- scikit-learn
- TensorFlow / Keras (Lab10 only)

## Repository Structure
```
main            -> this README (index only, no code)
Lab1            -> Lab1.ipynb
Lab2            -> Lab2.ipynb
lab3            -> lab3.ipynb
lab4            -> lab4.ipynb
lab5            -> lab5.ipynb
lab6            -> lab6.ipynb
lab7            -> lab7.ipynb
lab8            -> lab8.ipynb
lab9            -> lab9.ipynb
Lab10           -> Lab10.ipynb
Lab_Activity    -> lab7.ipynb (duplicate of lab7)
```

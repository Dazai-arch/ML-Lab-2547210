# Lab 8: Implementation and Performance Evaluation of Categorical Naive Bayes Classifier

## File
`lab8.ipynb`

## Objective
Build a classification pipeline on the **Play Tennis** dataset using a Categorical Naive Bayes classifier, evaluate its performance, run single-sample inference, and compare it against Decision Tree, Logistic Regression, and SVM classifiers.

## Dataset
- **Name:** Play Tennis Dataset
- **Records:** 50
- **Features:** `Outlook`, `Temperature`, `Humidity`, `Wind` (all categorical)
- **Target:** `Play Tennis` (Yes / No)

## Requirements
```
python >= 3.9
pandas
numpy
matplotlib
scikit-learn
```
Install with:
```bash
pip install pandas numpy matplotlib scikit-learn
```

## How to Run
1. Place `Lab_8.csv` in the same directory as `lab8.ipynb`.
2. Open the notebook:
   ```bash
   jupyter notebook lab8.ipynb
   ```
3. Run all cells in order (Kernel → Restart & Run All).

## Notebook Structure

| Task | Description |
|------|-------------|
| **1. Data Preprocessing** | Load dataset, separate features/target, encode categorical values using `LabelEncoder` |
| **2. Dataset Partitioning** | 80:20 stratified train-test split; includes Stratified K-Fold cross-validation to sanity-check the split and compare candidate models |
| **3. Naive Bayes Training & Evaluation** | Train `CategoricalNB`, report Accuracy, Confusion Matrix, Classification Report |
| **4. Single-Sample Inference** | Predict Play Tennis for Outlook=Sunny, Temperature=Cool, Humidity=High, Wind=Strong, with class probabilities |
| **5. Model Comparison** | Train Decision Tree, Logistic Regression, and SVM on the same data; compare accuracy, query prediction, and probabilities across all four models; visualize decision regions (incl. SVM margin/support vectors) |

Each task section includes a short **Interpretation** markdown cell, and the notebook ends with a consolidated **Final Analysis Report**.

## Key Results
- Naive Bayes Test Accuracy: **90%**
- Decision Tree Test Accuracy: **100%**
- Logistic Regression Test Accuracy: **90%**
- SVM Test Accuracy: **100%**
- Query prediction (Sunny, Cool, High, Strong): **No** (all models agree)

> Note: With only 40 training samples, 100% test accuracy (Decision Tree, SVM) should be read cautiously — it reflects the small test set size (10 samples) rather than guaranteed generalization.

## Output
- Console metrics: accuracy, confusion matrix, classification report
- Comparison table across all 4 models (accuracy, prediction, probabilities)
- Decision region plots for all 4 models (Naive Bayes, Decision Tree, Logistic Regression, SVM with margin and support vectors)
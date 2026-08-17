# Lab Exercise 10: Learning the XOR Boolean Function Using an MLP

## Overview
This lab implements a Multi-Layer Perceptron (MLP) to learn the non-linear **XOR** Boolean function in a **single notebook** containing two **independent, self-contained** implementations:
1. **Part A — Keras** (TensorFlow high-level API)
2. **Part B — TensorFlow low-level API** (manual weights + `tf.GradientTape`)

Each part has its own imports, dataset variables, model, and helper functions (no shared code between them), followed by a comparison section at the end that uses results from both.

XOR is not linearly separable, so a single-layer perceptron cannot learn it — a hidden layer with a non-linear activation (ReLU) is required.

## File
- `Lab10.ipynb` — Single notebook containing both independent implementations plus a comparison, with a short (max 2-line) interpretation after every code cell.

## Contents of the Notebook
| Section | Description |
|---|---|
| Part A: Keras | Self-contained — builds, compiles, trains, and evaluates an MLP using `keras.Sequential` |
| Part B: TensorFlow Low-Level | Self-contained — manually defines weights/biases, forward pass, loss, and a custom `GradientTape` training loop |
| Decision Boundaries | Plots the learned non-linear decision boundary for each implementation (own plotting function per part) |
| Training Curve Comparison | Compares loss/accuracy convergence between Keras and low-level TensorFlow |
| Hyperparameter Discussion | Notes on the effect of learning rate, activation function, hidden neurons, and epochs |
| Final Interpretation | Overall conclusion of the exercise |

## Model Architecture
- **Input layer:** 2 neurons (for the two binary inputs)
- **Hidden layer:** 4 neurons, ReLU activation
- **Output layer:** 1 neuron, Sigmoid activation (binary classification)

## Training Configuration
- **Loss:** Binary Cross-Entropy
- **Optimizer:** Adam (learning rate = 0.05)
- **Epochs:** 500

## How to Run
1. Install dependencies:
   ```bash
   pip install tensorflow numpy matplotlib
   ```
2. Open `Lab10.ipynb` in Jupyter Notebook / JupyterLab / VS Code / Google Colab.
3. Run all cells in order (Cell → Run All).

## Expected Results
- Both models converge to **100% training accuracy**, correctly predicting:
  | Input 1 | Input 2 | XOR Output | Predicted |
  |---|---|---|---|
  | 0 | 0 | 0 | 0 |
  | 0 | 1 | 1 | 1 |
  | 1 | 0 | 1 | 1 |
  | 1 | 1 | 0 | 0 |
- Decision boundary plots show a non-linear (curved) separation between the two classes.

## Key Takeaway
A hidden layer with a non-linear activation function is essential for solving XOR, since it is not linearly separable. Both the Keras and low-level TensorFlow implementations arrive at equivalent solutions, confirming that the choice of API does not affect the underlying learning capability of the network — only the level of control and boilerplate code required.

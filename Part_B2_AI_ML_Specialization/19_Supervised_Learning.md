# 19. Machine Learning — Supervised Learning

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 19.1 Overview of Supervised Learning

**Supervised learning:** Learn a mapping $f: X \to Y$ from labeled training data $\{(x_i, y_i)\}_{i=1}^{n}$.

```
Training Data                Model                    Prediction
[features, label] ------> Learn f(x) ≈ y ------> f(x_new) = ?
```

| Task | Output $Y$ | Loss Function | Example |
|------|-----------|---------------|---------|
| **Regression** | Continuous ($\mathbb{R}$) | MSE, MAE | House price prediction |
| **Classification** | Discrete (classes) | Cross-entropy, Hinge | Spam detection, disease diagnosis |

---

## 19.2 Regression

### 19.2.1 Linear Regression

**Model:** $\hat{y} = w_0 + w_1 x_1 + w_2 x_2 + ... + w_n x_n = \mathbf{w}^T \mathbf{x} + b$

**In matrix form:** $\hat{\mathbf{y}} = X\mathbf{w}$

**Loss function (MSE):**

$$J(\mathbf{w}) = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2 = \frac{1}{n} \| \mathbf{y} - X\mathbf{w} \|^2$$

**Closed-form solution (Normal Equation):**

$$\mathbf{w} = (X^T X)^{-1} X^T \mathbf{y}$$

When $n$ is large or $X^TX$ is not invertible, use gradient descent instead.

**Assumptions of Linear Regression:**

1. **Linearity:** Relationship between features and target is linear
2. **Independence:** Observations are independent
3. **Homoscedasticity:** Constant variance of residuals
4. **Normality:** Residuals are normally distributed (for valid hypothesis tests)
5. **No multicollinearity:** Features should not be highly correlated with each other

**Goodness of fit — $R^2$ Score:**

$$R^2 = 1 - \frac{SS_{res}}{SS_{tot}} = 1 - \frac{\sum(y_i - \hat{y}_i)^2}{\sum(y_i - \bar{y})^2}$$

- $R^2 = 1$: perfect fit
- $R^2 = 0$: model is as good as predicting the mean
- $R^2 < 0$: model is worse than predicting the mean

**Adjusted $R^2$** (penalizes extra features): $R^2_{adj} = 1 - \frac{(1-R^2)(n-1)}{n-p-1}$ where $p$ = number of features.

### 19.2.2 Polynomial Regression

Add polynomial features: $\hat{y} = w_0 + w_1 x + w_2 x^2 + w_3 x^3 + ...$

Still a linear model in terms of parameters (linear in weights), just non-linear features. Higher degree → more flexible → risk of **overfitting**.

### 19.2.3 Regularization

**Problem:** Without constraints, weights can grow very large → overfitting.

| Method | Loss Function | Effect | When to Use |
|--------|-------------|--------|-------------|
| **Ridge (L2)** | $J = MSE + \lambda \sum w_i^2$ | Shrinks all weights toward zero | Many small-effect features |
| **Lasso (L1)** | $J = MSE + \lambda \sum |w_i|$ | Drives some weights to exactly zero | Feature selection needed |
| **Elastic Net** | $J = MSE + \lambda_1 \sum |w_i| + \lambda_2 \sum w_i^2$ | Combines L1 + L2 | Many correlated features |

**$\lambda$ (regularization strength):** $\lambda = 0$ → no regularization (plain regression). $\lambda \to \infty$ → all weights → 0 (underfitting). Choose via cross-validation.

**Why Lasso produces sparse solutions:** The L1 penalty creates diamond-shaped constraint regions. The optimum often lands on a corner (axis), where some weights are exactly zero.

---

## 19.3 Classification

### 19.3.1 Logistic Regression

Despite the name, this is a **classification** algorithm.

**Sigmoid function:** $\sigma(z) = \frac{1}{1 + e^{-z}}$ maps any real number to $(0, 1)$.

```
  1.0 |                    ___________
      |                ___/
  0.5 |            ___/
      |        ___/
  0.0 |_______/
      +---+---+---+---+---+---+---+---
         -4  -3  -2  -1   0   1   2   3
```

**Model:** $P(y=1|x) = \sigma(\mathbf{w}^T \mathbf{x} + b)$

**Loss: Binary Cross-Entropy (Log Loss):**

$$J = -\frac{1}{n} \sum_{i=1}^{n} \left[ y_i \log(\hat{y}_i) + (1-y_i) \log(1-\hat{y}_i) \right]$$

**Multi-class extension:** Use **softmax** instead of sigmoid:

$$P(y=k|\mathbf{x}) = \frac{e^{z_k}}{\sum_{j=1}^{K} e^{z_j}}$$

with categorical cross-entropy loss.

### 19.3.2 K-Nearest Neighbors (KNN)

**Algorithm:**
1. Store all training data (lazy learning — no training phase)
2. For a new point, find the $k$ closest training points
3. Vote: majority class (classification) or average (regression)

**Distance metrics:**

| Metric | Formula | Best For |
|--------|---------|----------|
| **Euclidean (L2)** | $\sqrt{\sum(x_i - y_i)^2}$ | Continuous features |
| **Manhattan (L1)** | $\sum |x_i - y_i|$ | High-dimensional sparse data |
| **Minkowski** | $\left(\sum |x_i - y_i|^p\right)^{1/p}$ | General (p=2 is Euclidean) |
| **Cosine** | $1 - \frac{\mathbf{x} \cdot \mathbf{y}}{\|\mathbf{x}\|\|\mathbf{y}\|}$ | Text similarity |

**Choosing $k$:**
- Small $k$ (e.g., 1): Low bias, high variance (overfitting, noisy boundaries)
- Large $k$ (e.g., 100): High bias, low variance (underfitting, smooth boundaries)
- Use **odd $k$** for binary classification (avoids ties)
- Select via cross-validation

**Curse of dimensionality:** In high dimensions, all points become equidistant. KNN performance degrades significantly. Solution: dimensionality reduction (PCA) before KNN.

### 19.3.3 Naive Bayes

**Based on Bayes' theorem with the "naive" assumption that all features are conditionally independent given the class:**

$$P(C|x_1, x_2, ..., x_n) \propto P(C) \prod_{i=1}^{n} P(x_i | C)$$

| Variant | Feature Type | $P(x_i|C)$ Assumption | Use Case |
|---------|-------------|----------------------|----------|
| **Gaussian NB** | Continuous | Normal distribution | General numeric data |
| **Multinomial NB** | Counts/frequencies | Multinomial distribution | Text (word counts, TF-IDF) |
| **Bernoulli NB** | Binary | Bernoulli distribution | Binary features (word present/absent) |

**Pros:** Very fast, works well with small data, handles many features, good text classifier.  
**Cons:** Independence assumption rarely holds, poor probability estimates, zero-frequency problem (fixed with Laplace smoothing: add 1 to all counts).

### 19.3.4 Decision Trees

**Core idea:** Recursively split data using feature thresholds that maximize "purity" of resulting groups.

```
                [Is income > 50K?]
                /                \
           Yes /                  \ No
             /                    \
    [Age > 30?]              [Owns house?]
    /         \              /           \
  Yes         No           Yes           No
  APPROVE    DENY         APPROVE       DENY
```

**Splitting criteria:**

**Gini Impurity:** $Gini = 1 - \sum_{k=1}^{K} p_k^2$

- Pure node: Gini = 0
- Maximum impurity (2 classes, 50/50): Gini = 0.5

**Information Gain (using Entropy):**

$$H = -\sum_{k=1}^{K} p_k \log_2 p_k$$

$$IG = H(parent) - \sum_{j} \frac{|child_j|}{|parent|} H(child_j)$$

**Worked Example:**

Dataset: 10 samples — 6 Positive, 4 Negative.

Parent entropy: $H = -\frac{6}{10}\log_2\frac{6}{10} - \frac{4}{10}\log_2\frac{4}{10} = 0.971$

Split on Feature A → Left: [5P, 1N], Right: [1P, 3N]

$H_{left} = -\frac{5}{6}\log_2\frac{5}{6} - \frac{1}{6}\log_2\frac{1}{6} = 0.650$

$H_{right} = -\frac{1}{4}\log_2\frac{1}{4} - \frac{3}{4}\log_2\frac{3}{4} = 0.811$

$IG = 0.971 - \frac{6}{10}(0.650) - \frac{4}{10}(0.811) = 0.971 - 0.390 - 0.324 = 0.257$

**Tree algorithms:**

| Algorithm | Splitting Criterion | Feature Types | Multi-output |
|-----------|-------------------|---------------|--------------|
| **ID3** | Information Gain | Categorical only | No |
| **C4.5** | Gain Ratio | Both | No |
| **CART** | Gini (classification), MSE (regression) | Both | Yes |

**Preventing overfitting (Pruning):**
- **Pre-pruning:** Set max depth, min samples per split, min samples per leaf
- **Post-pruning:** Grow full tree, then remove nodes that don't improve validation performance

### 19.3.5 Support Vector Machines (SVM)

**Goal:** Find the hyperplane that **maximizes the margin** between classes.

```
    Class +     |  margin  |     Class -
  +     +       |          |       -    -
     +    +     |          |     -
  +       +     |  <--w-->  |   -     -
     +          | hyperplane|      -
                |   w·x+b=0|
```

**Support vectors:** The closest data points to the hyperplane — they define the margin.

**Hard margin SVM (linearly separable data):**

Maximize margin $= \frac{2}{\|\mathbf{w}\|}$ subject to $y_i(\mathbf{w} \cdot \mathbf{x}_i + b) \geq 1$ for all $i$.

**Soft margin SVM (allow some misclassification):**

$$\min \frac{1}{2}\|\mathbf{w}\|^2 + C \sum_{i=1}^{n} \xi_i$$

- $C$ large → small margin, fewer violations (overfit risk)
- $C$ small → large margin, more violations (underfit risk)

**Hinge loss:** $\max(0, 1 - y_i(\mathbf{w} \cdot \mathbf{x}_i + b))$

**Kernel Trick — for non-linearly separable data:**

Instead of explicitly mapping data to higher dimensions, compute dot products in high-dimensional space using a kernel function $K(x_i, x_j)$.

| Kernel | Formula | Use Case |
|--------|---------|----------|
| **Linear** | $\mathbf{x}_i \cdot \mathbf{x}_j$ | Linearly separable, high-dim text |
| **Polynomial** | $(\gamma \mathbf{x}_i \cdot \mathbf{x}_j + r)^d$ | Polynomial boundaries |
| **RBF (Gaussian)** | $\exp(-\gamma \|\mathbf{x}_i - \mathbf{x}_j\|^2)$ | Most common, flexible |
| **Sigmoid** | $\tanh(\gamma \mathbf{x}_i \cdot \mathbf{x}_j + r)$ | Similar to neural networks |

**RBF kernel intuition:** Maps each training point to a Gaussian bump in infinite-dimensional space. Points nearby in the original space → similar in the mapped space.

---

## 19.4 Ensemble Methods

**Core idea:** Combine multiple "weak" learners to create a "strong" learner.

### 19.4.1 Bagging (Bootstrap Aggregating)

```
Original Data ──┬──→ Bootstrap Sample 1 → Model 1 ──┐
                ├──→ Bootstrap Sample 2 → Model 2 ──┤
                ├──→ Bootstrap Sample 3 → Model 3 ──┤──→ Average/Vote → Final
                └──→ Bootstrap Sample n → Model n ──┘
```

- Bootstrap: Sample $n$ points **with replacement** (some points repeated, some missing)
- Each model sees ~63.2% of unique training points (the rest are **out-of-bag** samples)
- **Reduces variance**, doesn't change bias
- Models are trained **independently** (parallelizable)

### 19.4.2 Random Forest

**= Bagging + random feature selection at each split**

At each node, instead of considering all $p$ features, randomly select $\sqrt{p}$ features (classification) or $p/3$ features (regression) and split on the best among those.

**Why it works:** Decorrelates the trees. In plain bagging, if one feature dominates, all trees look similar. Random feature selection forces diversity.

**Feature importance:** Measure how much each feature decreases impurity across all trees (mean decrease in Gini / mean decrease in accuracy).

### 19.4.3 Boosting

**Sequential ensemble:** Each new model focuses on the mistakes of previous models.

```
Data → Model 1 → Errors ─→ Model 2 → Errors ─→ Model 3 → ... → Weighted Sum
         ↑                    ↑                    ↑
     All equal           Upweight misclassified   Further correction
```

**AdaBoost:**
1. Initialize: all samples have equal weight $w_i = 1/n$
2. Train weak learner on weighted data
3. Compute weighted error $\epsilon$
4. Compute model weight: $\alpha = \frac{1}{2}\ln\frac{1-\epsilon}{\epsilon}$
5. Update sample weights: increase weight of misclassified samples
6. Repeat. Final prediction: weighted vote of all models.

**Gradient Boosting:**
1. Start with a constant prediction (e.g., mean for regression)
2. Compute **residuals** (errors)
3. Fit new model to the residuals
4. Add new model's predictions (scaled by learning rate) to running sum
5. Repeat

$$F_m(x) = F_{m-1}(x) + \eta \cdot h_m(x)$$

where $h_m$ is the new tree fitted to residuals of $F_{m-1}$.

**Modern Boosting Implementations:**

| Library | Key Innovation | Speed | Best For |
|---------|---------------|-------|----------|
| **XGBoost** | Regularization, column subsampling, parallel tree building | Fast | Kaggle competitions, tabular data |
| **LightGBM** | Leaf-wise growth, GOSS (Gradient-based One-Side Sampling) | Fastest | Large datasets (>10K rows) |
| **CatBoost** | Ordered boosting, native categorical encoding | Fast | Categorical-heavy data |

### Bagging vs. Boosting Summary

| Aspect | Bagging | Boosting |
|--------|---------|----------|
| **Training** | Parallel (independent) | Sequential (dependent) |
| **Focus** | Reduce variance | Reduce bias |
| **Overfitting** | Resistant | Can overfit if too many rounds |
| **Models** | Typically same type (trees) | Weak learners (shallow trees) |
| **Example** | Random Forest | XGBoost, AdaBoost |
| **Diversity from** | Random data subsets + features | Focusing on hard examples |

---

## 19.5 Model Evaluation and Selection

### 19.5.1 Confusion Matrix

```
                    Predicted
                  Pos       Neg
  Actual  Pos  [ TP=85  |  FN=15 ]    ← Recall = 85/(85+15) = 85%
          Neg  [ FP=10  |  TN=890]    ← Specificity = 890/(890+10) = 98.9%
                  ↑
          Precision = 85/(85+10) = 89.5%
```

### 19.5.2 Classification Metrics

| Metric | Formula | Optimize When |
|--------|---------|---------------|
| **Accuracy** | $\frac{TP+TN}{TP+TN+FP+FN}$ | Balanced classes |
| **Precision** | $\frac{TP}{TP+FP}$ | Cost of FP is high (spam → inbox) |
| **Recall (Sensitivity)** | $\frac{TP}{TP+FN}$ | Cost of FN is high (miss cancer) |
| **F1-Score** | $\frac{2 \cdot P \cdot R}{P + R}$ | Need balance between P and R |
| **Specificity** | $\frac{TN}{TN+FP}$ | True negative rate matters |
| **AUC-ROC** | Area under ROC curve | Overall ranking ability |
| **F-beta** | $(1+\beta^2)\frac{P \cdot R}{\beta^2 P + R}$ | $\beta > 1$ favors recall, $\beta < 1$ favors precision |

**ROC Curve:** Plot True Positive Rate (Recall) vs. False Positive Rate ($\frac{FP}{FP+TN}$) at different classification thresholds.

- AUC = 1.0: perfect classifier
- AUC = 0.5: random classifier (diagonal line)
- AUC < 0.5: worse than random

**Precision-Recall Curve:** Better than ROC for **imbalanced datasets**. Plot Precision vs. Recall at different thresholds. Average Precision (AP) = area under PR curve.

### 19.5.3 Regression Metrics

| Metric | Formula | Properties |
|--------|---------|-----------|
| **MAE** | $\frac{1}{n}\sum |y_i - \hat{y}_i|$ | Robust to outliers, same units as target |
| **MSE** | $\frac{1}{n}\sum(y_i - \hat{y}_i)^2$ | Penalizes large errors more |
| **RMSE** | $\sqrt{MSE}$ | Same units as target, penalizes large errors |
| **$R^2$** | $1 - \frac{SS_{res}}{SS_{tot}}$ | Proportion of variance explained |
| **MAPE** | $\frac{100}{n}\sum \frac{|y_i - \hat{y}_i|}{|y_i|}$ | Percentage error (scale-independent) |

### 19.5.4 Bias-Variance Tradeoff

$$\text{Total Error} = \text{Bias}^2 + \text{Variance} + \text{Irreducible Noise}$$

| Problem | Diagnosis | Solutions |
|---------|-----------|----------|
| **High Bias (Underfitting)** | High train error, high test error | More complex model, add features, reduce regularization |
| **High Variance (Overfitting)** | Low train error, high test error | More data, regularization, simpler model, dropout, early stopping |

```
  Error
    |  \                        /
    |   \  Validation          /  ← High Variance
    |    \  Error             /     (overfitting)
    |     \       ___________/
    |      \_____/
    |      /          ← Sweet spot
    |     /
    |----/---- Training Error
    |   /
    |  / ← High Bias
    | /    (underfitting)
    +--------------------------------→ Model Complexity
```

### 19.5.5 Cross-Validation

| Method | Description | Use When |
|--------|-------------|----------|
| **K-Fold** | Split into $k$ folds, train on $k-1$, test on 1, rotate | Standard (k=5 or 10) |
| **Stratified K-Fold** | Like K-Fold but maintains class proportions in each fold | Imbalanced classes |
| **Leave-One-Out (LOO)** | $k = n$ (each sample is a test set once) | Very small datasets |
| **Repeated K-Fold** | Run K-Fold multiple times with different splits | More stable estimates |
| **Time Series Split** | Always train on past, test on future (no shuffling) | Temporal data |

**Hyperparameter Tuning:**

| Method | Description | Pros | Cons |
|--------|-------------|------|------|
| **Grid Search** | Try all combinations | Exhaustive | Exponential cost |
| **Random Search** | Random combinations | More efficient than grid | May miss optimal |
| **Bayesian Optimization** | Use previous results to guide search | Smart, efficient | More complex |

---

## 19.6 Practice Questions

**Q1.** Compare Lasso (L1) and Ridge (L2) regularization. When would you choose one over the other?
> **Answer:** **Ridge (L2)** adds $\lambda\sum w_i^2$ to the loss. It shrinks all weights toward zero but rarely sets them exactly to zero. Best when you believe all features contribute (many small effects). **Lasso (L1)** adds $\lambda\sum|w_i|$. It can set weights to exactly zero, performing automatic feature selection. Best when you believe only a few features matter (sparse model). Use **Elastic Net** (L1+L2) when features are correlated, as Lasso tends to arbitrarily pick one correlated feature while Elastic Net keeps groups together. Mathematically, Lasso produces sparse solutions because the L1 constraint region has corners on the axes.

**Q2.** Explain the kernel trick in SVM. Why is the RBF kernel most commonly used?
> **Answer:** The kernel trick computes dot products in a high-dimensional feature space WITHOUT explicitly transforming the data. For SVM, we only need $K(x_i, x_j) = \phi(x_i) \cdot \phi(x_j)$ rather than computing $\phi(x_i)$ directly. The **RBF kernel** $K = \exp(-\gamma\|x_i-x_j\|^2)$ is popular because: (1) It maps to infinite-dimensional space, so it can represent any decision boundary; (2) It has only one hyperparameter ($\gamma$); (3) It's bounded between 0 and 1; (4) It creates localized influence — each support vector affects only nearby regions.

**Q3.** What is the difference between bagging and boosting? When would you choose Random Forest over XGBoost?
> **Answer:** **Bagging** trains models independently on bootstrap samples and averages predictions (reduces variance). **Boosting** trains models sequentially, each correcting the previous model's errors (reduces bias). **Choose Random Forest when:** (1) You need robust out-of-the-box performance with minimal tuning; (2) Training data has label noise (boosting amplifies noise); (3) Parallelization is needed. **Choose XGBoost when:** (1) Maximum accuracy is needed; (2) Data is clean; (3) You can invest in hyperparameter tuning; (4) Structured/tabular data competitions.

**Q4.** A binary classifier has 95% accuracy on a dataset with 95% negative and 5% positive samples. Is this model good?
> **Answer:** **No.** A naive classifier that always predicts "Negative" would also achieve 95% accuracy. This is the **accuracy paradox** on imbalanced data. We need to check other metrics: Recall ($TP/(TP+FN)$) — is it catching the positives? Precision ($TP/(TP+FP)$), F1-score. Also check the **confusion matrix** — the model might have 0% recall (missing all positives). For imbalanced data, use **Precision-Recall curve** and **Average Precision** instead of ROC-AUC, and consider techniques like SMOTE (oversampling), class weights, or threshold tuning.

**Q5.** Explain the decision tree splitting process using information gain. Why are decision trees prone to overfitting?
> **Answer:** At each node, compute parent entropy $H = -\sum p_k \log_2 p_k$, then for each possible split, compute the weighted average entropy of children. **Information gain** = parent entropy − weighted child entropy. Choose the split with the highest IG. **Overfitting occurs because:** (1) Trees can grow until each leaf has one sample (memorizing data); (2) Small changes in data can lead to completely different trees (high variance); (3) No regularization by default. **Solutions:** Pre-pruning (max depth, min samples per leaf), post-pruning (cost-complexity pruning), or use ensemble methods (Random Forest averages many trees to reduce variance).

---

*Previous: [Chapter 18 — Math Foundations](18_Math_Foundations_for_ML.md) | Next: [Chapter 20 — Unsupervised Learning](20_Unsupervised_Learning.md)*

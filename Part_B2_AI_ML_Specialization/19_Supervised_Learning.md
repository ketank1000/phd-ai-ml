# 19. Machine Learning — Supervised Learning

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 19.1 Regression

- [ ] **Linear Regression**
  - Model: $y = w_0 + w_1 x_1 + w_2 x_2 + ... + w_n x_n + \epsilon$
  - Loss function: Mean Squared Error (MSE) = $\frac{1}{n} \sum (y_i - \hat{y}_i)^2$
  - Normal equation: $w = (X^T X)^{-1} X^T y$
  - Assumptions: linearity, independence, homoscedasticity, normality of residuals
  - R² score: $1 - \frac{SS_{res}}{SS_{tot}}$

- [ ] **Polynomial Regression**
  - Extends linear regression with polynomial features
  - Risk of overfitting with high degree

- [ ] **Regularization**
  - **Lasso (L1)**: $J = MSE + \lambda \sum |w_i|$ → Feature selection (sparse)
  - **Ridge (L2)**: $J = MSE + \lambda \sum w_i^2$ → Weight shrinkage
  - **Elastic Net**: L1 + L2 combined

## 19.2 Classification

- [ ] **Logistic Regression**
  - Sigmoid function: $\sigma(z) = \frac{1}{1 + e^{-z}}$
  - Loss: Binary cross-entropy = $-\frac{1}{n} \sum [y \log(\hat{y}) + (1-y) \log(1-\hat{y})]$
  - Decision boundary: linear

- [ ] **K-Nearest Neighbors (KNN)**
  - Non-parametric, instance-based learning
  - Decision: majority vote of k nearest neighbors
  - Distance metrics: Euclidean, Manhattan, Minkowski, Cosine
  - Curse of dimensionality: performance degrades in high dimensions
  - Choose k: odd number, use cross-validation

- [ ] **Naive Bayes**
  - Based on Bayes' theorem with "naive" independence assumption
  - $P(C|X) \propto P(C) \prod P(x_i | C)$
  - Variants: Gaussian (continuous), Multinomial (text), Bernoulli (binary)
  - Fast, works well for text classification (spam detection)

- [ ] **Decision Trees**
  - Split criteria:
    - **Gini impurity**: $Gini = 1 - \sum p_i^2$
    - **Information gain**: $IG = H(parent) - \sum \frac{|child|}{|parent|} H(child)$
    - **Entropy**: $H = -\sum p_i \log_2 p_i$
  - Algorithms: ID3, C4.5, CART
  - Pruning: pre-pruning (max depth, min samples), post-pruning

- [ ] **Support Vector Machines (SVM)**
  - Find hyperplane that maximizes margin between classes
  - Support vectors: closest points to the hyperplane
  - **Kernel trick**: Map to higher dimensions for non-linear separation
    - Linear, Polynomial, RBF (Gaussian), Sigmoid kernels
  - Soft margin: C parameter (trade-off between margin width and misclassification)
  - Hinge loss: $\max(0, 1 - y_i \cdot (w \cdot x_i + b))$

## 19.3 Ensemble Methods

- [ ] **Bagging (Bootstrap Aggregating)**
  - Train multiple models on random subsets (with replacement)
  - Combine by voting (classification) or averaging (regression)
  - Reduces variance

- [ ] **Random Forest**
  - Bagging + random feature subset at each split
  - Robust, handles overfitting well
  - Feature importance ranking

- [ ] **Boosting**
  - Sequential learners, each fixes predecessor's errors
  - **AdaBoost**: Increase weight of misclassified samples
  - **Gradient Boosting**: Fit new model to residual errors
  - **XGBoost**: Optimized gradient boosting with regularization
  - **LightGBM**: Leaf-wise growth, faster on large datasets
  - **CatBoost**: Handles categorical features natively

## 19.4 Model Evaluation & Selection

- [ ] **Metrics — Classification**

  | Metric | Formula | Use When |
  |--------|---------|----------|
  | **Accuracy** | $\frac{TP+TN}{TP+TN+FP+FN}$ | Balanced classes |
  | **Precision** | $\frac{TP}{TP+FP}$ | Cost of FP is high (spam detection) |
  | **Recall/Sensitivity** | $\frac{TP}{TP+FN}$ | Cost of FN is high (disease detection) |
  | **F1-Score** | $\frac{2 \cdot P \cdot R}{P + R}$ | Balance precision & recall |
  | **Specificity** | $\frac{TN}{TN+FP}$ | True negative rate |
  | **AUC-ROC** | Area under ROC curve | Overall model performance |

- [ ] **Metrics — Regression**
  - MAE: $\frac{1}{n} \sum |y_i - \hat{y}_i|$
  - MSE: $\frac{1}{n} \sum (y_i - \hat{y}_i)^2$
  - RMSE: $\sqrt{MSE}$
  - R² Score: $1 - \frac{SS_{res}}{SS_{tot}}$

- [ ] **Bias-Variance Tradeoff**
  - **High bias** (underfitting): Model too simple, high training error
  - **High variance** (overfitting): Model too complex, low training error but high test error
  - Total Error = Bias² + Variance + Irreducible Error
  - Solution: Regularization, cross-validation, more data, feature engineering

- [ ] **Cross-Validation**
  - K-Fold: Split data into k folds, rotate test fold
  - Stratified K-Fold: Maintains class proportions
  - Leave-one-out (LOO): k = n
  - Hyperparameter tuning: Grid search, Random search, Bayesian optimization

- [ ] **Confusion Matrix**
  ```
                Predicted
                Pos     Neg
  Actual Pos    TP      FN
  Actual Neg    FP      TN
  ```

---

### Recommended Resources
- **Book**: *Hands-On Machine Learning with Scikit-Learn, Keras, and TensorFlow* — Aurélien Géron
- **Book**: *The Elements of Statistical Learning* — Hastie, Tibshirani, Friedman
- **Book**: *Pattern Recognition and Machine Learning* — Christopher Bishop
- **Course**: Andrew Ng's Machine Learning (Coursera)

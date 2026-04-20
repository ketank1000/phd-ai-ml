# 18. Mathematical Foundations for AI/ML

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 18.1 Linear Algebra

- [ ] **Vectors and Matrices**
  - Vector operations: addition, scalar multiplication, dot product, cross product
  - Matrix operations: multiplication, transpose, inverse, determinant
  - Identity matrix, diagonal matrix, symmetric matrix, orthogonal matrix

- [ ] **Eigenvalues & Eigenvectors**
  - $Av = \lambda v$ where $\lambda$ = eigenvalue, $v$ = eigenvector
  - Characteristic equation: $\det(A - \lambda I) = 0$
  - Eigendecomposition: $A = Q \Lambda Q^{-1}$
  - Used in PCA, spectral clustering, Google PageRank

- [ ] **Singular Value Decomposition (SVD)**
  - $A = U \Sigma V^T$
  - U: left singular vectors, Σ: singular values (diagonal), V: right singular vectors
  - Applications: dimensionality reduction, recommender systems, image compression

- [ ] **Principal Component Analysis (PCA)**
  - Compute covariance matrix → find eigenvalues/eigenvectors → project onto top-k eigenvectors
  - Reduces dimensionality while preserving maximum variance

- [ ] **Key Concepts**
  - Vector spaces, basis, span, rank
  - Linear independence, null space
  - Norms: L1 (Manhattan), L2 (Euclidean), L∞ (max)
  - Positive definite/semi-definite matrices

## 18.2 Probability & Statistics

- [ ] **Basic Probability**
  - Sample space, events, conditional probability
  - $P(A|B) = \frac{P(A \cap B)}{P(B)}$
  - Independence: $P(A \cap B) = P(A) \cdot P(B)$

- [ ] **Bayes' Theorem**
  $$P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}$$
  - Prior, likelihood, posterior, evidence
  - Foundation of Bayesian ML methods

- [ ] **Random Variables & Distributions**
  - Discrete: Bernoulli, Binomial, Poisson, Multinomial
  - Continuous: Uniform, Normal/Gaussian, Exponential, Beta, Gamma
  - Expected value: $E[X] = \sum x_i P(x_i)$ or $\int x f(x) dx$
  - Variance: $Var(X) = E[X^2] - (E[X])^2$

- [ ] **Maximum Likelihood Estimation (MLE)**
  - Find parameters θ that maximize $L(\theta) = \prod P(x_i | \theta)$
  - In practice, maximize log-likelihood: $\ell(\theta) = \sum \log P(x_i | \theta)$

- [ ] **Maximum A Posteriori (MAP)**
  - $\theta_{MAP} = \arg\max_\theta P(\theta | X) = \arg\max_\theta P(X|\theta) P(\theta)$
  - MLE with a prior (regularization connection: L2 regularization ↔ Gaussian prior)

- [ ] **Information Theory**
  - Entropy: $H(X) = -\sum P(x) \log_2 P(x)$
  - Cross-entropy: $H(P, Q) = -\sum P(x) \log Q(x)$
  - KL Divergence: $D_{KL}(P||Q) = \sum P(x) \log \frac{P(x)}{Q(x)}$
  - Mutual information

## 18.3 Calculus & Optimization

- [ ] **Calculus Review**
  - Derivatives, partial derivatives
  - Chain rule: $\frac{dz}{dx} = \frac{dz}{dy} \cdot \frac{dy}{dx}$ (critical for backpropagation)
  - Gradient: $\nabla f = [\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, ..., \frac{\partial f}{\partial x_n}]$
  - Jacobian matrix, Hessian matrix

- [ ] **Optimization**
  - **Convex optimization**: Global minimum guaranteed
  - **Gradient Descent**: $\theta_{t+1} = \theta_t - \eta \nabla J(\theta_t)$
    - Learning rate (η): too high → diverge, too low → slow
  - **Variants**:
    - **Batch GD**: Full dataset per update
    - **Stochastic GD (SGD)**: One sample per update
    - **Mini-batch GD**: Subset per update
  - **Advanced Optimizers**:
    - **Momentum**: Accumulates past gradients
    - **RMSProp**: Adapts learning rate per parameter
    - **Adam**: Momentum + RMSProp (most commonly used)
    - **AdaGrad**: Adapts learning rate based on gradient history
  - **Learning Rate Scheduling**: Step decay, cosine annealing, warm-up

---

### Recommended Resources
- **Book**: *Mathematics for Machine Learning* — Deisenroth, Faisal, Ong (free PDF available)
- **Book**: *Pattern Recognition and Machine Learning* — Christopher Bishop (Chapters 1-2)
- **Book**: *Linear Algebra and Its Applications* — Gilbert Strang

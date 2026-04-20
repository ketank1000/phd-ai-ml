# 18. Mathematical Foundations for AI/ML

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 18.1 Linear Algebra

Linear algebra is the **language of machine learning**. Every ML model manipulates vectors and matrices — understanding linear algebra is non-negotiable.

### 18.1.1 Scalars, Vectors, and Matrices

| Object | Notation | Description | Example |
|--------|----------|-------------|---------|
| Scalar | $a$ | Single number | Temperature = 37.5 |
| Vector | $\mathbf{v}$ | Ordered array of numbers | Feature vector: [age, income, score] |
| Matrix | $A$ | 2D array (rows × columns) | Dataset: n samples × m features |
| Tensor | $\mathcal{T}$ | Multi-dimensional array | Color image: height × width × 3 |

### 18.1.2 Vector Operations

**Dot product** (inner product) — the most important operation in ML:

$$\mathbf{a} \cdot \mathbf{b} = \sum_{i=1}^{n} a_i b_i = \|\mathbf{a}\| \|\mathbf{b}\| \cos\theta$$

**Geometric interpretation:** Dot product measures how aligned two vectors are. If positive → same direction, if zero → perpendicular, if negative → opposite direction.

**ML significance:** Used in linear regression ($\hat{y} = \mathbf{w} \cdot \mathbf{x} + b$), neural network neurons, cosine similarity for text comparison.

**Vector norms** (measure vector "size"):

| Norm | Formula | Name | ML Use |
|------|---------|------|--------|
| $L_1$ | $\sum |x_i|$ | Manhattan | Lasso/L1 regularization, sparse models |
| $L_2$ | $\sqrt{\sum x_i^2}$ | Euclidean | Ridge/L2 regularization, distance metric |
| $L_\infty$ | $\max |x_i|$ | Max norm | Gradient clipping |

### 18.1.3 Matrix Operations

**Matrix multiplication:** $C = AB$ where $C_{ij} = \sum_k A_{ik} B_{kj}$

Requirements: A is $m \times n$, B is $n \times p$ → C is $m \times p$ (inner dimensions must match).

**Key matrix types:**

| Matrix | Property | Example |
|--------|----------|---------|
| **Identity** $I$ | $AI = IA = A$ | Diagonal of 1s |
| **Transpose** $A^T$ | Rows ↔ Columns | $A^T_{ij} = A_{ji}$ |
| **Symmetric** | $A = A^T$ | Covariance matrix |
| **Orthogonal** | $A^T A = I$ | Rotation matrices |
| **Diagonal** | Non-zero only on diagonal | Scaling operations |
| **Inverse** $A^{-1}$ | $AA^{-1} = I$ | Solving linear systems |

**Determinant:** Scalar value that measures how a matrix transforms volume.
- $\det(A) = 0$ → matrix is **singular** (no inverse, linearly dependent columns)
- $\det(A) \neq 0$ → matrix is **invertible**

**For a 2×2 matrix:**
$$\det\begin{pmatrix} a & b \\ c & d \end{pmatrix} = ad - bc$$

### 18.1.4 Vector Spaces and Key Concepts

**Linear independence:** Vectors $\mathbf{v}_1, \mathbf{v}_2, ..., \mathbf{v}_n$ are linearly independent if no vector can be written as a combination of others.

**Rank:** Number of linearly independent rows (or columns). For $m \times n$ matrix: $\text{rank} \leq \min(m, n)$.

**Null space (kernel):** Set of all vectors $\mathbf{x}$ such that $A\mathbf{x} = \mathbf{0}$.

| Concept | Definition | ML Significance |
|---------|-----------|----------------|
| **Span** | All possible linear combinations of vectors | Feature space |
| **Basis** | Minimal set of vectors that spans the space | Principal components in PCA |
| **Rank** | Dimension of column space | Effective dimensionality of data |

### 18.1.5 Eigenvalues and Eigenvectors

**Definition:** For matrix $A$, vector $\mathbf{v}$ is an eigenvector and $\lambda$ is its eigenvalue if:

$$A\mathbf{v} = \lambda \mathbf{v}$$

**Intuition:** $A$ transforms most vectors into a different direction, but eigenvectors only get scaled (by $\lambda$), not rotated.

**How to find them:**

1. Solve the **characteristic equation**: $\det(A - \lambda I) = 0$ to find eigenvalues $\lambda$
2. For each $\lambda$, solve $(A - \lambda I)\mathbf{v} = \mathbf{0}$ to find eigenvectors

**Worked Example:**

$$A = \begin{pmatrix} 4 & 1 \\ 2 & 3 \end{pmatrix}$$

Step 1: $\det(A - \lambda I) = (4-\lambda)(3-\lambda) - 2 = \lambda^2 - 7\lambda + 10 = 0$

$\lambda_1 = 5, \quad \lambda_2 = 2$

Step 2: For $\lambda_1 = 5$: $(A - 5I)\mathbf{v} = 0$

$$\begin{pmatrix} -1 & 1 \\ 2 & -2 \end{pmatrix}\mathbf{v} = 0 \Rightarrow \mathbf{v}_1 = \begin{pmatrix} 1 \\ 1 \end{pmatrix}$$

**Eigendecomposition:** $A = Q \Lambda Q^{-1}$ where $Q$ = matrix of eigenvectors, $\Lambda$ = diagonal matrix of eigenvalues.

| ML Application | How Eigenvalues Are Used |
|---------------|-------------------------|
| **PCA** | Top-k eigenvectors of covariance matrix = principal components |
| **Spectral Clustering** | Eigenvectors of graph Laplacian |
| **PageRank** | Dominant eigenvector of web link matrix |
| **Stability Analysis** | Eigenvalues determine system stability |

### 18.1.6 Singular Value Decomposition (SVD)

**Any** matrix $A$ (even non-square) can be decomposed as:

$$A = U \Sigma V^T$$

| Component | Size | Description |
|-----------|------|-------------|
| $U$ | $m \times m$ | Left singular vectors (orthonormal) |
| $\Sigma$ | $m \times n$ | Diagonal matrix of singular values ($\sigma_1 \geq \sigma_2 \geq ... \geq 0$) |
| $V^T$ | $n \times n$ | Right singular vectors (orthonormal) |

**Truncated SVD:** Keep only top-$k$ singular values → best rank-$k$ approximation of $A$.

**Applications:**
- **Dimensionality reduction:** Latent Semantic Analysis (LSA) for text
- **Recommender systems:** Netflix Prize used SVD
- **Image compression:** Keep top-$k$ components; discard small singular values
- **Noise reduction:** Small singular values often correspond to noise

### 18.1.7 Positive Definite Matrices

A symmetric matrix $A$ is:
- **Positive definite** if $\mathbf{x}^T A \mathbf{x} > 0$ for all $\mathbf{x} \neq 0$ (all eigenvalues > 0)
- **Positive semi-definite** if $\mathbf{x}^T A \mathbf{x} \geq 0$ (all eigenvalues ≥ 0)

**ML significance:** Covariance matrices are always positive semi-definite. Loss functions that produce PSD Hessians guarantee convexity (a unique minimum exists).

---

## 18.2 Probability and Statistics for ML

### 18.2.1 Basic Probability

**Sample space** ($\Omega$): Set of all possible outcomes.  
**Event**: A subset of the sample space.

**Axioms of probability:**
1. $0 \leq P(A) \leq 1$
2. $P(\Omega) = 1$
3. For mutually exclusive events: $P(A \cup B) = P(A) + P(B)$

**Conditional probability:**

$$P(A|B) = \frac{P(A \cap B)}{P(B)}$$

**Independence:** $A$ and $B$ are independent if $P(A \cap B) = P(A) \cdot P(B)$, equivalently $P(A|B) = P(A)$.

**Law of Total Probability:**

$$P(B) = \sum_i P(B|A_i) P(A_i)$$

### 18.2.2 Bayes' Theorem

$$\boxed{P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}}$$

| Term | Name | ML Interpretation |
|------|------|-------------------|
| $P(A \| B)$ | **Posterior** | Updated belief after seeing data |
| $P(B \| A)$ | **Likelihood** | How likely is this data given hypothesis |
| $P(A)$ | **Prior** | Initial belief before seeing data |
| $P(B)$ | **Evidence** | Normalizing constant |

**Worked Example: Medical Test**

- Disease prevalence: $P(D) = 0.01$ (1%)
- Test sensitivity: $P(+|D) = 0.99$ (99%)
- Test specificity: $P(-|\neg D) = 0.95$ (5% false positive)

What is $P(D|+)$? (Probability of disease given a positive test)

$$P(D|+) = \frac{P(+|D) \cdot P(D)}{P(+|D) \cdot P(D) + P(+|\neg D) \cdot P(\neg D)}$$

$$= \frac{0.99 \times 0.01}{0.99 \times 0.01 + 0.05 \times 0.99} = \frac{0.0099}{0.0099 + 0.0495} = \frac{0.0099}{0.0594} \approx 0.167$$

**Only 16.7%!** Even with a 99% accurate test, most positive results are false positives when the disease is rare. This is the **base rate fallacy**.

### 18.2.3 Random Variables and Distributions

**Key Discrete Distributions:**

| Distribution | PMF | Mean | Variance | ML Use |
|-------------|-----|------|----------|--------|
| **Bernoulli** | $P(X=1) = p$ | $p$ | $p(1-p)$ | Binary classification output |
| **Binomial** | $\binom{n}{k} p^k (1-p)^{n-k}$ | $np$ | $np(1-p)$ | Number of successes in n trials |
| **Poisson** | $\frac{\lambda^k e^{-\lambda}}{k!}$ | $\lambda$ | $\lambda$ | Rare event counts |
| **Multinomial** | $\frac{n!}{\prod k_i!} \prod p_i^{k_i}$ | $np_i$ | $np_i(1-p_i)$ | Multi-class softmax output |

**Key Continuous Distributions:**

| Distribution | PDF | Mean | Variance | ML Use |
|-------------|-----|------|----------|--------|
| **Uniform** | $\frac{1}{b-a}$ | $\frac{a+b}{2}$ | $\frac{(b-a)^2}{12}$ | Random initialization |
| **Normal** | $\frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$ | $\mu$ | $\sigma^2$ | Everywhere in ML (CLT, errors) |
| **Exponential** | $\lambda e^{-\lambda x}$ | $1/\lambda$ | $1/\lambda^2$ | Time between events |

**The Normal (Gaussian) distribution** is the most important in ML:

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} \exp\left(-\frac{(x-\mu)^2}{2\sigma^2}\right)$$

- **Central Limit Theorem (CLT):** Average of many independent random variables → Normal, regardless of original distribution. This is why Gaussian assumptions work so often in practice.
- **Multivariate Normal:** $\mathbf{x} \sim \mathcal{N}(\boldsymbol{\mu}, \Sigma)$ where $\Sigma$ is the covariance matrix.

### 18.2.4 Expected Value and Variance

$$E[X] = \sum_x x \cdot P(x) \quad \text{(discrete)} \qquad E[X] = \int_{-\infty}^{\infty} x \cdot f(x) \, dx \quad \text{(continuous)}$$

$$Var(X) = E[(X - \mu)^2] = E[X^2] - (E[X])^2$$

**Properties:**
- $E[aX + b] = aE[X] + b$
- $Var(aX + b) = a^2 Var(X)$
- $E[X + Y] = E[X] + E[Y]$ (always)
- $Var(X + Y) = Var(X) + Var(Y)$ (only if X, Y independent)

**Covariance and Correlation:**

$$Cov(X,Y) = E[(X-\mu_X)(Y-\mu_Y)] = E[XY] - E[X]E[Y]$$

$$\rho_{XY} = \frac{Cov(X,Y)}{\sigma_X \sigma_Y} \quad \in [-1, 1]$$

- $\rho = 1$: perfect positive linear relationship
- $\rho = 0$: no linear relationship (but could be non-linear!)
- $\rho = -1$: perfect negative linear relationship

### 18.2.5 Maximum Likelihood Estimation (MLE)

**Goal:** Find parameter values $\theta$ that make the observed data most likely.

**Likelihood function:** $L(\theta) = \prod_{i=1}^{n} P(x_i | \theta)$

**Log-likelihood** (easier to work with — products become sums):

$$\ell(\theta) = \sum_{i=1}^{n} \log P(x_i | \theta)$$

**MLE:** $\hat{\theta}_{MLE} = \arg\max_\theta \ell(\theta)$

**Worked Example: MLE for Normal Distribution Mean**

Given data $x_1, x_2, ..., x_n$ from $\mathcal{N}(\mu, \sigma^2)$ with known $\sigma$:

$$\ell(\mu) = -\frac{n}{2}\log(2\pi\sigma^2) - \frac{1}{2\sigma^2}\sum_{i=1}^{n}(x_i - \mu)^2$$

Taking derivative and setting to zero:

$$\frac{d\ell}{d\mu} = \frac{1}{\sigma^2}\sum(x_i - \mu) = 0 \Rightarrow \hat{\mu}_{MLE} = \frac{1}{n}\sum x_i = \bar{x}$$

The MLE of the mean is simply the sample mean — intuitive!

### 18.2.6 Maximum A Posteriori (MAP) Estimation

**MAP adds a prior belief about $\theta$:**

$$\hat{\theta}_{MAP} = \arg\max_\theta P(\theta | X) = \arg\max_\theta \left[ \log P(X|\theta) + \log P(\theta) \right]$$

**Connection to regularization:**
- If prior $P(\theta) \sim \mathcal{N}(0, \sigma^2)$ (Gaussian prior) → $\log P(\theta) \propto -\|\theta\|_2^2$ → **L2 regularization (Ridge)**
- If prior $P(\theta) \sim \text{Laplace}(0, b)$ → $\log P(\theta) \propto -\|\theta\|_1$ → **L1 regularization (Lasso)**

This is a profound insight: **regularization in ML is equivalent to putting a prior on the parameters!**

| Estimation | Formula | Regularization Equivalent |
|-----------|---------|--------------------------|
| **MLE** | Maximize likelihood only | No regularization (can overfit) |
| **MAP (Gaussian prior)** | Likelihood + L2 penalty | Ridge regression |
| **MAP (Laplace prior)** | Likelihood + L1 penalty | Lasso regression |

### 18.2.7 Information Theory

**Entropy** — measures uncertainty/information content:

$$H(X) = -\sum_{x} P(x) \log_2 P(x)$$

- Fair coin: $H = -0.5 \log_2 0.5 - 0.5 \log_2 0.5 = 1$ bit (maximum uncertainty)
- Biased coin (99% heads): $H \approx 0.08$ bits (low uncertainty)

**Cross-Entropy** — measures how well distribution $Q$ approximates true distribution $P$:

$$H(P, Q) = -\sum_x P(x) \log Q(x)$$

**This is the loss function used in classification!** Binary cross-entropy for logistic regression, categorical cross-entropy for multi-class.

**KL Divergence** — measures how different two distributions are:

$$D_{KL}(P \| Q) = \sum_x P(x) \log \frac{P(x)}{Q(x)} = H(P,Q) - H(P) \geq 0$$

- $D_{KL} = 0$ only when $P = Q$
- **Not symmetric:** $D_{KL}(P\|Q) \neq D_{KL}(Q\|P)$
- Used in VAEs, knowledge distillation, policy optimization (PPO in RL)

**Mutual Information:**

$$I(X;Y) = H(X) - H(X|Y) = D_{KL}(P(X,Y) \| P(X)P(Y))$$

Measures how much knowing $Y$ reduces uncertainty about $X$. Used in feature selection and decision tree splitting.

---

## 18.3 Calculus and Optimization

### 18.3.1 Derivatives and Gradients

**Derivative** (single variable): Rate of change of $f(x)$ with respect to $x$.

$$f'(x) = \lim_{h \to 0} \frac{f(x+h) - f(x)}{h}$$

**Common derivatives needed in ML:**

| Function | Derivative |
|----------|-----------|
| $x^n$ | $nx^{n-1}$ |
| $e^x$ | $e^x$ |
| $\ln(x)$ | $1/x$ |
| $\sigma(x) = \frac{1}{1+e^{-x}}$ | $\sigma(x)(1-\sigma(x))$ |
| $\tanh(x)$ | $1 - \tanh^2(x)$ |
| $\text{ReLU}(x) = \max(0,x)$ | $0$ if $x<0$, $1$ if $x>0$ |

**Partial derivative:** Derivative with respect to one variable while holding others constant.

$$\frac{\partial f}{\partial x_1} \quad \text{(vary } x_1 \text{, fix everything else)}$$

**Gradient:** Vector of all partial derivatives — points in the direction of steepest ascent.

$$\nabla f(\mathbf{x}) = \begin{bmatrix} \frac{\partial f}{\partial x_1} \\ \frac{\partial f}{\partial x_2} \\ \vdots \\ \frac{\partial f}{\partial x_n} \end{bmatrix}$$

### 18.3.2 Chain Rule — The Heart of Backpropagation

If $z = f(g(x))$, then:

$$\frac{dz}{dx} = \frac{dz}{dg} \cdot \frac{dg}{dx}$$

**Multi-variable chain rule:**

If $L = L(y)$, $y = f(w_1, w_2)$, $w_1 = g(x)$:

$$\frac{\partial L}{\partial x} = \frac{\partial L}{\partial y} \cdot \frac{\partial y}{\partial w_1} \cdot \frac{\partial w_1}{\partial x}$$

**This IS backpropagation!** The loss gradient flows backward through the network, applying the chain rule at each layer.

**Worked Example: Gradient of MSE Loss for Linear Regression**

Model: $\hat{y} = wx + b$, Loss: $L = \frac{1}{2}(y - \hat{y})^2$

$$\frac{\partial L}{\partial w} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial w} = -(y - \hat{y}) \cdot x$$

$$\frac{\partial L}{\partial b} = -(y - \hat{y}) \cdot 1$$

### 18.3.3 Jacobian and Hessian

**Jacobian** — matrix of first-order partial derivatives of a vector-valued function:

For $\mathbf{f}: \mathbb{R}^n \to \mathbb{R}^m$:

$$J = \begin{bmatrix} \frac{\partial f_1}{\partial x_1} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \vdots & \ddots & \vdots \\ \frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n} \end{bmatrix}$$

Used in: generative models (normalizing flows use the Jacobian determinant).

**Hessian** — matrix of second-order partial derivatives (curvature information):

$$H_{ij} = \frac{\partial^2 f}{\partial x_i \partial x_j}$$

Used in: Newton's method ($\theta_{t+1} = \theta_t - H^{-1} \nabla f$), checking convexity (positive definite Hessian → convex → unique minimum).

### 18.3.4 Gradient Descent

The workhorse optimization algorithm of ML:

$$\boxed{\theta_{t+1} = \theta_t - \eta \nabla J(\theta_t)}$$

where $\eta$ = learning rate, $J$ = loss function, $\nabla J$ = gradient of loss.

```
     Loss
      |
      |  *                        Start (random initialization)
      |    *
      |      *                    Gradient points "uphill"
      |        *  <-- step        We move OPPOSITE to gradient
      |          *
      |            *
      |              *            Minimum (convergence)
      |________________*_________ θ
```

**Variants of Gradient Descent:**

| Variant | Data Per Update | Pros | Cons |
|---------|----------------|------|------|
| **Batch GD** | Entire dataset | Stable convergence | Slow for large data, needs memory |
| **Stochastic GD (SGD)** | 1 sample | Fast updates, escapes local minima | Noisy, unstable |
| **Mini-batch GD** | $B$ samples (32-512) | Best of both worlds | Batch size is hyperparameter |

### 18.3.5 Advanced Optimizers

**Momentum:** Accelerates convergence using exponential moving average of past gradients.

$$v_t = \beta v_{t-1} + (1-\beta) \nabla J(\theta_t)$$
$$\theta_{t+1} = \theta_t - \eta v_t$$

Analogy: A ball rolling downhill gains momentum and can pass through small valleys (local minima).

**RMSProp:** Adapts learning rate per parameter using squared gradient history.

$$s_t = \beta s_{t-1} + (1-\beta)(\nabla J)^2$$
$$\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{s_t + \epsilon}} \nabla J$$

Parameters with large gradients get smaller learning rates — prevents zigzagging.

**Adam (Adaptive Moment Estimation):** Combines Momentum + RMSProp. **Most popular optimizer.**

$$m_t = \beta_1 m_{t-1} + (1-\beta_1) \nabla J \quad \text{(1st moment: mean)}$$
$$v_t = \beta_2 v_{t-1} + (1-\beta_2) (\nabla J)^2 \quad \text{(2nd moment: variance)}$$
$$\hat{m}_t = \frac{m_t}{1-\beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1-\beta_2^t} \quad \text{(bias correction)}$$
$$\theta_{t+1} = \theta_t - \frac{\eta}{\sqrt{\hat{v}_t} + \epsilon} \hat{m}_t$$

Default hyperparameters: $\beta_1 = 0.9, \beta_2 = 0.999, \epsilon = 10^{-8}$.

**Optimizer Comparison:**

| Optimizer | Adaptive LR | Momentum | Default Use Case |
|-----------|------------|----------|-----------------|
| **SGD** | No | Optional | Simple problems, with tuning |
| **SGD + Momentum** | No | Yes | Computer vision (ResNets) |
| **AdaGrad** | Yes | No | Sparse features (NLP embeddings) |
| **RMSProp** | Yes | No | RNNs, non-stationary problems |
| **Adam** | Yes | Yes | Default choice for most problems |
| **AdamW** | Yes | Yes | Adam with decoupled weight decay (Transformers) |

### 18.3.6 Convexity

A function $f$ is **convex** if for any two points $x_1, x_2$ and $0 \leq t \leq 1$:

$$f(tx_1 + (1-t)x_2) \leq t f(x_1) + (1-t) f(x_2)$$

**Why it matters:** Convex functions have a single global minimum — gradient descent is guaranteed to find it. Linear regression loss (MSE) is convex. Neural network losses are NOT convex (many local minima), but SGD works surprisingly well in practice (most local minima are nearly as good as global).

### 18.3.7 Learning Rate Scheduling

| Schedule | Formula | When to Use |
|----------|---------|-------------|
| **Step Decay** | Reduce by factor every $k$ epochs | Simple, predictable |
| **Exponential Decay** | $\eta_t = \eta_0 \cdot e^{-\lambda t}$ | Smooth reduction |
| **Cosine Annealing** | $\eta_t = \frac{\eta_0}{2}(1 + \cos(\pi t / T))$ | Modern Transformers |
| **Warm-up** | Slowly increase $\eta$ for first $k$ steps | Large models (BERT, GPT) |
| **ReduceOnPlateau** | Reduce when validation loss stops improving | Adaptive, safe default |

---

## 18.4 Practice Questions

**Q1.** Given matrix $A = \begin{pmatrix} 3 & 1 \\ 1 & 3 \end{pmatrix}$, find the eigenvalues and eigenvectors.
> **Answer:** Characteristic equation: $\det(A - \lambda I) = (3-\lambda)^2 - 1 = \lambda^2 - 6\lambda + 8 = 0$. So $\lambda_1 = 4, \lambda_2 = 2$. For $\lambda_1 = 4$: $(A-4I)\mathbf{v} = 0 \Rightarrow \begin{pmatrix}-1&1\\1&-1\end{pmatrix}\mathbf{v}=0 \Rightarrow \mathbf{v}_1 = (1,1)^T$. For $\lambda_2 = 2$: $(A-2I)\mathbf{v}=0 \Rightarrow \begin{pmatrix}1&1\\1&1\end{pmatrix}\mathbf{v}=0 \Rightarrow \mathbf{v}_2 = (1,-1)^T$.

**Q2.** A disease affects 1 in 1000 people. A test is 99% sensitive and 95% specific. If a person tests positive, what is the probability they have the disease?
> **Answer:** Using Bayes: $P(D|+) = \frac{P(+|D)P(D)}{P(+|D)P(D)+P(+|\neg D)P(\neg D)} = \frac{0.99 \times 0.001}{0.99 \times 0.001 + 0.05 \times 0.999} = \frac{0.00099}{0.00099 + 0.04995} = \frac{0.00099}{0.05094} \approx 0.0194$. Only about 1.94%. The low base rate overwhelms the test accuracy.

**Q3.** Explain why Adam optimizer is preferred over vanilla SGD for training deep neural networks.
> **Answer:** Adam combines two benefits: (1) **Momentum** (exponential moving average of gradients) — smooths out noisy gradients and accelerates convergence in consistent gradient directions; (2) **Adaptive learning rates** (via RMSProp-style second moment) — gives each parameter its own effective learning rate. Parameters with large gradients get smaller updates and vice versa. Adam also includes bias correction for early training steps. Vanilla SGD uses a single global learning rate and is more sensitive to its choice, though SGD with momentum can generalize better in some vision tasks.

**Q4.** What is the connection between MAP estimation with a Gaussian prior and L2 regularization?
> **Answer:** MAP maximizes $\log P(\theta|X) = \log P(X|\theta) + \log P(\theta)$. If the prior is $P(\theta) \sim \mathcal{N}(0, \sigma^2)$, then $\log P(\theta) = -\frac{\|\theta\|_2^2}{2\sigma^2} + C$. So MAP = maximize log-likelihood minus $\frac{1}{2\sigma^2}\|\theta\|_2^2$. This is identical to minimizing the loss function plus $\lambda\|\theta\|_2^2$ (Ridge/L2 regularization), where $\lambda = \frac{1}{2\sigma^2}$. Stronger prior (smaller $\sigma$) = stronger regularization (larger $\lambda$).

**Q5.** Explain KL divergence and why it is not a true distance metric. How is it used in ML?
> **Answer:** $D_{KL}(P\|Q) = \sum P(x) \log \frac{P(x)}{Q(x)}$ measures how much distribution $Q$ deviates from $P$. It is NOT a true distance because it is **asymmetric** ($D_{KL}(P\|Q) \neq D_{KL}(Q\|P)$) and doesn't satisfy the triangle inequality. In ML: (1) **VAEs** minimize KL divergence between the learned latent distribution and a standard Gaussian prior; (2) **Knowledge distillation** minimizes KL between teacher and student predictions; (3) **PPO (RL)** constrains policy updates using KL divergence; (4) **Cross-entropy loss** = $H(P) + D_{KL}(P\|Q)$, and since $H(P)$ is constant, minimizing cross-entropy = minimizing KL divergence.

---

*Previous: [Chapter 17 — Programming & OOP](../Part_B1_Core_CS/17_Programming_and_OOP.md) | Next: [Chapter 19 — Supervised Learning](19_Supervised_Learning.md)*

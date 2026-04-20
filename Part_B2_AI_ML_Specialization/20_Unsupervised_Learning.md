# 20. Machine Learning — Unsupervised Learning

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 20.1 Overview

**Unsupervised learning:** Learn patterns from unlabeled data — no $y$ values, only $\{x_i\}_{i=1}^{n}$.

| Task | Goal | Methods |
|------|------|---------|
| **Clustering** | Group similar data points | K-Means, DBSCAN, GMM |
| **Dimensionality Reduction** | Reduce features while preserving information | PCA, t-SNE, UMAP |
| **Association Rules** | Find co-occurrence patterns | Apriori, FP-Growth |
| **Anomaly Detection** | Identify outliers | Isolation Forest, One-Class SVM |
| **Density Estimation** | Estimate the data distribution | KDE, GMM |

---

## 20.2 Clustering

### 20.2.1 K-Means Clustering

**Algorithm:**

1. Choose $k$ (number of clusters)
2. Initialize $k$ centroids (randomly or using K-Means++)
3. **Assign** each point to the nearest centroid
4. **Update** each centroid to the mean of its assigned points
5. Repeat steps 3-4 until convergence (assignments stop changing)

```
 Iteration 0          Iteration 1          Convergence
  .  .  *  .           .  .  *  .           .  .  *  .
  . .    . .          [. .]  [. .]         [. .]  [. .]
     *                   *                   *
  .  .  .  .           .  .  .  .           .  .  .  .
  . .    . .          [. .]  [. .]         [. .]  [. .]
  
  * = centroid (moves)   → settled
```

**Objective (Inertia / WCSS):**

$$J = \sum_{i=1}^{n} \min_{j} \| x_i - \mu_j \|^2$$

**K-Means++ Initialization:** Instead of random, choose first centroid randomly, then each subsequent centroid with probability proportional to distance squared from nearest existing centroid. This avoids poor initializations and converges faster.

**Choosing $k$:**

| Method | How It Works | Choose $k$ When |
|--------|-------------|-----------------|
| **Elbow Method** | Plot inertia vs. $k$, find "elbow" bend | Inertia curve bends sharply |
| **Silhouette Score** | $\frac{b-a}{\max(a,b)}$ where $a$ = avg intra-cluster, $b$ = avg nearest-cluster distance | Score is maximized (range -1 to 1) |
| **Gap Statistic** | Compare inertia to random uniform data | Gap is maximized |

**Limitations of K-Means:**
- Assumes **spherical, equal-size** clusters
- Sensitive to outliers (single outlier can shift centroid)
- Must specify $k$ in advance
- Gets stuck in local minima (run multiple times)
- Cannot handle non-convex shapes

**Time complexity:** $O(n \cdot k \cdot d \cdot \text{iterations})$

### 20.2.2 Hierarchical Clustering

**Two approaches:**
- **Agglomerative (bottom-up):** Start with $n$ clusters (one per point), repeatedly merge the two closest clusters until one remains.
- **Divisive (top-down):** Start with one cluster, repeatedly split.

**Linkage criteria** (how to measure cluster-to-cluster distance):

| Linkage | Distance Between Clusters | Effect |
|---------|--------------------------|--------|
| **Single** | Minimum distance between any two points | Chain-like clusters (can merge dissimilar) |
| **Complete** | Maximum distance between any two points | Compact, spherical clusters |
| **Average** | Average of all pairwise distances | Compromise between single and complete |
| **Ward's** | Increase in total WCSS after merge | Minimizes variance, produces equal-size clusters |

**Dendrogram:** Tree diagram showing merge/split history. Cut at a height to get $k$ clusters.

```
Height
  4  |         ┌───────────┐
  3  |     ┌───┤           │
  2  |  ┌──┤   │        ┌──┤
  1  |  │  │   │     ┌──┤  │
  0  |──A──B───C─────D──E──F
                 ↑
          Cut here for 2 clusters: {A,B,C} and {D,E,F}
```

**Pros:** No need to specify $k$ upfront, produces a hierarchy of clusters, handles any shape.  
**Cons:** $O(n^2)$ space, $O(n^3)$ time (or $O(n^2 \log n)$ for some linkages), cannot undo a merge.

### 20.2.3 DBSCAN (Density-Based Spatial Clustering)

**Parameters:** $\varepsilon$ (neighborhood radius), $\text{minPts}$ (minimum neighbors)

**Point types:**
- **Core point:** Has ≥ minPts neighbors within $\varepsilon$
- **Border point:** Within $\varepsilon$ of a core point but < minPts neighbors
- **Noise point:** Neither core nor border (outlier)

**Algorithm:**
1. For each unvisited point, check if it's a core point
2. If core, create a new cluster and expand: add all density-reachable points
3. Border points are assigned to the nearest core point's cluster
4. Noise points remain unassigned

```
    Core points           Border point        Noise
   (≥ minPts              (near core,         (isolated)
    neighbors)             < minPts)

     • • •                    •                    •
    • ● • •                 near ●
     • • •
```

**Advantages:**
- Finds clusters of **arbitrary shape** (not just spherical)
- Automatically determines number of clusters
- Naturally identifies **outliers/noise**
- No need to specify $k$

**Disadvantages:**
- Struggles with clusters of **varying density**
- Sensitive to $\varepsilon$ and minPts choice
- $O(n^2)$ without spatial index ($O(n \log n)$ with KD-tree)

### 20.2.4 Gaussian Mixture Models (GMM)

**Soft clustering:** Each point has a probability of belonging to each cluster (unlike K-Means' hard assignment).

**Model:** Data is generated from a mixture of $K$ Gaussian distributions:

$$P(x) = \sum_{k=1}^{K} \pi_k \cdot \mathcal{N}(x | \mu_k, \Sigma_k)$$

where $\pi_k$ = mixing coefficient (weight of cluster $k$), $\sum \pi_k = 1$.

**EM (Expectation-Maximization) Algorithm:**

| Step | Name | Action |
|------|------|--------|
| **E-step** | Expectation | Compute responsibility: $r_{ik} = P(\text{point } i \in \text{cluster } k | x_i)$ |
| **M-step** | Maximization | Update $\mu_k, \Sigma_k, \pi_k$ using weighted data |

Repeat until convergence (log-likelihood stops improving).

**GMM vs. K-Means:**

| Feature | K-Means | GMM |
|---------|---------|-----|
| Assignment | Hard (0 or 1) | Soft (probability) |
| Cluster shape | Spherical | Ellipsoidal (any covariance) |
| Interpretation | Distance-based | Probabilistic (generative model) |
| Complexity | Simple, fast | More complex, slower |

**Model selection:** Use **BIC** (Bayesian Information Criterion) or **AIC** (Akaike Information Criterion) to choose $K$. Lower is better.

### Clustering Comparison Summary

| Algorithm | # Clusters | Cluster Shape | Outliers | Scalability |
|-----------|-----------|---------------|----------|-------------|
| **K-Means** | Must specify $k$ | Spherical | Sensitive | $O(nkd)$, fast |
| **Hierarchical** | Cut dendrogram | Any | Moderate | $O(n^2)$ to $O(n^3)$ |
| **DBSCAN** | Automatic | Any shape | Robust (identifies them) | $O(n \log n)$ with index |
| **GMM** | Must specify $k$ | Ellipsoidal | Moderate | $O(nkd^2)$ |

---

## 20.3 Dimensionality Reduction

### 20.3.1 PCA (Principal Component Analysis)

**Goal:** Find new orthogonal axes (principal components) that capture maximum variance.

**Algorithm:**
1. **Standardize** data (zero mean, unit variance)
2. Compute **covariance matrix** $C = \frac{1}{n-1} X^T X$
3. Compute **eigenvalues** and **eigenvectors** of $C$
4. Sort eigenvectors by eigenvalue (descending)
5. **Project** data onto top-$k$ eigenvectors

**Choosing $k$ (number of components):**
- Plot **explained variance ratio** (scree plot)
- Choose $k$ such that cumulative explained variance ≥ 95% (or 99%)

**Worked Example:**

Original data in 2D: features $x_1, x_2$ highly correlated.

Covariance matrix eigenvalues: $\lambda_1 = 3.8, \lambda_2 = 0.2$

Explained variance: PC1 = $\frac{3.8}{4.0} = 95\%$, PC2 = $\frac{0.2}{4.0} = 5\%$

→ 1 component captures 95% of the information. Project from 2D to 1D.

**Properties of PCA:**
- **Linear** transformation
- Components are **orthogonal** (uncorrelated)
- **Unsupervised** (doesn't use labels)
- Sensitive to **feature scaling** (always standardize first)
- First PC has maximum variance, second PC has maximum remaining variance perpendicular to first, etc.

### 20.3.2 t-SNE (t-distributed Stochastic Neighbor Embedding)

**Goal:** Non-linear dimensionality reduction for **visualization** (typically to 2D or 3D).

**How it works:**
1. Compute pairwise **similarities** in high-dimensional space (using Gaussian kernel)
2. Initialize random low-dimensional representation
3. Compute pairwise similarities in low-dimensional space (using **t-distribution** — heavier tails)
4. **Minimize KL divergence** between the two similarity distributions using gradient descent

**Why t-distribution?** The "crowding problem" — in low dimensions, moderate-distance points would all be pushed together. The t-distribution's heavier tails allow moderate-distance points to be spread out.

**Hyperparameter — Perplexity (5–50):** Roughly how many neighbors each point considers. Low perplexity → local focus. High perplexity → more global structure preserved.

**Important caveats:**
- **Cannot project new data** (no learned transformation matrix)
- **Distances between clusters are not meaningful** (only within-cluster structure is reliable)
- **Different runs give different results** (stochastic)
- **Slow:** $O(n^2)$ naive, but Barnes-Hut approximation $O(n \log n)$

### 20.3.3 UMAP (Uniform Manifold Approximation and Projection)

**Similar goals to t-SNE** but with advantages:
- **Much faster** (scales to millions of points)
- Preserves **global structure** better (cluster-to-cluster distances are more meaningful)
- **Can project new data** (learns a parametric mapping)
- Based on topological data analysis theory (Riemannian geometry + fuzzy simplicial sets)

**Key hyperparameters:** `n_neighbors` (local vs. global balance), `min_dist` (how tight clusters appear).

### 20.3.4 LDA (Linear Discriminant Analysis)

**Supervised dimensionality reduction** (uses labels, unlike PCA):
- Maximizes **between-class variance**
- Minimizes **within-class variance**
- Projects to at most $K-1$ dimensions (where $K$ = number of classes)

**LDA vs. PCA:**

| Feature | PCA | LDA |
|---------|-----|-----|
| Supervision | Unsupervised | Supervised |
| Objective | Max total variance | Max class separability |
| Max components | $\min(n, d)$ | $K - 1$ |
| Assumption | None | Gaussian classes, equal covariance |

---

## 20.4 Association Rule Mining

**Find interesting relationships (co-occurrences) in transactional data.**

Example: Market basket analysis — "customers who buy bread AND butter often also buy milk."

### Key Metrics

| Metric | Formula | Interpretation |
|--------|---------|---------------|
| **Support** | $\frac{\text{transactions containing } X}{N}$ | How frequent is $X$? |
| **Confidence** | $\frac{\text{support}(X \cup Y)}{\text{support}(X)}$ | If $X$, how likely $Y$? |
| **Lift** | $\frac{\text{confidence}(X \to Y)}{\text{support}(Y)}$ | Is the association interesting? |

**Lift interpretation:**
- Lift = 1 → Independent (no association)
- Lift > 1 → Positive association ($X$ and $Y$ co-occur more than expected)
- Lift < 1 → Negative association (buying $X$ makes $Y$ less likely)

### Apriori Algorithm

**Anti-monotone property (Apriori principle):** If an itemset is infrequent, all its supersets are also infrequent.

**Algorithm:**
1. Find all frequent 1-itemsets (support ≥ min_support)
2. Generate candidate 2-itemsets from frequent 1-itemsets
3. Prune candidates using the anti-monotone property
4. Count support, keep frequent 2-itemsets
5. Repeat: generate $(k+1)$-itemsets from frequent $k$-itemsets

**Worked Example:**

Transactions: {A,B,C}, {A,B}, {A,C}, {B,C}, {A,B,C}. Min support = 0.4 (2/5).

Frequent 1-items: A(4/5), B(4/5), C(4/5). All frequent.  
Frequent 2-items: {A,B}(3/5), {A,C}(3/5), {B,C}(3/5). All frequent.  
Frequent 3-items: {A,B,C}(2/5). Frequent.  

Rule: $A \to B$: confidence = support({A,B})/support(A) = 0.6/0.8 = 0.75 (75%)

### FP-Growth (Frequent Pattern Growth)

- **Avoids candidate generation** (much faster than Apriori)
- Builds a compressed **FP-tree** of the data
- Mines patterns by recursively building conditional FP-trees
- Typically 10× or more faster than Apriori on large datasets

---

## 20.5 Anomaly Detection

**Goal:** Identify data points that are significantly different from the majority.

| Method | Approach | Best For |
|--------|----------|----------|
| **Z-score / IQR** | Points beyond $\mu \pm 3\sigma$ or $Q_1 - 1.5 \cdot IQR$ | Simple univariate data |
| **Isolation Forest** | Random splits; anomalies are isolated in fewer splits (shorter path) | High-dimensional, efficient |
| **One-Class SVM** | Learns a boundary around "normal" data in kernel space | Small datasets, clear boundary |
| **Local Outlier Factor (LOF)** | Compares local density of a point to its neighbors | Varying-density data |
| **Autoencoder** | High reconstruction error = anomaly (model learns "normal" patterns) | Complex data (images, time series) |

**Isolation Forest intuition:** Anomalies are "few and different" — random binary splits isolate them with fewer cuts than normal points.

```
Normal point needs many splits:          Anomaly isolated quickly:
  ┌────────────────────────┐              ┌────────────────────────┐
  │     │    ...    │..... │              │                    *   │
  │ ....│....  │....│.....│              │  ...................│   │
  │     │      │    │     │              │  ...................│   │
  └────────────────────────┘              └────────────────────────┘
   Path length: 8-10                       Path length: 2-3
```

---

## 20.6 Practice Questions

**Q1.** Compare K-Means and DBSCAN. When would you choose DBSCAN over K-Means?
> **Answer:** **K-Means** requires specifying $k$, assumes spherical clusters of similar size, is sensitive to outliers, and uses distance to centroids. **DBSCAN** discovers $k$ automatically, finds clusters of arbitrary shape, automatically identifies outliers as noise, and is based on density. **Choose DBSCAN when:** (1) clusters are non-spherical or have varying shapes (e.g., crescent-shaped); (2) outliers are expected and should be identified; (3) you don't know the number of clusters. **Choose K-Means when:** clusters are roughly spherical, you know $k$, or you need fast performance on very large datasets.

**Q2.** Explain the EM algorithm for Gaussian Mixture Models. Why is it used instead of direct optimization?
> **Answer:** EM alternates between two steps: **E-step** — compute the "responsibility" (posterior probability) that each cluster generated each data point, using current parameters. **M-step** — update parameters (means, covariances, mixing weights) using weighted data, where weights are the responsibilities. EM is needed because the **likelihood function for mixtures is non-convex** and involves a sum inside a log: $\log \sum_k \pi_k \mathcal{N}(x|\mu_k,\Sigma_k)$, which is hard to optimize directly. EM avoids this by treating cluster assignments as latent variables, converting the problem into a sequence of tractable optimizations. EM is guaranteed to **increase the log-likelihood at every step** and converge to a local maximum.

**Q3.** What is the difference between PCA and t-SNE? When would you use each?
> **Answer:** **PCA** is a linear method that preserves global variance structure — useful for feature reduction before ML models, fast ($O(nd^2)$), and deterministic. **t-SNE** is non-linear, preserves local neighborhood structure — excellent for visualization but not for feature reduction (can't project new data, slow, stochastic). **Use PCA** when: reducing features for a downstream model (50D → 10D), speed matters, or you need to explain variance. **Use t-SNE** when: you need to visualize high-dimensional data in 2D/3D to see cluster structure (e.g., visualizing word embeddings, MNIST digits).

**Q4.** Explain the Apriori principle and how it makes association rule mining efficient.
> **Answer:** The **Apriori principle (anti-monotone property)** states: if an itemset is infrequent, all its supersets are also infrequent. Conversely, all subsets of a frequent itemset must be frequent. This enables **pruning**: when generating candidate $(k+1)$-itemsets, we only consider combinations of frequent $k$-itemsets. Without this pruning, we'd need to check all $2^{|items|}$ possible itemsets (exponential). With Apriori pruning, we avoid generating candidates that cannot possibly be frequent, dramatically reducing computation.

**Q5.** How does Isolation Forest detect anomalies? Why is it efficient compared to distance-based methods?
> **Answer:** Isolation Forest builds multiple random binary trees. At each node, it randomly selects a feature and a random split value. **Anomalies**, being "few and different," get isolated (reach a leaf node) in **fewer splits** than normal points. The anomaly score is based on the **average path length** across all trees — shorter paths = more anomalous. It's efficient because: (1) It has **linear time complexity** $O(n \log n)$ vs. $O(n^2)$ for distance-based methods; (2) It only needs a **subsample** of data (e.g., 256 points per tree); (3) It doesn't require computing pairwise distances; (4) It naturally handles high-dimensional data without the curse of dimensionality.

---

*Previous: [Chapter 19 — Supervised Learning](19_Supervised_Learning.md) | Next: [Chapter 21 — Deep Learning](21_Deep_Learning.md)*

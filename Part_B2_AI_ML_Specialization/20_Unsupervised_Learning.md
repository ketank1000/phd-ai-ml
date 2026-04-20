# 20. Machine Learning — Unsupervised Learning

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 20.1 Clustering

- [ ] **K-Means Clustering**
  - Algorithm: Initialize k centroids → Assign points → Update centroids → Repeat
  - Loss: Within-cluster sum of squares (WCSS / inertia)
  - Choosing k: Elbow method, Silhouette score
  - Limitations: Assumes spherical clusters, sensitive to initialization (use K-means++)
  - Time complexity: O(n × k × d × iterations)

- [ ] **Hierarchical Clustering**
  - Agglomerative (bottom-up): Start with each point as cluster, merge closest
  - Divisive (top-down): Start with one cluster, split
  - Linkage: single (min), complete (max), average, Ward's
  - Dendrogram for visualization
  - No need to specify k upfront

- [ ] **DBSCAN (Density-Based)**
  - Parameters: ε (neighborhood radius), minPts (minimum points)
  - Core points, border points, noise points
  - Can find arbitrary-shaped clusters
  - Robust to outliers
  - No need to specify k

- [ ] **Gaussian Mixture Models (GMM)**
  - Soft clustering: probabilistic assignment
  - Each cluster = Gaussian distribution (mean, covariance)
  - **Expectation-Maximization (EM)** algorithm:
    - E-step: Compute responsibilities (soft assignments)
    - M-step: Update parameters (mean, covariance, weights)
  - Model selection: BIC, AIC

## 20.2 Dimensionality Reduction

- [ ] **PCA (Principal Component Analysis)** — Also covered in Section 18.1
  - Linear, unsupervised
  - Steps: Standardize → Covariance matrix → Eigen decomposition → Project
  - Explained variance ratio for choosing components

- [ ] **t-SNE (t-distributed Stochastic Neighbor Embedding)**
  - Non-linear, for visualization (2D/3D)
  - Preserves local structure
  - Perplexity parameter
  - Not suitable for new data projection

- [ ] **UMAP (Uniform Manifold Approximation and Projection)**
  - Faster than t-SNE, preserves global structure better
  - Good for both visualization and downstream ML tasks

- [ ] **LDA (Linear Discriminant Analysis)**
  - Supervised dimensionality reduction
  - Maximizes between-class, minimizes within-class variance

## 20.3 Association Rule Mining

- [ ] **Key Concepts**
  - Support: $\frac{\text{transactions containing X}}{total transactions}$
  - Confidence: $\frac{support(X \cup Y)}{support(X)}$
  - Lift: $\frac{confidence(X \to Y)}{support(Y)}$ (lift > 1 → positive association)

- [ ] **Algorithms**
  - **Apriori**: Level-wise candidate generation, anti-monotone property
  - **FP-Growth**: FP-tree construction, no candidate generation, faster

## 20.4 Anomaly Detection

- [ ] **Statistical Methods**: Z-score, IQR-based
- [ ] **Isolation Forest**: Random partitioning, anomalies isolated quickly
- [ ] **One-Class SVM**: Learns boundary of normal data
- [ ] **Autoencoders**: High reconstruction error → anomaly

---

### Recommended Resources
- **Book**: *Hands-On Machine Learning* — Géron (Part I, unsupervised chapters)
- **Book**: *Data Mining: Concepts and Techniques* — Jiawei Han

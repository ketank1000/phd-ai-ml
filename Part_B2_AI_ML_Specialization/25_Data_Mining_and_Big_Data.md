# 25. Data Mining & Big Data

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 25.1 Data Mining — Overview

**Data Mining:** Extracting useful patterns, correlations, and knowledge from large datasets.

### 25.1.1 KDD Process (Knowledge Discovery in Databases)

```
Raw Data → Selection → Preprocessing → Transformation → Data Mining → Evaluation → Knowledge
```

| Step | Description | Example |
|------|-------------|---------|
| **1. Selection** | Choose relevant data from databases | Select customer purchase records |
| **2. Preprocessing** | Clean data (handle missing values, outliers, noise) | Remove duplicates, fix errors |
| **3. Transformation** | Normalize, aggregate, create features | Feature engineering, scaling |
| **4. Data Mining** | Apply algorithms to find patterns | Clustering, classification, association |
| **5. Evaluation** | Assess discovered patterns for validity and usefulness | Statistical significance, domain relevance |
| **6. Knowledge Presentation** | Visualize and communicate findings | Dashboards, reports |

### 25.1.2 Data Preprocessing (Critical for ML Success)

**"Garbage in, garbage out"** — preprocessing often determines model success more than algorithm choice.

#### Missing Values

| Method | How It Works | When To Use |
|--------|-------------|-------------|
| **Deletion (listwise)** | Remove rows with missing values | Few missing values, MCAR (Missing Completely At Random) |
| **Mean/Median imputation** | Replace with column mean or median | Numerical, few missing, no strong relationships |
| **Mode imputation** | Replace with most frequent value | Categorical features |
| **KNN imputation** | Use K nearest neighbors to estimate | Preserves relationships, moderate missing % |
| **Regression imputation** | Predict missing value using other features | Strong feature correlations |
| **MICE** (Multiple Imputation) | Iterative imputation using all features | Best for complex missing patterns |
| **Indicator variable** | Add binary column indicating "was missing" | Missingness itself may be informative |

#### Feature Scaling

| Method | Formula | Range | When To Use |
|--------|---------|-------|-------------|
| **Min-Max** | $\frac{x - x_{min}}{x_{max} - x_{min}}$ | [0, 1] | Fixed bounds needed (neural networks, images) |
| **Z-score (Standardization)** | $\frac{x - \mu}{\sigma}$ | ~[-3, 3] | Assumes normal distribution, no fixed bounds (SVM, PCA) |
| **Robust Scaling** | $\frac{x - \text{median}}{\text{IQR}}$ | Varies | Data with outliers |
| **Log transform** | $\log(x+1)$ | Varies | Right-skewed data (income, counts) |

#### Feature Encoding

| Method | Description | Use Case |
|--------|-------------|----------|
| **One-Hot Encoding** | Binary column per category | Nominal categories (<15 unique values) |
| **Label Encoding** | Assign integer per category | Ordinal categories (low/medium/high) |
| **Target Encoding** | Replace category with mean of target | High-cardinality features |
| **Binary Encoding** | Encode as binary digits | Moderate cardinality |

### 25.1.3 Feature Selection

Reduce dimensionality by selecting the most informative features:

| Approach | Methods | How It Works |
|----------|---------|-------------|
| **Filter** | Correlation, Chi-square, Mutual Information, Variance threshold | Score features independently, rank and select top-k |
| **Wrapper** | Forward selection, Backward elimination, Recursive Feature Elimination (RFE) | Train model with feature subsets, evaluate performance |
| **Embedded** | Lasso (L1), Tree-based importance, ElasticNet | Feature selection built into the learning algorithm |

**Filter vs. Wrapper vs. Embedded:**
- **Filter:** Fast, model-agnostic, but ignores feature interactions
- **Wrapper:** Considers interactions, but slow (train model many times)
- **Embedded:** Best of both worlds — considers interactions, efficient (done during training)

### 25.1.4 Data Mining Tasks Summary

| Task | Type | Goal | Algorithms |
|------|------|------|------------|
| **Classification** | Supervised | Predict discrete label | Decision Tree, SVM, Neural Network |
| **Regression** | Supervised | Predict continuous value | Linear Regression, Random Forest |
| **Clustering** | Unsupervised | Group similar items | K-Means, DBSCAN, Hierarchical |
| **Association Rules** | Unsupervised | Find co-occurrence patterns | Apriori, FP-Growth |
| **Anomaly Detection** | Semi/Unsupervised | Find outliers | Isolation Forest, LOF |
| **Sequential Pattern Mining** | Unsupervised | Find patterns in ordered data | GSP, PrefixSpan |

---

## 25.2 Big Data

### 25.2.1 The 5 V's of Big Data

| V | Description | Example |
|---|-------------|---------|
| **Volume** | Massive amounts of data | Petabytes of social media data |
| **Velocity** | Speed of data generation and processing | Real-time stock trading, IoT sensor streams |
| **Variety** | Different data types and formats | Structured (SQL), semi-structured (JSON), unstructured (images, text) |
| **Veracity** | Quality and trustworthiness of data | Noisy sensor data, fake reviews |
| **Value** | Business/research value extracted from data | Actionable insights, predictions |

### 25.2.2 Hadoop Ecosystem

**Hadoop:** Open-source framework for distributed storage and processing of big data.

```
  ┌─────────────────────────────────────────────┐
  │                Applications                  │
  │  Hive (SQL) │ Pig (scripting) │ HBase (NoSQL)│
  ├─────────────────────────────────────────────┤
  │           YARN (Resource Manager)            │
  ├─────────────────────────────────────────────┤
  │           MapReduce (Processing)             │
  ├─────────────────────────────────────────────┤
  │           HDFS (Storage)                     │
  └─────────────────────────────────────────────┘
```

| Component | Role | Key Feature |
|-----------|------|-------------|
| **HDFS** | Distributed File System | Splits files into 128MB blocks, 3× replication |
| **MapReduce** | Distributed computation | Map (transform) → Shuffle (group) → Reduce (aggregate) |
| **YARN** | Resource management | Allocates CPU/memory across cluster |
| **Hive** | SQL-like queries on Hadoop | HiveQL → MapReduce jobs |
| **HBase** | NoSQL column-family database on HDFS | Real-time read/write |
| **ZooKeeper** | Coordination service | Leader election, configuration management |

### MapReduce — Detailed Example

**Task:** Count word frequencies in a large text corpus.

```
Input: "hello world hello"  "world hello world"

MAP Phase (parallel on each machine):
  Mapper 1: "hello world hello"
    → (hello, 1), (world, 1), (hello, 1)
  
  Mapper 2: "world hello world"
    → (world, 1), (hello, 1), (world, 1)

SHUFFLE Phase (group by key):
  hello → [1, 1, 1]
  world → [1, 1, 1]

REDUCE Phase (aggregate):
  Reducer: hello → 3
  Reducer: world → 3

Output: {hello: 3, world: 3}
```

**Limitations of MapReduce:** Writes intermediate results to disk → slow for iterative algorithms (ML needs many iterations). This motivated **Apache Spark**.

### 25.2.3 Apache Spark

**In-memory distributed computing framework — up to 100× faster than MapReduce for iterative jobs.**

| Component | Description |
|-----------|-------------|
| **Spark Core** | RDDs (Resilient Distributed Datasets) — immutable, distributed collections |
| **Spark SQL** | Structured data processing with DataFrames (like Pandas but distributed) |
| **Spark Streaming** | Near-real-time stream processing (micro-batches) |
| **MLlib** | Machine learning library (classification, regression, clustering, collaborative filtering) |
| **GraphX** | Graph processing (PageRank, connected components) |

**RDD (Resilient Distributed Dataset):**
- **Immutable:** Once created, cannot be modified
- **Distributed:** Partitioned across cluster nodes
- **Fault-tolerant:** Can be recomputed from lineage (transformation history)
- **Lazy evaluation:** Transformations are not executed until an action is called

**Transformations vs. Actions:**

| Transformations (lazy) | Actions (trigger execution) |
|------------------------|---------------------------|
| `map()`, `filter()`, `flatMap()` | `count()`, `collect()`, `reduce()` |
| `groupByKey()`, `join()` | `first()`, `take(n)`, `saveAsTextFile()` |

**DataFrame:** Distributed table with named columns (like a distributed Pandas DataFrame). Supports SQL queries and optimized by Catalyst query optimizer.

```python
# Spark DataFrame example
df = spark.read.csv("data.csv", header=True)
result = df.filter(df.age > 25).groupBy("department").count()
result.show()
```

### Hadoop vs. Spark Comparison

| Feature | Hadoop MapReduce | Apache Spark |
|---------|-----------------|--------------|
| **Processing** | Disk-based | In-memory |
| **Speed** | Slower (disk I/O) | Up to 100× faster |
| **Ease of use** | Verbose Java code | Concise (Python, Scala, R) |
| **Iterative algorithms** | Poor (disk writes between iterations) | Excellent (data in memory) |
| **Real-time** | No (batch only) | Yes (Spark Streaming) |
| **ML support** | Mahout (limited) | MLlib (rich) |

### 25.2.4 Stream Processing

| Technology | Type | Key Feature |
|-----------|------|-------------|
| **Apache Kafka** | Distributed messaging/streaming platform | Pub/sub, durable log, high throughput |
| **Apache Flink** | Stream processing engine | True event-time processing, exactly-once semantics |
| **Spark Streaming** | Micro-batch stream processing | Integrates with Spark ecosystem |

**Window operations:**

| Window Type | Description | Example |
|------------|-------------|---------|
| **Tumbling** | Fixed-size, non-overlapping | Count events every 5 minutes |
| **Sliding** | Fixed-size, overlapping | Average over last 10 min, computed every 1 min |
| **Session** | Dynamic, activity-based | Group events within idle gaps |

---

## 25.3 Data Warehousing

| Concept | Description |
|---------|-------------|
| **Data Warehouse** | Central repository of integrated data from multiple sources, optimized for analysis |
| **ETL** | Extract → Transform → Load pipeline |
| **OLAP** | Online Analytical Processing — multi-dimensional data analysis |
| **OLTP** | Online Transaction Processing — day-to-day operations |
| **Star Schema** | Fact table (metrics) surrounded by dimension tables (attributes) |
| **Snowflake Schema** | Normalized star schema (dimension tables have sub-dimensions) |

**OLTP vs. OLAP:**

| Feature | OLTP | OLAP |
|---------|------|------|
| **Purpose** | Day-to-day transactions | Analysis and reporting |
| **Queries** | Simple, short | Complex, long (aggregations) |
| **Data** | Current, detailed | Historical, summarized |
| **Schema** | Normalized (3NF) | Star/Snowflake |
| **Example** | Banking transaction | Sales trend analysis |

---

## 25.4 Practice Questions

**Q1.** Explain the KDD process. Why is data preprocessing the most time-consuming step?
> **Answer:** KDD (Knowledge Discovery in Databases) has six steps: Selection → Preprocessing → Transformation → Mining → Evaluation → Presentation. **Preprocessing is most time-consuming** (typically 60-80% of project time) because: (1) Real-world data is messy — missing values, inconsistencies, duplicates, errors; (2) Different data sources have different formats, scales, and codes that need integration; (3) Outlier detection and treatment requires domain knowledge; (4) Feature engineering (creating useful features) is iterative and creative; (5) Data quality directly determines model quality — no algorithm can compensate for bad data. "Data scientists spend 80% of their time on data preparation."

**Q2.** Compare MapReduce and Spark for iterative machine learning algorithms.
> **Answer:** **MapReduce** writes intermediate results to HDFS disk after each Map-Reduce step. For iterative ML (e.g., gradient descent with 100 epochs), each epoch requires reading from and writing to disk — extremely slow. **Spark** keeps data in memory (RDDs/DataFrames) across iterations — data is read from disk once, then subsequent iterations operate on cached in-memory data. This makes Spark **10-100× faster** for ML tasks. Spark's MLlib provides built-in ML algorithms (gradient descent, k-means, ALS) optimized for distributed in-memory computation. Additionally, Spark supports lazy evaluation and DAG optimization (Catalyst), further reducing unnecessary computation.

**Q3.** What is the difference between filter, wrapper, and embedded feature selection methods?
> **Answer:** **Filter methods** (correlation, chi-square, mutual information) score features independently of the model — fast but miss feature interactions. **Wrapper methods** (forward selection, backward elimination, RFE) train the model with different feature subsets and select based on performance — considers interactions but computationally expensive ($O(2^n)$ subsets theoretically). **Embedded methods** (Lasso L1, tree feature importance) perform feature selection during model training — efficient and considers interactions. **Example:** For 100 features, filter takes minutes (compute 100 scores), wrapper takes hours (train model many times), embedded is part of normal training. **Best practice:** Use filter for initial screening (remove obviously irrelevant), then embedded for final selection.

**Q4.** Explain the 5 V's of Big Data with examples from AI/ML.
> **Answer:** (1) **Volume:** ImageNet has 14M images; GPT-3 trained on 570GB of text. ML needs massive data for generalization. (2) **Velocity:** Self-driving cars process sensor data in real-time (LiDAR, cameras, radar). Real-time fraud detection processes millions of transactions per second. (3) **Variety:** Multimodal AI combines text, images, audio, video. Healthcare ML uses structured records, unstructured doctor notes, image scans. (4) **Veracity:** Noisy labels in crowdsourced datasets (Amazon Mechanical Turk), adversarial examples. Data quality directly impacts model reliability. (5) **Value:** The entire point — ML extracts predictions and insights from raw data, creating value (disease diagnosis, recommendation systems, autonomous driving).

**Q5.** What is lazy evaluation in Spark? Why is it important for performance?
> **Answer:** **Lazy evaluation** means transformations (map, filter, groupBy) are not executed immediately — Spark just records the computation plan (a DAG of operations). Computation only happens when an **action** (count, collect, save) is called. **Why important:** (1) **Optimization:** Spark's Catalyst optimizer can analyze the entire DAG and find efficiencies — e.g., combine consecutive filters, push predicates down to the data source, eliminate unnecessary columns early. (2) **Efficiency:** If you filter → map → filter → count, Spark can fuse these into a single pass over the data instead of 4 passes. (3) **Memory:** Intermediate results don't need to be materialized unless necessary. (4) **Fault tolerance:** The DAG serves as a "recipe" — if a partition is lost, only that partition needs recomputation.

---

*Previous: [Chapter 24 — Reinforcement Learning](24_Reinforcement_Learning.md) | Next: [Chapter 26 — Ethical AI & Emerging Topics](26_Ethical_AI_and_Emerging_Topics.md)*

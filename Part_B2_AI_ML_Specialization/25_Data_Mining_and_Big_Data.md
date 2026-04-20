# 25. Data Mining & Big Data

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 25.1 Data Mining

- [ ] **KDD Process** (Knowledge Discovery in Databases)
  1. Data selection
  2. Data preprocessing (cleaning, integration, transformation)
  3. Data mining (pattern extraction)
  4. Pattern evaluation
  5. Knowledge presentation

- [ ] **Data Preprocessing**
  - Missing values: deletion, mean/median imputation, KNN imputation
  - Outlier detection and treatment
  - Feature scaling: min-max normalization, z-score standardization
  - Feature encoding: one-hot, label encoding, target encoding

- [ ] **Feature Selection**
  - Filter methods: correlation, chi-square, mutual information
  - Wrapper methods: forward selection, backward elimination, recursive feature elimination
  - Embedded methods: Lasso, decision tree feature importance

- [ ] **Data Mining Tasks**
  - Classification (supervised)
  - Clustering (unsupervised)
  - Regression (supervised)
  - Association rule mining
  - Anomaly detection
  - Sequential pattern mining

## 25.2 Big Data (Conceptual)

- [ ] **Characteristics of Big Data (5 V's)**
  - Volume, Velocity, Variety, Veracity, Value

- [ ] **Hadoop Ecosystem**
  - HDFS: Distributed file system
  - MapReduce: Programming model (Map → Shuffle → Reduce)
  - YARN: Resource management
  - Hive: SQL-like queries on Hadoop
  - HBase: NoSQL database on HDFS

- [ ] **Apache Spark**
  - In-memory processing (faster than MapReduce)
  - RDDs (Resilient Distributed Datasets)
  - Spark SQL, Spark Streaming, MLlib, GraphX
  - DataFrames, lazy evaluation

- [ ] **Stream Processing**
  - Apache Kafka: Distributed streaming platform
  - Apache Flink: Real-time stream processing
  - Window operations: tumbling, sliding, session

---

### Recommended Resources
- **Book**: *Data Mining: Concepts and Techniques* — Jiawei Han
- **Book**: *Mining of Massive Datasets* — Leskovec, Rajaraman, Ullman (free online)

# 4. Sampling Techniques

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 4.1 Key Concepts: Population, Sample, and Sampling

### Population
The **entire group** of individuals, items, or data points that you want to study and draw conclusions about.

> *Example:* "All software engineers in India" or "All images in the ImageNet database" or "All academic papers on NLP published between 2020-2025."

### Sample
A **subset** of the population that is actually studied. We use samples because studying the entire population is usually impractical, too expensive, or too time-consuming.

> *Example:* "500 software engineers from Pune, Bangalore, and Hyderabad" surveyed out of millions nationwide.

### Sampling Frame
A **list or database** of all members of the population from which the sample is drawn.

> *Example:* LinkedIn profiles of software engineers in India, or the list of all papers in IEEE Xplore matching your search query.

### Why Sampling?

| Reason | Explanation |
|--------|-------------|
| **Cost** | Studying millions of people/records is expensive |
| **Time** | Collecting data from everyone takes too long |
| **Practicality** | The population may be infinite or inaccessible |
| **Accuracy** | A well-designed sample can be MORE accurate than a poorly conducted census (fewer errors in data collection) |
| **Feasibility** | Destructive testing (crash-testing cars, testing batteries to failure) requires sampling |

### Key Terms

| Term | Definition |
|------|-----------|
| **Sampling unit** | The individual element or unit being sampled (a person, a record, a data point) |
| **Sampling error** | The difference between the sample statistic and the true population parameter — exists even in well-designed samples |
| **Non-sampling error** | Errors from other sources: measurement error, non-response bias, data entry errors |
| **Census** | Studying the ENTIRE population (100% sample) |

---

## 4.2 Probability Sampling

In probability sampling, every member of the population has a **known, non-zero probability** of being selected. This allows statistical inference — you can generalize findings from sample to population.

### 4.2.1 Simple Random Sampling (SRS)

**How it works:** Every member of the population has an **equal chance** of being selected. Selection is completely random.

**Methods:**
- Lottery method (put all names in a hat, draw blindly)
- Random number table
- Computer-generated random numbers (Python: `random.sample()`)

**Example:**
> Population: 10,000 GitHub repositories using Python ML libraries.
> Sample: Randomly select 500 using `random.sample(repo_list, 500)`.
> Each repo has a 500/10,000 = 5% chance of selection.

**Advantages:**
- Simple to understand and implement
- No bias in selection
- Statistical calculations are straightforward

**Disadvantages:**
- Requires a **complete list** (sampling frame) of the population — often unavailable
- May not represent subgroups proportionally (by random chance, you might get 90% NLP repos and only 10% computer vision repos)
- Impractical for very large or geographically spread populations

### 4.2.2 Stratified Random Sampling

**How it works:** 
1. Divide the population into **strata** (homogeneous subgroups) based on a characteristic
2. Randomly sample from EACH stratum

**Why?** Ensures that important subgroups are adequately represented.

**Example:**
> You want to survey AI researchers in India. The population includes:
> - 60% from academia, 30% from industry, 10% from government labs
> 
> **Without stratification:** Random sampling might give you 85% academia and 5% government (by chance).
> **With stratification:**
> - Stratum 1 (Academia): Randomly select 60 researchers
> - Stratum 2 (Industry): Randomly select 30 researchers
> - Stratum 3 (Government): Randomly select 10 researchers
> - Total sample: 100 — proportional to population

**Types of allocation:**

| Type | How samples are distributed | When to use |
|------|---------------------------|-------------|
| **Proportional** | Each stratum gets sample proportional to its population size | Default choice |
| **Equal** | Same sample size from each stratum regardless of size | When each subgroup is equally important |
| **Disproportional** | More samples from smaller/more variable strata | When smaller groups need adequate representation |

**Advantages:**
- Ensures representation of all important subgroups
- Lower sampling error than SRS (more precise)
- Allows separate analysis of each stratum

**Disadvantages:**
- Requires knowledge of the population to create strata
- More complex to implement
- Strata must be clearly defined

### 4.2.3 Cluster Sampling

**How it works:**
1. Divide the population into **clusters** (usually geographic or organizational groups)
2. Randomly select some clusters
3. Study ALL members within the selected clusters (or sample within them)

**Key difference from stratified:** In stratified, strata are **homogeneous** (similar within, different between). In cluster, clusters are **heterogeneous** (each cluster mirrors the whole population).

**Example:**
> You want to study AI adoption in Indian colleges.
> - Population: All engineering colleges in India (≈6,000)
> - It's impractical to visit all 6,000
>
> **Cluster Sampling:**
> - Clusters = colleges (each college has diverse departments, students, etc.)
> - Randomly select 30 colleges
> - Survey all CS/IT department faculty in those 30 colleges

**Multi-stage Cluster Sampling:**
```
Stage 1: Randomly select 5 states from 28 states
Stage 2: Randomly select 3 cities from each selected state
Stage 3: Randomly select 2 colleges from each selected city
Stage 4: Survey all CS faculty in selected colleges

Total: 5 × 3 × 2 = 30 colleges
```

**Advantages:**
- Cost-effective (no need to travel everywhere)
- Does NOT require a complete list of all individuals — just a list of clusters
- Practical for large, geographically spread populations

**Disadvantages:**
- Higher sampling error than SRS or stratified (clusters may not perfectly represent population)
- Members within a cluster may be more similar to each other than to the overall population

### 4.2.4 Systematic Sampling

**How it works:**
1. Calculate the sampling interval: $k = N/n$ (population size / desired sample size)
2. Randomly choose a starting point between 1 and k
3. Select every k-th element after that

**Example:**
> Population: 10,000 customer reviews in a database
> Desired sample: 200 reviews
> k = 10,000 / 200 = 50
> Random start: 23
> Select: review #23, #73, #123, #173, #223, ... (every 50th)

**Advantages:**
- Very easy to implement
- Spreads the sample evenly across the population
- No need for random number tables

**Disadvantages:**
- If there's a **periodic pattern** in the list that matches the interval k, the sample will be biased
  > *Example:* If every 50th review is from the same product category because of how the database is ordered

### Comparison of Probability Sampling Methods

| Method | Best For | Requires Population List? | Precision | Cost |
|--------|---------|--------------------------|-----------|------|
| **Simple Random** | Small, accessible populations | Yes (complete) | Good | Medium |
| **Stratified** | Populations with important subgroups | Yes (with strata info) | Best | Medium-High |
| **Cluster** | Large, geographically spread populations | No (just list clusters) | Lower | Low |
| **Systematic** | Ordered lists/databases | Yes (ordered list) | Good | Low |

---

## 4.3 Non-Probability Sampling

In non-probability sampling, members do NOT have a known probability of selection. Selection is based on convenience, judgment, or other non-random criteria. **Cannot statistically generalize** to the population.

### 4.3.1 Convenience Sampling

**How it works:** Select whoever is most easily accessible or available.

**Example:**
> A researcher surveys 100 computer science students from their own university about AI tool preferences — because they're conveniently accessible.

**Advantages:** Quick, easy, inexpensive
**Disadvantages:** Highly biased. Students from one university don't represent all CS students. Results may not generalize.

**When acceptable:** Pilot studies, preliminary research, when the population is truly hard to access.

### 4.3.2 Purposive (Judgmental) Sampling

**How it works:** The researcher deliberately selects participants based on their judgment of who would be most informative for the study.

**Example:**
> Studying the challenges of deploying large language models in Indian enterprises. You specifically select:
> - 5 CTOs from companies that have deployed LLMs
> - 5 ML engineers who implemented the deployments
> - 5 domain experts who define use cases
>
> You choose THESE specific people because they have the knowledge you need.

**Advantages:** Targets the most relevant participants
**Disadvantages:** Subject to researcher bias; others might select different "experts"

### 4.3.3 Snowball Sampling

**How it works:** Start with a few known participants; they refer you to other participants, who refer you to more, and so on (like a snowball getting bigger).

```
Initial contact (Participant 1)
    ├──→ Referred to Participant 2
    │         ├──→ Referred to Participant 5
    │         └──→ Referred to Participant 6
    └──→ Referred to Participant 3
              └──→ Referred to Participant 7
```

**Example:**
> You want to interview researchers working on adversarial attacks (a niche area). You start with one known researcher, who introduces you to colleagues in the same area, who introduce you to more.

**Advantages:** Excellent for hard-to-reach or hidden populations
**Disadvantages:** Biased toward well-connected individuals; early participants shape the entire sample

### 4.3.4 Quota Sampling

**How it works:** Similar to stratified sampling in structure, but selection within each category is **non-random** (based on convenience or judgment).

**Example:**
> You want to survey 100 developers: 50 male, 50 female (quota). You approach developers at a tech conference and keep interviewing until you fill each quota. The selection within each quota is NOT random.

**Advantages:** Ensures proportional representation without needing a sampling frame
**Disadvantages:** Selection within quotas is non-random → still biased

### Comparison of Non-Probability Methods

| Method | Best For | Bias Level |
|--------|---------|-----------|
| **Convenience** | Quick pilot studies | Very High |
| **Purposive** | Expert opinions, specific knowledge needed | Medium-High |
| **Snowball** | Hidden or hard-to-reach populations | Medium-High |
| **Quota** | Ensuring representation without a full list | Medium |

---

## 4.4 Sample Size Determination

### Why Sample Size Matters

| Too Small | Too Large |
|-----------|-----------|
| Results unreliable, high sampling error | Unnecessary cost and time |
| May miss real effects (low statistical power) | Diminishing returns in precision |
| Hard to generalize | May detect trivially small effects |

### Factors Affecting Sample Size

1. **Confidence Level** — How sure do you want to be? (usually 95%, corresponding to Z = 1.96)
2. **Margin of Error (e)** — How much error are you willing to accept? (usually 5%)
3. **Population Variability (p)** — How much do values vary? (if unknown, use p = 0.5 for maximum variability)
4. **Population Size (N)** — Matters only for small populations

### Formula for Sample Size (Proportions)

For large (or infinite) populations:

$$n = \frac{Z^2 \cdot p \cdot (1-p)}{e^2}$$

Where:
- $n$ = required sample size
- $Z$ = Z-score for desired confidence level
- $p$ = estimated proportion (use 0.5 if unknown)
- $e$ = margin of error (as decimal)

| Confidence Level | Z-score |
|-----------------|---------|
| 90% | 1.645 |
| 95% | 1.96 |
| 99% | 2.576 |

### Worked Example:

> **Problem:** You want to survey Indian developers about AI tool usage. You want 95% confidence with a ±5% margin of error. You don't know the proportion who use AI tools, so use p = 0.5.
>
> $$n = \frac{(1.96)^2 \times 0.5 \times 0.5}{(0.05)^2} = \frac{3.8416 \times 0.25}{0.0025} = \frac{0.9604}{0.0025} = 384.16$$
>
> **Answer:** You need at least **385 respondents**.

### Finite Population Correction

If the population is small (say, N = 2,000), apply the correction:

$$n_{adjusted} = \frac{n}{1 + \frac{n-1}{N}} = \frac{385}{1 + \frac{384}{2000}} = \frac{385}{1.192} = 323$$

### Rules of Thumb for Sample Size

| Research Type | Minimum Sample Size |
|--------------|-------------------|
| Surveys | 384 (for 95% confidence, 5% margin) |
| Experiments (comparing 2 groups) | At least 30 per group |
| Correlational studies | At least 50, preferably 100+ |
| Qualitative research | 15–30 for interviews, until "saturation" |
| Machine Learning experiments | Not a "people" sample — but use K-fold CV, multiple random seeds (min. 5 runs) |

---

## 4.5 Sampling in Machine Learning Context

In ML research, "sampling" has additional meanings:

### Train-Test Split
- **Training set** (70-80%): Used to train the model
- **Validation set** (10-15%): Used to tune hyperparameters
- **Test set** (10-15%): Used ONCE for final evaluation

### K-Fold Cross-Validation
A form of repeated sampling:
1. Split data into k folds (e.g., k=5)
2. Train on k-1 folds, test on 1 fold
3. Repeat k times, rotating the test fold
4. Report mean ± standard deviation of performance

### Stratified Sampling in ML
When classes are imbalanced (e.g., 95% non-fraud, 5% fraud):
- **Stratified split** ensures both train and test sets maintain the 95/5 ratio
- Python: `train_test_split(X, y, stratify=y)`

### Bootstrapping
Sampling **with replacement** from the dataset:
- Used in bagging (Random Forest)
- Used for confidence interval estimation
- Each bootstrap sample may contain duplicates

---

## 4.6 Practice Questions

**Q1.** A researcher wants to study the work-life balance of IT professionals across India. The population includes professionals in Tier-1 cities (60%), Tier-2 cities (30%), and rural areas (10%). Which sampling method best ensures representation of all three groups?
> **Answer:** Stratified random sampling. Create three strata (Tier-1, Tier-2, Rural) and randomly sample from each, proportional to their population share.

**Q2.** Calculate the required sample size for a survey with 99% confidence level and ±3% margin of error (p = 0.5).
> **Answer:** $n = \frac{(2.576)^2 \times 0.5 \times 0.5}{(0.03)^2} = \frac{6.635 \times 0.25}{0.0009} = \frac{1.659}{0.0009} = 1,843.3$ → **1,844 respondents**

**Q3.** A researcher wants to interview cybersecurity experts who work on zero-day exploits (a highly secretive and niche group). Which sampling technique is most appropriate?
> **Answer:** Snowball sampling. This niche group is hard to reach through a formal list. Starting with one known expert and getting referrals is the most practical approach.

**Q4.** What is the difference between stratified sampling and cluster sampling?
> **Answer:** In **stratified sampling**, the population is divided into homogeneous subgroups (strata), and random samples are drawn from EVERY stratum. In **cluster sampling**, the population is divided into heterogeneous clusters, and ENTIRE clusters are randomly selected. Stratified goes "wide" across all groups; clustering goes "deep" into selected groups.

**Q5.** Why can't you generalize findings from a convenience sample to the entire population?
> **Answer:** Because participants were not randomly selected — they were chosen based on accessibility. The sample may not represent the population (e.g., surveying only students from one college doesn't represent all students in India). Without random selection, there's no statistical basis for generalization.

---

*Previous: [Chapter 3 — Research Design](03_Research_Design.md) | Next: [Chapter 5 — Data Collection Methods](05_Data_Collection_Methods.md)*

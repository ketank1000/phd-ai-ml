# 6. Statistical Analysis

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 6.1 Descriptive Statistics

Descriptive statistics **summarize** and **describe** the main features of a dataset. They do NOT make inferences about the population — they just describe what you have.

### 6.1.1 Measures of Central Tendency

These answer: "What is the typical/central value?"

**Mean (Arithmetic Average)**

$$\bar{x} = \frac{\sum_{i=1}^{n} x_i}{n} = \frac{x_1 + x_2 + ... + x_n}{n}$$

**Example:** Test scores: 72, 85, 90, 68, 95 → Mean = (72+85+90+68+95)/5 = 410/5 = **82**

**Properties:**
- Uses ALL data points → sensitive to outliers
- If one student scored 200 (data entry error), the mean shoots up to 104
- Best for: symmetric, interval/ratio data without outliers

**Median (Middle Value)**

1. Arrange data in order
2. If n is odd: the middle value
3. If n is even: average of the two middle values

**Example:** Scores: 68, 72, 85, 90, 95 → Median = **85** (middle value)
**Even count:** 68, 72, 85, 90 → Median = (72+85)/2 = **78.5**

**Properties:**
- NOT affected by outliers → robust measure
- Best for: skewed data, ordinal data
- Cannot be distorted by extreme values

**Mode (Most Frequent Value)**

**Example:** Scores: 72, 85, 85, 90, 95 → Mode = **85** (appears twice)
- A dataset can have no mode, one mode (unimodal), or multiple modes (bimodal, multimodal)
- Best for: nominal data, identifying the most common category

### When to Use Which?

| Situation | Best Measure | Why |
|-----------|-------------|-----|
| Symmetric data, no outliers | Mean | Uses all data, most precise |
| Skewed data or outliers | Median | Not affected by extreme values |
| Categorical data | Mode | Only measure that works for categories |
| Income data | Median | Income distributions are heavily right-skewed |

**Relationship in Skewed Distributions:**
```
Left-skewed:     Mean < Median < Mode
Symmetric:       Mean ≈ Median ≈ Mode  
Right-skewed:    Mode < Median < Mean

Left-skewed              Symmetric              Right-skewed
    ╱╲                     ╱╲                      ╱╲
   ╱  ╲                  ╱    ╲                   ╱  ╲
  ╱    ╲                ╱      ╲                 ╱    ╲╲
╱╱      ╲              ╱        ╲               ╱      ╲╲╲
```

### 6.1.2 Measures of Dispersion (Spread)

These answer: "How spread out is the data?"

**Range**
$$Range = Maximum - Minimum$$

**Example:** Scores: 68, 72, 85, 90, 95 → Range = 95 - 68 = 27

Problem: Only considers two extreme values. Very sensitive to outliers.

**Variance**

Population variance:
$$\sigma^2 = \frac{\sum_{i=1}^{N} (x_i - \mu)^2}{N}$$

Sample variance (Bessel's correction — divides by n-1 for unbiased estimate):
$$s^2 = \frac{\sum_{i=1}^{n} (x_i - \bar{x})^2}{n - 1}$$

**Worked Example:**
> Data: 4, 8, 6, 5, 7 → Mean = 30/5 = 6
> 
> | $x_i$ | $x_i - \bar{x}$ | $(x_i - \bar{x})^2$ |
> |-------|-----------------|---------------------|
> | 4 | -2 | 4 |
> | 8 | +2 | 4 |
> | 6 | 0 | 0 |
> | 5 | -1 | 1 |
> | 7 | +1 | 1 |
> | **Sum** | **0** | **10** |
> 
> Sample variance: $s^2 = 10/(5-1) = 10/4 = 2.5$

**Standard Deviation**
$$s = \sqrt{s^2} = \sqrt{2.5} = 1.58$$

**Why SD instead of variance?** SD is in the SAME UNITS as the original data (e.g., marks), while variance is in squared units (marks²).

**Interquartile Range (IQR)**
$$IQR = Q3 - Q1$$

Where Q1 = 25th percentile, Q3 = 75th percentile.

**Why useful?** Like the median, IQR is resistant to outliers. It captures the spread of the middle 50% of data.

**Coefficient of Variation (CV)**
$$CV = \frac{s}{\bar{x}} \times 100\%$$

**Why useful?** Allows comparing variability of datasets with different units or scales.

> *Example:* Heights (mean=170cm, SD=10cm) vs. Weights (mean=70kg, SD=8kg)
> - CV(height) = 10/170 × 100 = 5.9%
> - CV(weight) = 8/70 × 100 = 11.4%
> - Weights are relatively more variable

### 6.1.3 Measures of Shape

**Skewness** — measures asymmetry

| Type | Skewness Value | Tail | Mean vs Median |
|------|---------------|------|---------------|
| **Positive (right) skew** | > 0 | Long right tail | Mean > Median |
| **Symmetric** | ≈ 0 | Equal tails | Mean ≈ Median |
| **Negative (left) skew** | < 0 | Long left tail | Mean < Median |

> *AI/ML Example:* In an image classification task, the distribution of class sizes is often right-skewed (a few classes have thousands of examples, most have fewer).

**Kurtosis** — measures "tailedness" (how heavy the tails are)

| Type | Kurtosis | Shape | Real-World Example |
|------|----------|-------|-------------------|
| **Mesokurtic** | = 3 (or excess = 0) | Normal distribution tails | Height of adult males |
| **Leptokurtic** | > 3 | Heavy tails, more outliers | Stock market returns, financial data |
| **Platykurtic** | < 3 | Light tails, fewer outliers | Uniform-like distributions |

---

## 6.2 Probability Distributions

### 6.2.1 Normal Distribution (Gaussian)

The most important distribution in statistics. Bell-shaped, symmetric, defined by mean ($\mu$) and standard deviation ($\sigma$).

$$f(x) = \frac{1}{\sigma\sqrt{2\pi}} e^{-\frac{(x-\mu)^2}{2\sigma^2}}$$

**The 68-95-99.7 Rule (Empirical Rule):**

```
         99.7% (within ±3σ)
       ┌─────────────────────┐
       │  95% (within ±2σ)   │
       │ ┌─────────────────┐ │
       │ │ 68% (within ±1σ)│ │
       │ │    ┌───────┐    │ │
       │ │    │       │    │ │
───────┴─┴────┴───────┴────┴─┴───────
   μ-3σ μ-2σ  μ-σ    μ   μ+σ  μ+2σ μ+3σ
```

- 68% of data falls within 1 SD of mean
- 95% within 2 SDs
- 99.7% within 3 SDs

**Standard Normal Distribution:** $Z = \frac{x - \mu}{\sigma}$ → mean = 0, SD = 1

**Z-scores tell you** how many standard deviations a value is from the mean.
> Score = 85, Mean = 70, SD = 10 → Z = (85-70)/10 = 1.5 → 1.5 SDs above mean

### 6.2.2 Binomial Distribution

Models the number of successes in n independent trials, each with probability p.

$$P(X = k) = \binom{n}{k} p^k (1-p)^{n-k}$$

Where $\binom{n}{k} = \frac{n!}{k!(n-k)!}$

**Parameters:** n (number of trials), p (probability of success)
**Mean:** $\mu = np$, **Variance:** $\sigma^2 = np(1-p)$

**Example:**
> A spam classifier has 90% accuracy (p = 0.9). Out of 10 emails (n = 10), what's the probability that exactly 8 are classified correctly?
> $P(X=8) = \binom{10}{8}(0.9)^8(0.1)^2 = 45 \times 0.4305 \times 0.01 = 0.1937 ≈ 19.4\%$

### 6.2.3 Poisson Distribution

Models the number of events occurring in a fixed interval (time/space) when events happen independently at a constant rate.

$$P(X = k) = \frac{\lambda^k e^{-\lambda}}{k!}$$

**Parameter:** $\lambda$ (average rate of occurrence)
**Mean = Variance = $\lambda$**

**Example:**
> A web server receives an average of 5 requests per second ($\lambda$ = 5). What's the probability of receiving exactly 3 requests in a given second?
> $P(X=3) = \frac{5^3 \times e^{-5}}{3!} = \frac{125 \times 0.0067}{6} = 0.1404 ≈ 14\%$

### 6.2.4 Other Important Distributions

| Distribution | Use Case | Parameters |
|-------------|----------|-----------|
| **Uniform** | Equal probability for all values in a range | a (min), b (max) |
| **Exponential** | Time between events in a Poisson process | $\lambda$ (rate) |
| **Chi-square ($\chi^2$)** | Test of independence, goodness-of-fit | df (degrees of freedom) |
| **t-distribution** | Like normal but heavier tails; used for small samples or unknown σ | df |
| **F-distribution** | Ratio of two chi-square distributions; used in ANOVA | df1, df2 |

---

## 6.3 Inferential Statistics

Inferential statistics use sample data to make **generalizations** about the population. The two main tools are **hypothesis testing** and **confidence intervals**.

### 6.3.1 Hypothesis Testing Framework

**Step-by-step process:**

1. **State hypotheses:**
   - $H_0$ (Null Hypothesis): "No effect" or "no difference" — the default assumption
   - $H_1$ (Alternative Hypothesis): "There IS an effect" or "there IS a difference"

2. **Choose significance level:** $\alpha$ = 0.05 (most common), meaning 5% chance of false positive

3. **Select the appropriate test** (see tables below)

4. **Compute test statistic** and its **p-value**

5. **Decision Rule:**
   - If **p-value < α** → **Reject $H_0$** (result is statistically significant)
   - If **p-value ≥ α** → **Fail to reject $H_0$** (not enough evidence)

**Example:**
> $H_0$: "There is no difference in accuracy between Model A and Model B"
> $H_1$: "There IS a difference in accuracy between Model A and Model B"
> α = 0.05
> p-value = 0.032
> Since 0.032 < 0.05 → **Reject $H_0$** → The difference is statistically significant

### One-tailed vs. Two-tailed Tests

| Type | $H_1$ | When to Use |
|------|-------|-------------|
| **Two-tailed** | $\mu_1 \neq \mu_2$ (different in either direction) | You don't know which is better |
| **Right-tailed** | $\mu_1 > \mu_2$ | You predict Model A is BETTER than B |
| **Left-tailed** | $\mu_1 < \mu_2$ | You predict Model A is WORSE than B |

### 6.3.2 Type I and Type II Errors

|  | $H_0$ is TRUE | $H_0$ is FALSE |
|--|--------------|----------------|
| **Reject $H_0$** | Type I Error (α) — False Positive | Correct! (Power = 1 - β) |
| **Fail to reject $H_0$** | Correct! | Type II Error (β) — False Negative |

**Analogy with AI:**

| Statistical Term | ML Equivalent |
|-----------------|---------------|
| Type I Error (false positive) | Predicting "spam" when it's not spam |
| Type II Error (false negative) | Predicting "not spam" when it IS spam |
| Significance level (α) | False positive rate |
| Power (1 - β) | Recall / Sensitivity |

**Key relationships:**
- Decreasing α → Increases β (harder to detect real effects)
- Increasing sample size → Decreases BOTH α and β
- Power should ideally be ≥ 0.80 (80%)

### 6.3.3 Parametric Tests

These assume the data follows a specific distribution (usually normal).

**t-test — Comparing Means**

| Type | When to Use | Formula |
|------|------------|---------|
| **One-sample t-test** | Compare sample mean to a known value | $t = \frac{\bar{x} - \mu_0}{s / \sqrt{n}}$ |
| **Independent (two-sample) t-test** | Compare means of TWO unrelated groups | $t = \frac{\bar{x}_1 - \bar{x}_2}{\sqrt{\frac{s_1^2}{n_1} + \frac{s_2^2}{n_2}}}$ |
| **Paired t-test** | Compare means of same group at two times | $t = \frac{\bar{d}}{s_d / \sqrt{n}}$ where $d$ = differences |

**Worked Example — Independent t-test:**
> Model A accuracy on 5 runs: 88, 90, 87, 91, 89 → $\bar{x}_1$ = 89, $s_1$ = 1.58
> Model B accuracy on 5 runs: 84, 86, 83, 85, 87 → $\bar{x}_2$ = 85, $s_2$ = 1.58
> 
> $t = \frac{89 - 85}{\sqrt{\frac{1.58^2}{5} + \frac{1.58^2}{5}}} = \frac{4}{\sqrt{0.499 + 0.499}} = \frac{4}{\sqrt{0.998}} = \frac{4}{0.999} = 4.004$
> 
> With df = 8 and α = 0.05, critical t ≈ 2.306
> Since 4.004 > 2.306 → **Reject $H_0$** → Model A is significantly better.

**ANOVA (Analysis of Variance)**

Tests whether the means of 3 or more groups are different.

| Type | When to Use | Example |
|------|-------------|---------|
| **One-way ANOVA** | One factor, 3+ levels | Compare accuracy of 4 different ML models |
| **Two-way ANOVA** | Two factors | Compare 3 models × 2 datasets (model and dataset both matter) |

> $H_0$: $\mu_1 = \mu_2 = \mu_3 = ... = \mu_k$ (all means are equal)
> $H_1$: At least one mean is different

$$F = \frac{MS_{between}}{MS_{within}} = \frac{\text{variance between groups}}{\text{variance within groups}}$$

If F is large → group means are different → reject $H_0$

**Post-hoc tests** (after significant ANOVA): Tukey HSD, Bonferroni — these tell you WHICH specific groups differ.

**Pearson's Correlation Coefficient (r)**

Measures the **linear** relationship between two continuous variables.

$$r = \frac{\sum (x_i - \bar{x})(y_i - \bar{y})}{\sqrt{\sum(x_i - \bar{x})^2 \sum(y_i - \bar{y})^2}}$$

| r value | Interpretation |
|---------|---------------|
| +1.00 | Perfect positive correlation |
| +0.70 to +0.99 | Strong positive |
| +0.40 to +0.69 | Moderate positive |
| +0.10 to +0.39 | Weak positive |
| 0.00 | No correlation |
| -0.10 to -0.39 | Weak negative |
| -0.40 to -0.69 | Moderate negative |
| -0.70 to -0.99 | Strong negative |
| -1.00 | Perfect negative correlation |

> **CRITICAL:** Correlation ≠ Causation. High correlation between ice cream sales and drowning deaths doesn't mean ice cream causes drowning (confounding variable: hot weather).

**Linear Regression**

Predicts the value of a dependent variable (Y) from one or more independent variables (X).

$$Y = \beta_0 + \beta_1 X + \epsilon$$

Where:
- $\beta_0$ = y-intercept
- $\beta_1$ = slope (change in Y per unit change in X)
- $\epsilon$ = error term

**R² (Coefficient of Determination):** The proportion of variance in Y explained by X.
- R² = 0.75 means "75% of the variation in Y is explained by X"

### 6.3.4 Non-Parametric Tests

Used when data violates assumptions of parametric tests (not normal, ordinal data, small samples).

| Non-Parametric Test | Replaces | When to Use |
|--------------------|----------|-------------|
| **Chi-square test** | — | Test association between two categorical variables |
| **Mann-Whitney U** | Independent t-test | Compare two independent groups (ordinal data) |
| **Wilcoxon signed-rank** | Paired t-test | Compare two related groups (ordinal data) |
| **Kruskal-Wallis** | One-way ANOVA | Compare 3+ independent groups (ordinal data) |
| **Spearman's rank correlation** | Pearson's r | Monotonic (not necessarily linear) relationship |

**Chi-Square Test of Independence — Worked Example:**

> Question: Is there an association between gender and preference for Python vs. R?
>
> Observed frequencies:
> |  | Python | R | Total |
> |--|--------|---|-------|
> | Male | 80 | 20 | 100 |
> | Female | 60 | 40 | 100 |
> | Total | 140 | 60 | 200 |
>
> Expected (if independent): $E = \frac{Row Total \times Column Total}{Grand Total}$
> - Male/Python: (100 × 140)/200 = 70
> - Male/R: (100 × 60)/200 = 30
> - Female/Python: (100 × 140)/200 = 70
> - Female/R: (100 × 60)/200 = 30
>
> $\chi^2 = \sum \frac{(O - E)^2}{E} = \frac{(80-70)^2}{70} + \frac{(20-30)^2}{30} + \frac{(60-70)^2}{70} + \frac{(40-30)^2}{30}$
> $= \frac{100}{70} + \frac{100}{30} + \frac{100}{70} + \frac{100}{30} = 1.43 + 3.33 + 1.43 + 3.33 = 9.52$
>
> df = (rows-1)(cols-1) = 1×1 = 1, Critical $\chi^2$ at α=0.05 = 3.841
> Since 9.52 > 3.841 → **Reject $H_0$** → Gender and language preference ARE associated.

### 6.3.5 Confidence Intervals

A range of values that is likely to contain the true population parameter.

$$CI = \bar{x} \pm Z_{\alpha/2} \times \frac{s}{\sqrt{n}}$$

**Example:**
> Sample mean accuracy = 87%, s = 3%, n = 25
> 95% CI = 87 ± 1.96 × (3/√25) = 87 ± 1.96 × 0.6 = 87 ± 1.176
> CI = **(85.82%, 88.18%)**
> 
> Interpretation: We are 95% confident that the true population accuracy lies between 85.82% and 88.18%.

### 6.3.6 Effect Size

P-values tell you IF an effect exists; effect size tells you HOW BIG it is.

**Cohen's d** (for comparing two means):
$$d = \frac{\bar{x}_1 - \bar{x}_2}{s_{pooled}}$$

| d value | Interpretation |
|---------|---------------|
| 0.2 | Small effect |
| 0.5 | Medium effect |
| 0.8 | Large effect |

**R² (coefficient of determination):** Already discussed in regression.

> **Why effect size matters in ML:** With very large datasets, even a tiny difference (0.1% accuracy) can be "statistically significant" (p < 0.05), but it may not be **practically significant**. Effect size helps distinguish meaningful improvements from trivial ones.

---

## 6.4 Choosing the Right Statistical Test — Decision Flowchart

```
What is your research question?
│
├── Comparing groups?
│   ├── How many groups?
│   │   ├── 2 groups
│   │   │   ├── Related/paired? → Paired t-test (or Wilcoxon)
│   │   │   └── Independent? → Independent t-test (or Mann-Whitney U)
│   │   └── 3+ groups
│   │       ├── One factor? → One-way ANOVA (or Kruskal-Wallis)
│   │       └── Two factors? → Two-way ANOVA
│   └── Data is ordinal/non-normal? → Use the non-parametric alternative
│
├── Examining relationships?
│   ├── Both variables continuous? → Pearson r (or Spearman if non-linear)
│   ├── Both variables categorical? → Chi-square test
│   └── Predicting one from another? → Regression
│
└── Predicting an outcome?
    ├── One predictor? → Simple linear regression
    └── Multiple predictors? → Multiple linear regression
```

---

## 6.5 Practice Questions

**Q1.** Dataset: 12, 15, 18, 22, 25, 28, 30, 95. Calculate mean and median. Which is a better measure of central tendency here, and why?
> **Answer:** Mean = (12+15+18+22+25+28+30+95)/8 = 245/8 = **30.6**. Median = (22+25)/2 = **23.5**. The **median (23.5)** is better because the outlier (95) inflates the mean to 30.6, which doesn't represent the typical value.

**Q2.** You ran 3 different ML models on the same dataset and recorded their F1-scores across 10 runs each. Which statistical test would you use to determine if there's a significant difference between the three models?
> **Answer:** **One-way ANOVA** (if the F1-scores are normally distributed and variances are equal across groups). If these assumptions are violated, use **Kruskal-Wallis test**. If ANOVA is significant, follow up with Tukey HSD post-hoc test to identify which specific pairs of models differ.

**Q3.** A researcher finds a Pearson correlation of r = -0.85 between model complexity (number of parameters) and inference speed. Interpret this.
> **Answer:** There is a **strong negative** correlation: as model complexity increases, inference speed decreases (models get slower). However, this correlation does not necessarily imply causation — there could be other factors (hardware, optimization, batch size) mediating this relationship.

**Q4.** Type I error and Type II error — give a real-world ML example of each.
> **Answer:** **Type I (false positive):** A fraud detection system flags a legitimate transaction as fraud, blocking a customer's genuine purchase. **Type II (false negative):** The same system fails to detect an actual fraudulent transaction, allowing a thief to steal money. In medical AI: Type I = diagnosing healthy person as sick (unnecessary worry/treatment); Type II = missing a real disease (dangerous).

**Q5.** Explain why "p < 0.05" doesn't mean there's a 95% chance the result is true.
> **Answer:** The p-value is the probability of observing data as extreme as (or more extreme than) the actual data, **given that $H_0$ is true**. It is NOT the probability that $H_0$ is true or false. P = 0.03 means: "If there were truly no effect, we'd see data this extreme only 3% of the time." It doesn't tell us the probability of the hypothesis itself. This is a common misinterpretation. The probability of a hypothesis being true requires Bayesian reasoning with prior probabilities.

---

*Previous: [Chapter 5 — Data Collection Methods](05_Data_Collection_Methods.md) | Next: [Chapter 7 — Research Ethics](07_Research_Ethics.md)*

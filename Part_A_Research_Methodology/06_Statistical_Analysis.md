# 6. Statistical Analysis

> **Part A — Research Methodology** | SIU PET Study Guide

---

## 6.1 Descriptive Statistics

- [ ] **Measures of Central Tendency**
  - **Mean**: $\bar{x} = \frac{\sum x_i}{n}$
  - **Median**: Middle value when ordered
  - **Mode**: Most frequent value

- [ ] **Measures of Dispersion**
  - **Range**: Max − Min
  - **Variance**: $\sigma^2 = \frac{\sum (x_i - \bar{x})^2}{n}$ (population) or $s^2 = \frac{\sum (x_i - \bar{x})^2}{n-1}$ (sample)
  - **Standard Deviation**: $\sigma = \sqrt{\sigma^2}$
  - **Interquartile Range (IQR)**: Q3 − Q1
  - **Coefficient of Variation**: $CV = \frac{\sigma}{\bar{x}} \times 100$

- [ ] **Measures of Shape**
  - **Skewness**: Positive (right tail), Negative (left tail), Zero (symmetric)
  - **Kurtosis**: Leptokurtic (>3), Mesokurtic (=3), Platykurtic (<3)

---

## 6.2 Probability Distributions

- [ ] **Normal Distribution**: Bell curve, $\mu$ = mean, $\sigma$ = SD; 68-95-99.7 rule
- [ ] **Binomial Distribution**: $P(X=k) = \binom{n}{k} p^k (1-p)^{n-k}$
- [ ] **Poisson Distribution**: $P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}$
- [ ] **Uniform, Exponential, Chi-square, t-distribution, F-distribution**

---

## 6.3 Inferential Statistics

- [ ] **Hypothesis Testing Framework**
  1. State H₀ and H₁
  2. Choose significance level (α = 0.05 typically)
  3. Select test statistic
  4. Compute test statistic and p-value
  5. Decision: Reject H₀ if p-value < α

- [ ] **Type I and Type II Errors**
  - **Type I (α)**: Rejecting H₀ when it's true (false positive)
  - **Type II (β)**: Failing to reject H₀ when it's false (false negative)
  - **Power**: 1 − β (probability of correctly rejecting false H₀)

- [ ] **Parametric Tests**

  | Test | Purpose | Assumptions |
  |------|---------|-------------|
  | **t-test (one sample)** | Compare sample mean to known value | Normal distribution |
  | **t-test (independent)** | Compare means of two independent groups | Normal, equal variance |
  | **t-test (paired)** | Compare means of related groups | Normal differences |
  | **ANOVA (one-way)** | Compare means of 3+ groups | Normal, equal variance |
  | **ANOVA (two-way)** | Two independent factors | Normal, equal variance |
  | **Pearson's correlation** | Linear relationship between two variables | Normal, interval/ratio |
  | **Linear regression** | Predict DV from IV(s) | Linearity, normality of residuals |

- [ ] **Non-Parametric Tests**

  | Test | Purpose | Replaces |
  |------|---------|----------|
  | **Chi-square test** | Association between categorical variables | — |
  | **Mann-Whitney U** | Compare two independent groups | Independent t-test |
  | **Wilcoxon signed-rank** | Compare two related groups | Paired t-test |
  | **Kruskal-Wallis** | Compare 3+ independent groups | One-way ANOVA |
  | **Spearman's rank correlation** | Monotonic relationship | Pearson's correlation |

- [ ] **Confidence Intervals**
  - CI = $\bar{x} \pm Z_{\alpha/2} \times \frac{\sigma}{\sqrt{n}}$
  - 95% CI means: 95% of such intervals contain the true mean

- [ ] **Effect Size**
  - Cohen's d: Small (0.2), Medium (0.5), Large (0.8)
  - R²: Proportion of variance explained

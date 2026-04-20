# 5. Data Collection Methods

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 5.1 Primary vs. Secondary Data

| Aspect | Primary Data | Secondary Data |
|--------|-------------|---------------|
| **Definition** | Data collected firsthand by the researcher for the specific study | Data that already exists, collected by someone else for a different purpose |
| **Freshness** | New, original | Pre-existing |
| **Cost** | Higher (you collect it) | Lower (already available) |
| **Time** | More time-consuming | Quick to access |
| **Control** | Full control over quality and relevance | Limited — may not fit your needs perfectly |
| **Examples** | Surveys, interviews, experiments | Census data, published papers, government reports, Kaggle datasets |

---

## 5.2 Primary Data Collection Methods

### 5.2.1 Questionnaire / Survey

A set of written questions administered to respondents. The most common data collection method in social and applied research.

**Types of Questionnaires:**

| Type | Description | Example |
|------|-------------|---------|
| **Structured** | Fixed questions with predetermined answer options (closed-ended) | Multiple-choice survey on tool preferences |
| **Semi-structured** | Mix of closed and open-ended questions | Rate your satisfaction (1-5) + "Please explain why" |
| **Unstructured** | Open-ended questions, respondent writes freely | "Describe your experience with AI tools" |

**Question Types:**

| Type | Example |
|------|---------|
| **Dichotomous** | "Do you use AI in your work? Yes / No" |
| **Multiple Choice** | "Which AI framework do you primarily use? a) TensorFlow b) PyTorch c) JAX d) Other" |
| **Likert Scale** | "AI tools improve my productivity: 1-Strongly Disagree to 5-Strongly Agree" |
| **Ranking** | "Rank these ML frameworks from most to least preferred" |
| **Open-ended** | "What challenges do you face when deploying ML models?" |

**The Likert Scale (Important!)**

A 5-point or 7-point scale measuring agreement/frequency/satisfaction:

```
1          2          3          4          5
Strongly   Disagree   Neutral    Agree      Strongly
Disagree                                    Agree
```

**Guidelines for Good Questionnaire Design:**
1. Use simple, clear language — avoid jargon unless the audience is technical
2. Avoid **double-barreled questions**: "Do you find Python easy and powerful?" (What if they find it easy but not powerful?)
3. Avoid **leading questions**: "Don't you agree that AI is the future?" → biased
4. Keep it short — long surveys have high dropout rates
5. Pilot test on 10-20 people before full deployment
6. Place sensitive/demographic questions at the end
7. Use logical flow — group related questions together

**Administration Methods:**
- Online (Google Forms, SurveyMonkey, Typeform)
- Paper-based (in-person distribution)
- Email/postal
- Phone-assisted

### 5.2.2 Interview

A conversation between the researcher and respondent, usually more in-depth than a questionnaire.

| Type | Description | When to Use |
|------|-------------|-------------|
| **Structured** | Fixed questions, same order for everyone | Comparing responses across many participants |
| **Semi-structured** | Guide questions + freedom to explore | Most common in qualitative research |
| **Unstructured** | Free-flowing conversation around a topic | Exploratory studies, new areas |
| **In-depth** | Detailed, lengthy (30-90 min) one-on-one | Deep understanding of experiences |
| **Focus Group** | Group interview (6-12 participants) | Exploring group dynamics, consensus/disagreement |

**Advantages over Questionnaires:**
- Can probe deeper ("Can you explain what you mean by that?")
- Can observe non-verbal cues (body language, tone)
- Higher response rate (people find it harder to say no face-to-face)
- Rich, detailed, qualitative data

**Disadvantages:**
- Time-consuming and expensive
- Interviewer bias can affect responses
- Difficult to standardize and compare across interviews
- Transcription and analysis is labor-intensive

### 5.2.3 Observation

Systematically watching and recording behavior or events as they naturally occur.

| Type | Description | Example |
|------|-------------|---------|
| **Participant** | Researcher joins the group being studied | Researcher works in an AI startup for 3 months to understand DevOps culture |
| **Non-participant** | Researcher watches without involvement | Observing how users interact with a chatbot through screen recordings |
| **Structured** | Predefined checklist of behaviors to record | Counting error types during software testing sessions |
| **Unstructured** | Open-ended notes on everything observed | Ethnographic study of a research lab |

**Advantages:** Captures real behavior (not self-reported), good for studying processes
**Disadvantages:** Observer effect (people change behavior when watched), time-consuming, subjective interpretation

### 5.2.4 Experiment

The researcher manipulates an independent variable and measures its effect on the dependent variable while controlling other variables.

| Type | Description | Example |
|------|-------------|---------|
| **Laboratory** | Controlled environment, high internal validity | Testing two UI designs for an AI tool in a usability lab |
| **Field** | Real-world setting, high external validity | A/B testing two recommendation algorithms on live users |
| **Natural** | Researcher doesn't manipulate — observes a naturally occurring "treatment" | Comparing coding productivity before vs. after a company adopts GitHub Copilot |

**In AI/ML Research:**
- Training model A vs. model B on the same dataset → comparing accuracy
- Ablation studies — removing components to measure their contribution
- Hyperparameter experiments — grid search / random search

---

## 5.3 Secondary Data Sources

### Published Sources
- **Journals:** IEEE, ACM, Springer, Elsevier
- **Conference proceedings:** NeurIPS, ICML, CVPR, AAAI, ACL
- **Books and textbooks**
- **Government reports:** Census data, NASSCOM reports, MEITY publications
- **Industry reports:** Gartner, McKinsey AI Index

### Unpublished Sources
- PhD theses and dissertations (Shodhganga, ProQuest)
- Internal company reports and databases
- Unpublished research papers (preprints on arXiv)

### Electronic / Digital Sources
- **Datasets:** Kaggle, UCI ML Repository, Hugging Face Datasets, Google Dataset Search
- **APIs:** Twitter/X API, Reddit API, weather APIs
- **Web scraping:** BeautifulSoup, Scrapy (with ethical considerations)
- **Code repositories:** GitHub (for analyzing software engineering practices)

### Advantages of Secondary Data:
- Already available — saves time and money
- Large-scale data (e.g., census covers millions)
- Enables longitudinal analysis (data over many years)

### Disadvantages:
- May not exactly match your research needs
- Data quality depends on the original collector
- May be outdated
- Format may need significant cleaning/transformation

---

## 5.4 Scales of Measurement (Stevens' Classification)

Understanding measurement scales is **crucial** — they determine which statistical tests you can use.

### 5.4.1 Nominal Scale
**Definition:** Categories with no inherent order. Just labels.

**Examples:**
- Programming language used: Python, Java, C++, R
- Disease type: Type 1, Type 2
- ML model type: CNN, RNN, Transformer

**Allowed operations:** Count, mode, frequency, chi-square test
**NOT allowed:** Mean, median (meaningless — average of "Python" and "Java"?)

### 5.4.2 Ordinal Scale
**Definition:** Categories WITH a meaningful order, but unequal intervals between categories.

**Examples:**
- Customer satisfaction: Very Unsatisfied < Unsatisfied < Neutral < Satisfied < Very Satisfied
- Education level: High School < Bachelor's < Master's < PhD
- Competition rank: 1st, 2nd, 3rd

**Problem:** The "distance" between 1st and 2nd may be very different from the distance between 2nd and 3rd.

**Allowed operations:** Median, percentile, Spearman correlation, Mann-Whitney U
**NOT allowed:** Mean, standard deviation (technically — though Likert scale data is often treated as interval in practice)

### 5.4.3 Interval Scale
**Definition:** Equal intervals between values, but NO true zero point.

**Examples:**
- Temperature in Celsius: 0°C does not mean "no temperature" — it's just freezing point of water
- IQ scores: IQ of 0 doesn't mean "no intelligence"
- Year: Year 0 is arbitrary

**Allowed operations:** Mean, standard deviation, Pearson correlation, t-test, ANOVA

**Key property:** You can say "the difference between 20°C and 30°C equals the difference between 30°C and 40°C" but you CANNOT say "40°C is twice as hot as 20°C."

### 5.4.4 Ratio Scale
**Definition:** Equal intervals AND a true zero point. Zero means "none."

**Examples:**
- Height: 0 cm = no height
- Weight: 0 kg = no weight
- Model accuracy: 0% = no correct predictions
- Inference time: 0 ms = instant
- Money: ₹0 = no money

**Allowed operations:** ALL statistical operations including geometric mean, coefficient of variation

**Key property:** You CAN say "200 ms inference time is twice as long as 100 ms."

### Quick Decision Chart

```
Does the data have categories?
├── Yes → Are the categories ordered?
│         ├── No  → NOMINAL (e.g., colors, names)
│         └── Yes → Are intervals equal?
│                   ├── No  → ORDINAL (e.g., rankings)
│                   └── Yes → Is there a true zero?
│                             ├── No  → INTERVAL (e.g., temperature °C)
│                             └── Yes → RATIO (e.g., height, weight)
└── No → It's quantitative → check equal intervals and true zero as above
```

---

## 5.5 Data Quality and Triangulation

### Dimensions of Data Quality

| Dimension | Description | Example of Poor Quality |
|-----------|-------------|------------------------|
| **Accuracy** | Data reflects reality | A sensor reading 25°C when actual is 30°C |
| **Completeness** | No missing values | 40% of survey respondents skipped Q5 |
| **Consistency** | Same entity, same data everywhere | Age listed as 25 in one field and 32 in another |
| **Timeliness** | Data is current | Using 2015 salary data for a 2025 analysis |
| **Uniqueness** | No duplicate records | Same patient entered twice in the database |

### Handling Missing Data

| Strategy | When to Use | Method |
|----------|-------------|--------|
| **Listwise deletion** | Very little missing data (<5%) | Remove entire row if any value missing |
| **Mean/Median imputation** | Data is MCAR (missing completely at random) | Replace missing with column mean or median |
| **Mode imputation** | Categorical data | Replace missing with most frequent category |
| **Regression imputation** | Data is MAR (missing at random) | Predict missing value from other variables |
| **Multiple imputation** | Best practice for serious research | Create multiple imputed datasets, analyze each, pool results |
| **KNN imputation** | ML context | Replace with average of K nearest neighbors |

### Triangulation

Using **multiple sources or methods** to cross-verify findings and increase credibility.

| Type | Description | Example |
|------|-------------|---------|
| **Data triangulation** | Multiple data sources | Comparing survey results with interview data |
| **Method triangulation** | Multiple methods | Using both quantitative surveys and qualitative interviews |
| **Investigator triangulation** | Multiple researchers | Two researchers independently code qualitative data |
| **Theory triangulation** | Multiple theoretical frameworks | Analyzing adoption of AI using TAM and DOI theories |

---

## 5.6 Practice Questions

**Q1.** A researcher wants to understand how students feel about using ChatGPT for assignments. They distribute a questionnaire with the item: "ChatGPT helps me learn better: 1-Strongly Disagree to 5-Strongly Agree." What type of scale is this?
> **Answer:** This is an **ordinal scale** (Likert scale). While it has numbers, the intervals between categories are not guaranteed to be equal. "Strongly Disagree to Disagree" may represent a different psychological distance than "Agree to Strongly Agree." Note: In practice, researchers often treat Likert data as interval for statistical analysis, but strictly speaking, it is ordinal.

**Q2.** What is the difference between a structured interview and a structured questionnaire?
> **Answer:** A **structured questionnaire** is a self-administered written instrument where respondents read and answer questions independently. A **structured interview** uses the same fixed questions but is administered by the researcher in person (or via phone/video) — allowing the researcher to clarify questions, probe further, and observe non-verbal cues. The content structure is similar, but the mode of administration and richness of data differ.

**Q3.** A researcher measures ML model performance using "accuracy percentage." What scale of measurement is this? What if they rank models as "best, second-best, third-best"?
> **Answer:** Accuracy percentage is a **ratio scale** — it has equal intervals and a true zero (0% = no correct predictions). Ranking models as best/second-best/third-best is **ordinal** — there is an order, but the difference in performance between best and second-best might not equal the difference between second and third.

**Q4.** You have a dataset with 15% missing values in a key column. The data appears to be Missing At Random (MAR). Which imputation strategy would you choose?
> **Answer:** With 15% missing data that is MAR, **multiple imputation** or **regression imputation** would be appropriate. Simple listwise deletion would lose too much data (15% of rows), and mean imputation would distort the distribution and underestimate variance. Regression imputation preserves relationships between variables, and multiple imputation provides associated uncertainty estimates.

**Q5.** Name one advantage and one disadvantage each for: (a) Primary data, (b) Secondary data.
> **Answer:** (a) **Primary data** — Advantage: Tailored to your exact research question. Disadvantage: Time-consuming and expensive to collect. (b) **Secondary data** — Advantage: Readily available, saves time and money. Disadvantage: May not perfectly fit your research needs (collected for a different purpose).

---

*Previous: [Chapter 4 — Sampling Techniques](04_Sampling_Techniques.md) | Next: [Chapter 6 — Statistical Analysis](06_Statistical_Analysis.md)*

# 1. Introduction to Research

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 1.1 What is Research?

**Research** is a systematic, organized, and scientific process of collecting, analyzing, and interpreting information (data) to increase our understanding of a phenomenon.

**Formal Definition (C.R. Kothari):** *"Research is an academic activity and as such the term should be used in a technical sense. Research comprises defining and redefining problems, formulating hypothesis or suggested solutions; collecting, organizing and evaluating data; making deductions and reaching conclusions."*

**Key words in the definition:**
- **Systematic** — follows a step-by-step logical procedure
- **Organized** — structured and planned, not haphazard
- **Scientific** — based on observable, measurable evidence

### Research vs. Everyday Problem-Solving

| Aspect | Everyday Problem-Solving | Research |
|--------|-------------------------|----------|
| Approach | Intuition, trial-and-error | Systematic, methodical |
| Evidence | Anecdotal, personal experience | Empirical, verifiable data |
| Bias | Often biased by personal views | Aims for objectivity |
| Replicability | Not reproducible | Designed to be reproducible |
| Documentation | Usually informal | Formally documented |
| Generalizability | Specific to one situation | Aims for broader applicability |

**Example:** If your Wi-Fi is slow, you might restart the router (everyday problem-solving). A researcher would systematically measure speeds at different times, distances, with different devices, control for variables, collect data, and statistically analyze to identify the actual cause.

---

## 1.2 Objectives of Research

Research is conducted for one or more of these broad purposes:

### 1. To Gain Familiarity (Exploratory Objective)
When little is known about a topic, research helps explore and gain initial understanding.

*Example:* "What are the challenges faced by Indian hospitals in adopting AI-based diagnostic tools?" — We don't know much yet, so we explore.

### 2. To Describe Accurately (Descriptive Objective)
To portray the characteristics of a particular individual, group, or situation accurately.

*Example:* "What percentage of Indian IT companies use machine learning in production?" — We want an accurate picture.

### 3. To Determine Frequency (Diagnostic Objective)
To find how often something occurs or how it is associated with something else.

*Example:* "How frequently do autonomous vehicles encounter edge-case scenarios in Indian traffic conditions?"

### 4. To Test Causal Relationships (Experimental Objective)
To test whether one thing causes another — the most rigorous form of research.

*Example:* "Does using transfer learning (cause) improve classification accuracy on small medical datasets (effect) compared to training from scratch?"

---

## 1.3 Types of Research

### Classification 1: By Purpose

#### Basic (Fundamental/Pure) Research
- **Goal:** Generate new knowledge and theories; no immediate practical application
- **Driven by:** Curiosity and desire to expand knowledge
- **Example:** Studying why certain neural network architectures converge faster (understanding the theory, not building a product)
- **Outcome:** Theories, principles, generalizations

#### Applied Research
- **Goal:** Solve a specific, practical problem using existing knowledge
- **Driven by:** Real-world needs
- **Example:** Developing an ML model to detect fraudulent credit card transactions for a bank
- **Outcome:** Solutions, products, techniques

#### Action Research
- **Goal:** Solve an immediate problem while it's occurring, in the real setting
- **Driven by:** Practitioners (teachers, managers) wanting to improve their own practice
- **Example:** A teacher implementing a new AI-assisted tutoring tool in their class and simultaneously studying its effect on student learning
- **Outcome:** Immediate improvements, localized solutions

### Classification 2: By Approach

#### Quantitative Research
- Uses **numerical data** and **statistical analysis**
- Seeks to **quantify** variables and **generalize** results
- Large samples, structured instruments (surveys, experiments)
- **Example:** Measuring the accuracy of 5 different ML models on 10 benchmark datasets and comparing them using ANOVA

#### Qualitative Research
- Uses **non-numerical data** — words, images, observations
- Seeks to **understand** meanings, experiences, perspectives
- Small samples, unstructured methods (interviews, focus groups, observation)
- **Example:** Conducting in-depth interviews with 15 data scientists to understand why they choose certain tools over others

#### Mixed Methods Research
- **Combines** both quantitative and qualitative approaches
- Uses numbers AND words/themes to get a complete picture
- **Example:** Surveying 500 developers about AI tool usage (quantitative) AND interviewing 20 of them in depth (qualitative)

### Classification 3: By Design

| Type | What it does | Example |
|------|-------------|---------|
| **Descriptive** | Describes "what is" — current state of affairs | Survey: "How many Indian IT firms use cloud AI services?" |
| **Analytical** | Analyzes existing data/facts critically | Meta-analysis of published ML accuracy results across 50 papers |
| **Exploratory** | Explores new/unknown areas | Investigating ethical implications of deepfake technology |
| **Experimental** | Tests cause-and-effect with controlled conditions | Testing if data augmentation improves model accuracy (with control and experimental groups) |

### Classification 4: By Time Dimension

| Type | Description | Example |
|------|-------------|---------|
| **Cross-sectional** | Data collected at one point in time | Survey of AI adoption in 2025 |
| **Longitudinal** | Data collected over multiple time periods | Tracking AI adoption annually from 2020 to 2025 |

### Classification 5: By Logic

| Type | Direction | Process |
|------|-----------|---------|
| **Deductive** | General → Specific | Start with theory → form hypothesis → test with data |
| **Inductive** | Specific → General | Start with observations → find patterns → build theory |

**Deductive Example:** "Deep learning theory says more layers improve feature extraction. Hypothesis: ResNet-50 will outperform ResNet-18 on ImageNet. Test it."

**Inductive Example:** "We observe that our model's accuracy drops every Monday. We investigate and discover it's because weekend data has different patterns. New theory: temporal distribution shift affects model performance."

---

## 1.4 The Research Process (Step-by-Step)

The research process is a series of interconnected stages. Think of it as a roadmap:

```
Step 1: Identify Research Problem
         ↓
Step 2: Review Literature
         ↓
Step 3: Formulate Hypothesis
         ↓
Step 4: Design the Research
         ↓
Step 5: Collect Data
         ↓
Step 6: Analyze Data
         ↓
Step 7: Interpret & Discuss Results
         ↓
Step 8: Write Report / Thesis
```

### Step 1: Identify the Research Problem
- What do you want to study? What gap exists in current knowledge?
- A good problem is **specific**, **feasible**, and **significant**
- *Example:* "There is no efficient method to detect hate speech in Hindi-English code-mixed social media text"

### Step 2: Review of Literature
- Read existing research papers, theses, books on the topic
- Understand what has already been done, what methods were used, what gaps remain
- Helps refine your problem and avoid duplication
- Sources: Google Scholar, IEEE Xplore, ACM Digital Library, arXiv

### Step 3: Formulate Hypothesis
- A **hypothesis** is a tentative statement about the expected relationship between variables
- It must be **testable** and **falsifiable**
- *Example:* "A BERT-based model fine-tuned on Hindi-English code-mixed data will achieve at least 85% F1-score in hate speech detection, outperforming traditional TF-IDF + SVM approach"
- **Null Hypothesis (H₀):** "There is no significant difference in F1-scores between BERT and TF-IDF+SVM"
- **Alternative Hypothesis (H₁):** "BERT achieves significantly higher F1-score than TF-IDF+SVM"

### Step 4: Design the Research
- Plan HOW you will conduct the study
- Decide: What data? What methods? What variables? What controls?
- Choose: experimental, quasi-experimental, survey, case study, etc.

### Step 5: Collect Data
- Gather the actual data using your chosen methods
- Primary data: collected first-hand (experiments, surveys, interviews)
- Secondary data: already existing (datasets, published statistics, databases)

### Step 6: Analyze Data
- Apply appropriate statistical or analytical techniques
- Quantitative: statistical tests (t-test, ANOVA, regression)
- Qualitative: coding, thematic analysis

### Step 7: Interpret and Discuss Results
- What do the results mean? Do they support or reject the hypothesis?
- Compare with existing literature
- Discuss implications, limitations, unexpected findings

### Step 8: Write the Report / Thesis
- Document everything in a structured format
- Sections: Abstract, Introduction, Literature Review, Methodology, Results, Discussion, Conclusion, References

---

## 1.5 Characteristics of Good Research

Good research must have these qualities:

| Characteristic | Meaning |
|---------------|---------|
| **Systematic** | Follows a defined procedure/methodology step by step |
| **Logical** | Based on logical reasoning (deductive or inductive) |
| **Empirical** | Based on observable, measurable evidence (not just opinions) |
| **Replicable** | Another researcher should be able to repeat the study and get similar results |
| **Objective** | Free from personal bias; findings should not depend on who conducts the study |
| **Controlled** | Extraneous variables are controlled so we can isolate the effect of the variable under study |
| **Rigorous** | Careful, thorough, and accurate in its procedures |
| **Valid** | Actually measures what it claims to measure |
| **Reliable** | Produces consistent results when repeated |
| **Ethical** | Follows ethical guidelines — informed consent, no fabrication, no plagiarism |

---

## 1.6 Significance of Research

### In Academia
- Advances human knowledge
- Contributes to theory building
- Trains critical thinking and analytical skills
- Fuels innovation and technological progress

### In Industry
- Data-driven decision making
- Product development and improvement
- Competitive advantage through innovation
- Market research and strategy

### In Society
- Evidence-based policy making
- Healthcare improvements
- Environmental solutions
- Social problem identification and solutions

### In Computer Science / AI Specifically
- Developing new algorithms and models
- Benchmarking and comparing techniques
- Understanding limitations of existing approaches
- Pushing the boundaries of what machines can do

---

## 1.7 Research in Computer Science vs. Other Disciplines

| Aspect | CS/AI Research | Social Science Research |
|--------|---------------|----------------------|
| Data | Often quantitative (accuracy, F1, benchmarks) | Often qualitative or mixed |
| Experiments | Computational experiments on datasets | Often involves human subjects |
| Reproducibility | Code, data, environments can be shared | Harder to replicate human behavior |
| Publication | Conferences (NeurIPS, ICML) as important as journals | Journals dominate |
| Peer review | Often single-blind or open | Usually double-blind |
| Speed | Fast iteration (arXiv preprints) | Slower publication cycles |

---

## 1.8 Key Terms to Remember

| Term | Definition |
|------|-----------|
| **Variable** | Any characteristic that can take different values (age, accuracy, learning rate) |
| **Hypothesis** | A testable statement about the relationship between variables |
| **Population** | The entire group you want to study |
| **Sample** | A subset of the population actually studied |
| **Data** | Facts, figures, or information collected for analysis |
| **Theory** | A well-substantiated explanation of some aspect of the world, based on evidence |
| **Paradigm** | A framework of beliefs and methods shared by a research community |
| **Empirical** | Based on observation or experiment, not just theory |

---

## 1.9 Practice Questions

**Q1.** What is the primary difference between basic and applied research?
> **Answer:** Basic research aims to generate new knowledge and expand understanding without immediate practical application (e.g., studying mathematical properties of neural networks). Applied research uses existing knowledge to solve specific practical problems (e.g., building a spam detection system).

**Q2.** A researcher collects data from 500 software developers through an online questionnaire with rating scales. What type of research approach is this?
> **Answer:** Quantitative research (numerical data from rating scales, large sample, structured instrument).

**Q3.** Arrange the research process steps in correct order: (a) Analyze data, (b) Formulate hypothesis, (c) Identify problem, (d) Review literature, (e) Collect data
> **Answer:** c → d → b → e → a (Identify problem → Review literature → Formulate hypothesis → Collect data → Analyze data)

**Q4.** Which characteristic of good research ensures that another researcher can repeat the study?
> **Answer:** Replicability.

**Q5.** Give an example of inductive reasoning in AI research.
> **Answer:** A researcher observes that transformer models consistently outperform RNNs on multiple NLP benchmarks. From these specific observations, they formulate a general theory that self-attention mechanisms are fundamentally better at capturing long-range dependencies than recurrent architectures.

---

*Next: [Chapter 2 — Research Problem & Literature Review](../Part_A_Research_Methodology/02_Research_Problem_and_Literature_Review.md)*

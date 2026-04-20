# 2. Research Problem & Literature Review

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 2.1 What is a Research Problem?

A **research problem** is a specific issue, difficulty, contradiction, or gap in knowledge that a researcher aims to address through systematic investigation.

Think of it this way: **A research problem is a question that needs an answer, and the answer is not yet known.**

### A Good Research Problem Must Be:

| Criterion | Meaning | Example |
|-----------|---------|---------|
| **Specific** | Clearly defined, not vague | "Does BERT outperform LSTM for sentiment analysis on Hindi tweets?" (specific) vs. "Is deep learning good?" (vague) |
| **Feasible** | Can be investigated with available resources (time, data, equipment) | You need access to Hindi tweet data, GPUs for training, and enough time |
| **Novel** | Adds something new — not a mere repetition of existing work | If 100 papers already compared BERT vs. LSTM on English text, try a new language or domain |
| **Significant** | Important to the field or society; worth investigating | Hindi NLP is under-researched, so this contributes meaningfully |
| **Ethical** | Does not violate ethical principles | Don't scrape private messages without consent |

---

## 2.2 Sources of Research Problems

Where do research ideas come from?

### 1. Personal Experience and Observation
You notice a problem in your work or daily life.
> *Example:* "I work in a hospital's IT department and notice that radiologists spend 4 hours daily reviewing normal X-rays. Can AI help screen the normals automatically?"

### 2. Existing Literature (Research Gap)
While reading papers, you find something that hasn't been studied.
> *Example:* You read 20 papers on object detection and realize none of them benchmark performance in low-light conditions specific to Indian traffic. That's a gap.

### 3. Previous Research Recommendations
Research papers often end with "Future Work" sections suggesting what should be studied next.
> *Example:* A paper on federated learning says: "Future work should investigate the impact of non-IID data distributions in healthcare settings."

### 4. Practical/Industry Problems
Real-world problems in organizations, government, or society.
> *Example:* An e-commerce company struggles with fake product reviews. Can NLP detect them?

### 5. Technological Advances
New technologies create new research questions.
> *Example:* Large Language Models (LLMs) are new. Questions arise: "How do LLMs perform on Indian legal documents?" "Can we fine-tune LLaMA for Marathi?"

### 6. Contradictions in Existing Findings
Different studies report conflicting results.
> *Example:* Paper A says dropout improves generalization; Paper B says it hurts performance on small datasets. Which is right? Under what conditions?

---

## 2.3 Formulating a Research Problem

Once you have a broad idea, you need to **narrow it down** into a precise, researchable statement.

### From Broad Topic to Specific Problem:

```
Broad Area:    Artificial Intelligence in Healthcare
    ↓ (narrow down)
Topic:         Medical Image Analysis using Deep Learning
    ↓ (narrow down)  
Specific Area: Chest X-ray abnormality detection
    ↓ (narrow down)
Research Problem: "Existing CNN models for chest X-ray classification show 
                   reduced accuracy on images from Indian hospitals due to 
                   different equipment and demographics. There is a need for 
                   a domain-adapted model."
```

### Components of a Well-Formulated Problem:

1. **Problem Statement** — A clear, concise declaration of what you plan to investigate
   > "This research investigates the effectiveness of domain adaptation techniques for improving chest X-ray classification accuracy when models trained on Western datasets are deployed in Indian hospital settings."

2. **Research Questions** — Specific questions your study will answer
   > - RQ1: How much does a model trained on ChestX-ray14 (US dataset) lose in accuracy when tested on Indian hospital X-rays?
   > - RQ2: Does fine-tuning with 500 Indian X-ray samples significantly improve performance?
   > - RQ3: Which domain adaptation technique (fine-tuning, adversarial DA, or self-training) works best?

3. **Research Objectives** — What you aim to achieve (stated as actions)
   > - To measure the performance gap of pre-trained models on Indian hospital X-ray data
   > - To develop a domain adaptation pipeline for cross-dataset X-ray classification
   > - To compare three domain adaptation techniques on accuracy, F1-score, and AUC

### Research Questions vs. Research Objectives

| Research Questions | Research Objectives |
|-------------------|-------------------|
| Start with "What", "How", "Why", "Does" | Start with "To" + verb (measure, develop, compare, evaluate) |
| Ask what you want to KNOW | State what you want to DO |
| "Does data augmentation improve accuracy?" | "To evaluate the effect of data augmentation on classification accuracy" |
| Questions-form | Action-form |

---

## 2.4 Literature Review

### What is a Literature Review?

A **literature review** is a comprehensive survey and critical analysis of existing research relevant to your topic. It is NOT just a list of summaries — it must **synthesize**, **compare**, **critique**, and **identify gaps**.

### Why is Literature Review Essential?

| Purpose | How it helps |
|---------|-------------|
| **Avoid duplication** | Ensures your work hasn't already been done |
| **Identify gaps** | Shows what hasn't been studied, leading to your research problem |
| **Build theoretical framework** | Understand the theories and models underlying your area |
| **Learn methods** | See what methods, datasets, and metrics others have used |
| **Position your work** | Show how your work fits in and extends existing knowledge |
| **Establish credibility** | Proves you understand the field |

### Types of Sources

#### Primary Sources (Most Important for Research)
Direct, first-hand accounts of original research:
- **Research papers** (journal articles, conference papers)
- **Theses and dissertations**
- **Technical reports**
- **Patents**
- **Raw data/datasets**

> *Example:* The original "Attention Is All You Need" paper by Vaswani et al. (2017) is a primary source.

#### Secondary Sources
Interpret, analyze, or summarize primary sources:
- **Review articles** / Survey papers
- **Textbooks**
- **Handbooks**
- **Meta-analyses**

> *Example:* A survey paper titled "A Review of Transformer Architectures in NLP (2017–2024)" is a secondary source.

#### Tertiary Sources
Compilations that point you to primary and secondary sources:
- **Encyclopedias** (e.g., Encyclopedia of Machine Learning)
- **Bibliographies, indexes, abstracts**
- **Directories**

### Where to Search for Literature

| Database | Best For | URL |
|----------|---------|-----|
| **Google Scholar** | Broad search across all fields | scholar.google.com |
| **IEEE Xplore** | Electrical engineering, CS, AI | ieeexplore.ieee.org |
| **ACM Digital Library** | Computer science specifically | dl.acm.org |
| **Scopus** | Multi-disciplinary, citation analysis | scopus.com |
| **Web of Science** | High-quality indexed journals | webofscience.com |
| **arXiv** | Preprints (latest, not peer-reviewed) | arxiv.org |
| **PubMed** | Biomedical, healthcare AI | pubmed.ncbi.nlm.nih.gov |
| **Semantic Scholar** | AI-powered literature search | semanticscholar.org |
| **DBLP** | CS bibliography | dblp.org |
| **Papers With Code** | Papers with linked code & benchmarks | paperswithcode.com |

### How to Conduct a Literature Review

#### Step 1: Define Your Search Terms
- Start with key concepts from your research problem
- Use synonyms and related terms
- *Example:* For "hate speech detection in Hindi", search for: `"hate speech" AND ("Hindi" OR "code-mixed" OR "Devanagari")`, `"offensive language detection" AND "Indian languages"`, `"abusive content" AND "multilingual NLP"`

#### Step 2: Search Systematically
- Use Boolean operators: AND, OR, NOT
- Use quotation marks for exact phrases: "transfer learning"
- Use filters: year range, publication type, subject area

#### Step 3: Screen and Select
- Read titles and abstracts first — is it relevant?
- Apply inclusion/exclusion criteria
- Typically, you'll find 200+ papers in initial search → narrow to 50-80 highly relevant ones

#### Step 4: Read and Extract Information
For each paper, note:
- **Authors, year, venue** (publication details)
- **Problem addressed** (what they studied)
- **Method used** (how they did it)
- **Dataset** (what data they used)
- **Key results** (what they found — accuracy, F1, etc.)
- **Limitations** (what they couldn't do)
- **Relevance to your work** (how it connects to your research)

#### Step 5: Organize and Synthesize
Don't just summarize paper by paper. Organize **thematically**:

> **Bad approach (paper-by-paper):**
> "Smith (2020) did X. Jones (2021) did Y. Lee (2022) did Z."

> **Good approach (thematic):**
> "Hate speech detection has been approached using three main paradigms: (1) Traditional ML with handcrafted features (Smith, 2020; Brown, 2019), (2) Deep learning with word embeddings (Jones, 2021; Lee, 2022), and (3) Transformer-based pre-trained models (Kumar, 2023; Patel, 2024). While approaches (1) and (2) have shown accuracy up to 78% on Hindi data, transformer-based methods remain largely unexplored for Hindi-English code-mixed text, which is the gap this research addresses."

#### Step 6: Identify the Gap
After reviewing all literature, clearly state what has NOT been done:
> "While extensive work exists on hate speech detection in English, only 3 studies address Hindi-English code-mixed text, and none of them use multilingual transformer models fine-tuned specifically on Indian social media data."

### Types of Literature Review Methods

| Method | Description | When to use |
|--------|------------|-------------|
| **Narrative Review** | General overview, less structured, author's interpretation | When exploring a broad topic |
| **Systematic Review** | Follows a strict, predefined protocol with explicit criteria | For comprehensive, unbiased coverage |
| **Meta-Analysis** | Statistical combination of results from multiple studies | When you want a quantitative summary |
| **Bibliometric Analysis** | Analyzes publication patterns, citation networks, trending topics | Understanding the landscape of a research area |
| **Scoping Review** | Maps the breadth of literature on a topic without assessing quality | When the topic is broad and not well-defined |

---

## 2.5 Hypothesis

### What is a Hypothesis?

A **hypothesis** is a tentative, testable statement that predicts the relationship between two or more variables.

Think of it as an **educated guess** based on existing knowledge that can be **tested** and either **supported or rejected** through data.

### Types of Hypotheses

#### 1. Null Hypothesis (H₀)
States that there is **no significant difference, effect, or relationship**.
> H₀: "There is no significant difference in classification accuracy between BERT and LSTM for Hindi sentiment analysis."

This is the hypothesis we **try to reject** through statistical testing.

#### 2. Alternative Hypothesis (H₁ or Hₐ)
States that there **IS** a significant difference, effect, or relationship.
> H₁: "BERT achieves significantly higher classification accuracy than LSTM for Hindi sentiment analysis."

This is what the researcher **hopes to demonstrate**.

#### 3. Directional vs. Non-Directional

| Type | Statement | Example |
|------|-----------|---------|
| **Directional** (one-tailed) | Predicts the DIRECTION of the difference | "BERT will perform **better** than LSTM" |
| **Non-directional** (two-tailed) | Predicts a difference exists but not its direction | "BERT and LSTM will perform **differently**" |

### Characteristics of a Good Hypothesis

| Characteristic | Meaning |
|---------------|---------|
| **Testable** | Can be tested with empirical data and experiments |
| **Falsifiable** | Must be possible to prove it wrong (Karl Popper's criterion) |
| **Specific** | Precisely states the expected relationship |
| **Clear** | Written in simple, unambiguous language |
| **Relevant** | Related to the research problem |
| **Grounded** | Based on existing knowledge, theory, or prior research |

### Examples of Good vs. Bad Hypotheses

| Bad Hypothesis | Problem | Good Hypothesis |
|---------------|---------|-----------------|
| "Deep learning is better" | Too vague — better than what? At what? | "ResNet-50 achieves higher accuracy than VGG-16 on CIFAR-100 image classification" |
| "AI will change the world" | Not testable or specific | "Implementing AI-based triage reduces average ER wait time by at least 15%" |
| "Students like online learning" | Vague, not measurable | "Students using AI tutoring tools score at least 10% higher on assessments than those using traditional methods" |

### How Hypothesis Testing Works (Preview)

```
Start with H₀ (no effect) and H₁ (there IS an effect)
          ↓
Collect data and run experiment
          ↓
Apply statistical test (t-test, ANOVA, etc.)
          ↓
Get p-value
          ↓
If p-value < α (significance level, usually 0.05):
    → Reject H₀ → Support H₁ → "Significant result"
If p-value ≥ α:
    → Fail to reject H₀ → "No significant evidence for H₁"
```

> **Important:** We never "prove" H₁ or "accept" H₀. We either **reject H₀** or **fail to reject H₀**.

---

## 2.6 Theoretical Framework and Conceptual Framework

### Theoretical Framework
A structure based on **existing theories** that guides your research.
> *Example:* Using the Technology Acceptance Model (TAM) to study adoption of AI tools in education. TAM provides the theory that perceived usefulness and perceived ease of use influence technology adoption.

### Conceptual Framework
A **visual or narrative representation** of the key variables and their relationships in YOUR specific study.

```
Example Conceptual Framework:

Independent Variables          Dependent Variable
┌─────────────────────┐       ┌──────────────────┐
│ Model Architecture  │──────→│                  │
│ (BERT, LSTM, CNN)   │       │  Classification  │
├─────────────────────┤       │  Accuracy (F1)   │
│ Training Data Size  │──────→│                  │
│ (500, 1000, 5000)   │       │                  │
├─────────────────────┤       └──────────────────┘
│ Preprocessing       │──────→        ↑
│ (with/without aug.) │       ┌───────┴──────────┐
└─────────────────────┘       │ Control Variables │
                              │ - Same test set   │
                              │ - Same hardware   │
                              │ - Same epochs     │
                              └──────────────────┘
```

---

## 2.7 Practice Questions

**Q1.** List three sources from which a researcher can identify a research problem.
> **Answer:** (1) Gaps identified in existing literature, (2) Practical problems observed in industry/society, (3) Recommendations from the "Future Work" section of published research papers.

**Q2.** What is the difference between a primary source and a secondary source?
> **Answer:** A primary source is the original research itself (e.g., a research paper reporting new experimental results). A secondary source interprets or summarizes primary sources (e.g., a review article or textbook chapter).

**Q3.** Write a null hypothesis and an alternative hypothesis for a study comparing the performance of Random Forest and XGBoost on a fraud detection dataset.
> **Answer:**
> - H₀: There is no significant difference in AUC-ROC between Random Forest and XGBoost for fraud detection.
> - H₁: XGBoost achieves a significantly higher AUC-ROC than Random Forest for fraud detection.

**Q4.** Why should a literature review be organized thematically rather than paper-by-paper?
> **Answer:** Thematic organization synthesizes findings across multiple papers under common themes, making it easier to identify patterns, contradictions, and gaps. Paper-by-paper organization reads like a list of summaries and fails to show how different works relate to each other.

**Q5.** What is the role of Boolean operators in literature searching?
> **Answer:** Boolean operators (AND, OR, NOT) help refine search queries. AND narrows results (both terms must appear), OR broadens results (either term), and NOT excludes results. Example: `"deep learning" AND "medical imaging" NOT "survey"` finds original deep learning medical imaging papers while excluding survey papers.

---

*Previous: [Chapter 1 — Introduction to Research](01_Introduction_to_Research.md) | Next: [Chapter 3 — Research Design](03_Research_Design.md)*

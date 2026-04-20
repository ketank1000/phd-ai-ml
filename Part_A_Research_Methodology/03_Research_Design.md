# 3. Research Design

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 3.1 What is a Research Design?

A **research design** is the overall plan or blueprint that specifies how data will be collected, measured, and analyzed to answer the research questions. It is the framework that connects the research problem to the data collection and analysis strategy.

Think of it as the **architecture** of your research — just as an architect designs a building before construction begins, you design your research before collecting data.

### Key Decisions in Research Design:
1. **What** type of study? (experimental, survey, case study, etc.)
2. **Who** will be studied? (population, sample)
3. **How** will data be collected? (instruments, procedures)
4. **When** will data be collected? (one time, over months?)
5. **Where** will data be collected? (lab, field, online?)
6. **How** will data be analyzed? (statistical methods)

---

## 3.2 Types of Research Design

### 3.2.1 Experimental Design

**What it is:** The researcher **manipulates** the independent variable (IV) and **measures** its effect on the dependent variable (DV), while **controlling** all other variables.

**Key requirement:** Random assignment of subjects to groups.

**Why it matters:** The ONLY design that can establish **cause-and-effect** relationships.

#### Structure of a Classic Experiment:

```
Random Assignment
     ├──→ Experimental Group → Receives Treatment → Measure DV
     └──→ Control Group      → No Treatment      → Measure DV
                                                      ↓
                                              Compare results
```

#### Example in AI Research:
> **Research Question:** Does data augmentation improve image classification accuracy?
>
> **Setup:**
> - IV (manipulated): Data augmentation (with vs. without)
> - DV (measured): Test accuracy on CIFAR-10
> - Control variables: Same model (ResNet-18), same learning rate (0.001), same epochs (100), same hardware
>
> - Experimental group: Train ResNet-18 WITH augmentation (flip, rotate, crop)
> - Control group: Train ResNet-18 WITHOUT augmentation
> - Run each experiment 5 times with different random seeds
> - Compare mean accuracy using a t-test

#### Types of Experimental Designs:

| Design | Description | Example |
|--------|-------------|---------|
| **Pre-test/Post-test Control Group** | Measure DV before AND after treatment in both groups | Test students before AI tutoring, apply tutoring to experimental group, test again |
| **Post-test Only Control Group** | Measure DV only after treatment (no pre-test) | Compare accuracy of augmented vs. non-augmented models (no "before" measurement) |
| **Solomon Four-Group** | Combines pre-test/post-test with post-test only (4 groups total) | Most rigorous; controls for pre-test sensitization |
| **Factorial Design** | Tests TWO or more IVs simultaneously | Test both augmentation (yes/no) AND learning rate (0.01/0.001) → 4 combinations (2×2 factorial) |

#### Factorial Design Example (2×2):

```
                    Learning Rate
                    0.01        0.001
Augmentation: Yes   Group A     Group B
              No    Group C     Group D
```
This lets you study the **main effect** of each variable AND their **interaction effect** (does augmentation help more with a higher learning rate?).

### 3.2.2 Quasi-Experimental Design

**What it is:** Similar to experimental design BUT **without random assignment**. The researcher manipulates the IV but uses pre-existing groups.

**Why use it?** Random assignment is often impossible in real-world settings.

**Example:**
> Comparing the performance of students in two existing sections of a class — one using AI-assisted learning, the other not. You can't randomly assign students to sections (they're already enrolled).

**Limitation:** Because there's no random assignment, there may be pre-existing differences between groups that confound the results.

### 3.2.3 Non-Experimental (Observational) Design

**What it is:** The researcher does NOT manipulate any variable. Simply observes and measures variables as they naturally occur.

**Types:**

#### Descriptive Design
Describes "what is" — the current state of affairs.
> **Example:** "A survey of 500 Indian IT companies to determine the percentage that use AI/ML in production systems."

#### Correlational Design
Examines the relationship between two variables (but does NOT establish causation).
> **Example:** "Is there a correlation between the number of GitHub contributions and job salary among Indian developers?"
>
> **Important:** Finding a correlation does NOT mean one causes the other!
> "Ice cream sales correlate with drowning deaths" — they don't cause each other; both are caused by summer heat (confounding variable).

#### Case Study Design
In-depth investigation of a single individual, group, event, or organization.
> **Example:** "A detailed case study of how Flipkart implemented its recommendation system — challenges, solutions, and outcomes."

### 3.2.4 Time-Based Designs

| Design | Data Collection | Example |
|--------|----------------|---------|
| **Cross-Sectional** | Data collected at ONE point in time (snapshot) | Survey of AI tool usage among developers in April 2026 |
| **Longitudinal** | Data collected at MULTIPLE time points | Tracking the same 200 developers' AI tool usage every 6 months for 3 years |
| **Panel Study** | Longitudinal with the SAME subjects each time | Following 100 specific companies' AI adoption from 2024-2027 |
| **Trend Study** | Longitudinal with DIFFERENT subjects (same population) each time | Surveying different sets of graduates each year about AI skill readiness |

---

## 3.3 Variables in Research

A **variable** is any characteristic, attribute, or quantity that can take on different values.

### Types of Variables:

#### Independent Variable (IV)
The variable that the researcher **manipulates** or changes. It is the **cause**.
> *Example:* The learning rate used for training → {0.001, 0.01, 0.1}

#### Dependent Variable (DV)
The variable that is **measured** as the outcome. It is the **effect**.
> *Example:* Test accuracy of the model

#### Control Variable (Constant)
Variables that are **held constant** so they don't influence the results.
> *Example:* Same dataset, same model architecture, same number of epochs

#### Confounding Variable (Extraneous)
An unwanted variable that **accidentally varies** with the IV, making it hard to know if the IV or the confounder caused the effect.
> *Example:* If you test different models on different hardware, hardware speed is a confounder — you can't tell if better accuracy is due to the model or the faster GPU.

#### Moderating Variable
A variable that **changes the strength or direction** of the relationship between IV and DV.
> *Example:* Dataset size MODERATES the effect of model complexity on accuracy. A complex model might perform better on large datasets but worse on small ones.

```
IV (Model Complexity) ──→ DV (Accuracy)
                            ↑
                   Moderator (Dataset Size)
```

#### Mediating Variable
A variable that **explains the mechanism** through which the IV affects the DV.
> *Example:* Data augmentation → increases training data diversity → improves accuracy

```
IV (Augmentation) ──→ Mediator (Data Diversity) ──→ DV (Accuracy)
```

### Variable Relationship Summary:

```
Independent Variable ──causes──→ Dependent Variable
        ↑                              ↑
   Controlled by                  Influenced by
   researcher                     confounder (unwanted)
                                  moderator (changes strength)
                                  mediator (explains mechanism)
```

---

## 3.4 Validity

**Validity** answers the question: "Are we measuring what we think we're measuring, and are our conclusions trustworthy?"

### Types of Validity:

#### 1. Internal Validity
**Question:** Did the IV actually cause the change in DV, or was it something else?

**High internal validity** = You can confidently say the IV caused the effect.
**Threats to internal validity:**

| Threat | Meaning | Example |
|--------|---------|---------|
| **History** | External events occur during the study | A new pre-trained model is released midway through your experiment |
| **Maturation** | Subjects change naturally over time | Students get better at coding simply through practice, not because of the AI tutor |
| **Selection bias** | Groups are not equivalent at the start | The "AI tutor" group had smarter students to begin with |
| **Testing effect** | The act of being tested changes behavior | Pre-test makes students aware of what to study |
| **Instrumentation** | Measurement tools change during the study | You update your evaluation metric midway |
| **Attrition** | Subjects drop out during the study | Weaker students leave the study, making the remaining group look better |

**How to improve internal validity:**
- Random assignment to groups
- Use control groups
- Blind/double-blind procedures
- Control for confounders

#### 2. External Validity
**Question:** Can the results be generalized to other populations, settings, and times?

**Example of poor external validity:** You test your model only on MNIST digits and claim it works for "all image classification tasks."

**How to improve:** Test on diverse datasets, populations, and conditions.

#### 3. Construct Validity
**Question:** Does the test/instrument truly measure the theoretical construct it claims to measure?

**Example:** If you're studying "intelligence" of an AI system, is measuring accuracy on one benchmark really measuring "intelligence"? Maybe it's only measuring performance on that specific task.

**How to improve:** Use multiple measures for the same construct, validate against known standards.

#### 4. Content Validity
**Question:** Does the test cover the full range of the concept being measured?

**Example:** If an exam claims to test "machine learning knowledge," but only asks about supervised learning and ignores unsupervised, reinforcement, and deep learning, it has poor content validity.

**How to ensure:** Expert review, comprehensive coverage of all aspects.

#### 5. Face Validity
**Question:** Does the test APPEAR to measure what it claims? (superficial check)

**Note:** This is the weakest form of validity — something can "look right" but actually measure the wrong thing.

---

## 3.5 Reliability

**Reliability** answers the question: "If we repeat the measurement, will we get the same result?"

A reliable measure is **consistent** and **stable**.

### Types of Reliability:

| Type | What it checks | How it's measured | Example |
|------|---------------|------------------|---------|
| **Test-Retest** | Consistency OVER TIME | Give the same test twice to the same group, correlate scores | A survey gives similar results when administered 2 weeks apart |
| **Inter-Rater** | Agreement BETWEEN observers | Two evaluators rate the same items, compute agreement (Cohen's Kappa) | Two annotators label the same 1000 tweets for sentiment — do they agree? |
| **Internal Consistency** | Consistency WITHIN the test | Cronbach's Alpha (α) | Survey questions about "AI readiness" — do all items measure the same thing? |
| **Split-Half** | Consistency between two halves of a test | Split test in half, correlate scores | Odd-numbered vs. even-numbered questions should give similar results |

### Cronbach's Alpha Interpretation:

| Alpha (α) Value | Interpretation |
|-----------------|---------------|
| α ≥ 0.90 | Excellent |
| 0.80 ≤ α < 0.90 | Good |
| 0.70 ≤ α < 0.80 | Acceptable |
| 0.60 ≤ α < 0.70 | Questionable |
| 0.50 ≤ α < 0.60 | Poor |
| α < 0.50 | Unacceptable |

### Reliability vs. Validity — Key Relationship

```
A measure can be reliable but NOT valid:
   → A broken scale that always reads 5 kg heavier is reliable (consistent)
     but not valid (not accurate).

A measure CANNOT be valid without being reliable:
   → If results change randomly every time, it can't be measuring
     the right thing. Validity requires reliability as a prerequisite.
```

| | Reliable | Not Reliable |
|---|---------|-------------|
| **Valid** | ✅ Ideal — consistent AND accurate | ❌ Impossible |
| **Not Valid** | ⚠️ Consistently wrong | ❌ Inconsistent and wrong |

**Archery analogy:**
- **Reliable + Valid:** All arrows hit the bullseye 🎯
- **Reliable + Not Valid:** All arrows hit the same spot, but it's not the bullseye
- **Not Reliable + Not Valid:** Arrows are scattered everywhere

---

## 3.6 Practice Questions

**Q1.** A researcher trains 3 different model architectures on the same dataset and compares their accuracy. What type of research design is this?
> **Answer:** Experimental design. The IV is the model architecture (manipulated), the DV is accuracy (measured), and the dataset is a control variable (kept constant).

**Q2.** What is the key difference between an experimental and a quasi-experimental design?
> **Answer:** In a true experimental design, subjects are **randomly assigned** to groups. In a quasi-experimental design, the researcher uses **pre-existing groups** without random assignment (e.g., two existing classrooms).

**Q3.** A researcher finds that GPU usage correlates with publication count in AI research. Can they conclude that using more GPUs CAUSES more publications?
> **Answer:** No. Correlation does not imply causation. There could be a confounding variable — well-funded labs (confounder) may have both more GPUs and more researchers, leading to more publications.

**Q4.** What is the difference between a moderating variable and a mediating variable?
> **Answer:** A **moderator** changes the STRENGTH of the IV→DV relationship (e.g., dataset size affects how much model complexity impacts accuracy). A **mediator** explains the MECHANISM through which IV affects DV (e.g., augmentation → increased diversity → better accuracy).

**Q5.** A survey about "AI readiness" gives very different results when the same employees retake it one week later. What type of reliability is lacking?
> **Answer:** Test-retest reliability. The measure is not consistent over time.

---

*Previous: [Chapter 2 — Research Problem & Literature Review](02_Research_Problem_and_Literature_Review.md) | Next: [Chapter 4 — Sampling Techniques](04_Sampling_Techniques.md)*

# 7. Research Ethics

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 7.1 Plagiarism

### Definition
Presenting someone else's work, ideas, text, data, or creative output as your own, without proper acknowledgment. This is the most common and serious ethical violation in academia.

### Types of Plagiarism

| Type | Description | Example |
|------|-------------|---------|
| **Verbatim (Direct)** | Copying text word-for-word without quotation marks or citation | Copy-pasting a paragraph from a paper into your thesis |
| **Mosaic (Patchwork)** | Mixing copied phrases from multiple sources, rearranging slightly | Taking sentences from 3 different papers and stitching them together |
| **Paraphrasing without citation** | Rewording someone's idea but not giving credit | Rephrasing a novel algorithm description without citing the original paper |
| **Self-plagiarism** | Reusing your own previously published work without disclosure | Submitting the same paper to two different conferences |
| **Idea plagiarism** | Using someone's original idea/concept without attribution | Claiming a novel approach that was actually proposed by another researcher |
| **Data/Image plagiarism** | Using someone's data, figures, or graphs without permission/citation | Using a graph from another paper in your presentation |

### How to Avoid Plagiarism

1. **Always cite your sources** — when in doubt, cite
2. **Use quotation marks** for direct quotes (and still cite)
3. **Paraphrase properly** — truly rewrite in your own words AND cite the source
4. **Keep track of all sources** while reading — use reference managers
5. **Use plagiarism detection tools** before submission

### Plagiarism Detection Tools

| Tool | Used By | Notes |
|------|---------|-------|
| **Turnitin** | Most universities globally | Industry standard, checks against massive database |
| **iThenticate** | Journal publishers, researchers | Used by IEEE, Springer, Elsevier |
| **Urkund (Ouriginal)** | European universities | Now part of Turnitin |
| **Grammarly** | Individual use | Basic plagiarism check included |
| **Copyleaks** | Universities, businesses | AI-powered detection |

### Consequences of Plagiarism
- Paper retraction (removed from journal)
- Academic penalties (failing grade, suspension, expulsion)
- Degree revocation (even years after graduation)
- Loss of research funding
- Permanent damage to professional reputation
- Legal consequences (copyright infringement)

---

## 7.2 Ethical Principles in Research

### 7.2.1 Informed Consent

Participants must be told:
- The **purpose** of the research
- What **participation involves** (time, tasks, risks)
- That participation is **voluntary**
- That they can **withdraw at any time** without penalty
- How their **data will be used** and stored

**Format:** Written consent form, signed by participant (or digital equivalent)

**When informed consent can be waived:**
- Retrospective analysis of anonymized public data
- Analysis of publicly available datasets (e.g., Twitter data that is already public)
- When research involves minimal risk and consent is impractical

### 7.2.2 Confidentiality and Anonymity

| Concept | Definition | Example |
|---------|-----------|---------|
| **Confidentiality** | Data is collected with identifiers but not disclosed | Researcher knows who said what, but doesn't reveal it |
| **Anonymity** | No identifying information is collected at all | Survey responses cannot be linked to any individual |

**Data protection practices:**
- Encrypt sensitive data
- Use participant codes instead of names (P001, P002, ...)
- Store consent forms separately from data
- Comply with data protection laws (GDPR in EU, IT Act in India)

### 7.2.3 No Harm to Participants

The Belmont Report (1979) established three core principles:

| Principle | Meaning |
|-----------|---------|
| **Respect for Persons** | Treat people as autonomous agents; protect those with diminished autonomy |
| **Beneficence** | Maximize benefits, minimize potential harm |
| **Justice** | Fair distribution of research benefits and burdens |

**Types of harm to consider:**
- Physical harm (rare in CS research)
- Psychological harm (stress, anxiety from sensitive survey questions)
- Social harm (stigmatization if participation is known)
- Economic harm (time lost, opportunity cost)
- Digital harm (data breaches, privacy violations)

### 7.2.4 Institutional Ethics Review

Before conducting research with human participants, you typically need approval from:
- **Institutional Ethics Committee (IEC)** — in Indian universities
- **Institutional Review Board (IRB)** — in US universities
- **Ethics Committee** — in European institutions

**Process:**
1. Submit research proposal with methodology details
2. Include consent forms, questionnaires, risk assessment
3. Committee reviews and may request modifications
4. Approval granted → you can begin data collection
5. Report any adverse events during the study

---

## 7.3 Publication Ethics

### 7.3.1 Authorship

**ICMJE (International Committee of Medical Journal Editors) Criteria:**
All four conditions must be met for authorship:

1. **Substantial contribution** to conception/design, or data acquisition/analysis
2. **Drafting** the article or **critically revising** it for intellectual content
3. **Final approval** of the version to be published
4. **Accountability** for all aspects of the work

**Problematic Authorship Practices:**

| Practice | Description | Ethical? |
|----------|-------------|----------|
| **Gift authorship** | Adding someone who didn't contribute (e.g., department head) | No |
| **Ghost authorship** | Not listing someone who DID contribute (e.g., a student who did the work) | No |
| **Author order disputes** | Disagreements about who is first/last author | Resolve early |

**Author Order Convention in CS:**
- **First author:** Did the most work (usually the PhD student)
- **Last author:** Senior researcher / supervisor / PI
- **Corresponding author:** Handles communication with the journal

### 7.3.2 Peer Review Process

```
Author submits manuscript
         │
    Editor screens
    (desk reject?)
    ├── Yes → Rejected
    └── No  ↓
    Sent to 2-3 reviewers
    (4-12 weeks typically)
         │
    Reviews returned
         │
    Editor decision:
    ├── Accept (rare on first submission)
    ├── Minor revisions
    ├── Major revisions
    └── Reject
         │
    Author revises & resubmits
    (with response letter)
         │
    Second round review
         │
    Final decision: Accept/Reject
```

**Types of Peer Review:**

| Type | Description |
|------|-------------|
| **Single-blind** | Reviewers know authors; authors don't know reviewers (most common) |
| **Double-blind** | Neither authors nor reviewers know each other's identity |
| **Open review** | Both identities known; reviews may be published |
| **Post-publication** | Review happens after publication (e.g., PubPeer comments) |

### 7.3.3 Predatory Journals

Fake or low-quality journals that charge fees but provide little or no peer review.

**How to identify predatory journals:**
- Unsolicited email invitations to submit
- Extremely fast "peer review" (days instead of weeks/months)
- No established editorial board or fake board members
- Not indexed in reputable databases (Scopus, Web of Science)
- Poor grammar on the journal website
- Unclear or hidden publisher contact information
- Journal scope is suspiciously broad ("all areas of science")

**Tools to verify:**
- Beall's List (list of predatory publishers)
- Think. Check. Submit. (thinkchecksubmit.org)
- DOAJ (Directory of Open Access Journals) — legitimate OA journals
- UGC-CARE list (approved journals for Indian researchers)

### 7.3.4 Open Access vs. Subscription

| Model | Access | Cost to Author | Examples |
|-------|--------|----------------|---------|
| **Subscription** | Behind paywall, institutions pay | Free to publish | IEEE, Elsevier (many) |
| **Gold OA** | Free to read immediately | Author pays APC (Article Processing Charge) ₹50K-₹5L+ | PLOS ONE, MDPI |
| **Green OA** | Author self-archives preprint/postprint | Free | arXiv, institutional repositories |
| **Hybrid** | Some articles OA, others paywalled | Optional APC for OA option | Many Springer/Wiley journals |

---

## 7.4 Intellectual Property Rights (IPR)

### Types of IP Protection

| Type | What It Protects | Duration | Example |
|------|-----------------|----------|---------|
| **Copyright** | Original creative works (text, code, music, art) | Author's lifetime + 60 years (India) | Research paper, book, software source code |
| **Patent** | Inventions (novel, useful, non-obvious product/process) | 20 years from filing | A novel neural network architecture, a compression algorithm |
| **Trademark** | Brand identity (names, logos, slogans) | 10 years, renewable indefinitely | "TensorFlow™", Google logo |
| **Trade Secret** | Confidential business information | As long as it remains secret | Google's search ranking algorithm |
| **Industrial Design** | Aesthetic design of a product | 10 years (+ 5 year renewal, India) | The physical design of a smartphone |

### Software Licensing

| License | Key Feature | Can Use in Commercial? | Must Share Source? |
|---------|-------------|----------------------|-------------------|
| **MIT** | Very permissive, minimal restrictions | Yes | No |
| **Apache 2.0** | Like MIT + patent protection | Yes | No |
| **GPL v3** | Copyleft — derivatives must also be GPL | Yes | Yes (if distributed) |
| **LGPL** | Like GPL but allows linking from proprietary code | Yes | Only modifications to the library |
| **BSD** | Very permissive, similar to MIT | Yes | No |
| **Creative Commons (CC)** | For non-software works (papers, datasets) | Depends on variant | Depends on variant |

**Creative Commons Variants:**

| License | Meaning |
|---------|---------|
| **CC BY** | Attribution only — most permissive |
| **CC BY-SA** | Attribution + ShareAlike (derivatives must use same license) |
| **CC BY-NC** | Attribution + NonCommercial |
| **CC BY-ND** | Attribution + NoDerivatives |
| **CC0** | Public domain — no rights reserved |

---

## 7.5 Research Integrity and Misconduct

### The Three Big Sins of Research Misconduct (FFP)

| Misconduct | Definition | Example |
|-----------|-----------|---------|
| **Fabrication** | Making up data or results | Reporting experiment results for an experiment that was never conducted |
| **Falsification** | Manipulating data, equipment, or processes; changing/omitting results | Removing data points that don't support your hypothesis; cherry-picking results |
| **Plagiarism** | Using others' work without credit (detailed in Section 7.1) | Copy-pasting from another paper |

### Questionable Research Practices (QRP)

Not outright misconduct, but ethically problematic:

| Practice | Description |
|----------|-------------|
| **P-hacking** | Running many statistical tests until you find p < 0.05, then reporting only that one |
| **HARKing** | Hypothesizing After Results are Known — presenting a post-hoc finding as if it were predicted |
| **Salami slicing** | Breaking one study into many thin papers to inflate publication count |
| **Selective reporting** | Reporting only the results that support your hypothesis |
| **Data dredging** | Mining data for patterns without a prior hypothesis |

### How to Maintain Integrity

1. **Pre-register** your study (state hypotheses BEFORE collecting data) — OSF, ClinicalTrials.gov
2. **Share data and code** when possible (reproducibility)
3. **Report negative results** (not just positive ones)
4. **Declare conflicts of interest**
5. **Follow responsible AI principles** (fairness, transparency, accountability)

---

## 7.6 Ethics in AI/ML Research (Especially Relevant)

| Ethical Issue | Description | Example |
|--------------|-------------|---------|
| **Bias in training data** | Models learn and amplify societal biases | Facial recognition performing poorly on dark-skinned individuals |
| **Privacy** | Models may memorize sensitive training data | GPT models leaking personal information from training data |
| **Consent for data use** | Was data collected with proper consent? | Scraping social media photos for facial recognition without user consent |
| **Deepfakes** | AI-generated fake content | Generating realistic fake videos of public figures |
| **Autonomous weapons** | AI in military applications | Lethal autonomous weapon systems (LAWS) |
| **Job displacement** | AI replacing human workers | Automation of customer service, content creation |
| **Explainability** | Black-box models making critical decisions | AI denying loans without explanation |

---

## 7.7 Practice Questions

**Q1.** A PhD student copy-pastes two paragraphs from a Wikipedia article into their literature review, changing a few words. Is this plagiarism? What type?
> **Answer:** Yes, this is **mosaic (patchwork) plagiarism**. Even though some words were changed, the structure and ideas are directly taken from the source without proper citation. Changing a few words is not adequate paraphrasing. The student should rewrite entirely in their own words, and cite Wikipedia (though academic sources are preferred over Wikipedia).

**Q2.** What are the ICMJE criteria for authorship? A professor adds their name to a student's paper despite contributing nothing beyond providing lab access. Is this ethical?
> **Answer:** ICMJE requires: (1) substantial contribution to design/data/analysis, (2) drafting or critical revision, (3) final approval, and (4) accountability. Providing lab access alone does NOT meet criterion 1. This is **gift/honorary authorship** and is unethical.

**Q3.** You develop an ML model trained on a public Kaggle dataset. What IPR and licensing considerations should you check?
> **Answer:** Check the **license** of the Kaggle dataset (CC BY, CC0, competition-specific rules, etc.). If it's CC BY, you must give attribution. If it's competition-specific, you may be restricted from commercial use. For your model: you own the copyright on your code, but the trained weights may have restrictions derived from the training data license. If using pre-trained models (e.g., from Hugging Face), check their license too (some are Apache 2.0, others are restricted).

**Q4.** Explain the difference between copyright and patent with an example from computer science.
> **Answer:** **Copyright** protects the expression/implementation (the actual code you wrote for a sorting algorithm — your specific code is copyrighted). **Patent** protects the invention/idea (a novel algorithm itself — the concept, regardless of how it's coded, can be patented if it meets novelty, utility, and non-obviousness criteria). You could write your own code for a patented algorithm and still infringe the patent, even though the code itself has its own copyright.

**Q5.** What is "p-hacking" and why is it a problem? How can it be prevented?
> **Answer:** **P-hacking** is the practice of running many different statistical tests, trying different variable combinations, or repeatedly collecting data until a statistically significant result (p < 0.05) is found by chance. It's problematic because it inflates the false positive rate — with 20 tests at α = 0.05, you'd expect one "significant" result purely by chance. **Prevention:** Pre-register hypotheses and analysis plans before data collection, apply multiple comparison corrections (Bonferroni), report all analyses conducted (not just significant ones), and use effect sizes rather than relying solely on p-values.

---

*Previous: [Chapter 6 — Statistical Analysis](06_Statistical_Analysis.md) | Next: [Chapter 8 — Report Writing & Thesis Structure](08_Report_Writing_and_Thesis_Structure.md)*

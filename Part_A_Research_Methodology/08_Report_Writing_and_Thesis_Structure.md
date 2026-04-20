# 8. Report Writing & Thesis Structure

> **Part A — Research Methodology** | SIU PET Complete Study Guide

---

## 8.1 Structure of a PhD Thesis / Dissertation

A standard PhD thesis in Computer Engineering / AI-ML follows this structure:

### Front Matter

| Component | Description |
|-----------|-------------|
| **Title Page** | Title, author name, degree (PhD), university, year |
| **Declaration** | Statement that the work is original and conducted by the author |
| **Certificate** | Signed by supervisor(s) certifying the work |
| **Acknowledgements** | Thank supervisor, institution, funding agency, family |
| **Abstract** | 300-500 word summary of the ENTIRE thesis (problem, method, key results, conclusion) |
| **Table of Contents** | Auto-generated chapter/section listing with page numbers |
| **List of Figures** | All figures with captions and page numbers |
| **List of Tables** | All tables with captions and page numbers |
| **List of Abbreviations** | CNN, NLP, LSTM, etc. — define all abbreviations used |

### Main Body — Chapter by Chapter

**Chapter 1: Introduction**
- Background and context of the research area
- Problem statement (what gap exists?)
- Research questions / objectives
- Motivation (why is this important?)
- Scope and limitations
- Contributions of the thesis (what's new?)
- Organization of the thesis (brief summary of each chapter)

> *Example:* "This thesis addresses the gap in efficient real-time object detection for resource-constrained edge devices. Existing models like YOLOv5 achieve high accuracy but require significant computational resources..."

**Chapter 2: Literature Review**
- Comprehensive survey of existing work
- Organized thematically or chronologically
- Critical analysis (not just summaries — compare, contrast, critique)
- Research gap identification
- Summary table of related works

> *Tip:* Use a comparison table:
> | Author (Year) | Method | Dataset | Accuracy | Limitation |
> |--------------|--------|---------|----------|-----------|
> | Smith (2022) | CNN+LSTM | IMDB | 89.2% | Slow inference |
> | Lee (2023) | Transformer | SST-2 | 92.1% | High memory |
> | **Proposed** | LightTransformer | Both | 91.5% | — |

**Chapter 3: Research Methodology**
- Research design (experimental, comparative, etc.)
- Dataset description (source, size, preprocessing)
- Proposed model/algorithm architecture (with diagrams)
- Experimental setup (hardware, software, hyperparameters)
- Evaluation metrics (accuracy, precision, recall, F1, etc.)
- Baseline methods for comparison

**Chapter 4: Results and Analysis**
- Experimental results presented in tables and graphs
- Statistical analysis of results
- Comparison with baselines and state-of-the-art
- Ablation studies (removing components to test their contribution)
- Qualitative examples (sample predictions, visualizations)

**Chapter 5: Discussion**
- Interpret the results — what do they MEAN?
- Why did the proposed method work (or not work)?
- Comparison with findings from literature
- Practical implications
- Unexpected findings and possible explanations

**Chapter 6: Conclusion and Future Work**
- Summary of contributions (2-3 key contributions)
- Limitations of the study
- Future research directions
- Closing statement on the significance of the work

### Back Matter

| Component | Description |
|-----------|-------------|
| **References / Bibliography** | All cited works in a consistent format (IEEE for CS) |
| **Appendices** | Supplementary material: code snippets, questionnaires, additional tables, proofs |
| **Publications** | List of papers published during the PhD |

---

## 8.2 Writing the Abstract

The abstract is the most-read part of any thesis or paper. It must stand alone — someone should understand your work from JUST the abstract.

### Structure (IMRaD for abstracts)

| Part | Content | Approximate Length |
|------|---------|-------------------|
| **Background** | Context and problem | 1-2 sentences |
| **Objective** | What you set out to do | 1 sentence |
| **Method** | How you did it | 2-3 sentences |
| **Results** | Key quantitative findings | 2-3 sentences |
| **Conclusion** | Significance and implication | 1-2 sentences |

### Example Abstract

> *"Deep learning models for medical image analysis require large annotated datasets, which are scarce in clinical settings (Background). This thesis proposes a semi-supervised learning framework, MedSSL, that leverages unlabeled medical images to improve diagnostic accuracy (Objective). MedSSL combines contrastive pre-training with pseudo-label fine-tuning on chest X-ray datasets (Method). On the CheXpert dataset, MedSSL achieves 92.3% AUC using only 10% labeled data, outperforming fully supervised baselines trained on 100% labels by 1.2% (Results). The framework significantly reduces the annotation burden for clinical AI deployment (Conclusion)."*

---

## 8.3 Citation and Referencing

### Why Cite?
1. Give credit to original authors
2. Allow readers to find and verify your sources
3. Demonstrate the breadth of your reading
4. Avoid plagiarism
5. Strengthen your arguments with evidence

### Major Citation Styles

**IEEE Style (Standard for CS/Engineering)**
- In-text: numbered references in square brackets [1], [2], [3-5]
- Reference list: numbered, in order of appearance
- Example in-text: "Recent work on transformers [1] has shown..."
- Example reference: [1] A. Vaswani et al., "Attention is all you need," in *Proc. NeurIPS*, 2017, pp. 5998-6008.

**APA Style (Social Sciences)**
- In-text: (Author, Year) — e.g., (Vaswani et al., 2017)
- Reference list: alphabetical by first author
- Example: Vaswani, A., Shazeer, N., Parmar, N., ... (2017). Attention is all you need. *Advances in Neural Information Processing Systems*, 30, 5998-6008.

**Harvard Style**
- Similar to APA
- In-text: (Author Year) — e.g., (Vaswani 2017)

### Reference Management Tools

| Tool | Type | Key Feature |
|------|------|-------------|
| **Zotero** | Free, open-source | Browser plugin to save papers with one click |
| **Mendeley** | Free (Elsevier) | PDF annotation, social networking for researchers |
| **EndNote** | Paid | Deep integration with Word; standard in many institutions |
| **BibTeX / BibLaTeX** | Free (LaTeX ecosystem) | Text-based, version-controllable, standard for CS papers |
| **Google Scholar** | Free | Click "Cite" under any paper → copy BibTeX entry |

### BibTeX Example

```bibtex
@inproceedings{vaswani2017attention,
  title     = {Attention is All You Need},
  author    = {Vaswani, Ashish and Shazeer, Noam and Parmar, Niki and 
               Uszkoreit, Jakob and Jones, Llion and Gomez, Aidan N and 
               Kaiser, Lukasz and Polosukhin, Illia},
  booktitle = {Advances in Neural Information Processing Systems},
  volume    = {30},
  pages     = {5998--6008},
  year      = {2017}
}
```

In LaTeX: `\cite{vaswani2017attention}` → renders as [1] or (Vaswani et al., 2017) depending on style.

---

## 8.4 Academic Writing Best Practices

### Dos and Don'ts

| Do | Don't |
|----|-------|
| Use precise, specific language | Use vague words ("good," "nice," "a lot") |
| Use past tense for methods/results ("We trained...") | Mix tenses inconsistently |
| Use present tense for established facts ("CNNs are used for...") | Use overconfident claims ("This proves that...") |
| Define abbreviations on first use | Assume the reader knows all abbreviations |
| Use hedging language ("suggests," "indicates," "may") | Use emotional/subjective language |
| Support every claim with evidence or citation | Make unsupported assertions |
| Write in third person (most formal) or first person plural ("we") | Use "I" in formal academic writing (unless accepted in your field) |

### Common Mistakes to Avoid

1. **Run-on sentences** — keep sentences under 25-30 words when possible
2. **Passive voice overuse** — "The model was trained" is fine, but vary with active: "We trained the model"
3. **Redundancy** — "The results obtained showed..." → "The results showed..."
4. **Unsupported claims** — "Deep learning is the best approach" → needs a citation
5. **Missing transitions** — use connectors: "However," "Furthermore," "In contrast," "Consequently"

### Paragraph Structure

Each paragraph should:
1. Start with a **topic sentence** (main point)
2. Provide **supporting details** (evidence, examples, citations)
3. End with a **concluding/transition sentence** (link to the next paragraph)

---

## 8.5 Figures, Tables, and Equations

### Figures

Rules for figures in academic writing:
- Every figure MUST be referenced in the text: "As shown in Fig. 3..."
- Use high-resolution images (300+ DPI for print)
- Include clear labels (axis labels, legends, units)
- Caption goes BELOW the figure
- Caption should be self-explanatory (reader should understand without reading the main text)
- Number sequentially: Fig. 1, Fig. 2, ... (or Figure 1, Figure 2)

**Example caption:** "Fig. 3. Comparison of training loss curves for ResNet-50, VGG-16, and the proposed LightNet across 100 epochs on CIFAR-10. LightNet converges faster (by epoch 40) while achieving comparable final loss."

### Tables

- Caption goes ABOVE the table (unlike figures!)
- Every table MUST be referenced in text
- Use consistent formatting
- Align numbers by decimal point
- Bold the best results in comparison tables

**Example:**
> Table 2. Classification accuracy (%) on CIFAR-10 test set.
> | Model | Params (M) | FLOPs (G) | Accuracy (%) |
> |-------|-----------|-----------|-------------|
> | ResNet-50 | 25.6 | 4.1 | 93.62 |
> | VGG-16 | 138.4 | 15.5 | 93.25 |
> | **Proposed** | **8.2** | **1.3** | **93.48** |

### Equations

- Number important equations: Equation (1), Equation (2)
- Reference in text: "...as defined in Eq. (1)"
- Define ALL symbols immediately after the equation
- Use consistent notation throughout

---

## 8.6 Research Paper Structure (for journal/conference papers)

Shorter than a thesis but follows a similar structure:

| Section | Approximate Length (8-page paper) |
|---------|----------------------------------|
| **Title** | Concise, specific, includes key method/contribution |
| **Abstract** | 150-250 words |
| **Introduction** | 1-1.5 pages |
| **Related Work** | 1-1.5 pages |
| **Proposed Method** | 2-3 pages (with figures, algorithms) |
| **Experiments** | 2-3 pages (setup, results, analysis) |
| **Conclusion** | 0.5 page |
| **References** | 20-40 citations for a good paper |

### Conference Paper vs. Journal Paper

| Aspect | Conference Paper | Journal Paper |
|--------|-----------------|---------------|
| **Length** | 6-10 pages | 15-30+ pages |
| **Review time** | 2-4 months | 3-12 months |
| **Acceptance rate** | Top venues: 15-25% | Varies widely |
| **Presentation** | Oral talk or poster at the conference | No presentation required |
| **Prestige in CS** | Very high (NeurIPS, ICML, CVPR) | Also high (TPAMI, JMLR) |

---

## 8.7 LaTeX — The Standard Tool for Academic Writing in CS

Most CS researchers use LaTeX rather than Word. Key reasons:
- Superior handling of equations, figures, citations
- Consistent formatting (journals provide templates)
- Version-controllable (plain text files → Git)
- BibTeX integration for references

**Essential LaTeX commands:**

| Command | What It Does |
|---------|-------------|
| `\section{Title}` | Creates a section heading |
| `\cite{key}` | Inserts a citation |
| `\ref{fig:name}` | References a figure/table |
| `\begin{equation}` | Numbered equation |
| `\begin{figure}` | Insert figure |
| `\begin{table}` | Insert table |
| `\textbf{bold}` | Bold text |
| `\textit{italic}` | Italic text |

**Where to write LaTeX:** Overleaf (online, collaborative), TeXstudio, VS Code + LaTeX Workshop

---

## 8.8 Practice Questions

**Q1.** What are the key differences between a thesis abstract and a research paper abstract?
> **Answer:** A **thesis abstract** is longer (300-500 words) and covers the entire PhD work — multiple experiments, comprehensive literature context, and broader implications. A **paper abstract** is shorter (150-250 words) and focuses on one specific contribution. Both follow the IMRaD structure (Introduction, Method, Results, and Discussion), but the thesis abstract has more breadth while the paper abstract is more focused.

**Q2.** Arrange the following in the correct order for a thesis: (a) Results and Analysis (b) Abstract (c) Literature Review (d) Research Methodology (e) Introduction
> **Answer:** (b) Abstract → (e) Introduction → (c) Literature Review → (d) Research Methodology → (a) Results and Analysis. Note: While the Abstract appears first in the thesis, it is usually written LAST (after all chapters are complete).

**Q3.** What is the difference between IEEE and APA citation styles? Which is more common in computer science?
> **Answer:** **IEEE** uses numbered references in square brackets [1] with the reference list ordered by appearance. **APA** uses author-date format (Author, Year) with an alphabetical reference list. **IEEE is the standard in CS/Engineering**, while APA is more common in social sciences and psychology. CS conferences and IEEE/ACM journals typically require IEEE format.

**Q4.** A student writes: "Neural networks are the best method for all classification tasks." What is wrong with this statement for academic writing?
> **Answer:** Multiple problems: (1) It's an **unsupported claim** — no citation, no evidence. (2) It uses **absolute language** ("best," "all") which is rarely true. (3) It's an **overgeneralization** — neural networks are not always the best (e.g., for small tabular datasets, gradient boosting often wins). A better version: "Neural networks have achieved state-of-the-art results on many classification tasks, particularly in computer vision and NLP (LeCun et al., 2015)."

**Q5.** Where does the caption go for a figure? Where does it go for a table? Why?
> **Answer:** **Figure caption goes BELOW** the figure; **table caption goes ABOVE** the table. This convention comes from how readers scan visual elements: for figures, the image draws the eye first, then the reader looks down for explanation. For tables, readers need context BEFORE reading the data, so the caption appears above. This is a universal academic convention followed by IEEE, APA, and most journals.

---

*Previous: [Chapter 7 — Research Ethics](07_Research_Ethics.md) | Next: [Chapter 9 — Data Structures & Algorithms](../Part_B1_Core_CS/09_Data_Structures_and_Algorithms.md)*

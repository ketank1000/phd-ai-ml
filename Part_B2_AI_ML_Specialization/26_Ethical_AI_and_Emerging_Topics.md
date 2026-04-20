# 26. Ethical AI & Emerging Topics

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 26.1 Bias and Fairness in AI

### 26.1.1 Sources of Bias

| Source | Description | Example |
|--------|-------------|---------|
| **Data Bias** | Training data doesn't represent the real population | Facial recognition trained mostly on light-skinned faces → poor accuracy on dark skin |
| **Historical Bias** | Data reflects past societal inequalities | Hiring model trained on past decisions that discriminated against women |
| **Sampling Bias** | Data collected from non-representative sample | Medical AI trained on data from one hospital/region |
| **Measurement Bias** | Features proxy for protected attributes | Using zip code as feature → proxy for race |
| **Algorithmic Bias** | Algorithm amplifies existing disparities | Recommendation systems creating filter bubbles |
| **Label Bias** | Labels reflect annotator biases | Subjective labeling tasks (sentiment, toxicity) |
| **Representation Bias** | Some groups underrepresented in data | Voice assistants trained on mostly adult speech → poor with children/accents |

### 26.1.2 Fairness Definitions

| Definition | Meaning | Mathematical Form |
|-----------|---------|-------------------|
| **Demographic Parity** | Equal positive prediction rate across groups | $P(\hat{Y}=1 \| A=0) = P(\hat{Y}=1 \| A=1)$ |
| **Equalized Odds** | Equal TPR and FPR across groups | $P(\hat{Y}=1 \| Y=y, A=0) = P(\hat{Y}=1 \| Y=y, A=1)$ for $y \in \{0,1\}$ |
| **Equal Opportunity** | Equal TPR across groups | $P(\hat{Y}=1 \| Y=1, A=0) = P(\hat{Y}=1 \| Y=1, A=1)$ |
| **Calibration** | Predicted probability matches actual probability across groups | $P(Y=1 \| \hat{Y}=p, A=a) = p$ for all groups |
| **Individual Fairness** | Similar individuals get similar predictions | $d(\hat{y}_i, \hat{y}_j) \leq d(x_i, x_j)$ |

**Impossibility Theorem (Chouldechova, 2017):** Except in trivial cases, it's mathematically impossible to simultaneously satisfy demographic parity, equalized odds, AND calibration. You must choose which fairness criterion matters most.

### 26.1.3 Bias Mitigation Strategies

| Stage | Method | Description |
|-------|--------|-------------|
| **Pre-processing** | Resampling/Reweighting | Oversample underrepresented groups, reweight training examples |
| **Pre-processing** | Fair representation | Learn data representation that removes protected attribute info |
| **In-processing** | Adversarial debiasing | Add adversary that tries to predict protected attribute from model output; train model to fool adversary |
| **In-processing** | Fairness constraints | Add fairness penalty to loss function |
| **Post-processing** | Threshold adjustment | Use different decision thresholds per group to equalize metrics |

---

## 26.2 Explainable AI (XAI)

### Why Explainability Matters

- **Trust:** Users/doctors/judges need to understand AI decisions
- **Debugging:** Find model errors and biases
- **Regulation:** EU AI Act, GDPR ("right to explanation")
- **Domain adoption:** Healthcare, finance, legal — high-stakes decisions

### Interpretable vs. Black-Box Models

| Interpretable (inherently explainable) | Black-Box (need XAI tools) |
|---------------------------------------|---------------------------|
| Linear Regression, Logistic Regression | Deep Neural Networks |
| Decision Trees | Random Forest, Gradient Boosting |
| Rule-based systems | Transformer models (BERT, GPT) |

### XAI Techniques

#### LIME (Local Interpretable Model-agnostic Explanations)

**How it works:**
1. For a given prediction, generate perturbed samples around the input
2. Get model predictions for all perturbed samples
3. Fit a simple, interpretable model (linear/decision tree) locally
4. The simple model's coefficients explain the original prediction

**Result:** "This image was classified as 'cat' because of these highlighted pixels" or "This loan was denied because: income (−0.4), credit score (−0.3)."

#### SHAP (SHapley Additive exPlanations)

**Based on game theory — Shapley values.** Each feature's contribution is calculated as the average marginal contribution across all possible feature combinations.

$$\phi_i = \sum_{S \subseteq N \setminus \{i\}} \frac{|S|!(|N|-|S|-1)!}{|N|!} [f(S \cup \{i\}) - f(S)]$$

**Properties (unique to SHAP):**
- **Local accuracy:** Feature attributions sum to the prediction
- **Missingness:** Missing features have zero attribution
- **Consistency:** If a feature's contribution increases, its Shapley value doesn't decrease

**Types:** TreeSHAP (fast for tree models), KernelSHAP (model-agnostic), DeepSHAP (for neural networks).

#### Grad-CAM (Gradient-weighted Class Activation Mapping)

**For CNNs — visual explanations:**
1. Compute gradients of the target class score with respect to the final convolutional layer
2. Global average pooling of gradients → importance weights per channel
3. Weighted combination of feature maps → activation heatmap
4. Overlay on original image → shows which regions the CNN focused on

```
  Input Image        Grad-CAM Heatmap        Overlay
  ┌──────────┐      ┌──────────┐            ┌──────────┐
  │  🐱      │  →   │  ████    │     →      │  🔴🐱    │
  │           │      │  ████    │            │  🔴       │
  │           │      │          │            │           │
  └──────────┘      └──────────┘            └──────────┘
  Predicted: Cat     Hot = important         CNN focused on cat's face
```

#### Attention Visualization (for Transformers)

Visualize attention weights to see which input tokens the model attends to for each output. Not a perfect explanation (attention ≠ explanation), but provides useful insights.

---

## 26.3 Federated Learning

**Train ML models on decentralized data WITHOUT sharing raw data.**

```
  ┌──────────┐     ┌──────────┐     ┌──────────┐
  │ Device 1  │    │ Device 2  │    │ Device 3  │
  │ Local data│    │ Local data│    │ Local data│
  │ Train local│    │ Train local│   │ Train local│
  └─────┬─────┘    └─────┬─────┘   └─────┬─────┘
        │  gradients      │               │
        └────────┬────────┴───────────────┘
                 ↓
        ┌──────────────────┐
        │  Central Server   │
        │  Aggregate models │
        │  (FedAvg)         │
        └────────┬─────────┘
                 │  Updated global model
        ┌────────┼────────────────────────┐
        ↓        ↓                        ↓
  Device 1    Device 2                Device 3
```

**FedAvg (Federated Averaging):**
1. Server sends global model to selected devices
2. Each device trains on its local data for a few epochs
3. Devices send model updates (gradients/weights) to server
4. Server aggregates updates (weighted average by data size)
5. Repeat until convergence

**Applications:**
- **Mobile keyboard prediction** (Google Gboard): Train on users' typing without reading their messages
- **Healthcare:** Hospitals collaborate on models without sharing patient data (HIPAA compliance)
- **Financial:** Banks build fraud detection models without sharing customer data

**Challenges:**
- **Non-IID data:** Each device has different data distribution (heterogeneous)
- **Communication cost:** Sending model updates over network is expensive
- **Stragglers:** Some devices are slow (mobile battery, network)
- **Privacy:** Gradients can still leak information → use **Differential Privacy** (add noise)

---

## 26.4 AI Safety and Alignment

### Key Concepts

| Concept | Description | Example |
|---------|-------------|---------|
| **Reward Hacking** | Agent optimizes reward proxy, not intended goal | Robot rewarded for "cleaning" — learns to hide mess instead |
| **Specification Gaming** | Agent finds loopholes in reward function | Racing game: agent goes in circles collecting points instead of finishing race |
| **Adversarial Attacks** | Small perturbations fool ML models | Adding invisible noise to image changes cat → dog prediction |
| **Alignment** | Ensuring AI goals match human intentions | RLHF aligns LLMs with human preferences |

### Adversarial Robustness

**Adversarial examples:** Small, imperceptible perturbations that cause misclassification:

$$x_{adv} = x + \epsilon \cdot \text{sign}(\nabla_x L(x, y))$$

This is the **FGSM (Fast Gradient Sign Method)** — add perturbation in the direction that maximizes loss.

**Defense strategies:**
- **Adversarial training:** Include adversarial examples in training data
- **Defensive distillation:** Train a smoother model less sensitive to perturbations
- **Certified defenses:** Provide provable robustness guarantees
- **Input preprocessing:** Denoise inputs before classification

---

## 26.5 Emerging Topics

### 26.5.1 Large Language Models (LLMs)

| Model | Organization | Parameters | Key Innovation |
|-------|-------------|-----------|----------------|
| GPT-4 | OpenAI | ~1.8T | Multimodal (text + images), reasoning |
| LLaMA 2/3 | Meta | 7B-70B | Open-source, competitive performance |
| PaLM 2 / Gemini | Google | — | Multilingual, long context |
| Claude | Anthropic | — | Constitutional AI, safety-focused |

**Scaling Laws:** Model performance improves predictably with: more data, more parameters, more compute. Chinchilla findings: optimal to scale data and parameters equally.

**RLHF (Reinforcement Learning from Human Feedback):** Fine-tune LLMs to follow human preferences (covered in Chapter 24.8).

### 26.5.2 AutoML (Automated Machine Learning)

**Automate the ML pipeline:** Feature engineering → model selection → hyperparameter tuning.

| Component | What It Automates |
|-----------|------------------|
| **Neural Architecture Search (NAS)** | Design neural network architecture (EfficientNet was found by NAS) |
| **Hyperparameter Optimization** | Grid search, Bayesian optimization, Hyperband |
| **Feature Engineering** | Automated feature generation and selection |
| **Tools** | AutoKeras, Google Cloud AutoML, H2O AutoML, TPOT |

### 26.5.3 Few-Shot and Zero-Shot Learning

| Type | Training Examples | How It Works |
|------|-------------------|-------------|
| **Zero-shot** | None for target task | Use pre-trained knowledge (GPT: "Classify this as positive/negative") |
| **One-shot** | One example per class | Learn from a single example (Siamese networks, prototypical networks) |
| **Few-shot** | 2-10 examples per class | Meta-learning, prompt engineering, in-context learning |

### 26.5.4 Graph Neural Networks (GNNs)

**Apply deep learning to graph-structured data** (social networks, molecules, knowledge graphs):

| Task | Description | Example |
|------|-------------|---------|
| **Node classification** | Predict label for each node | User category in social network |
| **Link prediction** | Predict if edge should exist | Friend recommendation |
| **Graph classification** | Predict label for entire graph | Molecule toxicity prediction |

**Key architectures:** GCN (Graph Convolutional Network), GAT (Graph Attention Network), GraphSAGE.

**Message passing:** Each node aggregates information from its neighbors, then updates its representation:

$$h_v^{(l+1)} = \text{UPDATE}(h_v^{(l)}, \text{AGGREGATE}(\{h_u^{(l)} : u \in \mathcal{N}(v)\}))$$

### 26.5.5 Edge AI

**Run ML models on edge devices** (smartphones, IoT sensors, embedded systems) instead of cloud:

| Technique | Description |
|-----------|-------------|
| **Model Compression** | Reduce model size (pruning, quantization, knowledge distillation) |
| **Quantization** | Float32 → Int8/Int4 (reduce memory 4-8×, faster inference) |
| **Knowledge Distillation** | Train small "student" to mimic large "teacher" model |
| **Pruning** | Remove unimportant weights/neurons |
| **TinyML** | Models running on microcontrollers (<1MB memory) |

### 26.5.6 Multimodal AI

**Models that process multiple data types (text + images + audio):**

| Model | Modalities | Capability |
|-------|-----------|------------|
| **CLIP** | Image + Text | Zero-shot image classification via text prompts |
| **DALL-E / Stable Diffusion** | Text → Image | Generate images from text descriptions |
| **GPT-4V** | Text + Image → Text | Visual question answering, image understanding |
| **Whisper** | Audio → Text | Speech recognition |

---

## 26.6 Practice Questions

**Q1.** What is the difference between demographic parity and equalized odds? Can both be satisfied simultaneously?
> **Answer:** **Demographic parity** requires equal positive prediction rates across groups ($P(\hat{Y}=1|A=0) = P(\hat{Y}=1|A=1)$) — regardless of actual outcomes. **Equalized odds** requires equal TPR AND FPR across groups ($P(\hat{Y}=1|Y=y, A=0) = P(\hat{Y}=1|Y=y, A=1)$) — conditions on actual labels. **No, both cannot generally be satisfied simultaneously** (Impossibility Theorem by Chouldechova/Kleinberg). If base rates differ between groups (group A has 10% positive rate, group B has 30%), achieving demographic parity forces different thresholds → violates equalized odds. Practitioners must choose the appropriate fairness criterion for their context.

**Q2.** Compare LIME and SHAP for model explainability. When would you prefer SHAP?
> **Answer:** **LIME** perturbs the input locally and fits a simple interpretable model. It's fast and intuitive but: (1) explanations can be unstable (different perturbations → different explanations); (2) no theoretical guarantees on faithfulness. **SHAP** uses Shapley values from game theory — computes each feature's average marginal contribution. It has strong theoretical guarantees: local accuracy (attributions sum to prediction), consistency, and missingness. **Prefer SHAP when:** (1) You need consistent, theoretically grounded explanations; (2) Using tree models (TreeSHAP is exact and fast); (3) You want global feature importance (aggregate SHAP values across all predictions). **Prefer LIME when:** quick local explanations are needed, or for non-standard data types.

**Q3.** Explain federated learning. How does it address privacy concerns?
> **Answer:** Federated Learning trains ML models on decentralized data by sending the model TO the data instead of data to the model. Process: (1) Server sends global model to devices; (2) Each device trains on local data; (3) Only model updates (gradients/weights) are sent back — NOT raw data; (4) Server aggregates updates (FedAvg). **Privacy benefits:** Raw data never leaves the device — addresses GDPR, HIPAA compliance. **However,** gradients can still leak information (gradient inversion attacks). **Additional protections:** Differential Privacy (add calibrated noise to gradients), Secure Aggregation (cryptographic protocols ensure server only sees aggregate), Homomorphic Encryption (compute on encrypted data).

**Q4.** What are adversarial examples? Why are they a concern for deployed AI systems?
> **Answer:** Adversarial examples are inputs with small, often imperceptible perturbations that cause ML models to make wrong predictions with high confidence. Example: Adding tiny noise to a stop sign image makes a self-driving car's classifier predict "speed limit sign." **Concern because:** (1) **Safety:** Autonomous vehicles, medical diagnosis could make dangerous errors; (2) **Security:** Attackers can craft adversarial inputs to bypass security systems (biometric, content filters); (3) **Transferability:** Adversarial examples crafted for one model often fool other models too (black-box attacks); (4) **Robustness gap:** Models that are 99% accurate on clean data may drop to 0% on adversarial inputs. FGSM, PGD, and C&W are common attack methods.

**Q5.** What is knowledge distillation? How is it used for Edge AI?
> **Answer:** Knowledge distillation trains a small "student" model to mimic a large "teacher" model. The student learns from the teacher's **soft labels** (probability distributions) rather than hard labels (0/1). Soft labels contain richer information — e.g., for digit "7", the teacher might output [0.01, 0.02, 0.01, 0.05, 0.01, 0.01, 0.01, 0.85, 0.02, 0.01] showing "7" looks somewhat like "1" and "9." **For Edge AI:** (1) Train a large, accurate teacher model on a powerful server; (2) Distill into a compact student model (10-100× smaller); (3) Deploy the student on edge devices (phones, IoT). The student achieves much better accuracy than training a small model from scratch, because it leverages the teacher's learned knowledge. Combined with quantization (Float32→Int8), pruning, and architecture optimization, this enables real-time inference on resource-constrained devices.

---

*Previous: [Chapter 25 — Data Mining & Big Data](25_Data_Mining_and_Big_Data.md) | Back to: [README](../README.md)*

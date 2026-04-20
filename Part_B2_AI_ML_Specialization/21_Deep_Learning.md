# 21. Deep Learning

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 21.1 Neural Network Fundamentals

### 21.1.1 The Perceptron

Single artificial neuron — the building block of all neural networks:

$$y = \sigma\left(\sum_{i=1}^{n} w_i x_i + b\right) = \sigma(\mathbf{w}^T \mathbf{x} + b)$$

```
  x1 ──w1──┐
  x2 ──w2──┤──→ Σ ──→ σ(z) ──→ y (output)
  x3 ──w3──┤     ↑
            └─── b (bias)
```

**Limitation:** Can only learn linearly separable functions. Famous failure: cannot learn **XOR** (solved by adding a hidden layer → MLP).

### 21.1.2 Multi-Layer Perceptron (MLP)

```
Input Layer     Hidden Layer(s)     Output Layer
  ○ x1            ○ h1                ○ y1
  ○ x2  ───→     ○ h2     ───→      ○ y2
  ○ x3            ○ h3                ○ y3
  ○ x4            ○ h4
```

**Forward pass (one hidden layer):**

$$\mathbf{h} = \sigma(W_1 \mathbf{x} + \mathbf{b}_1) \quad \text{(hidden layer)}$$
$$\hat{\mathbf{y}} = \text{softmax}(W_2 \mathbf{h} + \mathbf{b}_2) \quad \text{(output layer)}$$

**Universal Approximation Theorem:** A single hidden layer with enough neurons can approximate any continuous function. However, deeper networks are **exponentially more efficient** (fewer parameters for the same complexity).

### 21.1.3 Activation Functions

| Function | Formula | Range | Derivative | Use Case |
|----------|---------|-------|------------|----------|
| **Sigmoid** | $\frac{1}{1+e^{-x}}$ | (0, 1) | $\sigma(1-\sigma)$ | Binary output, gates in LSTM |
| **Tanh** | $\frac{e^x - e^{-x}}{e^x + e^{-x}}$ | (-1, 1) | $1-\tanh^2$ | Zero-centered, RNN hidden states |
| **ReLU** | $\max(0, x)$ | [0, ∞) | 0 or 1 | Default for hidden layers |
| **Leaky ReLU** | $\max(0.01x, x)$ | (-∞, ∞) | 0.01 or 1 | Fixes dying ReLU |
| **ELU** | $x$ if $x>0$; $\alpha(e^x-1)$ else | (-α, ∞) | Smooth | Variant of ReLU |
| **GELU** | $x \cdot \Phi(x)$ | ≈(-0.17, ∞) | Complex | Transformers (BERT, GPT) |
| **Swish** | $x \cdot \sigma(x)$ | ≈(-0.28, ∞) | Complex | EfficientNet, modern CNNs |
| **Softmax** | $\frac{e^{x_i}}{\sum_j e^{x_j}}$ | (0,1), sum=1 | — | Multi-class output layer |

**Why non-linearity?** Without activation functions, stacking linear layers just produces another linear function. Non-linearity allows networks to learn complex patterns.

**Vanishing gradient problem:** Sigmoid/Tanh — derivatives are near zero for large/small inputs → gradients shrink to ~0 in deep networks → early layers stop learning. **ReLU solves this** (gradient = 1 for positive inputs).

**Dying ReLU:** If a neuron gets a large negative bias, all inputs produce negative pre-activation → ReLU always outputs 0 → gradient is 0 → neuron never updates. Fixed by Leaky ReLU, ELU, or careful initialization.

### 21.1.4 Backpropagation

**The algorithm that makes deep learning possible.** Efficiently computes gradients of the loss with respect to all parameters using the chain rule.

**Steps:**

1. **Forward pass:** Compute output $\hat{y}$ layer by layer
2. **Compute loss:** $L = \text{loss}(y, \hat{y})$
3. **Backward pass:** Compute $\frac{\partial L}{\partial w}$ for every weight using the chain rule, starting from the output

**Example (2-layer network):**

$$\frac{\partial L}{\partial W_1} = \frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial \mathbf{h}} \cdot \frac{\partial \mathbf{h}}{\partial W_1}$$

4. **Update weights:** $W = W - \eta \frac{\partial L}{\partial W}$

**Computational graph perspective:** Each operation stores intermediate values during forward pass, then uses them during backward pass. This is called **automatic differentiation** (implemented in PyTorch, TensorFlow).

### 21.1.5 Loss Functions

| Loss | Formula | Task |
|------|---------|------|
| **MSE** | $\frac{1}{n}\sum(y-\hat{y})^2$ | Regression |
| **Binary Cross-Entropy** | $-\frac{1}{n}\sum[y\log\hat{y}+(1-y)\log(1-\hat{y})]$ | Binary classification |
| **Categorical Cross-Entropy** | $-\sum_c y_c \log \hat{y}_c$ | Multi-class |
| **Hinge Loss** | $\max(0, 1-y\hat{y})$ | SVM-style |
| **Huber Loss** | MSE if $|e|<\delta$, MAE otherwise | Robust regression |
| **Focal Loss** | $-\alpha(1-\hat{y})^\gamma \log\hat{y}$ | Imbalanced classification |

### 21.1.6 Weight Initialization

Bad initialization → vanishing/exploding gradients from the start.

| Method | Formula | Use With |
|--------|---------|----------|
| **Xavier / Glorot** | $W \sim \mathcal{N}(0, \frac{2}{n_{in}+n_{out}})$ | Sigmoid, Tanh |
| **He / Kaiming** | $W \sim \mathcal{N}(0, \frac{2}{n_{in}})$ | ReLU, Leaky ReLU |

---

## 21.2 Regularization in Deep Learning

| Technique | How It Works | Effect |
|-----------|-------------|--------|
| **Dropout** | Randomly zero out neurons with probability $p$ during training | Prevents co-adaptation, acts like ensemble |
| **Batch Normalization** | Normalize activations to mean=0, variance=1 per mini-batch | Faster training, mild regularization, allows higher LR |
| **Layer Normalization** | Normalize across features (not batch) | Used in Transformers (batch size independent) |
| **L2 / Weight Decay** | Add $\lambda\|W\|^2$ to loss | Penalizes large weights |
| **Early Stopping** | Stop when validation loss starts increasing | Prevents overfitting |
| **Data Augmentation** | Random crops, flips, rotations, color jitter | Effectively more training data |
| **Label Smoothing** | Replace hard labels (0/1) with soft (0.05/0.95) | Prevents overconfident predictions |

**Dropout detail:** During training, each neuron is kept with probability $(1-p)$. During inference, all neurons are active but outputs are scaled by $(1-p)$. Typical $p$: 0.2-0.5.

**Batch Normalization detail:** For each mini-batch:
$$\hat{x} = \frac{x - \mu_B}{\sqrt{\sigma_B^2 + \epsilon}}, \quad y = \gamma \hat{x} + \beta$$

$\gamma$ (scale) and $\beta$ (shift) are learnable. During inference, use running mean/variance from training.

---

## 21.3 Convolutional Neural Networks (CNN)

### 21.3.1 Convolution Operation

Slide a **filter (kernel)** over the input and compute element-wise products + sum at each position.

```
Input (5×5)           Filter (3×3)          Output (3×3)
┌───────────────┐     ┌─────────┐          ┌─────────┐
│ 1  0  1  0  1 │     │ 1  0  1 │          │ 4  3  4 │
│ 0  1  0  1  0 │  *  │ 0  1  0 │    =     │ 2  4  3 │
│ 1  0  1  0  1 │     │ 1  0  1 │          │ 4  3  4 │
│ 0  1  0  1  0 │     └─────────┘          └─────────┘
│ 1  0  1  0  1 │
└───────────────┘
```

**Output size formula:**

$$\text{Output} = \frac{W - F + 2P}{S} + 1$$

where $W$ = input size, $F$ = filter size, $P$ = padding, $S$ = stride.

**Example:** Input 32×32, Filter 5×5, Padding 0, Stride 1 → Output = $\frac{32-5+0}{1}+1 = 28$

### Key CNN Components

| Component | Purpose |
|-----------|---------|
| **Convolution layer** | Extract features (edges, textures, patterns) |
| **Activation (ReLU)** | Add non-linearity |
| **Pooling** | Reduce spatial dimensions, add translation invariance |
| **Flatten** | Convert 2D feature maps to 1D vector |
| **Fully connected** | Classification/regression head |

**Pooling:** Max pooling (take max in each window) or Average pooling. Typical: 2×2 with stride 2 → halves spatial dimensions.

**Parameter sharing:** Same filter weights applied across all positions → massive parameter reduction vs. fully connected. A 3×3 filter has only 9 parameters regardless of image size.

### 21.3.2 CNN Architectures Evolution

| Architecture | Year | Depth | Key Innovation | Top-5 Error (ImageNet) |
|-------------|------|-------|----------------|----------------------|
| **LeNet-5** | 1998 | 5 | Pioneer: Conv-Pool-Conv-Pool-FC | — (MNIST) |
| **AlexNet** | 2012 | 8 | Deep CNN + ReLU + Dropout + GPU | 15.3% |
| **VGGNet** | 2014 | 16/19 | Uniform 3×3 filters throughout | 7.3% |
| **GoogLeNet** | 2014 | 22 | Inception module (parallel filter sizes) | 6.7% |
| **ResNet** | 2015 | 152 | **Residual (skip) connections** | 3.6% |
| **DenseNet** | 2017 | 121+ | Each layer connects to ALL previous layers | 3.5% |
| **EfficientNet** | 2019 | - | Compound scaling (depth+width+resolution) | 2.9% |

### ResNet — The Most Important Innovation

**Problem:** Very deep networks (>20 layers) had HIGHER training error than shallow ones. Not overfitting — training error was worse!

**Solution: Skip (residual) connections:**

$$\text{output} = F(x) + x \quad (\text{shortcut/skip connection})$$

```
  x ──────────────────────┐
  │                       │ (identity/skip)
  ↓                       │
  [Conv → BN → ReLU]      │
  ↓                       │
  [Conv → BN]             │
  ↓                       │
  ─────── + ──────────────┘
  ↓
  [ReLU]
```

**Why it works:** The network only needs to learn the **residual** $F(x) = H(x) - x$ rather than the full mapping $H(x)$. If the optimal function is close to identity, it's easier to learn $F(x) \approx 0$ than $H(x) \approx x$. Also, gradients flow directly through skip connections, solving the vanishing gradient problem in very deep networks.

---

## 21.4 Recurrent Neural Networks (RNN)

### 21.4.1 Vanilla RNN

Process **sequential data** (text, time series, audio) by maintaining a hidden state:

$$h_t = \tanh(W_{hh} h_{t-1} + W_{xh} x_t + b_h)$$
$$y_t = W_{hy} h_t + b_y$$

```
  x1 → [RNN] → h1 → y1
         ↓ h1
  x2 → [RNN] → h2 → y2
         ↓ h2
  x3 → [RNN] → h3 → y3
```

**Problem: Vanishing/Exploding Gradients** — for long sequences, gradients are multiplied by $W_{hh}$ at each time step. If eigenvalues of $W_{hh}$ < 1 → gradients vanish. If > 1 → gradients explode. **Solution:** LSTM and GRU.

### 21.4.2 LSTM (Long Short-Term Memory)

Introduces a **cell state** $C_t$ (highway for information) and three **gates** to control information flow:

```
                    ┌──────────────────────────────────────────────────┐
                    │                Cell State  Ct                    │
       ┌──────┐    │   ┌─────┐     ┌─────┐     ┌─────┐             │
Ct-1 ──│      │────┼──→│  ×  │────→│  +  │────→│     │────→ Ct     │
       │      │    │   └──↑──┘     └──↑──┘     └─────┘             │
       │      │    │      │           │                              │
       │      │    │   Forget       Input                            │
       │      │    │   Gate ft      Gate it × C̃t                    │
ht-1 ──│      │    │   σ(Wf)       σ(Wi)·tanh(Wc)                  │
       │      │    │                                                 │
xt   ──│      │    │              Output Gate                        │
       │      │    │              ot = σ(Wo)                         │
       └──────┘    │              ht = ot × tanh(Ct)                │
                    └──────────────────────────────────────────────────┘
```

**Gates (all use sigmoid → output between 0 and 1):**

| Gate | Formula | Function |
|------|---------|----------|
| **Forget** $f_t$ | $\sigma(W_f [h_{t-1}, x_t] + b_f)$ | What to forget from cell state |
| **Input** $i_t$ | $\sigma(W_i [h_{t-1}, x_t] + b_i)$ | What new info to store |
| **Output** $o_t$ | $\sigma(W_o [h_{t-1}, x_t] + b_o)$ | What to output from cell state |

**Cell state update:**
$$C_t = f_t \odot C_{t-1} + i_t \odot \tilde{C}_t$$

where $\tilde{C}_t = \tanh(W_C [h_{t-1}, x_t] + b_C)$ is the candidate new memory.

**Why LSTM solves vanishing gradients:** Gradients flow through the cell state with only **element-wise multiplications** (by forget gate values near 1), not matrix multiplications. The cell state acts like a highway.

### 21.4.3 GRU (Gated Recurrent Unit)

Simplified LSTM with **two gates** instead of three:

| Gate | Formula | Analogy to LSTM |
|------|---------|----------------|
| **Update** $z_t$ | $\sigma(W_z [h_{t-1}, x_t])$ | Combines forget + input gates |
| **Reset** $r_t$ | $\sigma(W_r [h_{t-1}, x_t])$ | Controls how much past to forget |

$$h_t = (1-z_t) \odot h_{t-1} + z_t \odot \tilde{h}_t$$

**GRU vs LSTM:** Fewer parameters (faster), similar performance. Use GRU for smaller datasets, LSTM for complex long-range dependencies.

### 21.4.4 Bidirectional RNN

Process sequence in BOTH directions and concatenate:

$$\overrightarrow{h_t} = \text{RNN}(x_t, \overrightarrow{h_{t-1}}) \quad \overleftarrow{h_t} = \text{RNN}(x_t, \overleftarrow{h_{t+1}})$$
$$h_t = [\overrightarrow{h_t}; \overleftarrow{h_t}]$$

Useful when future context matters (e.g., NER: "I went to the **bank** of the river" — "river" disambiguates "bank").

---

## 21.5 Transformers and Attention

### 21.5.1 Attention Mechanism (2014)

**Problem:** Seq2seq models compress the entire input into a fixed-length vector (bottleneck).

**Solution:** At each decoder step, **attend** to all encoder hidden states with learned weights:

$$\text{context}_t = \sum_{i} \alpha_{ti} \cdot h_i$$

where $\alpha_{ti}$ = attention weight (how much the decoder at step $t$ should focus on encoder state $i$).

### 21.5.2 Self-Attention (Scaled Dot-Product)

**Core innovation of Transformers.** Each position attends to all other positions in the same sequence.

From each input, compute three vectors:
- **Query (Q):** What am I looking for?
- **Key (K):** What do I contain?
- **Value (V):** What information do I provide?

$$\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V$$

**Step by step:**
1. Compute similarity: $QK^T$ (dot product of queries with all keys)
2. Scale by $\sqrt{d_k}$ (prevents softmax from saturating for large $d_k$)
3. Apply softmax → attention weights (sum to 1)
4. Weighted sum of values

### 21.5.3 Multi-Head Attention

Run $h$ attention heads in parallel, each with different learned projections:

$$\text{MultiHead}(Q, K, V) = \text{Concat}(\text{head}_1, ..., \text{head}_h) \cdot W^O$$

where $\text{head}_i = \text{Attention}(QW_i^Q, KW_i^K, VW_i^V)$

**Why multiple heads?** Each head can attend to different relationship types (e.g., head 1: syntax, head 2: semantics, head 3: position).

### 21.5.4 Transformer Architecture ("Attention Is All You Need", 2017)

```
              ┌─────────────────────────┐
              │       DECODER (×N)      │
              │  ┌───────────────────┐  │
Output  ←──── │  │ Feed-Forward NN   │  │
              │  └───────────────────┘  │
              │  ┌───────────────────┐  │
              │  │ Cross-Attention    │  │ ←── from Encoder
              │  │ (Q from decoder,  │  │
              │  │  K,V from encoder)│  │
              │  └───────────────────┘  │
              │  ┌───────────────────┐  │
              │  │ Masked Self-Attn   │  │
              │  └───────────────────┘  │
              └──────────↑──────────────┘
                         │
              ┌──────────┴──────────────┐
              │       ENCODER (×N)      │
              │  ┌───────────────────┐  │
              │  │ Feed-Forward NN   │  │
              │  └───────────────────┘  │
              │  ┌───────────────────┐  │
              │  │ Self-Attention     │  │
              │  └───────────────────┘  │
              └──────────↑──────────────┘
                         │
              ┌──────────┴──────────────┐
              │ Input Embedding +        │
              │ Positional Encoding      │
              └─────────────────────────┘
```

**Key components:**
- **Positional encoding:** Since Transformers have no recurrence, they add sinusoidal or learned position information to embeddings
- **Residual connections:** Around every sub-layer ($x + \text{sublayer}(x)$)
- **Layer normalization:** After each residual connection
- **Masked self-attention (decoder):** Prevent attending to future positions during training

**Advantages over RNNs:**
- **Parallelizable** (no sequential dependency in self-attention)
- **Long-range dependencies** without vanishing gradients
- Scales to **very large models** efficiently

### 21.5.5 Pre-trained Transformer Models

| Model | Year | Type | Pre-training Task | Key Use |
|-------|------|------|-------------------|---------|
| **BERT** | 2018 | Encoder only | Masked LM + Next Sentence Prediction | Classification, NER, QA |
| **GPT-2/3/4** | 2019-23 | Decoder only | Autoregressive LM (next token prediction) | Text generation, reasoning |
| **T5** | 2020 | Encoder-Decoder | Text-to-text (all tasks as text generation) | Any NLP task |
| **ViT** | 2020 | Encoder only | Image patch classification | Vision tasks |
| **CLIP** | 2021 | Dual Encoder | Contrastive image-text matching | Zero-shot classification |

---

## 21.6 Generative Models

### 21.6.1 GANs (Generative Adversarial Networks)

**Two networks competing:**
- **Generator $G$:** Takes random noise $z$ → generates fake data $G(z)$
- **Discriminator $D$:** Takes data → predicts real (1) or fake (0)

$$\min_G \max_D \; E_{x \sim p_{data}}[\log D(x)] + E_{z \sim p_z}[\log(1 - D(G(z)))]$$

```
  Random Noise z ──→ [Generator G] ──→ Fake Image ──┐
                                                       ├──→ [Discriminator D] ──→ Real/Fake?
                            Real Image ───────────────┘
```

**Training:** Alternately train D (to distinguish better) and G (to fool D better). At equilibrium, $D(x) = 0.5$ and $G$ generates realistic data.

**GAN variants:**

| Variant | Innovation |
|---------|-----------|
| **DCGAN** | Deep convolutional architecture for both G and D |
| **WGAN** | Wasserstein distance instead of JS divergence (more stable training) |
| **Conditional GAN** | Generate specific classes by conditioning on labels |
| **CycleGAN** | Unpaired image-to-image translation (horse↔zebra) |
| **StyleGAN** | High-quality face generation with style control |
| **Pix2Pix** | Paired image-to-image translation |

**Challenges:** Mode collapse (G produces limited variety), training instability, hard to evaluate.

### 21.6.2 VAE (Variational Autoencoder)

**Probabilistic generative model** that learns a latent representation:

```
  Input x ──→ [Encoder] ──→ μ, σ ──→ z ~ N(μ,σ²) ──→ [Decoder] ──→ x̂ (reconstruction)
                              ↑
                     Reparameterization trick:
                     z = μ + σ · ε, ε ~ N(0,1)
```

**Loss = Reconstruction + KL divergence:**

$$L = \underbrace{-E_{q(z|x)}[\log p(x|z)]}_{\text{Reconstruction loss}} + \underbrace{D_{KL}(q(z|x) \| p(z))}_{\text{KL loss (pushes toward N(0,1))}}$$

**Reparameterization trick:** Instead of sampling $z \sim q(z|x)$ (non-differentiable), compute $z = \mu + \sigma \odot \epsilon$ where $\epsilon \sim \mathcal{N}(0,1)$. Now the gradient can flow through $\mu$ and $\sigma$.

### 21.6.3 Diffusion Models

**Current state-of-the-art for image generation** (DALL-E 2, Stable Diffusion, Midjourney).

**Forward process:** Gradually add Gaussian noise over $T$ steps until data becomes pure noise.
$$q(x_t | x_{t-1}) = \mathcal{N}(x_t; \sqrt{1-\beta_t} x_{t-1}, \beta_t I)$$

**Reverse process:** Learn to denoise step by step (a neural network predicts the noise at each step).
$$p_\theta(x_{t-1} | x_t) = \mathcal{N}(x_{t-1}; \mu_\theta(x_t, t), \sigma_t^2 I)$$

**Why they work so well:** The denoising task is relatively easy at each step, and the model can generate extremely high-quality samples.

---

## 21.7 Transfer Learning

**Use knowledge from one task/domain to improve performance on another.**

| Approach | Description | When to Use |
|----------|-------------|-------------|
| **Feature Extraction** | Freeze pre-trained layers, train only the new head | Small target dataset |
| **Fine-tuning** | Unfreeze some/all layers, train with small LR | Medium target dataset |
| **Full training** | Train from scratch | Very large target dataset, very different domain |

**Transfer learning recipe:**
1. Start with model pre-trained on large dataset (ImageNet, BERT)
2. Replace final layer(s) with task-specific head
3. Freeze early layers (generic features: edges, textures)
4. Train new head with higher learning rate
5. Optionally unfreeze deeper layers with very small learning rates

---

## 21.8 Practice Questions

**Q1.** Explain the vanishing gradient problem and how ReLU and residual connections address it.
> **Answer:** During backpropagation, gradients are multiplied through many layers via the chain rule. **Vanishing gradient:** With Sigmoid/Tanh, derivatives are small (max 0.25 for sigmoid), so multiplying many such values → gradient approaches 0 → early layers don't learn. **ReLU** has derivative = 1 for positive inputs, so gradients pass through unchanged. **Residual connections** ($y = F(x) + x$) provide a direct gradient path: $\frac{\partial y}{\partial x} = \frac{\partial F}{\partial x} + 1$. The "+1" ensures gradients are at least 1, preventing vanishing even in 100+ layer networks.

**Q2.** Compare LSTM and GRU. When would you prefer one over the other?
> **Answer:** **LSTM** has 3 gates (forget, input, output) and a separate cell state — more parameters, more expressive. **GRU** has 2 gates (update, reset) and merges cell/hidden state — fewer parameters, faster training. Performance is usually similar. **Choose LSTM** for: very long sequences, tasks requiring precise memory control (machine translation). **Choose GRU** for: smaller datasets (less overfitting), faster experiments, when LSTM and GRU perform similarly (GRU is simpler). In practice, Transformers have largely replaced both for most sequence tasks.

**Q3.** Explain the self-attention mechanism. Why does it scale by $\sqrt{d_k}$?
> **Answer:** Self-attention computes: $\text{Attention}(Q,K,V) = \text{softmax}(\frac{QK^T}{\sqrt{d_k}})V$. For each position, Q (query) is compared with all K (keys) via dot product → attention weights → weighted sum of V (values). **Scaling by $\sqrt{d_k}$:** When $d_k$ is large, dot products $q \cdot k$ have variance proportional to $d_k$ (each element contributes ~1 to the variance). Large dot products push softmax into regions with extremely small gradients (near 0 or 1). Dividing by $\sqrt{d_k}$ normalizes the variance to ~1, keeping softmax in a well-behaved region for gradient flow.

**Q4.** What is the difference between GANs and VAEs? Compare their strengths and weaknesses.
> **Answer:** **GANs** use adversarial training (generator vs. discriminator) — produce sharp, realistic images but suffer from mode collapse and training instability. No explicit density estimation. **VAEs** use variational inference — optimize a reconstruction loss + KL divergence. They learn a smooth, continuous latent space (good for interpolation) but produce blurrier outputs. **GANs win** for: image quality, realism. **VAEs win** for: latent space interpretation, stable training, density estimation. **Diffusion models** now outperform both for image generation quality.

**Q5.** Explain Batch Normalization. Why does it help training, and why is Layer Normalization preferred in Transformers?
> **Answer:** **Batch Normalization (BN):** Normalizes activations across the batch dimension to mean=0, variance=1, then applies learnable scale/shift. Benefits: (1) reduces internal covariate shift, (2) allows higher learning rates, (3) acts as mild regularizer. **Problem with BN in Transformers:** (1) Depends on batch size — breaks with small batches; (2) Sequence lengths vary, making batch statistics unreliable; (3) At inference, needs running statistics which are unstable for variable-length sequences. **Layer Normalization (LN):** Normalizes across the feature dimension for each individual sample — independent of batch size and other sequences. This makes it ideal for Transformers, RNNs, and any setting with variable-length inputs.

---

*Previous: [Chapter 20 — Unsupervised Learning](20_Unsupervised_Learning.md) | Next: [Chapter 22 — NLP](22_NLP.md)*

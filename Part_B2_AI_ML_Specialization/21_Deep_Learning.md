# 21. Deep Learning

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 21.1 Neural Network Fundamentals

- [ ] **Perceptron**
  - Single neuron: $y = \sigma(w \cdot x + b)$
  - Can only model linearly separable functions (XOR problem)

- [ ] **Multi-Layer Perceptron (MLP)**
  - Input layer → Hidden layer(s) → Output layer
  - Universal approximation theorem: single hidden layer can approximate any continuous function

- [ ] **Activation Functions**

  | Function | Formula | Range | Pros | Cons |
  |----------|---------|-------|------|------|
  | **Sigmoid** | $\frac{1}{1+e^{-x}}$ | (0, 1) | Smooth, probabilistic | Vanishing gradient |
  | **Tanh** | $\frac{e^x - e^{-x}}{e^x + e^{-x}}$ | (-1, 1) | Zero-centered | Vanishing gradient |
  | **ReLU** | $\max(0, x)$ | [0, ∞) | Simple, no vanishing | Dying ReLU (dead neurons) |
  | **Leaky ReLU** | $\max(0.01x, x)$ | (-∞, ∞) | Fixes dying ReLU | — |
  | **ELU** | $x$ if $x>0$; $\alpha(e^x-1)$ if $x≤0$ | (-α, ∞) | Smooth | Computationally expensive |
  | **Softmax** | $\frac{e^{x_i}}{\sum e^{x_j}}$ | (0, 1), sum=1 | Multi-class output | — |
  | **GELU** | $x \cdot \Phi(x)$ | — | Used in Transformers | — |

- [ ] **Backpropagation**
  - Forward pass: Compute output
  - Compute loss
  - Backward pass: Compute gradients using chain rule
  - Update weights: $w = w - \eta \frac{\partial L}{\partial w}$

- [ ] **Loss Functions**
  - **MSE**: Regression
  - **Binary Cross-Entropy**: Binary classification
  - **Categorical Cross-Entropy**: Multi-class classification
  - **Hinge Loss**: SVM
  - **Huber Loss**: Robust to outliers

## 21.2 Regularization Techniques

- [ ] **Dropout**: Randomly set neurons to 0 during training (typically p=0.2–0.5)
- [ ] **Batch Normalization**: Normalize layer inputs (faster training, regularization effect)
- [ ] **Layer Normalization**: Normalize across features (used in Transformers)
- [ ] **L1/L2 Regularization (Weight Decay)**: Add penalty to loss
- [ ] **Early Stopping**: Stop training when validation loss increases
- [ ] **Data Augmentation**: Expand training data with transformations

## 21.3 Convolutional Neural Networks (CNN)

- [ ] **Core Operations**
  - **Convolution**: Slide filter/kernel over input, compute dot products
  - **Padding**: Same (keep size) vs. Valid (no padding)
  - **Stride**: Step size of the filter
  - Output size: $\frac{W - F + 2P}{S} + 1$ (W=input, F=filter, P=padding, S=stride)
  - **Pooling**: Max pooling, average pooling (reduce spatial dimensions)
  - **Feature maps**: Output of convolution layer

- [ ] **CNN Architectures**

  | Architecture | Year | Key Innovation |
  |-------------|------|----------------|
  | **LeNet-5** | 1998 | Pioneer CNN for digit recognition |
  | **AlexNet** | 2012 | Deep CNN + ReLU + Dropout + GPU training |
  | **VGGNet** | 2014 | Very deep (16/19 layers), small 3×3 filters |
  | **GoogLeNet/Inception** | 2014 | Inception modules (parallel convolutions) |
  | **ResNet** | 2015 | Residual connections (skip connections), 152 layers |
  | **DenseNet** | 2017 | Dense connections (each layer connects to all previous) |
  | **EfficientNet** | 2019 | Compound scaling (depth, width, resolution) |

- [ ] **Applications**: Image classification, object detection, segmentation, face recognition

## 21.4 Recurrent Neural Networks (RNN)

- [ ] **Vanilla RNN**
  - Hidden state: $h_t = \tanh(W_{hh} h_{t-1} + W_{xh} x_t + b)$
  - Good for sequential data
  - Problem: **Vanishing/exploding gradients** for long sequences

- [ ] **LSTM (Long Short-Term Memory)**
  - Gates: forget gate, input gate, output gate
  - Cell state: long-term memory
  - Solves vanishing gradient problem
  - $f_t = \sigma(W_f [h_{t-1}, x_t] + b_f)$ (forget gate)
  - $i_t = \sigma(W_i [h_{t-1}, x_t] + b_i)$ (input gate)
  - $o_t = \sigma(W_o [h_{t-1}, x_t] + b_o)$ (output gate)

- [ ] **GRU (Gated Recurrent Unit)**
  - Simplified LSTM: reset gate + update gate
  - Fewer parameters, comparable performance
  - $z_t = \sigma(W_z [h_{t-1}, x_t])$ (update gate)
  - $r_t = \sigma(W_r [h_{t-1}, x_t])$ (reset gate)

- [ ] **Bidirectional RNN**: Process sequence forward and backward
- [ ] **Seq2Seq (Sequence-to-Sequence)**: Encoder-decoder architecture

## 21.5 Transformers & Attention Mechanism

- [ ] **Attention Mechanism**
  - Problem: Fixed-length context vector in seq2seq is a bottleneck
  - Solution: Weighted sum of all encoder states
  - Attention weights: How much each source word contributes to each target word

- [ ] **Self-Attention**
  - Query (Q), Key (K), Value (V) from the same sequence
  - $\text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right) V$
  - $d_k$ = dimension of keys (scaling factor)

- [ ] **Multi-Head Attention**
  - Multiple attention heads running in parallel
  - Captures different relationships/patterns
  - Output concatenated and projected

- [ ] **Transformer Architecture** (Vaswani et al., 2017 — "Attention Is All You Need")
  - Encoder: Self-attention + Feed-forward (×N)
  - Decoder: Masked self-attention + Cross-attention + Feed-forward (×N)
  - Positional encoding (since no recurrence)
  - Layer normalization, residual connections

- [ ] **Pre-trained Transformer Models**
  - **BERT** (2018): Bidirectional encoder, masked language model + next sentence prediction
  - **GPT** (2018→): Autoregressive decoder, language generation
  - **T5**: Text-to-text framework
  - **Vision Transformer (ViT)**: Transformers for images (patch-based)

## 21.6 Generative Models

- [ ] **Generative Adversarial Networks (GANs)**
  - Generator (G): Creates fake data from noise
  - Discriminator (D): Distinguishes real from fake
  - Min-max game: $\min_G \max_D E[\log D(x)] + E[\log(1-D(G(z)))]$
  - Variants: DCGAN, WGAN, CycleGAN, StyleGAN, Conditional GAN
  - Challenges: Mode collapse, training instability

- [ ] **Variational Autoencoders (VAE)**
  - Encoder → latent space (mean, variance) → Decoder
  - Loss: Reconstruction loss + KL divergence
  - Learns continuous latent representations
  - Reparameterization trick for backpropagation

- [ ] **Diffusion Models**
  - Forward process: Gradually add noise
  - Reverse process: Learn to denoise step by step
  - State-of-the-art for image generation (DALL-E 2, Stable Diffusion, Midjourney)

## 21.7 Transfer Learning

- [ ] **Concept**: Use a model pre-trained on large dataset, fine-tune on your task
- [ ] **Approaches**:
  - Feature extraction: Freeze pre-trained layers, train new classifier head
  - Fine-tuning: Unfreeze some/all layers, train with small learning rate
- [ ] **Common Pre-trained Models**: ImageNet models (ResNet, VGG), BERT, GPT

---

### Recommended Resources
- **Book**: *Deep Learning* — Ian Goodfellow, Yoshua Bengio, Aaron Courville (free online)
- **Book**: *Hands-On Machine Learning* — Géron (Part II)
- **Course**: Deep Learning Specialization — Andrew Ng (Coursera)
- **Paper**: "Attention Is All You Need" — Vaswani et al. (2017)

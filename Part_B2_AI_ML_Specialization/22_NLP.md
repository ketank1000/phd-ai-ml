# 22. Natural Language Processing (NLP)

> **Part B2 — AI/ML Specialization** | SIU PET Complete Study Guide

---

## 22.1 Text Preprocessing Pipeline

Raw text must be cleaned and structured before ML models can process it.

```
Raw Text → Tokenize → Lowercase → Remove Stop Words → Stem/Lemmatize → Vectorize
```

| Step | Description | Example |
|------|-------------|---------|
| **Tokenization** | Split text into tokens (words, subwords, characters) | "I can't run" → ["I", "ca", "n't", "run"] |
| **Lowercasing** | Normalize case | "NLP" → "nlp" |
| **Stop word removal** | Remove common words with low information | Remove: "the", "is", "at", "in" |
| **Stemming** | Chop word to approximate root (rule-based) | "running" → "run", "better" → "better" |
| **Lemmatization** | Reduce to dictionary form (uses vocabulary) | "running" → "run", "better" → "good" |
| **POS Tagging** | Assign part of speech to each word | "run" → VERB, "fast" → ADJ |

**Stemming vs. Lemmatization:**
- **Stemming** (Porter, Snowball): Fast, crude. "studies" → "studi", "studying" → "studi"
- **Lemmatization** (WordNet, spaCy): Slower, accurate. "studies" → "study", "studying" → "study"

**Subword tokenization (modern):** BPE (Byte-Pair Encoding), WordPiece, SentencePiece — splits rare words into known subwords. "unhappiness" → ["un", "happiness"] or ["un", "happ", "iness"]. Used by BERT (WordPiece), GPT (BPE).

---

## 22.2 Text Representation

### 22.2.1 Bag of Words (BoW)

Represent each document as a vector of word counts:

```
Doc1: "I love NLP"         → [1, 1, 1, 0, 0]
Doc2: "I love deep learning" → [1, 1, 0, 1, 1]
Vocabulary: [I, love, NLP, deep, learning]
```

**Weakness:** Ignores word order ("dog bites man" = "man bites dog"), sparse vectors, no semantic meaning.

### 22.2.2 TF-IDF (Term Frequency — Inverse Document Frequency)

**Weight words by how important they are in a document relative to the whole corpus:**

$$\text{TF-IDF}(t, d) = \text{TF}(t, d) \times \text{IDF}(t)$$

$$\text{TF}(t,d) = \frac{\text{count of } t \text{ in } d}{\text{total words in } d}, \quad \text{IDF}(t) = \log\frac{N}{\text{DF}(t)}$$

- **High TF-IDF:** Word is frequent in this document but rare across corpus → important
- **Low TF-IDF:** Word is common everywhere (e.g., "the") → not discriminative

### 22.2.3 Word Embeddings — Dense Vector Representations

**Key insight:** Represent words as dense vectors (100-300 dimensions) where semantically similar words are close together.

#### Word2Vec (Google, 2013)

| Architecture | Task | Input → Output |
|-------------|------|----------------|
| **CBOW** | Predict center word from context | "The ___ sat on mat" → "cat" |
| **Skip-gram** | Predict context from center word | "cat" → "The", "sat", "on", "mat" |

**Famous property — vector arithmetic:**

$$\vec{\text{king}} - \vec{\text{man}} + \vec{\text{woman}} \approx \vec{\text{queen}}$$

**Training:** Use a shallow neural network with one hidden layer. The hidden layer weights become the word vectors.

#### GloVe (Stanford, 2014)

- Based on **word co-occurrence statistics** from the entire corpus
- Combines global matrix factorization with local context window methods
- Objective: $\sum_{i,j} f(X_{ij})(w_i^T \tilde{w}_j + b_i + \tilde{b}_j - \log X_{ij})^2$

#### FastText (Facebook, 2016)

- Represents words as **bag of character n-grams**
- "where" → ["<wh", "whe", "her", "ere", "re>"]
- **Handles OOV words** by composing n-gram vectors
- Better for morphologically rich languages

**Embedding Comparison:**

| Property | Word2Vec | GloVe | FastText |
|----------|----------|-------|----------|
| Training | Local context windows | Global co-occurrence | Subword n-grams |
| OOV handling | None | None | Yes (via subwords) |
| Morphology | Poor | Poor | Excellent |
| Speed | Fast | Fast (pre-computed) | Moderate |

### 22.2.4 Contextual Embeddings

**Problem with static embeddings:** "bank" has the same vector whether it means financial or river bank.

**Solution: Contextual embeddings** — the same word gets different vectors based on context:
- **ELMo** (2018): Bi-LSTM based, 3 layers of context
- **BERT** (2018): Transformer-based, bidirectional — different embedding for "bank" in different sentences

---

## 22.3 Language Models

A language model assigns probability to sequences of words:

$$P(w_1, w_2, ..., w_n) = \prod_{i=1}^{n} P(w_i | w_1, ..., w_{i-1})$$

### 22.3.1 N-gram Models

Approximate by looking at only the last $n-1$ words:

$$P(w_i | w_1...w_{i-1}) \approx P(w_i | w_{i-n+1}...w_{i-1})$$

| Model | Context | Example |
|-------|---------|---------|
| Unigram | $P(w)$ | Independent word probabilities |
| Bigram | $P(w_i \| w_{i-1})$ | "I am" → P("am" \| "I") |
| Trigram | $P(w_i \| w_{i-2}, w_{i-1})$ | "I am happy" → P("happy" \| "I", "am") |

**Smoothing:** Handle unseen n-grams (zero probability). Add-k (Laplace), Kneser-Ney, Good-Turing.

**Perplexity** — evaluation metric for language models:

$$\text{PPL} = 2^{H(P)} = 2^{-\frac{1}{N}\sum \log_2 P(w_i | \text{context})}$$

Lower perplexity = better model. Perplexity of 100 means the model is as confused as choosing uniformly from 100 words at each step.

### 22.3.2 BERT (Bidirectional Encoder Representations from Transformers)

**Architecture:** Transformer encoder only (no decoder).

**Pre-training tasks:**

1. **Masked Language Model (MLM):** Randomly mask 15% of tokens, predict them.
   - "The [MASK] sat on the [MASK]" → predict "cat", "mat"
   - Forces bidirectional understanding

2. **Next Sentence Prediction (NSP):** Given two sentences, predict if B follows A.
   - (A: "The cat sat.", B: "It purred softly.") → IsNext
   - (A: "The cat sat.", B: "Stock prices rose.") → NotNext

**Fine-tuning:** Add a task-specific head on top:
- **Classification:** [CLS] token → linear layer → softmax
- **NER:** Each token → label (B-PER, I-PER, O, ...)
- **QA:** Predict start and end positions of answer span

**BERT Sizes:** BERT-base (110M params, 12 layers, 768 hidden), BERT-large (340M, 24 layers, 1024 hidden).

### 22.3.3 GPT (Generative Pre-trained Transformer)

**Architecture:** Transformer decoder only (masked self-attention — cannot see future tokens).

**Pre-training:** Autoregressive language modeling — predict next token.

| Model | Year | Parameters | Key Capability |
|-------|------|-----------|----------------|
| GPT-1 | 2018 | 117M | Transfer learning for NLP |
| GPT-2 | 2019 | 1.5B | Coherent long text generation |
| GPT-3 | 2020 | 175B | Few-shot learning, in-context learning |
| GPT-4 | 2023 | ~1.8T (estimated) | Multimodal, reasoning |

**In-context learning (GPT-3+):** Provide examples in the prompt, no fine-tuning needed:
```
Translate English to French:
sea otter → loutre de mer
cheese → fromage
hello →
```

### 22.3.4 BERT vs GPT Comparison

| Feature | BERT | GPT |
|---------|------|-----|
| Architecture | Encoder only | Decoder only |
| Context | Bidirectional | Left-to-right (causal) |
| Pre-training | Masked LM + NSP | Next token prediction |
| Best for | Understanding tasks (NER, QA, classification) | Generation tasks (text, code, dialogue) |
| Fine-tuning | Task-specific head | Prompt engineering / fine-tune |

---

## 22.4 Core NLP Tasks

### 22.4.1 Text Classification

| Task | Input → Output | Methods |
|------|---------------|---------|
| **Sentiment Analysis** | "Great movie!" → Positive | BERT, LSTM, Logistic Reg + TF-IDF |
| **Spam Detection** | Email → Spam/Ham | Naive Bayes, SVM, BERT |
| **Topic Classification** | Article → Category | CNN text, BERT |

### 22.4.2 Named Entity Recognition (NER)

Identify and classify named entities in text:

```
[Barack Obama]_PERSON was born in [Hawaii]_LOCATION in [1961]_DATE.
He served as president of the [United States]_GPE.
```

| Entity Type | Abbreviation | Examples |
|------------|-------------|---------|
| Person | PER | Barack Obama, Marie Curie |
| Organization | ORG | Google, WHO |
| Location | LOC | Mount Everest, Pacific Ocean |
| Geo-Political Entity | GPE | India, New York |
| Date | DATE | January 2024, 1961 |

**Approaches:** BiLSTM-CRF (classic), BERT + token classification (modern).

**BIO tagging:** B-PER (begin person), I-PER (inside person), O (outside entity).

### 22.4.3 Machine Translation

**Evolution:**
1. **Rule-based:** Linguistic rules (1950s-1990s)
2. **Statistical MT:** Phrase-based models (2000s)
3. **Neural MT:** Seq2seq + Attention (2014+)
4. **Transformer-based:** Google Translate (2016+) — state of the art

**Evaluation — BLEU score (Bilingual Evaluation Understudy):**

Measures n-gram overlap between machine translation and reference translations. Score 0-100, higher is better. BLEU considers precision of 1-gram through 4-gram matches with a brevity penalty.

### 22.4.4 Question Answering

| Type | Description | Example |
|------|-------------|---------|
| **Extractive QA** | Find answer span in given passage | SQuAD dataset — BERT extracts "1961" from passage |
| **Generative QA** | Generate answer from knowledge | GPT generates explanation |
| **Open-domain QA** | Retrieve relevant passages + extract/generate answer | Wikipedia search + BERT |

### 22.4.5 Text Summarization

| Type | Method | Pros/Cons |
|------|--------|-----------|
| **Extractive** | Select most important sentences from original | Faithful but may lack coherence |
| **Abstractive** | Generate new summary text (seq2seq/Transformer) | Fluent but may hallucinate |

### 22.4.6 Seq2Seq with Attention

```
Encoder:   [hello] → h1, [world] → h2

Attention:  For each decoder step, compute weighted sum of h1, h2
            α1·h1 + α2·h2 = context vector

Decoder:   context + previous output → [bonjour] → [monde]
```

---

## 22.5 Practice Questions

**Q1.** Compare TF-IDF with Word2Vec for text representation. When would you use each?
> **Answer:** **TF-IDF** produces sparse, high-dimensional vectors based on word frequency statistics. Doesn't capture semantics — "good" and "great" are unrelated vectors. Best for: document retrieval, simple classifiers, when interpretability matters. **Word2Vec** produces dense, low-dimensional vectors (100-300D) trained on context — captures semantic relationships ("king-man+woman≈queen"). Best for: when semantic similarity matters, as input to deep learning models, analogy tasks. **Key difference:** TF-IDF is document-level (reflects word importance in a document), Word2Vec is word-level (reflects word meaning). Modern systems often use contextual embeddings (BERT) which give different representations per context.

**Q2.** Explain BERT's masked language model pre-training. Why is bidirectionality important?
> **Answer:** BERT randomly masks 15% of tokens and trains the model to predict them using context from BOTH sides. Example: "The [MASK] sat on mat" — BERT uses "The" AND "sat on mat" to predict "cat". **Why bidirectional matters:** GPT can only use left context ("The" → predict next). BERT uses both sides, giving it deeper understanding. For NER: in "The bank of the river," only seeing "bank" and left context might suggest financial; seeing "river" (right context) clarifies it's a riverbank. The 15% masking uses: 80% [MASK] token, 10% random word, 10% unchanged — this prevents the model from just learning to predict [MASK] tokens.

**Q3.** What is the difference between stemming and lemmatization? Give examples where they differ.
> **Answer:** Both reduce words to base forms, but differently. **Stemming** uses heuristic rules to chop suffixes — fast but crude. Porter stemmer: "studies" → "studi", "studying" → "studi", "dies" → "di". **Lemmatization** uses vocabulary and morphological analysis — slower but accurate. WordNet: "studies" → "study", "studying" → "study", "better" → "good", "was" → "be". **Key difference:** Stemming may produce non-words ("studi"), lemmatization always produces valid dictionary words. **Use stemming** for fast, approximate matching (search engines). **Use lemmatization** for tasks needing accuracy (text analysis, NLP pipelines).

**Q4.** Explain the attention mechanism in Seq2seq models. Why was it a breakthrough?
> **Answer:** In basic Seq2seq, the encoder compresses the entire input into a single fixed-length vector — this **bottleneck** loses information for long sequences. **Attention** lets the decoder look at ALL encoder hidden states at each generation step. At each decoder step $t$: (1) compute alignment scores between decoder state and all encoder states; (2) softmax → attention weights $\alpha$; (3) weighted sum of encoder states → context vector; (4) use context + previous output to predict next word. **Breakthrough because:** handles long sequences (no bottleneck), provides interpretable alignment (which input words influenced each output word), and significantly improved translation quality. This directly led to the Transformer's self-attention.

**Q5.** How does GPT-3's "in-context learning" work? How is it different from traditional fine-tuning?
> **Answer:** **Traditional fine-tuning:** Update model weights on task-specific labeled data (requires gradient computation, GPU, training loop). **In-context learning:** Provide task demonstrations in the prompt — the model "learns" the pattern from examples without any weight updates. Example: "Translate: cat→gato, dog→perro, house→" → model infers "casa". **How it works:** GPT-3's 175B parameters encode vast knowledge during pre-training. The prompt acts as a "soft specification" — the model uses pattern matching in its attention mechanism to follow the demonstrated format. **Few-shot** (few examples), **One-shot** (one example), **Zero-shot** (just instruction). Limitation: context window limits the number of examples.

---

*Previous: [Chapter 21 — Deep Learning](21_Deep_Learning.md) | Next: [Chapter 23 — Computer Vision](23_Computer_Vision.md)*

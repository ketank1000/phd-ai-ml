# 22. Natural Language Processing (NLP)

> **Part B2 — AI/ML Specialization** | SIU PET Study Guide

---

## 22.1 Text Preprocessing

- [ ] **Tokenization**: Split text into words/subwords/characters
- [ ] **Lowercasing**: Convert to lowercase
- [ ] **Stop word removal**: Remove common words (the, is, at)
- [ ] **Stemming**: Reduce to root form (running → run); Porter stemmer
- [ ] **Lemmatization**: Reduce to dictionary form (better → good); WordNet
- [ ] **Sentence segmentation, POS tagging**

## 22.2 Text Representation

- [ ] **Bag of Words (BoW)**: Count of each word in document
- [ ] **TF-IDF**: Term Frequency × Inverse Document Frequency
  - $TF\text{-}IDF(t,d) = TF(t,d) \times \log\frac{N}{DF(t)}$
  - High value → word is important in this document but rare overall

- [ ] **Word Embeddings**
  - **Word2Vec** (Google, 2013):
    - CBOW: Predict word from context
    - Skip-gram: Predict context from word
    - Properties: king − man + woman ≈ queen
  - **GloVe**: Global Vectors, based on co-occurrence matrix
  - **FastText**: Subword embeddings, handles OOV (out-of-vocabulary) words

## 22.3 Language Models

- [ ] **N-gram Models**: $P(w_n | w_1...w_{n-1}) \approx P(w_n | w_{n-k}...w_{n-1})$
- [ ] **Neural Language Models**: RNN/LSTM-based
- [ ] **BERT**: Masked LM + Next Sentence Prediction, bidirectional encoder
- [ ] **GPT Series**: Autoregressive, decoder-only, generative
- [ ] **Sentence Transformers**: Sentence-BERT for semantic similarity

## 22.4 NLP Tasks

- [ ] **Text Classification**: Sentiment analysis, spam detection, topic classification
- [ ] **Named Entity Recognition (NER)**: Identify entities (person, location, organization)
- [ ] **Machine Translation**: Seq2seq with attention, Transformer-based
- [ ] **Question Answering**: Extractive (find answer span) vs. Generative
- [ ] **Text Summarization**: Extractive vs. Abstractive
- [ ] **Information Retrieval**: Document ranking, relevance scoring

---

### Recommended Resources
- **Book**: *Speech and Language Processing* — Jurafsky & Martin (free online draft)
- **Book**: *Natural Language Processing with Python* — Bird, Klein, Loper (NLTK book)
- **Course**: CS224N — NLP with Deep Learning (Stanford, free on YouTube)

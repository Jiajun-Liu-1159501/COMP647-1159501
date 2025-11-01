# COMP647-1159501 ML and AI

[Kaggle Link](https://www.kaggle.com/datasets/atulanandjha/stanford-sentiment-treebank-v2-sst2?select=Writing+Code+for+NLP+Research.pdf)

This project implements a **LSTM (Long Short-Term Memory)** neural network for binary sentiment classification on the **Stanford Sentiment Treebank (SST)** dataset. The goal is to train a model that can automatically determine the sentiment polarity (positive or negative) of movie reviews.

---

## Project Objectives

The main objectives of this project are:

1. **Implement LSTM Model**: Build an LSTM neural network from scratch for text classification
2. **Data Preprocessing**: Process the raw Stanford Sentiment Treebank dataset
3. **Model Training & Evaluation**: Train the model on SST-2 dataset and evaluate performance
4. **Sentiment Prediction**: Perform sentiment classification on new movie reviews

---

## Implementation

### 1. Sentiment Analysis

Sentiment analysis is a fundamental task in Natural Language Processing (NLP) that aims to identify the emotional tone expressed in text. Common applications include:

- Social media sentiment monitoring
- Product review analysis
- Customer feedback processing
- Movie/book review classification

### 2. LSTM

**LSTM** is a specialized type of Recurrent Neural Network (RNN), proposed by Hochreiter and Schmidhuber in 1997.

**Application in Sentiment Analysis**:

- LSTM can understand word order and contextual relationships in sentences
- Can recognize the impact of negation words and transition words on sentiment

### 3. Stanford Sentiment Treebank (SST)

**SST** is a sentiment analysis benchmark dataset released by Stanford University in 2013, widely used for evaluating NLP model performance.

**Data Source**: Movie reviews collected from Rotten Tomatoes

**Version Differences**:

- **SST-1**: Five-class classification (very negative, negative, neutral, positive, very positive)
- **SST-2**: Binary classification (negative, positive), excluding neutral samples

---

## Dataset

The downloaded dataset contains three folders.

### 1. `/SST2-Data/stanfordSentimentTreebank/`

Main processed dataset folder, has 11,855 sentences (parsed sub-sentences)

- `datasetSentences.txt`: All sentences with their indices

  - Format: `sentence_index [TAB] sentence_text`
  - Contains 11,855 sentences parsed from original snippets

- `datasetSplit.txt`: Dataset split labels

  - Format: `sentence_index,split_label`
  - Split labels: 1 = train, 2 = test, 3 = dev (validation)

- `dictionary.txt`: All phrases and their IDs

  - Format: `phrase|phrase_id`
  - Contains 239,232 phrases (including sub-phrases from parse trees)

- `sentiment_labels.txt`: Sentiment scores for all phrases

  - Format: `phrase_id|sentiment_value`
  - Sentiment values range from 0 (most negative) to 1 (most positive)

- `SOStr.txt` & `STree.txt`: Parse tree structures
  - Encodes syntactic parse trees for each sentence
  - Useful for tree-based models (not needed for standard LSTM)

**For SST-2 Binary Classification**:

- Sentiment value ≤ 0.4 → Negative (label = 0)
- Sentiment value ≥ 0.6 → Positive (label = 1)
- 0.4 < Sentiment value < 0.6 → Neutral (excluded in SST-2)

### 2. `stanfordSentimentTreebankRaw/`

Raw, unprocessed data, has 10,605 original snippets

- `original_rt_snippets.txt`: 10,605 raw snippets from Rotten Tomatoes HTML files
  - Original review text before sentence parsing
  - Some snippets contain multiple sentences

### 3. `trainDevTestTrees_PTB/`

Pre-split data in Penn Treebank (PTB) parse tree format

- `train.txt`: Training set with parse trees
- `dev.txt`: Development/validation set with parse trees
- `test.txt`: Test set with parse trees

Each line contains a parse tree with sentiment labels at each node

```
(3 (2 (2 The) (2 movie)) (4 (3 (2 is) (4 great))))
```

- Numbers in parentheses are sentiment labels (0-4 for 5-class)
- Tree structure shows syntactic composition

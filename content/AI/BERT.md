---
title: BERT
aliases:
  - BERT
draft: false
tags:
  - ArtificialIntelligence
  - "#ML"
  - "#Framework"
  - Status200
author:
  - Sarthak Chandajkar
---
# BERT

**BERT** (Bidirectional Encoder Representations from Transformers) is a transformative model in [[Natural Language Processing]] (NLP), designed to understand and generate contextualized word representations. Built on the [[Transformers]] architecture, BERT’s bidirectional approach captures word context from both directions, making it highly effective for tasks like text classification, question answering, and named entity recognition. This note details BERT’s architecture, training process, and applications, with backlinks to related concepts.

## Architecture

BERT is based on the encoder component of the [[Transformers]] architecture, consisting of multiple layers of interconnected nodes. Key components include:

- **Input Embeddings**: Converts input tokens into dense vectors, combining:
    
    - **Token Embeddings**: Represent individual words or subwords (using WordPiece tokenization).
    - **Positional Embeddings**: Encode word positions to capture sequence order.
    - **Segment Embeddings**: Distinguish between sentence pairs (e.g., in question-answering tasks).
- **Transformer Layers**: Stacked layers (e.g., 12 for BERT-base, 24 for BERT-large) with:
    
    - **Multi-Head Self-Attention**: Captures relationships between all tokens in a sequence, enabling bidirectionality.
    - **Feed-Forward Networks**: Apply non-linear transformations to each token.
    - **Layer Normalization**: Stabilizes training (see [[Batch Normalization]] for related concepts).
- **Output**: Contextualized representations for each token, plus a special `[CLS]` token for sentence-level tasks.
    

> [!NOTE] Bidirectional Context  
> Unlike unidirectional models (e.g., GPT), BERT processes the entire input sequence simultaneously, capturing left and right context for each word.

### Mathematical Representation

For an input sequence of tokens $x_1, x_2, \dots, x_n$, BERT computes contextualized representations $h_i$ for each token via:  
$$  
h_i = \text{Transformer}(x_i, x_1, \dots, x_n)  
$$  
The `[CLS]` token’s output $h_{\text{CLS}}$ is often used for classification tasks, processed through a feed-forward layer:  
$$  
p = \text{softmax}(W h_{\text{CLS}} + b)  
$$

- $W$, $b$: Learnable weights and biases.
- $p$: Probability distribution over classes.

## Training BERT

BERT is pre-trained on large corpora using two unsupervised objectives, then fine-tuned for specific tasks.

### Pre-Training Objectives

1. **Masked Language Model (MLM)**:
    - Randomly masks 15% of input tokens (replaced with `[MASK]`, random tokens, or unchanged).
    - Predicts masked tokens based on context.
    - Loss: Cross-entropy over masked token predictions.
2. **Next Sentence Prediction (NSP)**:
    - Given two sentences, predicts if the second follows the first (50% positive, 50% negative pairs).
    - Loss: Binary cross-entropy.

Pre-training uses datasets like Wikipedia and BooksCorpus, optimized with [[Adam Optimizer]] and [[Backpropagation]].

### Fine-Tuning

BERT is fine-tuned on task-specific labeled data (e.g., sentiment analysis, question answering) by:

- Adding a task-specific output layer (e.g., linear layer for classification).
- Updating all parameters using [[Gradient Descent Algorithm]].
- Adjusting the [[Cost Function]] (e.g., cross-entropy for classification).

> [!TIP] Practical Tip  
> Fine-tune with a small learning rate (e.g., $2 \times 10^{-5}$) to preserve pre-trained weights. Use [[Feature Scaling]] for input embeddings if custom preprocessing is applied.

### Real-World Example

Fine-tuning BERT for sentiment analysis on IMDB reviews:

- **Input**: Movie review text (e.g., “This film was amazing!”).
- **Output**: Positive or negative sentiment.
- **Process**: Tokenize text, feed through BERT, use `[CLS]` output for classification, and optimize with [[Adam Optimizer]].
- **Result**: High accuracy in detecting sentiment, even for nuanced reviews.

## Advantages

- **Bidirectional Context**: Captures richer word representations than unidirectional models.
- **Transfer Learning**: Pre-trained BERT can be fine-tuned for diverse tasks with minimal data.
- **Scalability**: Handles various input lengths and tasks (e.g., sentence classification, token-level tagging).
- **Versatility**: Excels in tasks like question answering, text classification, and named entity recognition.

## Challenges

1. **Computational Cost**: BERT’s large models (e.g., BERT-large with 340M parameters) require significant memory and compute power. Use GPUs or TPUs for efficiency.
2. **Overfitting on Small Datasets**: Fine-tuning on limited data may overfit. Apply [[Regularization]] techniques like dropout.
3. **Inference Speed**: Slow for real-time applications. Variants like DistilBERT or [[ALBERT]] improve efficiency.

## Applications

- **Question Answering**: Extracting answers from text (e.g., SQuAD dataset).
- **Text Classification**: Sentiment analysis, spam detection.
- **Named Entity Recognition**: Identifying entities like names or organizations in text.
- **Machine Translation**: Enhancing translation systems with contextual embeddings.

### Real-World Example

In a customer service chatbot, BERT processes user queries (e.g., “Where’s my order?”) to classify intent (e.g., “track order”) and extract entities (e.g., “order”). This enables accurate, context-aware responses.

## Implementation Example

Below is a [[PyTorch]] snippet for fine-tuning BERT on a classification task using the Hugging Face Transformers library:

```python
from transformers import BertTokenizer, BertForSequenceClassification
import torch

# Load pre-trained BERT and tokenizer
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
model = BertForSequenceClassification.from_pretrained('bert-base-uncased', num_labels=2)

# Sample input: Text for sentiment analysis
text = "This movie is fantastic!"
inputs = tokenizer(text, return_tensors="pt", padding=True, truncation=True, max_length=128)

# Forward pass
outputs = model(**inputs)
logits = outputs.logits
probs = torch.softmax(logits, dim=-1)

# Fine-tuning setup
optimizer = torch.optim.Adam(model.parameters(), lr=2e-5)
labels = torch.tensor([1])  # Positive sentiment
loss = torch.nn.CrossEntropyLoss()(logits, labels)
loss.backward()
optimizer.step()

print(f"Predicted probabilities: {probs}")
```

This code fine-tunes BERT for binary sentiment classification, leveraging [[Backpropagation]] and [[Adam Optimizer]].

## Related Concepts

- [[Transformers]]: Core architecture underlying BERT.
- [[Gradient Descent Algorithm]]: Optimizes BERT during training.
- [[Backpropagation]]: Computes gradients for parameter updates.
- [[Adam Optimizer]]: Default optimizer for BERT.
- [[Regularization]]: Mitigates overfitting during fine-tuning.
- [[Natural Language Processing]]: Field where BERT excels.

## Further Exploration

Experiment with BERT using Hugging Face’s [[Transformers]] library on datasets like GLUE or SQuAD. Explore variants like [[ALBERT]] or RoBERTa for improved efficiency or performance. Visualize attention weights to understand how BERT captures context.
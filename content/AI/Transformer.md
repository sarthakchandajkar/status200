---
title: Transformer
aliases: 
draft: false
tags:
  - AI
  - Status200
author:
  - Sarthak Chandajkar
---
**Transformers** are a powerful architecture in [[Machine Learning]] and [[Deep Learning]], revolutionizing [[Natural Language Processing]] (NLP) and extending to tasks like image processing and time-series analysis. Introduced in the paper "Attention is All You Need" (2017), Transformers rely on self-attention mechanisms to process input sequences, enabling efficient and scalable modeling of long-range dependencies. This note covers their architecture, training, and applications, with backlinks to related concepts.

## Architecture

Transformers consist of an **encoder** and **decoder**, each composed of multiple layers, designed to process sequential data (e.g., text, images). Unlike [[Recurrent Neural Networks]], Transformers process all tokens simultaneously, leveraging parallelization for efficiency.

### Key Components

1. **Input Embeddings**:
    
    - Converts tokens (e.g., words, subwords) into dense vectors.
    - Adds **positional encodings** to capture sequence order, as Transformers lack inherent sequential processing.
    - Formula: $x_i = \text{TokenEmbedding}(w_i) + \text{PositionalEncoding}(i)$, where $w_i$ is the $i$-th token.
2. **Self-Attention Mechanism**:
    
    - Computes relationships between all tokens in a sequence, weighting their importance.
    - **Scaled Dot-Product Attention**:  
        $$  
        \text{Attention}(Q, K, V) = \text{softmax}\left(\frac{QK^T}{\sqrt{d_k}}\right)V  
        $$
        - $Q$, $K$, $V$: Query, Key, and Value matrices derived from input embeddings.
        - $d_k$: Dimension of keys, used for scaling to prevent large values.
    - **Multi-Head Attention**: Applies attention multiple times in parallel, capturing diverse relationships.
3. **Feed-Forward Networks**:
    
    - Applies a two-layer neural network to each token independently, adding non-linearity.
    - Formula: $\text{FFN}(x) = \text{ReLU}(xW_1 + b_1)W_2 + b_2$.
4. **Layer Normalization**:
    
    - Stabilizes training by normalizing layer outputs (see [[Batch Normalization]]).
    - Applied after attention and feed-forward layers.
5. **Encoder-Decoder Structure**:
    
    - **Encoder**: Processes input sequence to produce contextualized representations.
    - **Decoder**: Generates output sequence, using encoder outputs and self-attention on partial outputs.
    - Used in tasks like machine translation (encoder: source language, decoder: target language).

> [!NOTE] Why Self-Attention?  
> Self-attention allows Transformers to weigh the importance of each token relative to all others, capturing long-range dependencies (e.g., relating “dog” to “barked” across a sentence) unlike [[Recurrent Neural Networks]].

## Training Transformers

Transformers are trained to minimize an [[Objective Function]] (e.g., cross-entropy loss) using [[Backpropagation]] and optimizers like [[Adam Optimizer]]. The process involves:

1. **Pre-Training**:
    
    - Train on large, unsupervised datasets (e.g., Wikipedia, Common Crawl) with tasks like masked language modeling (see [[BERT]]).
    - Example: Predict masked words in a sentence to learn contextual representations.
2. **Fine-Tuning**:
    
    - Adapt pre-trained model to specific tasks (e.g., sentiment analysis, question answering) using labeled data.
    - Use small [[Learning Rate]] (e.g., $2 \times 10^{-5}$) to preserve pre-trained weights.
3. **Data Pipeline**:
    
    - Tokenize input using methods like WordPiece or Byte-Pair Encoding.
    - Apply [[Feature Scaling]] or normalization to embeddings for stability.

### Real-World Example

Fine-tuning a Transformer like [[BERT]] for question answering on the SQuAD dataset:

- **Input**: Passage and question (e.g., “Who won the 2020 election?”).
- **Output**: Span of text answering the question.
- **Process**: Use [[Adam Optimizer]] with $\eta = 3 \times 10^{-5}$ to minimize cross-entropy loss, achieving high accuracy.

## Advantages

- **Parallelization**: Processes all tokens simultaneously, unlike [[Recurrent Neural Networks]], enabling faster training.
- **Long-Range Dependencies**: Captures relationships across long sequences via self-attention.
- **Scalability**: Handles large datasets and models (e.g., GPT, [[BERT]]) with GPUs/TPUs.
- **Versatility**: Applicable to NLP, vision (e.g., Vision Transformers), and more.

## Challenges

1. **Computational Cost**: Large models (e.g., [[BERT]]-large with 340M parameters) require significant resources.
    - **Solution**: Use efficient variants like DistilBERT or [[ALBERT]].
2. **Memory Usage**: Self-attention scales quadratically with sequence length ($O(n^2)$).
    - **Solution**: Apply techniques like sparse attention or windowed attention.
3. **Overfitting**: Large models may overfit on small datasets.
    - **Solution**: Use [[Regularization]] (e.g., dropout) or data augmentation.

> [!TIP] Practical Tip  
> When fine-tuning Transformers, use a small [[Learning Rate]] (e.g., $2 \times 10^{-5}$) and monitor validation loss to avoid overfitting. Ensure input sequences are padded or truncated to a fixed length (e.g., 512 tokens) for efficient batching.

### Real-World Example

In a machine translation system (e.g., English to Spanish), a Transformer model processes source sentences in the encoder and generates translations in the decoder. Trained on a dataset like WMT, it uses [[Adam Optimizer]] to minimize cross-entropy loss, achieving fluent translations.

## Implementation Example

Below is a [[TensorFlow]] example using the Hugging Face Transformers library to fine-tune a Transformer for text classification:

```python
from transformers import TFBertForSequenceClassification, BertTokenizer
import tensorflow as tf

# Load pre-trained BERT and tokenizer
tokenizer = BertTokenizer.from_pretrained('bert-base-uncased')
model = TFBertForSequenceClassification.from_pretrained('bert-base-uncased', num_labels=2)

# Sample input: Text for sentiment analysis
texts = ["This movie is great!", "I didn't enjoy the film."]
inputs = tokenizer(texts, return_tensors="tf", padding=True, truncation=True, max_length=128)

# Labels: Positive (1), Negative (0)
labels = tf.constant([1, 0])

# Compile model
optimizer = tf.keras.optimizers.Adam(learning_rate=2e-5)
model.compile(optimizer=optimizer, loss='sparse_categorical_crossentropy', metrics=['accuracy'])

# Train model
model.fit(inputs, labels, epochs=3, batch_size=8)

# Predict
predictions = model.predict(inputs)
print(f"Predicted probabilities: {tf.nn.softmax(predictions.logits)}")
```

This code fine-tunes [[BERT]] for sentiment analysis using [[Adam Optimizer]] and [[Backpropagation]].

## Applications

- **Natural Language Processing**: Tasks like text classification, question answering, and translation (e.g., [[BERT]], GPT).
- **Computer Vision**: Vision Transformers (ViT) for image classification or object detection (e.g., [[Faster R-CNN]] enhancements).
- **Speech Processing**: Audio-to-text transcription with models like Wav2Vec.
- **Time-Series Analysis**: Forecasting with Transformer-based models.

### Real-World Example

In a customer support chatbot, a Transformer model processes user queries (e.g., “Track my order”) to classify intents and extract entities, trained on a dialogue dataset using [[TensorFlow]] or [[PyTorch]], delivering accurate responses in real-time.

## Related Concepts

- [[BERT]]: A Transformer-based model for NLP tasks.
- [[Gradient Descent Algorithm]]: Optimizes the [[Objective Function]].
- [[Backpropagation]]: Computes gradients for training.
- [[Adam Optimizer]]: Common optimizer for Transformers.
- [[Feature Scaling]]: Stabilizes input embeddings.
- [[Natural Language Processing]]: Primary domain for Transformers.

## Further Exploration

Experiment with Transformers using Hugging Face’s [[Transformers]] library on datasets like GLUE or SQuAD. Visualize attention weights to understand token relationships. Explore variants like [[ALBERT]] or Vision Transformers for cutting-edge applications.


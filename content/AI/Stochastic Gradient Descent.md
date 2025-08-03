---
title: Stochastic Gradient Descent
aliases: 
draft: false
tags:
  - AI
  - Status200
author:
  - Sarthak Chandajkar
---
**Stochastic Gradient Descent (SGD)** is a widely used optimization algorithm in [[Machine Learning]] and [[Deep Learning]], a variant of the [[Gradient Descent Algorithm]] that updates model parameters using a single or small subset of training samples at each step. By introducing randomness, SGD accelerates convergence and can escape local minima, making it efficient for large datasets and complex models like [[Neural Networks]]. This note covers its mechanics, benefits, and applications, with backlinks to related concepts.

## Definition

SGD minimizes an [[Objective Function]] $J(\theta)$, where $\theta$ represents model parameters (e.g., weights in a [[Neural Network]]), by updating parameters based on the gradient of the loss for a single training example (or a small batch). The update rule is:  
$$  
\theta = \theta - \eta \cdot \nabla J(\theta; x_i, y_i)  
$$

- $\theta$: Model parameters.
- $\eta$: [[Learning Rate]], controlling step size.
- $\nabla J(\theta; x_i, y_i)$: [[Gradient Vector]] of the [[Objective Function]] for a single sample $(x_i, y_i)$.

In practice, SGD often refers to **Mini-Batch SGD**, where gradients are computed over a small batch of $n$ samples:  
$$  
\theta = \theta - \eta \cdot \frac{1}{n} \sum_{i=1}^n \nabla J(\theta; x_i, y_i)  
$$

> [!NOTE] Intuition  
> Unlike [[Gradient Descent Algorithm]], which uses the entire dataset, SGD takes quick, noisy steps based on one or a few samples, like navigating a maze by making small, frequent guesses rather than planning the entire route.

## Mechanics

SGD iterates over the following steps:

1. **Sample Selection**: Randomly select one sample (or a mini-batch) from the training dataset.
2. **Forward Pass**: Compute the model’s prediction for the sample(s).
3. **Compute Loss**: Evaluate the [[Objective Function]] (e.g., mean squared error, cross-entropy).
4. **Backward Pass**: Calculate the [[Gradient Vector]] using [[Backpropagation]].
5. **Update Parameters**: Adjust $\theta$ using the update rule above.

The randomness in sample selection introduces noise, which helps escape local minima but can make convergence less stable compared to batch [[Gradient Descent Algorithm]].

## Variants

1. **Pure SGD**: Uses a single sample per update. Fast but noisy.
2. **Mini-Batch SGD**: Uses a small batch (e.g., 32 or 64 samples). Balances speed and stability, widely used in [[Deep Learning]].
3. **SGD with Momentum**: Incorporates past gradients to smooth updates (see [[Momentum Method]]).
    - Update rule: $v_t = \gamma v_{t-1} + \eta \nabla J(\theta)$, $\theta = \theta - v_t$, where $\gamma$ is the momentum coefficient.

### Real-World Example

In training a [[Convolutional Neural Network]] for image classification (e.g., CIFAR-10), Mini-Batch SGD with a batch size of 32 and $\eta = 0.01$ optimizes the cross-entropy loss, achieving high accuracy while handling large datasets efficiently.

## Advantages

- **Efficiency**: Processes one or a few samples per iteration, reducing memory and computation compared to batch [[Gradient Descent Algorithm]].
- **Scalability**: Suitable for large datasets, as it doesn’t require loading all data into memory.
- **Escape Local Minima**: Randomness helps navigate non-convex [[Objective Function]]s in [[Deep Learning]].
- **Online Learning**: Adapts to streaming data, updating parameters as new samples arrive.

## Challenges

1. **Noisy Updates**: Single-sample gradients introduce variance, leading to erratic convergence.
    - **Solution**: Use Mini-Batch SGD or [[Momentum Method]] to smooth updates.
2. **Learning Rate Tuning**: Requires careful selection of $\eta$. Too high causes divergence; too low slows convergence.
    - **Solution**: Use a [[Learning Rate Scheduler]] or adaptive optimizers like [[Adam Optimizer]].
3. **Sensitivity to Feature Scales**: Uneven feature scales skew gradients.
    - **Solution**: Apply [[Feature Scaling]] (e.g., standardization).

> [!TIP] Practical Tip  
> Start with a batch size of 32 or 64 and $\eta = 0.01$ for Mini-Batch SGD. Monitor the [[Objective Function]] on a validation set and adjust $\eta$ using a [[Learning Rate Scheduler]] if the loss oscillates or plateaus.

### Real-World Example

In a recommendation system (e.g., Spotify), SGD optimizes a [[Neural Network]] to predict user song preferences. Using Mini-Batch SGD with a batch size of 64 and $\eta = 0.005$, the model updates weights incrementally as users stream songs, ensuring personalized recommendations.

## Implementation Example

Below is a [[PyTorch]] implementation of Mini-Batch SGD for linear regression:

```python
import torch
import torch.utils.data as data

# Sample data: house sizes (X) and prices (y)
X = torch.tensor([[1], [2], [3], [4], [5]], dtype=torch.float32)
y = torch.tensor([[2], [4], [5], [4], [5]], dtype=torch.float32)
dataset = data.TensorDataset(X, y)
loader = data.DataLoader(dataset, batch_size=2, shuffle=True)

# Model parameters
m = torch.tensor(0.0, requires_grad=True)
b = torch.tensor(0.0, requires_grad=True)
learning_rate = 0.01
epochs = 1000

# Optimizer
optimizer = torch.optim.SGD([m, b], lr=learning_rate)

# Training loop
for _ in range(epochs):
    for batch_x, batch_y in loader:
        y_pred = m * batch_x + b  # Forward pass
        loss = ((y_pred - batch_y) ** 2).mean()  # MSE loss
        optimizer.zero_grad()  # Clear gradients
        loss.backward()  # Compute gradients
        optimizer.step()  # Update parameters

print(f"Slope: {m.item()}, Intercept: {b.item()}")
```

This code uses Mini-Batch SGD to minimize the mean squared error, leveraging [[Backpropagation]] for gradient computation.

## Comparison with Other Optimizers

- **Vs. [[Gradient Descent Algorithm]]**: SGD is faster for large datasets but noisier due to single-sample updates.
- **Vs. [[Adam Optimizer]]**: SGD is simpler but less adaptive, requiring careful $\eta$ tuning.
- **Vs. [[Momentum Method]]**: SGD with momentum adds smoothing, improving convergence over vanilla SGD.

## Applications

- **Neural Networks**: Training [[Convolutional Neural Networks]] or [[Transformers]] for tasks like image recognition or text classification.
- **Online Learning**: Updating models in real-time, e.g., click prediction in ad systems.
- **Large-Scale Learning**: Optimizing models on massive datasets, like those in [[Natural Language Processing]].

### Real-World Example

In a fraud detection system, Mini-Batch SGD trains a [[Neural Network]] to classify transactions as “fraudulent” or “
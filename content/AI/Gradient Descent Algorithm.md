---
title: Gradient Descent Algorithm
aliases: 
draft: false
tags:
  - AI
  - Status200
author:
  - Sarthak Chandajkar
---
 # Gradient Descent Algorithm

The **Gradient Descent Algorithm** is a foundational optimization technique in [[Machine Learning]] and [[Deep Learning]], used to minimize a [[Cost Function]] by iteratively adjusting model parameters. It leverages the [[Gradient Vector]] to determine the direction and magnitude of parameter updates, converging toward a local or global minimum. This note explores its mechanics, variants, and applications, with backlinks to related concepts.

## Core Concept

Gradient Descent minimizes a [[Cost Function]] $J(\theta)$, where $\theta$ represents model parameters (e.g., weights in a [[Neural Network]]). The algorithm computes the [[Gradient Vector]] $\nabla J(\theta)$, which points in the direction of steepest increase. By moving in the opposite direction ($-\nabla J(\theta)$), it reduces the cost iteratively.

The update rule is:  
$$  
\theta = \theta - \eta \cdot \nabla J(\theta)  
$$

- $\theta$: Model parameters.
- $\eta$: Learning rate, a hyperparameter controlling step size.
- $\nabla J(\theta)$: [[Gradient Vector]] of the cost function.

> [!NOTE] Intuition  
> Imagine descending a foggy mountain (the cost function) to reach the lowest point. The gradient is like a compass pointing uphill; stepping in the opposite direction with steps sized by $\eta$ leads to the valley.

## Variants of Gradient Descent

Gradient Descent has three main variants, differing in how much data is used to compute the gradient:

1. **Batch Gradient Descent**:
    
    - Uses the entire dataset to compute $\nabla J(\theta)$.
    - **Pros**: Stable convergence, accurate gradient estimation.
    - **Cons**: Slow and memory-intensive for large datasets.
    - **Example**: Optimizing a linear regression model on a small dataset (e.g., 100 house price samples).

2. **Stochastic Gradient Descent (SGD)**:
    
    - Computes the gradient using a single data point, updating parameters incrementally.
    - **Pros**: Faster, escapes local minima due to randomness.
    - **Cons**: Noisy updates may cause erratic convergence.
    - **Example**: Training a [[Neural Network]] on streaming data, like real-time user clicks.

3. **Mini-Batch Gradient Descent**:
    
    - Uses a small batch (e.g., 32 or 64 samples) to compute the gradient.
    - **Pros**: Balances stability and speed, leverages vectorized operations.
    - **Cons**: Requires batch size tuning.
    - **Example**: Common in [[Deep Learning]] frameworks like [[PyTorch]] or [[TensorFlow]] for training [[Convolutional Neural Networks]].

## Learning Rate and Convergence

The learning rate $\eta$ is critical:

- **Too Large**: Overshoots the minimum, causing divergence.
- **Too Small**: Slows convergence, increasing training time.
- **Adaptive**: Methods like [[Adam Optimizer]] adjust $\eta$ dynamically.

> [!TIP] Practical Tip  
> Start with a learning rate like $0.01$ and use a [[Learning Rate Scheduler]] to reduce $\eta$ over time for better convergence.

### Real-World Example

In training a [[Neural Network]] for image classification (e.g., CIFAR-10), [[Mini-Batch Gradient Descent]] with $\eta = 0.001$ and [[Adam Optimizer]] adjusts weights to minimize cross-entropy loss, achieving high accuracy on object recognition.

## Techniques to Improve Convergence

- **Momentum**: Accelerates updates by accumulating past gradients (see [[Momentum Method]]).
- **Adaptive Optimizers**: Algorithms like [[Adam Optimizer]] or [[RMSprop]] adjust $\eta$ per parameter.
- **Learning Rate Schedulers**: Dynamically adjust $\eta$ (e.g., exponential decay).

## Challenges and Solutions

1. **Local Minima**: Non-convex cost functions may trap the algorithm. [[Stochastic Gradient Descent]] or [[Adam Optimizer]] can help escape.
2. **Vanishing/Exploding Gradients**: Common in deep [[Neural Networks]]. Use [[Gradient Clipping]] or [[Batch Normalization]].
3. **Feature Scaling**: Uneven feature scales skew gradients. Apply [[Feature Scaling]] (e.g., standardization) before training.

### Real-World Example

In a recommendation system (e.g., Netflix), Gradient Descent optimizes a [[Cost Function]] to predict user ratings based on viewing history, ensuring personalized movie suggestions.

## Implementation Example

Below is a [[PyTorch]] implementation of Gradient Descent for linear regression:

```python
import torch

# Sample data: house sizes (X) and prices (y)
X = torch.tensor([1, 2, 3, 4, 5], dtype=torch.float32)
y = torch.tensor([2, 4, 5, 4, 5], dtype=torch.float32)
m = torch.tensor(0.0, requires_grad=True)  # Slope
b = torch.tensor(0.0, requires_grad=True)  # Intercept
learning_rate = 0.01
epochs = 1000

# Training loop
for _ in range(epochs):
    y_pred = m * X + b  # Forward pass
    loss = ((y_pred - y) ** 2).mean()  # Mean squared error
    loss.backward()  # Compute gradients
    with torch.no_grad():
        m -= learning_rate * m.grad  # Update slope
        b -= learning_rate * b.grad  # Update intercept
        m.grad.zero_()  # Clear gradients
        b.grad.zero_()

print(f"Slope: {m.item()}, Intercept: {b.item()}")
```

This code minimizes mean squared error using [[Backpropagation]] and [[Stochastic Gradient Descent]].

## Related Concepts

- [[Gradient Vector]]: Guides parameter updates.
- [[Cost Function]]: Objective to minimize.
- [[Backpropagation]]: Computes gradients in [[Neural Networks]].
- [[Adam Optimizer]]: Advanced variant of Gradient Descent.
- [[Feature Scaling]]: Ensures stable gradient updates.
- [[Optimization Algorithms]]: Broader category including [[RMSprop]] and [[Momentum Method]].

## Further Exploration

Experiment with Gradient Descent in [[PyTorch]] or [[TensorFlow]] on datasets like MNIST. Visualize the [[Cost Function]] surface to understand convergence. Explore [[Adam Optimizer]] or [[RMSprop]] for faster optimization in complex models.


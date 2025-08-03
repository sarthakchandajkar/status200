---
title: ADAM
aliases:
  - ADAM
draft: false
tags:
  - AI
  - DeepLearning
  - Status200
author:
  - Sarthak Chandajkar
---
# Adam Optimizer

The **Adam Optimizer** (Adaptive Moment Estimation) is a widely used optimization algorithm in [[Machine Learning]] and [[Deep Learning]], combining momentum and adaptive learning rates to efficiently minimize [[Cost Function]]s. It accelerates [[Gradient Descent Algorithm]] by adapting to the loss landscape's geometry, making it ideal for training [[Neural Networks]]. This note covers its mechanics, advantages, and applications, with backlinks to related concepts.

## Core Concept

Adam optimizes a [[Cost Function]] $J(\theta)$, where $\theta$ represents model parameters (e.g., weights and biases in a [[Neural Network]]). It uses first-order gradients with adaptive estimates of first (mean) and second (uncentered variance) moments of the gradients to update parameters.

The update rule is:  
$$  
\theta_{t+1} = \theta_t - \eta \cdot \frac{\hat{m}_t}{\sqrt{\hat{v}_t} + \epsilon}  
$$

- $\theta_t$: Parameters at step $t$.
- $\eta$: Learning rate (typically $0.001$).
- $\hat{m}_t$: Bias-corrected first moment (mean of gradients).
- $\hat{v}_t$: Bias-corrected second moment (uncentered variance of gradients).
- $\epsilon$: Small constant (e.g., $10^{-8}$) for numerical stability.

### How It Works

Adam maintains two moving averages:

1. **First Moment ($m_t$)**: Exponential moving average of gradients, capturing the direction of updates (similar to [[Momentum Method]]).  
    $$  
    m_t = \beta_1 m_{t-1} + (1 - \beta_1) \nabla J(\theta_t)  
    $$
2. **Second Moment ($v_t$)**: Exponential moving average of squared gradients, estimating gradient variance.  
    $$  
    v_t = \beta_2 v_{t-1} + (1 - \beta_2) [\nabla J(\theta_t)]^2  
    $$

- $\beta_1$, $\beta_2$: Decay rates (typically $0.9$ and $0.999$).

These moments are bias-corrected to account for initialization:  
$$  
\hat{m}_t = \frac{m_t}{1 - \beta_1^t}, \quad \hat{v}_t = \frac{v_t}{1 - \beta_2^t}  
$$

The adaptive learning rate per parameter is computed as $\eta / (\sqrt{\hat{v}_t} + \epsilon)$, enabling larger updates for infrequent features and smaller updates for frequent ones.

> [!NOTE] Why Adaptive Moments?  
> Adam’s use of moment estimates makes it robust to noisy gradients and varying scales, outperforming standard [[Stochastic Gradient Descent]] in many [[Deep Learning]] tasks.

## Advantages

- **Adaptive Learning Rates**: Adjusts step sizes per parameter, improving convergence on complex loss surfaces.
- **Momentum**: Accelerates updates by incorporating past gradients, similar to [[Momentum Method]].
- **Efficiency**: Works well with sparse gradients and large datasets, common in [[Neural Networks]].
- **Robustness**: Less sensitive to hyperparameter choices than plain [[Gradient Descent Algorithm]].

## Challenges

1. **Non-Convergence in Some Cases**: Adam may fail to converge to the global minimum for certain non-convex problems. Variants like [[AMSGrad]] address this.
2. **Hyperparameter Tuning**: While robust, $\eta$, $\beta_1$, and $\beta_2$ may require tuning for optimal performance.
3. **Memory Usage**: Stores two moments per parameter, increasing memory compared to [[Stochastic Gradient Descent]].

> [!TIP] Practical Tip  
> Start with default hyperparameters ($\eta = 0.001$, $\beta_1 = 0.9$, $\beta_2 = 0.999$, $\epsilon = 10^{-8}$) and monitor training loss. Adjust $\eta$ or use a [[Learning Rate Scheduler]] if convergence is slow.

## Real-World Example

In training a [[Convolutional Neural Network]] for image classification (e.g., CIFAR-10 dataset), Adam optimizes the cross-entropy loss. Its adaptive learning rates handle the diverse scales of gradients from convolutional and dense layers, converging faster than [[Stochastic Gradient Descent]].

> **Scenario**: When fine-tuning a pre-trained model like ResNet for object detection, Adam adjusts weights efficiently, balancing large updates for new layers and small updates for pre-trained layers.

## Implementation Example

Below is an implementation of Adam in [[PyTorch]] for a simple [[Neural Network]]:

```python
import torch
import torch.nn as nn
import torch.optim as optim

# Define a simple neural network
class SimpleNN(nn.Module):
    def __init__(self):
        super(SimpleNN, self).__init__()
        self.layer1 = nn.Linear(2, 4)  # Input: 2 features, Output: 4 neurons
        self.relu = nn.ReLU()
        self.layer2 = nn.Linear(4, 1)  # Output: 1 neuron (binary classification)
        self.sigmoid = nn.Sigmoid()

    def forward(self, x):
        x = self.relu(self.layer1(x))
        x = self.sigmoid(self.layer2(x))
        return x

# Initialize model, loss, and Adam optimizer
model = SimpleNN()
criterion = nn.BCELoss()  # Binary cross-entropy loss
optimizer = optim.Adam(model.parameters(), lr=0.001, betas=(0.9, 0.999), eps=1e-8)

# Sample training loop
for epoch in range(100):
    inputs = torch.rand((100, 2))  # Dummy input data
    targets = torch.rand((100, 1))  # Dummy target data
    optimizer.zero_grad()  # Clear gradients
    outputs = model(inputs)  # Forward pass
    loss = criterion(outputs, targets)  # Compute loss
    loss.backward()  # Backpropagation
    optimizer.step()  # Update weights with Adam
```

This code uses Adam to train a binary classifier, leveraging [[Backpropagation]] for gradient computation.

## Comparison with Other Optimizers

- **Vs. [[Stochastic Gradient Descent]]**: Adam is faster and more robust due to adaptive learning rates but requires more memory.
- **Vs. [[Momentum Method]]**: Adam incorporates momentum and adds adaptive scaling, improving performance on non-convex problems.
- **Vs. [[RMSprop]]**: Adam extends RMSprop by adding first-moment estimates, enhancing stability.

## Applications

- **Deep Learning**: Training [[Convolutional Neural Networks]], [[Recurrent Neural Networks]], and [[Transformers]] for tasks like image recognition and language modeling.
- **Reinforcement Learning**: Optimizing policies in environments like game playing.
- **Natural Language Processing**: Fine-tuning models like BERT for text classification.

## Related Concepts

- [[Gradient Descent Algorithm]]: Foundation for Adam’s optimization.
- [[Backpropagation]]: Computes [[Gradient Vector]]s for updates.
- [[Cost Function]]: Objective minimized by Adam.
- [[RMSprop]]: Predecessor to Adam, focusing on second moments.
- [[Learning Rate Scheduler]]: Adjusts $\eta$ dynamically during training.
- [[Feature Scaling]]: Ensures stable gradient updates.

## Further Exploration

Experiment with Adam in [[PyTorch]] or [[TensorFlow]] on datasets like MNIST or CIFAR-10. Compare its performance with [[RMSprop]] or [[Stochastic Gradient Descent]]. Explore [[AMSGrad]] for cases where Adam’s convergence is suboptimal.
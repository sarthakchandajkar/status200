---
title: Neural Networks
aliases: 
draft: false
tags:
  - AI
  - Status200
author:
  - Sarthak Chandajkar
---
# Neural Networks

**Neural Networks** are computational models inspired by the human brain, widely used in [[Machine Learning]] and [[Deep Learning]] for tasks like image recognition, natural language processing, and reinforcement learning. They consist of interconnected nodes (neurons) organized in layers, processing input data to produce meaningful outputs. This note explores their structure, training process, and applications, using backlinks to connect related concepts.

## Structure of Neural Networks

A neural network typically comprises:

- **Input Layer**: Receives raw data (e.g., pixel values of an image).
- **Hidden Layers**: Process data through weighted connections and [[Activation Functions]].
- **Output Layer**: Produces the final prediction or classification.

Each neuron computes a weighted sum of inputs, applies a bias, and passes the result through an [[Activation Function]] (e.g., [[ReLU Activation]], sigmoid) to introduce non-linearity.

> **Example**: For a handwritten digit classifier, the input layer takes pixel intensities (e.g., $28 \times 28$ pixels = $784$ inputs), hidden layers extract features like edges or shapes, and the output layer predicts one of $10$ digits ($0$–$9$).

### Mathematical Representation

For a neuron in layer $l$: 
$[z = \sum_i w_i x_i + b]$  
$[  a = \sigma(z)  ]$

- $w_i$: Weights for inputs $x_i$.
- $b$: Bias term.
- $\sigma$: [[Activation Function]].
- $a$: Neuron’s output.

The network’s parameters (weights and biases) are learned during training.

## Training Neural Networks

Training involves optimizing a [[Cost Function]] $J(\theta)$, where $\theta$ represents weights and biases, using [[Gradient Descent Algorithm]] or its variants (e.g., [[Adam Optimizer]]).

### Key Steps

1. **Forward Propagation**: Compute predictions by passing inputs through layers.
2. **Compute Loss**: Measure error using a [[Cost Function]] (e.g., mean squared error for regression, cross-entropy for classification).
3. **Backpropagation**: Calculate gradients of the loss with respect to parameters via [[Backpropagation]], using the [[Gradient Vector]].
4. **Update Parameters**: Adjust weights and biases using:  
    [  
    \theta = \theta - \eta \cdot \nabla J(\theta)  
    ]
    - $\eta$: Learning rate.
    - $\nabla J(\theta)$: [[Gradient Vector]] of the cost function.

> [!NOTE] Why Backpropagation?  
> [[Backpropagation]] efficiently computes gradients across layers, enabling scalable training of deep networks with millions of parameters.

### Practical Example

Training a neural network to classify cats vs. dogs:

- **Input**: Grayscale images (e.g., $64 \times 64$ pixels = $4096$ inputs).
- **Hidden Layers**: Extract features like edges or textures using convolutional layers (see [[Convolutional Neural Networks]]).
- **Output**: Probability scores for "cat" or "dog."
- **Training**: Use a dataset like Kaggle’s Cats vs. Dogs, minimizing cross-entropy loss with [[Mini-Batch Gradient Descent]].

## Types of Neural Networks

1. **Feedforward Neural Networks (FNNs)**:
    
    - Data flows in one direction (input to output).
    - Used for simple tasks like regression or basic classification.
    - **Example**: Predicting house prices based on features like size and location.
2. **Convolutional Neural Networks (CNNs)**:
    
    - Specialized for image data, using convolutional layers to detect spatial patterns.
    - See [[Convolutional Neural Networks]] for details.
    - **Example**: Image classification in self-driving cars.
3. **Recurrent Neural Networks (RNNs)**:
    
    - Handle sequential data by maintaining a "memory" of previous inputs.
    - Used in [[Natural Language Processing]] (e.g., language modeling).
    - **Example**: Generating text or predicting stock prices.
4. **Transformers**:
    
    - Advanced architecture for [[Natural Language Processing]] and beyond, using attention mechanisms.
    - See [[Transformers]] for details.
    - **Example**: Powering models like BERT for text understanding.

## Challenges and Solutions

1. **Overfitting**: The network memorizes training data, failing to generalize. Use [[Regularization]] techniques like dropout or $L_2$ regularization.
2. **Vanishing/Exploding Gradients**: Deep networks may have unstable gradients. Mitigate with [[ReLU Activation]], [[Batch Normalization]], or [[Gradient Clipping]].
3. **Computational Cost**: Training large networks is resource-intensive. Use GPUs or frameworks like [[PyTorch]] or [[TensorFlow]] for efficiency.

> [!TIP] Practical Tip  
> Apply [[Feature Scaling]] to input data to ensure stable gradient updates. For images, normalize pixel values to $[0, 1]$ or $[-1, 1]$.

## Real-World Applications

- **Computer Vision**: Object detection in autonomous vehicles (e.g., Tesla’s Full Self-Driving).
- **Natural Language Processing**: Chatbots or translation systems (e.g., Google Translate).
- **Healthcare**: Diagnosing diseases from medical images (e.g., detecting tumors in X-rays).
- **Finance**: Fraud detection by analyzing transaction patterns.

> **Scenario**: A neural network in a recommendation system (e.g., YouTube) learns user preferences from watch history, predicting videos to maximize engagement.

## Implementation Example

Below is a simple feedforward neural network in [[PyTorch]] for binary classification:

```python
import torch
import torch.nn as nn

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

# Initialize model, loss, and optimizer
model = SimpleNN()
criterion = nn.BCELoss()  # Binary cross-entropy loss
optimizer = torch.optim.SGD(model.parameters(), lr=0.01)

# Sample training loop
for epoch in range(100):
    inputs = torch.rand((100, 2))  # Dummy input data
    targets = torch.rand((100, 1))  # Dummy target data
    optimizer.zero_grad()  # Clear gradients
    outputs = model(inputs)  # Forward pass
    loss = criterion(outputs, targets)  # Compute loss
    loss.backward()  # Backpropagation
    optimizer.step()  # Update weights
```

This code demonstrates a basic neural network with one hidden layer, trained using [[Stochastic Gradient Descent]].

## Related Concepts

- [[Gradient Descent Algorithm]]: Core optimization method for training.
- [[Backpropagation]]: Computes gradients for parameter updates.
- [[Activation Functions]]: Introduce non-linearity (e.g., [[ReLU Activation]], sigmoid).
- [[Convolutional Neural Networks]]: Specialized for image data.
- [[Regularization]]: Prevents overfitting.
- [[Feature Scaling]]: Ensures stable training.

## Further Exploration

Experiment with [[PyTorch]] or [[TensorFlow]] to build neural networks. Visualize layer outputs or gradients to understand feature learning. Dive into [[Convolutional Neural Networks]] or [[Transformers]] for advanced architectures.
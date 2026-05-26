# Deep Learning

Deep learning is a subset of machine learning that uses neural networks with multiple layers to learn complex representations.

## Why Deep Learning Matters

Deep learning works well when the input is highly structured, such as:

- Images
- Audio
- Text
- Video

It can learn features automatically instead of relying only on manual engineering.

## Neural Networks

A neural network contains layers of connected neurons.

### Simple structure

```text
Input -> Hidden Layer -> Hidden Layer -> Output
```

### Components
- Weights
- Biases
- Activation functions
- Loss function
- Optimizer

## Activation Functions

Activation functions decide how a neuron responds to its input.

### ReLU

ReLU(x) = max(0, x)

### Sigmoid

Sigmoid(x) = 1 / (1 + e^-x)

### Tanh

Tanh(x) is the hyperbolic tangent activation, which outputs values between -1 and 1.

## CNN

Convolutional Neural Networks are designed for image-like data.

### CNN building blocks
- Convolution layer
- Pooling layer
- Flatten layer
- Dense layer

### PyTorch example

```python
import torch
import torch.nn as nn

class CNN(nn.Module):
    def __init__(self):
        super().__init__()
        self.conv1 = nn.Conv2d(3, 32, kernel_size=3, padding=1)
        self.pool = nn.MaxPool2d(2)
        self.conv2 = nn.Conv2d(32, 64, kernel_size=3, padding=1)
        self.fc1 = nn.Linear(64 * 8 * 8, 128)
        self.fc2 = nn.Linear(128, 10)

    def forward(self, x):
        x = self.pool(torch.relu(self.conv1(x)))
        x = self.pool(torch.relu(self.conv2(x)))
        x = torch.flatten(x, 1)
        x = torch.relu(self.fc1(x))
        return self.fc2(x)
```

## RNN

RNNs process sequences by keeping hidden state across time steps.

### Use cases
- Time series
- Text sequences
- Speech

## LSTM

LSTMs are a stronger version of RNNs that handle long-term dependencies better.

### Important gates
- Forget gate
- Input gate
- Output gate

## Transformers

Transformers are the backbone of modern NLP and many multimodal systems.

### Key idea
Self-attention lets the model weigh the importance of different tokens.

### Core components
- Embedding layer
- Multi-head attention
- Feedforward network
- Layer normalization

## Attention Mechanism

Attention helps the model focus on relevant parts of the input.

### Simple intuition
If a sentence has several words, attention tells the model which words matter most right now.

## Backpropagation

Backpropagation computes gradients and updates weights to reduce the loss.

### Simplified process
1. Forward pass
2. Compute loss
3. Compute gradients
4. Update weights

### PyTorch gradient step

```python
loss.backward()
optimizer.step()
optimizer.zero_grad()
```

## Gradient Descent

Gradient descent updates weights in the direction that reduces error.

### Formula

theta = theta - eta * gradient of J(theta)

### Variants
- Batch gradient descent
- Stochastic gradient descent
- Mini-batch gradient descent

## Transfer Learning

Transfer learning reuses a pre-trained model for a new task.

### Benefits
- Faster training
- Better performance with less data
- Lower compute cost

### Example

```python
from torchvision import models
model = models.resnet18(weights='IMAGENET1K_V1')
model.fc = nn.Linear(model.fc.in_features, 5)
```

## Fine Tuning

Fine tuning adapts a pre-trained model to your domain.

### Best practices
- Freeze base layers initially
- Train the head first
- Unfreeze later for lower learning rate

## Training Loop

```python
for epoch in range(num_epochs):
    for inputs, labels in train_loader:
        optimizer.zero_grad()
        outputs = model(inputs)
        loss = criterion(outputs, labels)
        loss.backward()
        optimizer.step()
```

## Comparison of Architectures

| Architecture | Best for | Key Strength |
| --- | --- | --- |
| CNN | Images | Spatial feature extraction |
| RNN | Sequential data | Temporal memory |
| LSTM | Long sequences | Long-term dependency handling |
| Transformers | Text and multimodal | Parallel attention-based modeling |

## Practical Tips

- Start with a lightweight model for baselines.
- Use transfer learning before training large networks from scratch.
- Track validation loss and overfitting.
- Use data augmentation for vision tasks.

## Summary

Deep learning unlocks the most advanced AI systems today. Once you understand neural networks, backpropagation, and the main architectures, you can reason about vision, language, and multimodal systems.

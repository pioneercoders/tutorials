# AI Fundamentals

Artificial Intelligence is the field of building systems that can perceive, reason, learn, and act. In this chapter, we connect the big ideas behind AI, understand the AI lifecycle, and compare the main learning paradigms.

## Why AI Exists

AI exists because many real-world problems are hard to solve with static rules alone:

- **Complex patterns** are difficult to capture manually.
- **Large datasets** contain hidden structure that machines can detect.
- **Automation** is needed for repetitive, time-sensitive decisions.
- **Adaptation** matters when conditions change.

## Types of AI

### Narrow AI
Targeted systems built for specific tasks, such as recommendation engines, fraud detection, or face recognition.

### General AI
A hypothetical system that can perform broad tasks across many domains with human-like adaptability.

### Superintelligent AI
A future concept where AI exceeds human capabilities in most intellectual tasks.

## How AI Works

A classic AI pipeline looks like this:

1. **Problem definition**
2. **Data collection and labeling**
3. **Feature engineering or representation learning**
4. **Model training**
5. **Evaluation and validation**
6. **Deployment and monitoring**

## AI Lifecycle

### 1. Problem Framing
Define the business goal, constraints, acceptance criteria, and success metrics.

### 2. Data Preparation
Collect, clean, label, and split data into train, validation, and test sets.

### 3. Model Selection
Choose a suitable model or algorithm based on the problem.

### 4. Training
Optimize model parameters using data and algorithms.

### 5. Evaluation
Measure performance using metrics such as accuracy, precision, recall, F1, RMSE, or AUC.

### 6. Deployment
Expose the model through APIs, batch jobs, or embedded systems.

### 7. Monitoring
Track drift, latency, data quality, and business outcomes.

## Machine Learning vs Deep Learning

| Area | Machine Learning | Deep Learning |
| --- | --- | --- |
| Data requirement | Moderate | Large |
| Feature engineering | Often needed | Often learned automatically |
| Interpretability | Easier | Harder |
| Compute cost | Lower | Higher |
| Best for | Tabular and structured data | Images, speech, text |

## Neural Networks Basics

A neural network is a stack of simple mathematical units that transform input into outputs.

- **Input layer** receives data
- **Hidden layers** transform and combine signals
- **Output layer** produces predictions

Each connection has a weight, and each neuron applies an activation function.

## Training vs Inference

### Training
Training is the process of learning patterns from labeled or unlabeled data.

### Inference
Inference is the process of using the trained model to make predictions on new data.

### Example

```python
# Training phase
model.fit(X_train, y_train)

# Inference phase
predictions = model.predict(X_new)
```

## Supervised Learning

Supervised learning uses labeled examples.

**Examples**
- Spam detection
- House price prediction
- Fraud classification

**Common algorithms**
- Linear regression
- Logistic regression
- Decision trees
- Random forest
- SVM

## Unsupervised Learning

Unsupervised learning uses unlabeled data to find patterns.

**Examples**
- Customer segmentation
- Anomaly detection
- Topic discovery

**Common algorithms**
- K-Means
- Hierarchical clustering
- PCA

## Reinforcement Learning

Reinforcement learning teaches an agent to maximize rewards by interacting with an environment.

**Use cases**
- Robotics
- Game playing
- Recommendation policies
- Autonomous control

### Simple RL loop

```python
for episode in range(num_episodes):
    state = env.reset()
    done = False
    while not done:
        action = policy(state)
        next_state, reward, done, info = env.step(action)
        policy.update(state, action, reward, next_state)
        state = next_state
```

## Real-World Flow

```
Problem -> Data -> Model -> Evaluation -> Deployment -> Monitoring
```

## Interview Tips

- Explain the difference between AI, ML, and Deep Learning.
- Describe the AI lifecycle in simple steps.
- Mention why training and inference are separate phases.
- Explain when to use supervised vs unsupervised learning.

## Summary

AI fundamentals give you the mental model for every later topic. If you understand the lifecycle, the learning paradigms, and the difference between training and inference, you can reason about almost any ML or AI product.

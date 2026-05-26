# AI Tools & Frameworks

This topic covers the tools, libraries, and frameworks that make AI development faster and more reliable.

## Python Ecosystem

Python is the main language for AI research and production.

### Core packages
- NumPy
- Pandas
- Scikit-learn
- TensorFlow
- PyTorch
- Matplotlib

## TensorFlow

TensorFlow is a flexible framework for deep learning.

### Simple model example

```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Input(shape=(10,)),
    tf.keras.layers.Dense(64, activation='relu'),
    tf.keras.layers.Dense(1)
])

model.compile(optimizer='adam', loss='mse')
model.fit(X_train, y_train, epochs=10)
```

## PyTorch

PyTorch is popular for research and production due to its dynamic computation graph.

### Example

```python
import torch
import torch.nn as nn

class LinearModel(nn.Module):
    def __init__(self):
        super().__init__()
        self.layer = nn.Linear(10, 1)

    def forward(self, x):
        return self.layer(x)
```

## Scikit-learn

Scikit-learn is the standard library for classical machine learning.

### Example

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier()
model.fit(X_train, y_train)
```

## Pandas

Pandas is used for cleaning, transforming, and analyzing data.

### Example

```python
import pandas as pd

df = pd.read_csv('data.csv')
print(df.head())
```

## Hugging Face

Hugging Face provides pretrained models and tooling for NLP and generative AI.

### Example

```python
from transformers import pipeline

classifier = pipeline('sentiment-analysis')
print(classifier('AI is exciting'))
```

## OpenCV

OpenCV is widely used for image and video processing.

## MLflow

MLflow helps track experiments and manage model lifecycle.

## Streamlit

Streamlit enables rapid building of dashboards and demo apps.

### Example

```python
import streamlit as st

st.title('AI Demo')
st.write('Hello from Streamlit')
```

## VS Code Extensions

Useful tools for AI development:
- Python
- Jupyter
- Pylance
- Docker

## Feature Stores

Feature stores centralize reusable features for training and inference.

## Notebook Workflows

Notebooks help explore data and iterate quickly.

## Summary

The AI ecosystem includes languages, frameworks, notebooks, deployment tools, and orchestration utilities. Choosing the right tool depends on the problem, team experience, and production needs.

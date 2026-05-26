# MLOps & Deployment

MLOps is the operational discipline that helps machine learning systems move from experimentation to reliable production.

## Why MLOps Matters

Without MLOps, ML projects often fail because of unstable pipelines, poor reproducibility, weak monitoring, or missing governance.

## ML Lifecycle in Production

1. Data ingestion
2. Training and validation
3. Model packaging
4. Deployment
5. Monitoring
6. Retraining

## Model Packaging

Packaging turns a trained model into a portable artifact.

### Common formats
- Pickle
- ONNX
- SavedModel
- Joblib

### Example

```python
import joblib

joblib.dump(model, 'model.pkl')
```

## API Deployment

Many teams expose models through REST APIs.

### FastAPI example

```python
from fastapi import FastAPI
import joblib

app = FastAPI()
model = joblib.load('model.pkl')

@app.post('/predict')
def predict(payload: dict):
    features = payload['features']
    return {'prediction': model.predict([features])[0]}
```

## Docker

Docker packages the app and its dependencies into a portable container.

### Dockerfile sketch

```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install -r requirements.txt
COPY . .
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8000"]
```

## CI/CD for ML

CI/CD pipelines automate tests and deployment.

### What should be tested
- Data validation
- Model training reproducibility
- Prediction schema
- Performance thresholds

## Experiment Tracking

Experiment tracking stores model runs, parameters, and metrics.

### Common tools
- MLflow
- Weights & Biases
- Comet
- Neptune

## Monitoring

Monitoring checks model behavior in the real world.

### Metrics to watch
- Latency
- Throughput
- Error rate
- Data drift
- Prediction confidence shifts

## Data Drift

Data drift happens when incoming data changes distribution compared to training data.

### Example
If a fraud model trained on one customer mix is suddenly used with a very different mix, predictions may degrade.

## Model Drift

Model drift happens when the model's performance degrades due to shifting patterns or stale assumptions.

## Model Governance

Model governance covers:
- Access control
- Audit trails
- Explainability
- Compliance

## Model Registry

A model registry stores versioned model artifacts and metadata.

### Benefits
- Reproducibility
- Rollback support
- Deployment history

## Deployment Patterns

- **Batch inference** for scheduled jobs
- **Real-time inference** for APIs
- **Edge deployment** for mobile or IoT

## Responsible Deployment

- Add safety checks
- Log predictions
- Use human review for high-risk decisions
- Document model limitations

## Summary

MLOps makes AI deployable, measurable, and maintainable. The key ideas are packaging, monitoring, automation, and governance.

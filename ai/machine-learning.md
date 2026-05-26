# Machine Learning

Machine Learning is the branch of AI that learns patterns from data and improves performance without explicit rule-by-rule programming.

## Why Machine Learning Matters

Machine learning helps us solve problems where manual rules are too brittle or too expensive.

**Typical use cases**
- Customer churn prediction
- Risk scoring
- Fraud detection
- Demand forecasting
- Personalization

## Core ML Workflow

1. Define the business goal
2. Collect data
3. Clean and transform data
4. Split into train/test
5. Train model
6. Evaluate model
7. Tune hyperparameters
8. Deploy and monitor

## Linear Regression

Linear regression models the relationship between input features and a continuous target.

### Formula

Linear regression estimates y as a function of input x using a weighted line: y = wx + b.

### Python example

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(X_train, y_train)
predictions = model.predict(X_test)
```

### When to use
- Predicting salary
- Estimating house prices
- Forecasting demand

## Logistic Regression

Logistic regression is used for binary classification problems.

### Probability formula

The model estimates the probability of class 1 as p(y=1|x) = 1 / (1 + e^-z).

### Python example

```python
from sklearn.linear_model import LogisticRegression

clf = LogisticRegression()
clf.fit(X_train, y_train)
proba = clf.predict_proba(X_test)
```

## Decision Trees

Decision trees split data using feature thresholds and create a tree of if-else decisions.

### Why they are useful
- Easy to interpret
- Good for non-linear relationships
- Useful for tabular data

### Python example

```python
from sklearn.tree import DecisionTreeClassifier

model = DecisionTreeClassifier(max_depth=4)
model.fit(X_train, y_train)
```

## Random Forest

Random forest combines many decision trees and averages their predictions.

### Advantages
- Better generalization
- Robust to noise
- Feature importance available

### Python example

```python
from sklearn.ensemble import RandomForestClassifier

model = RandomForestClassifier(n_estimators=200, random_state=42)
model.fit(X_train, y_train)
```

## KNN

K-nearest neighbors predicts based on the nearest labeled examples.

### When to use
- Small datasets
- Intuitive similarity-based problems

### Python example

```python
from sklearn.neighbors import KNeighborsClassifier

model = KNeighborsClassifier(n_neighbors=5)
model.fit(X_train, y_train)
```

## SVM

Support Vector Machines maximize the margin between classes.

### Use cases
- Image classification
- Text classification
- Small to medium datasets

### Python example

```python
from sklearn.svm import SVC

model = SVC(kernel='rbf')
model.fit(X_train, y_train)
```

## Naive Bayes

Naive Bayes uses Bayes theorem and assumes feature independence.

### Best for
- Text classification
- Spam filtering
- Document categorization

### Python example

```python
from sklearn.naive_bayes import MultinomialNB

model = MultinomialNB()
model.fit(X_train, y_train)
```

## Clustering

Clustering groups similar samples without labels.

### K-Means example

```python
from sklearn.cluster import KMeans

model = KMeans(n_clusters=3, random_state=42)
model.fit(X)
labels = model.labels_
```

## Feature Engineering

Feature engineering transforms raw data into useful input for models.

### Common techniques
- Scaling and normalization
- One-hot encoding
- Binning
- Interaction features
- Text vectorization

### Example

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, StandardScaler
```

## Model Evaluation

### Classification metrics
- Accuracy
- Precision
- Recall
- F1 score
- ROC-AUC

### Regression metrics
- MAE
- MSE
- RMSE
- R2 score

### Python example

```python
from sklearn.metrics import accuracy_score, f1_score, roc_auc_score

acc = accuracy_score(y_test, y_pred)
f1 = f1_score(y_test, y_pred)
```

## Bias vs Variance

### Bias
High bias means the model is too simple and misses important patterns.

### Variance
High variance means the model is too sensitive to training data.

### Trade-off
A good model balances bias and variance.

## Cross Validation

Cross validation helps estimate performance on unseen data.

### Example

```python
from sklearn.model_selection import cross_val_score

scores = cross_val_score(model, X, y, cv=5)
print(scores.mean())
```

## End-to-End Example

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.impute import SimpleImputer
from sklearn.ensemble import RandomForestClassifier
from sklearn.metrics import accuracy_score

numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('encoder', OneHotEncoder(handle_unknown='ignore'))
])

preprocessor = ColumnTransformer([
    ('num', numeric_transformer, numeric_features),
    ('cat', categorical_transformer, categorical_features)
])

model = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', RandomForestClassifier(n_estimators=200))
])

model.fit(X_train, y_train)
pred = model.predict(X_test)
print(accuracy_score(y_test, pred))
```

## Practice Questions

### 1. Choose the right model

You have a tabular dataset with 50,000 rows, 25 numerical features, and a binary target.

- Which model would you try first?
- When would you consider a tree-based model instead?

### 2. Debug overfitting

A decision tree gets 99% accuracy on training data but performs poorly on validation data.

- What is happening?
- How can you reduce overfitting?

### 3. Short code challenge

Write a pipeline that:
1. standardizes numerical features
2. one-hot encodes categorical features
3. trains a RandomForestClassifier

```python
from sklearn.pipeline import Pipeline
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, StandardScaler
from sklearn.impute import SimpleImputer
from sklearn.ensemble import RandomForestClassifier

numeric_features = ['age', 'income']
categorical_features = ['city', 'employment_type']

numeric_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='median')),
    ('scaler', StandardScaler())
])

categorical_transformer = Pipeline([
    ('imputer', SimpleImputer(strategy='most_frequent')),
    ('onehot', OneHotEncoder(handle_unknown='ignore'))
])

preprocessor = ColumnTransformer([
    ('num', numeric_transformer, numeric_features),
    ('cat', categorical_transformer, categorical_features)
])

model = Pipeline([
    ('preprocessor', preprocessor),
    ('classifier', RandomForestClassifier(n_estimators=200, random_state=42))
])

model.fit(X_train, y_train)
```

## Interview Preparation

- Explain why feature engineering matters.
- Describe overfitting and underfitting.
- Compare decision trees and random forests.
- Explain when to use logistic regression vs tree-based models.

## Summary

Machine learning is the practical core of AI. It gives you tools to build systems that learn from data, measure performance, and improve continuously.

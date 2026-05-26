# NLP

Natural Language Processing helps computers understand, generate, and process human language.

## Why NLP Matters

NLP powers chatbots, translation systems, search, sentiment analysis, and summarization.

## Tokenization

Tokenization splits text into words or subwords.

### Example

```python
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained('distilbert-base-uncased')
encoded = tokenizer('AI helps machines understand language')
print(encoded)
```

## Text Classification

Text classification assigns labels to text such as spam, review sentiment, or intent.

### Python example

```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression

vectorizer = TfidfVectorizer()
X = vectorizer.fit_transform(texts)
model = LogisticRegression()
model.fit(X, labels)
```

## Sentiment Analysis

Sentiment analysis detects positive, negative, or neutral tone.

### Use cases
- Product reviews
- Customer support analytics
- Brand monitoring

## NER

Named Entity Recognition identifies names, organizations, dates, and locations.

### Example output

```text
Apple launched a new product in California.
Entities: Apple (ORG), California (LOC)
```

## Text Embeddings

Embeddings convert text into vectors used for search and retrieval.

### Example

```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')
vector = model.encode('machine learning is useful')
```

## Chatbots

Chatbots combine NLP, retrieval, and dialogue management.

### Typical chatbot flow
1. User intent detection
2. Search or retrieve knowledge
3. Generate response
4. Ask follow-up if needed

## Translation Systems

Translation systems convert text from one language to another and often rely on sequence-to-sequence models.

## Summarization

Summarization compresses long documents into short, useful outputs.

### Simple extractive approach
Select the most important sentences.

### Abstractive approach
Generate new sentences that preserve meaning.

## Speech Recognition

Speech recognition converts spoken language into text.

### Common stack
- Audio preprocessing
- Acoustic model
- Language model

## NLP Pipeline

```python
text = 'OpenAI brings AI to enterprise workflows'

# tokenization
words = text.split()

# vectorization
vectors = vectorizer.fit_transform([text])

# classification
prediction = model.predict(vectors)
```

## Practical Interview Questions

- What is the difference between tokenization and embeddings?
- When would you choose rule-based NLP vs ML-based NLP?
- How do you evaluate an NLP model?

## Summary

NLP enables machines to understand language and interact with humans more naturally. The core concepts are tokenization, embeddings, classification, retrieval, and generation.

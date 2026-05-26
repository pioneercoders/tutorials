# Generative AI

Generative AI creates new content such as text, images, code, audio, or videos from learned patterns.

## What is Generative AI?

Generative AI models learn distributions from large datasets and generate outputs that resemble the training data.

### Examples
- ChatGPT-style assistants
- Image generation tools
- Code generation systems
- Music generation

## LLMs

Large Language Models are trained on massive text corpora and respond to prompts in natural language.

### Why they matter
- General reasoning
- Summarization
- Translation
- Question answering

## GPT Models

GPT-style models use autoregressive generation.

### How they work
They predict the next token given the previous context.

### Example prompt

```text
Explain the difference between supervised and unsupervised learning.
```

## Prompt Engineering

Prompt engineering is the process of designing input instructions that improve output quality.

### Prompt templates

```text
You are a senior machine learning mentor.
Explain the difference between bias and variance.
Use simple examples and a short summary.
```

### Best practices
- Be specific
- Use examples
- Break tasks into steps
- Ask for structure

## RAG

Retrieval-Augmented Generation combines retrieval of external knowledge with generation.

### Workflow
1. User asks a question
2. Relevant documents are retrieved
3. Retrieved context is added to prompt
4. LLM generates grounded answer

### Benefits
- Better factual accuracy
- Easier updates without retraining
- Useful for enterprise knowledge systems

## Embeddings

Embeddings convert text or images into vectors that capture semantic meaning.

### Python example

```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')
embeddings = model.encode(['AI fundamentals', 'LLM pipelines'])
```

## Vector Databases

Vector databases store embeddings for similarity search.

### Common use cases
- Semantic search
- Retrieval for RAG
- Recommendation systems

## LangChain

LangChain helps build applications around LLMs.

### Simple example

```python
from langchain.prompts import PromptTemplate
from langchain.llms import OpenAI

prompt = PromptTemplate(input_variables=['topic'], template='Explain {topic} in simple terms.')
llm = OpenAI()
print(llm(prompt.format(topic='RAG')))
```

## AI Agents

AI agents use tools, memory, and reasoning to accomplish tasks.

### Example agent workflow
1. Understand task
2. Decide tool or step
3. Execute action
4. Review result
5. Repeat until complete

## Multimodal AI

Multimodal AI combines text, image, audio, and video signals.

### Examples
- Image captioning
- Video question answering
- Speech-to-text pipelines

## Fine-tuning LLMs

Fine-tuning adapts a pretrained model to a specific domain.

### Steps
1. Prepare domain dataset
2. Format prompts and responses
3. Run supervised fine-tuning
4. Evaluate outputs
5. Deploy with guardrails

## Open Source Models

Popular open source models include:

- Llama
- Mistral
- Gemma
- Qwen
- Phi

## Generative AI Product Patterns

### Text generation
- Chatbots
- Summarization
- Content writing

### Code generation
- Auto-completion
- Debugging suggestions
- Refactoring aids

### Creative generation
- Image generation
- Music and voice generation

## Best Practices

- Use system prompts carefully
- Add grounding for factual tasks
- Validate outputs with evals
- Monitor hallucinations

## Summary

Generative AI is one of the fastest-growing AI areas. To build good systems, you need prompt design, retrieval, embeddings, and production safeguards.

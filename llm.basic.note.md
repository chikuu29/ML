# AI/LLM Interview Notes

---

# 1. What is an LLM (Large Language Model)?

### Answer
A Large Language Model (LLM) is a deep learning model trained on massive amounts of text data to understand, generate, summarize, translate, and answer questions in natural language.

It predicts the **next most likely token** based on previous tokens.

### Examples
- GPT-4/5
- Llama
- Mistral
- Gemini
- Claude

### Real-world Uses
- Chatbots
- Code Generation
- Document Summarization
- Translation
- Question Answering

**Interview One-liner**

> An LLM is a Transformer-based neural network trained on massive text data that predicts the next token to generate human-like text.

---

# 2. What is Transformer?

### Answer

Transformer is the deep learning architecture introduced by Google in the paper:

**"Attention Is All You Need" (2017)**

Unlike RNNs and LSTMs, Transformers process all words simultaneously using Attention.

### Main Components

- Input Embeddings
- Positional Encoding
- Multi-head Self Attention
- Feed Forward Network
- Layer Normalization
- Residual Connections

### Advantages

- Parallel Processing
- Faster Training
- Better Long Context Understanding

---

# 3. What is Attention?

### Answer

Attention allows the model to focus on the most important words while processing a sentence.

Example:

> The cat sat on the mat because **it** was tired.

The word **it** should attend to **cat**, not **mat**.

Attention calculates how important every word is to every other word.

---

# 4. What is Self Attention?

### Answer

Self Attention means each word attends to every other word in the same sentence.

Example

Sentence:

```
I love Machine Learning
```

When processing "Learning", the model also looks at

- I
- Love
- Machine

to understand context.

### Formula

Attention(Q,K,V)

Where

- Q = Query
- K = Key
- V = Value

---

# 5. What is Embedding?

### Answer

Embedding converts words into numerical vectors.

Example

```
Dog → [0.32, -1.22, 0.87, ...]
Cat → [0.35, -1.18, 0.90, ...]
```

Since Dog and Cat are similar, their vectors are close.

Embeddings capture semantic meaning.

Common embedding models

- OpenAI Embeddings
- Sentence Transformers
- BGE
- E5

---

# 6. What is Token?

### Answer

LLMs don't read words.

They read **tokens**.

Examples

```
Hello

Token → Hello
```

```
Artificial Intelligence

Tokens

Artificial
Intelligence
```

```
unbelievable

Tokens

un
believ
able
```

Approximately

- 1 token ≈ 4 characters
- 100 tokens ≈ 75 words

---

# 7. What is Tokenization?

### Answer

Tokenization is the process of splitting text into tokens before feeding it into an LLM.

Example

Input

```
I love AI
```

Output

```
["I","love","AI"]
```

Tokenizer converts text into token IDs.

---

# 8. What is Context Window?

### Answer

Context Window is the maximum number of tokens an LLM can remember during one conversation.

Example

If context window = 128K

Model can read

- prompt
- chat history
- documents

up to 128K tokens.

Larger context = better long-document understanding.

---

# 9. What is Hallucination?

### Answer

Hallucination occurs when an LLM generates incorrect or fabricated information confidently.

Example

User:

> Who invented Python in 1800?

Model:

> John Smith.

This is false.

Ways to reduce hallucinations

- RAG
- Better prompts
- Grounding with documents
- Fine tuning (for specific domains)

---

# 10. What is Prompt Engineering?

### Answer

Prompt Engineering is designing prompts to get accurate responses from an LLM.

Examples

Bad Prompt

```
Explain AI.
```

Better Prompt

```
Explain AI to a 10-year-old using examples in under 200 words.
```

Techniques

- Zero-shot
- One-shot
- Few-shot
- Chain-of-thought (use internally where appropriate)
- Role prompting

---

# 11. What is Temperature?

### Answer

Temperature controls randomness.

Range

```
0 → Deterministic

1 → Balanced

2 → Highly Creative
```

Use

Temperature = 0

- Coding
- SQL
- Math

Temperature = 0.8

- Story writing
- Brainstorming

---

# 12. What is Top P?

### Answer

Top P (Nucleus Sampling) limits token selection to the smallest set of tokens whose cumulative probability reaches **P**.

Example

Top P = 0.9

Model selects from the top 90% cumulative probability.

Lower Top P = more focused responses.

Higher Top P = more diverse responses.

---

# 13. What is RAG?

### Answer

RAG = Retrieval Augmented Generation.

Instead of relying only on training data,

the model first retrieves relevant documents,

then generates the answer.

Pipeline

```
User Question
       ↓
Embedding
       ↓
Vector Search
       ↓
Relevant Documents
       ↓
LLM
       ↓
Answer
```

Advantages

- Reduces hallucination
- Uses latest documents
- No retraining required

---

# 14. What is a Vector Database?

### Answer

A Vector Database stores embeddings instead of traditional rows and columns.

It enables similarity search using vector distance.

Common similarity metrics

- Cosine Similarity
- Euclidean Distance
- Dot Product

Used in

- RAG
- Semantic Search
- Recommendation Systems

---

# 15. What is FAISS?

### Answer

FAISS (Facebook AI Similarity Search) is an open-source library from Meta for fast similarity search over vectors.

Features

- In-memory
- Very fast
- CPU/GPU support

Best for

- Local development
- Offline search

---

# 16. What is ChromaDB?

### Answer

ChromaDB is an open-source vector database designed for AI applications.

Features

- Easy setup
- Persistent storage
- Metadata filtering
- LangChain integration

Best for

- Small to medium RAG applications

---

# 17. What is Pinecone?

### Answer

Pinecone is a fully managed cloud vector database.

Features

- Scalable
- Managed infrastructure
- Automatic indexing
- High availability

Best for

- Production AI applications
- Large-scale RAG systems

---

# 18. What is Fine-Tuning?

### Answer

Fine-tuning means continuing the training of a pre-trained LLM on a specific dataset to adapt it to a domain or task.

Examples

- Medical chatbot
- Legal assistant
- Company-specific support

Advantages

- Learns domain-specific style and behavior

Disadvantages

- Expensive
- Requires GPUs and quality data
- Doesn't automatically include new knowledge

---

# 19. What is LoRA?

### Answer

LoRA (Low-Rank Adaptation) is a parameter-efficient fine-tuning technique.

Instead of updating all model weights,

LoRA trains only small adapter matrices.

Advantages

- Faster
- Less memory
- Cheaper
- Easy to swap adapters

Widely used for Llama, Mistral, and similar models.

---

# 20. What is RLHF?

### Answer

RLHF = Reinforcement Learning from Human Feedback.

Steps

1. Pre-train model
2. Humans rank model responses
3. Train a reward model
4. Optimize the LLM using reinforcement learning

Purpose

- Improve helpfulness
- Improve safety
- Align with human preferences

---

# 21. What are AI Agents?

### Answer

An AI Agent is an LLM-powered system that can:

- Reason
- Plan
- Use tools
- Execute tasks
- Observe results
- Iterate until a goal is achieved

Example

Travel Booking Agent

User

```
Book my flight tomorrow.
```

Agent

- Search flights
- Compare prices
- Ask for confirmation
- Book ticket
- Send itinerary

Frameworks

- LangGraph
- CrewAI
- AutoGen

---

# 22. What is MCP?

### Answer

MCP (Model Context Protocol) is an open standard that lets AI models securely connect to external tools, data sources, and applications through a common interface.

Instead of creating a custom integration for every tool, MCP provides a standard protocol.

Examples

- File systems
- Databases
- GitHub
- Slack
- Google Drive

Benefits

- Standardized tool integration
- Reusable connectors
- Easier interoperability between AI applications

---

# 23. What is Function Calling?

### Answer

Function Calling allows an LLM to decide when structured tool execution is needed and return the required function name and arguments instead of generating free-form text.

Example

User

```
What's the weather in Delhi?
```

LLM

```
Call:
get_weather(city="Delhi")
```

Application

- Executes the function
- Returns the result
- LLM generates the final answer

Use Cases

- Weather
- Payments
- Database queries
- Booking systems

---

# 24. What are Guardrails?

### Answer

Guardrails are mechanisms that keep AI applications safe, reliable, and within business rules.

Examples

- Prompt validation
- Input filtering
- Output moderation
- PII masking
- Jailbreak protection
- Hallucination checks
- Content safety policies

Why they matter

- Improve safety
- Protect sensitive data
- Ensure compliance
- Increase reliability in production AI systems

---

# Common Interview Question

## Explain the RAG Architecture

```
User Question
      │
      ▼
Embedding Model
      │
      ▼
Vector Database
(FAISS / ChromaDB / Pinecone)
      │
Similarity Search
      │
Relevant Documents
      │
      ▼
Prompt
(User + Context)
      │
      ▼
LLM
      │
      ▼
Final Answer
```

---

# Quick Revision (One-Liners)

| Topic | One-Liner |
|--------|-----------|
| LLM | Predicts the next token using a Transformer architecture. |
| Transformer | Neural network architecture based on attention mechanisms. |
| Attention | Focuses on the most relevant words in the input. |
| Self-Attention | Each token attends to all other tokens in the same sequence. |
| Embedding | Dense numerical vector representing semantic meaning. |
| Token | Smallest text unit processed by an LLM. |
| Tokenization | Converts text into tokens and token IDs. |
| Context Window | Maximum number of tokens the model can process at once. |
| Hallucination | Confidently generated but incorrect information. |
| Prompt Engineering | Designing prompts to improve model outputs. |
| Temperature | Controls randomness in generated text. |
| Top P | Limits sampling to the most probable cumulative tokens. |
| RAG | Retrieves external knowledge before generating an answer. |
| Vector Database | Stores embeddings for similarity search. |
| FAISS | Fast local vector similarity search library. |
| ChromaDB | Open-source vector database for AI applications. |
| Pinecone | Managed cloud vector database for production systems. |
| Fine-Tuning | Retrains a pre-trained model on task-specific data. |
| LoRA | Efficient fine-tuning using low-rank adapter matrices. |
| RLHF | Aligns models using human feedback and reinforcement learning. |
| Agents | LLM systems that reason, plan, and use tools to complete tasks. |
| MCP | Open standard for connecting AI models with external tools and data sources. |
| Function Calling | Structured mechanism for invoking external tools or APIs. |
| Guardrails | Safety and reliability controls for AI applications. |
# Embeddings and Vector Similarity Search

## What is an embedding?

An embedding is a dense vector of floats that represents the semantic meaning of text. Similar meanings produce similar vectors, regardless of exact wording.

```
"I love dogs"   → [0.12, -0.87, 0.34, ...]  ← close together
"I adore dogs"  → [0.11, -0.85, 0.36, ...]  ←
"quarterly tax" → [-0.92, 0.44, -0.21, ...] ← far away
```

Vectors typically have 768–3072 dimensions depending on the model.

## How embeddings are produced

A dedicated embedding model (not a generative LLM) encodes text into a fixed-size vector. You call it like an API:

```
input: "How do I reset my password?"
output: [0.021, -0.403, 0.817, ...] (1536 floats)
```

Common models: `text-embedding-3-small` (OpenAI), `embed-english-v3` (Cohere), `nomic-embed-text` (open source).

## Vector similarity search

Given a query vector, find the stored vectors most similar to it.

### Similarity metrics

| Metric | Formula | Use when |
|---|---|---|
| **Cosine similarity** | `cos(θ) = A·B / (‖A‖‖B‖)` | Text (most common) |
| **Dot product** | `A · B` | Normalized vectors, faster |
| **Euclidean distance** | `‖A - B‖` | When magnitude matters |

Cosine similarity is the default for text — it measures angle, not magnitude, so sentence length doesn't distort results.

### Approximate Nearest Neighbor (ANN)

Exact search over millions of vectors is too slow. ANN algorithms trade a small accuracy loss for large speed gains.

Common algorithms:
- **HNSW** (Hierarchical Navigable Small World) — graph-based, fast, most widely used
- **IVF** (Inverted File Index) — clusters vectors, searches only relevant clusters
- **PQ** (Product Quantization) — compresses vectors to reduce memory

Most vector DBs handle this for you.

## Vector databases

| DB | Notes |
|---|---|
| **pgvector** | Postgres extension — good default if you already use Postgres |
| **Pinecone** | Managed, serverless, easy to start |
| **Chroma** | Lightweight, good for local/dev |
| **Weaviate** | Built-in embedding + hybrid search |
| **Qdrant** | High performance, rich filtering |

## Practical considerations

- **Embed at write time** — when documents are ingested, not at query time
- **Re-embed if you change models** — vectors from different models are not compatible
- **Metadata filtering** — combine vector search with filters (date, category) to narrow results before similarity ranking
- **Dimensionality vs. cost** — larger vectors = more accuracy, more storage, more compute
- **Batching** — embed in bulk, not one at a time

## Where this fits in a system

```
Ingest pipeline:  document → chunk → embed → store in vector DB
Query pipeline:   user query → embed → similarity search → retrieve top-k chunks → LLM
```

Embeddings are the foundation of RAG, semantic search, recommendation, and duplicate detection.

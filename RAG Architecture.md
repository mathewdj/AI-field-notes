# RAG Architecture

RAG (Retrieval-Augmented Generation) is a pattern for giving an LLM access to external knowledge at query time, without fine-tuning.

## The problem it solves

LLMs have a knowledge cutoff and no access to your private data. RAG lets you inject relevant, up-to-date context into the prompt dynamically.

## Core flow

```
User query
    ↓
Embed query → vector
    ↓
Search vector DB for similar chunks
    ↓
Retrieve top-k chunks
    ↓
Stuff chunks into prompt as context
    ↓
LLM generates answer grounded in retrieved context
```

## Key components

| Component | Role |
|---|---|
| **Chunker** | Splits source documents into smaller pieces |
| **Embedder** | Converts text chunks → dense vectors (e.g. `text-embedding-3-small`) |
| **Vector DB** | Stores and indexes vectors for similarity search (e.g. pgvector, Pinecone, Chroma) |
| **Retriever** | Queries the vector DB with the embedded user query |
| **LLM** | Generates the final answer using retrieved chunks as context |

## Retrieval strategies

- **Semantic search** — cosine similarity between query and chunk embeddings (most common)
- **Keyword search (BM25)** — traditional full-text search
- **Hybrid** — combine both, rerank results

## Chunking considerations

- Chunk size affects recall — too large dilutes signal, too small loses context
- Overlap between chunks prevents splitting a key sentence across boundaries
- Metadata (source, date, section) on each chunk improves filtering

## Limitations

- Retrieval quality caps answer quality — garbage in, garbage out
- LLM still hallucinates if retrieved context is ambiguous or missing
- Latency adds up: embed → search → generate
- Context window limits how many chunks you can inject

# LLM Semantic Retrieval

Sparse, dense, and hybrid semantic retrieval experiments on noisy natural-language product queries.

## Overview

This project explores retrieval system behavior under noisy and semantically ambiguous user queries using:

- BM25 sparse retrieval
- dense semantic retrieval with sentence embeddings
- hybrid retrieval with weighted score fusion

The goal is to evaluate how different retrieval strategies perform when user-generated queries contain:

- informal phrasing
- weak lexical overlap
- implicit semantic intent
- conversational language

The project is implemented as a retrieval systems study using a real-world Amazon product review dataset.

---

# Retrieval Pipeline

## 1. Sparse Retrieval (BM25)

A lexical retrieval baseline based on exact token overlap.

BM25 performs reasonably well under strong keyword overlap conditions, but struggles when semantic intent is expressed indirectly.

---

## 2. Dense Semantic Retrieval

Dense retrieval is implemented using the `all-MiniLM-L6-v2` sentence-transformer model.

Both product documents and review queries are embedded into a shared semantic vector space and retrieved using cosine similarity.

This approach significantly improves retrieval quality under noisy natural-language conditions.

---

## 3. Hybrid Retrieval

A hybrid retriever combines normalized BM25 scores with dense semantic similarity scores using weighted score fusion.

The study also investigates situations where hybrid retrieval may underperform relative to pure dense retrieval due to lexical retrieval noise.

---

# Dataset

The project uses an Amazon product review dataset containing:

- product metadata
- product categories
- brand information
- user-generated review text

Retrieval setup:

| Component | Description |
|---|---|
| Query | User review text |
| Document | Product metadata |
| Ground Truth | Associated product |

---

# Evaluation

The primary evaluation metric is:

```text
Recall@5
```

A retrieval is considered successful if the correct product appears within the top-5 retrieved results.

## Results

| Method | Recall@5 |
|---|---|
| BM25 | 0.1674 |
| Dense Retrieval | 0.7099 |
| Hybrid Retrieval | 0.6697 |

The experiments demonstrate that dense semantic retrieval substantially outperforms sparse lexical retrieval under noisy query distributions.

---

# Key Insights

- Sparse lexical retrieval struggles under noisy natural-language queries
- Dense semantic retrieval significantly improves contextual matching
- Hybrid retrieval is not universally optimal
- Retrieval effectiveness strongly depends on query-document characteristics

---

# Technologies

- Python
- Pandas
- NumPy
- Sentence Transformers
- scikit-learn
- BM25 (`rank_bm25`)
- Jupyter Notebook

---

# Future Improvements

Potential future extensions include:

- ANN search (FAISS / HNSW)
- vector databases
- reranking pipelines
- cross-encoder rerankers
- query expansion
- retrieval-augmented generation (RAG)

---

# Repository Structure

```text
.
├── retrieval_study.ipynb
├── README.md
└── data/
```

---

# Notes

This repository is intended as a compact retrieval engineering study focused on semantic search behavior and retrieval system tradeoffs rather than production optimization.

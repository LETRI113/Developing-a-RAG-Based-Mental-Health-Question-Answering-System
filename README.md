# 🔍 Hybrid RAG Pipeline with LLaMA 3 (8B)

**Author:** Trí Lê  
**Role:** AI/ML Practitioner | Final-year student @ Ton Duc Thang University  
**LLM:** `letri345/llama3-8b-merge` (Hugging Face)

---

## 🚀 Overview

This repository implements a **production-style Hybrid Retrieval-Augmented Generation (RAG) pipeline**, combining:

- **BM25 lexical retrieval**
- **Vector semantic search**
- **Reciprocal Rank Fusion (RRF)**
- **Context-aware prompt assembly**
- **Chat history memory routing**
- **Automated RAG evaluation**

The system is designed to improve **answer correctness, grounding, and relevance** for document-based QA.

---

## 🧠 Model

- **LLM:** `letri345/llama3-8b-merge`
- Architecture: LLaMA 3 – 8B
- Optimized for:
  - Instruction-following
  - Context-grounded answering
  - Stable RAG evaluation

> ℹ️ This Hugging Face model ID is required to reproduce all results in this repo.

---

## 🏗️ System Architecture (Hybrid RAG)

```
User
 ↓
Router  ←────────────── Chat History Memory
 ↓
Hybrid Retrieval
 ├─ BM25
 └─ Vector Semantic Search (ChromaDB)
        ↓
Reciprocal Rank Fusion (RRF)
 ↓
Post-retrieval Processing
 (re-ranking, filtering, summarize)
 ↓
Contextual Prompt Assembly
 ↓
LLaMA 3 (8B)
 ↓
Answer
```

### Design Notes
- **Chat history feeds into the Router, not directly into the LLM**
- Prevents context pollution and improves retrieval precision
- Retrieval and generation are cleanly decoupled

---

## 📂 Project Structure

```
.
├── data/
│   ├── cache/
│   └── index_store/
│
├── Build_data.ipynb        # Document processing & indexing
├── RAG.ipynb               # Retrieval, inference & evaluation
│
├── questions_full.csv      # Auto-generated evaluation questions
├── eval_results.csv        # RAG evaluation outputs
├── DMS-5.pdf               # Sample source document
└── README.md
```

---

## 🔧 Data & Indexing (`Build_data.ipynb`)

Pipeline:
1. Load raw documents
2. Chunking with overlap
3. Metadata extraction (doc_id, chunk_id, source)
4. Embedding generation
5. BM25 text preparation
6. Store vectors in **ChromaDB**

Outputs:
- Vector index
- BM25-ready corpus
- Node-level metadata

---

## 🔎 Retrieval Strategy

### Hybrid Retrieval
- **BM25:** keyword precision
- **Vector search:** semantic similarity

### Fusion
- **Reciprocal Rank Fusion (RRF)** balances lexical & semantic signals
- Improves recall and ranking stability across query types

---

## ✍️ Prompting & Inference

- Retrieved chunks are post-processed before inference
- Final prompt includes:
  - System instruction
  - Retrieved evidence
  - User query
- Ensures grounded, context-aware responses

---

## 📊 RAG Evaluation (`RAG.ipynb`)

### Evaluation Setup
- Semi-Automatic Question Generation (SAQG)
- Each question linked to reference context
- Answers evaluated by an LLM judge

### Metrics
| Metric | Scale |
|------|------|
| Correctness | 0 – 5 |
| Faithfulness | 0 – 1 |
| Relevancy | 0 – 1 |

### Results (Average)
- **Correctness:** **4.24 / 5**
- **Faithfulness:** **0.86 / 1**
- **Relevancy:** **0.98 / 1**

➡ Demonstrates strong grounding and high answer relevance.

---

## 🎯 Use Cases

- Document-based QA systems
- Internal knowledge assistants
- RAG research & benchmarking
- AI/ML portfolio projects

---

## 👤 Author

**Trí Lê**  
AI/ML Practitioner – Final-year student @ Ton Duc Thang University  

Focused on:
- LLM fine-tuning
- RAG system design
- Evaluation-driven improvement

---

## 📜 License

For research and educational use.

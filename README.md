# 🔍 Semantic Search Engine

A local semantic search engine built from scratch using embeddings and vector databases. Given a folder of `.md` files, Vectra lets you search by **meaning**, not just keywords.

> Built as part of an AI Engineer learning journey — Phase 1: Embeddings & Vector Databases.

---

## ✨ What it does

- Ingests a folder of Markdown files (e.g. Obsidian vault)
- Chunks and embeds each document using `sentence-transformers` (no paid APIs)
- Stores vectors in ChromaDB for fast similarity search
- Exposes a FastAPI endpoint for semantic search queries
- Returns the top-K most relevant documents for any natural language query

---

## 🧠 Concepts covered

- What embeddings are and why semantically similar texts end up geometrically close
- Cosine similarity as a distance metric between vectors
- Approximate Nearest Neighbor (ANN) search with HNSW
- Chunking strategies for text documents
- Metadata filtering in vector databases

---

## 🛠️ Stack

| Layer | Technology |
|---|---|
| Embeddings | `sentence-transformers` — `BAAI/bge-large-en-v1.5` |
| Vector DB | ChromaDB (local) |
| API | FastAPI |
| Language | Python 3.11+ |

No OpenAI API key required. Everything runs locally.

---

## 🚀 Getting started

### 1. Clone the repo

```bash
git clone https://github.com/your-username/vectra.git
cd vectra
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Index your documents

```bash
python ingest.py --docs-path ./your-docs-folder
```

### 4. Start the API

```bash
uvicorn app.main:app --reload
```

### 5. Search

```bash
curl "http://localhost:8000/search?q=tools+for+managing+projects&k=5"
```

---

## 📁 Project structure

```
vectra/
├── app/
│   ├── main.py          # FastAPI app and routes
│   └── search.py        # Search logic
├── core/
│   ├── ingestion.py     # Document loading and chunking
│   ├── embedder.py      # Embedding model wrapper
│   └── vectorstore.py   # ChromaDB interface
├── ingest.py            # CLI script to index documents
├── requirements.txt
└── README.md
```

---

## 📡 API Reference

### `GET /search`

Search for semantically similar documents.

| Parameter | Type | Default | Description |
|---|---|---|---|
| `q` | `string` | required | Natural language query |
| `k` | `int` | `5` | Number of results to return |

**Example response:**

```json
{
  "query": "tools for managing music projects",
  "results": [
    {
      "document": "project-tracker.md",
      "chunk": "...",
      "score": 0.91,
      "metadata": { "source": "project-tracker.md" }
    }
  ]
}
```

### `GET /similar`

Find documents similar to a given document ID.

| Parameter | Type | Description |
|---|---|---|
| `doc_id` | `string` | ID of the reference document |
| `k` | `int` | Number of results |

---

## 🧪 Experiments

The `notebooks/` folder contains three standalone experiments to understand the core concepts before the full pipeline:

- `01_first_embeddings.ipynb` — generate your first embeddings and inspect their shape
- `02_similarity.ipynb` — compute cosine similarity between sentences and verify semantic behavior
- `03_chromadb_basics.ipynb` — store and retrieve vectors from ChromaDB

---

## 🗺️ Roadmap

- [x] Document ingestion and chunking
- [x] Local embeddings with sentence-transformers
- [x] ChromaDB vector storage
- [x] FastAPI search endpoint
- [ ] Hybrid search (BM25 + semantic)
- [ ] `/similar` endpoint
- [ ] Docker support
- [ ] Support for PDF and TXT files

---

## 📚 Learning resources

- [DeepLearning.AI: Building Applications with Vector Databases](https://www.deeplearning.ai/short-courses/building-applications-vector-databases/)
- [Sentence Transformers documentation](https://www.sbert.net/)
- [ChromaDB documentation](https://docs.trychroma.com/)
- [MTEB Leaderboard](https://huggingface.co/spaces/mteb/leaderboard) — for choosing embedding models
- [Andrej Karpathy: Intro to Large Language Models](https://www.youtube.com/watch?v=zjkBMFhNj_g)

---

## 🤝 Contributing

Contributions are welcome. If you find a bug or want to add a feature, open an issue or submit a PR.

---

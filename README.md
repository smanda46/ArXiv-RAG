# ArXiv-RAG: Retrieval-Augmented Generation for Research Papers

ArXiv-RAG is an end-to-end **Retrieval-Augmented Generation (RAG) pipeline** built to make research papers from [arXiv.org](https://arxiv.org) more searchable and useful. The system goes beyond plain text search by processing **text, images, tables, and even math formulas** inside PDFs, then serving relevant context to a Language Model for accurate, query-driven answers.

---

## Project Layout

```

ArXiv-RAG/
├── backend/             # Core backend logic for serving queries
├── faiss\_storage/       # FAISS index files for vector embeddings
├── json\_vectorization/  # Scripts for text & image embedding generation
├── llm-integration/     # Glue code for integrating with LLMs
├── pdf\_scraping/        # ArXiv PDF downloader & preprocessing scripts
├── rocks\_storage/       # RocksDB storage for metadata
├── tests/               # Unit & integration tests
├── handler/             # API or main service entrypoint
├── main.py              # Application bootstrap
├── Dockerfile           # Container setup for deployment
├── .gitignore           # Git ignore rules
└── README.md            # Project docs (this file)

````

*(virtual env, Git internals, and generated data directories excluded for clarity)*

---

## Features

- **Automated PDF Scraping**  
  Fetch and preprocess ArXiv papers by topic or time range.

- **Smart Metadata Storage**  
  - **RocksDB** → lightning-fast key-value lookups  
  - **FAISS** → high-performance vector similarity search

- **Text & Image Vectorization**  
  Embeds text, figures, and formulas into **512-dim CLIP embeddings**.

- **RAG Workflow**  
  Retrieves top-k relevant chunks and feeds them into an LLM for context-aware responses.

- **LLM Integration**  
  Combines embeddings and metadata for precise, human-like answers.

---

## Prerequisites

- **Python**: 3.10+
- **Libraries**:  
  `arxiv`, `requests`, `PyPDF2`, `pandas`, `tqdm`,  
  `faiss`, `rocksdb-python`, `clip`, `torch`, `langchain`
- **Optional**: Docker for containerized runs

---

## Setup

Clone the repo:
```bash
git clone https://github.com/smanda46/ArXiv-RAG.git
cd ArXiv-RAG
````

Create and activate a virtual environment:

```bash
python3 -m venv pdf-rag-venv
source pdf-rag-venv/bin/activate   # Linux/Mac
pdf-rag-venv\Scripts\activate      # Windows
```

Install dependencies:

```bash
pip install -r requirements.txt
```

(Optional) configure environment variables in a `.env` file.

---

## Usage

1. **Scrape PDFs**

   ```bash
   python pdf_scraping/main.py
   ```

2. **Vectorize content**

   ```bash
   python json_vectorization/vectorize.py
   ```

3. **Run backend API**

   ```bash
   python main.py
   ```

---

## Roadmap

* Migrate vector/metadata storage to cloud backends for scalability
* Add a lightweight web UI for real-time queries
* Expand support to other academic repositories (e.g., PubMed, IEEE Xplore)

---

## Notes

This project was built as a modular, research-friendly pipeline to help students, researchers, and developers interact with dense academic PDFs in a more natural way. Each stage is decoupled, making it easy to extend, swap, or scale.

---

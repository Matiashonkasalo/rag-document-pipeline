# DocuRAG

A production-ready Retrieval-Augmented Generation (RAG) pipeline for document question-answering.

## Overview

DocuRAG is an RAG system that processes PDF and text documents, generates semantic embeddings, stores them in a persistent vector database, and answers questions using retrieval-grounded LLM responses. Built with modern best practices, it provides a clear foundation for learning RAG architectures or deploying document QA systems.

## Features

- **Multi-format ingestion**: Load and process PDF and TXT documents
- **Intelligent chunking**: Recursive text splitting with configurable overlap
- **Semantic search**: Sentence Transformer embeddings with cosine similarity retrieval
- **Persistent storage**: ChromaDB vector store with on-disk persistence
- **Grounded responses**: LLM answers strictly based on retrieved context
- **Interactive exploration**: Jupyter notebooks for experimentation
- **Reproducible environment**: Locked dependencies via `uv.lock`

## Architecture
```
┌─────────────────────┐
│  PDF/TXT Documents  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│  Document Loaders   │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│   Text Chunking     │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Embedding Generation│
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ ChromaDB Vector DB  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ Semantic Retrieval  │
└──────────┬──────────┘
           │
           ▼
┌─────────────────────┐
│ LLM Answer Generation│
└─────────────────────┘
```

## Tech Stack

- **Python** 3.10+
- **LangChain** - RAG orchestration
- **ChromaDB** - Vector storage
- **Sentence Transformers** - Embedding generation
- **PyMuPDF** - PDF parsing
- **OpenAI API** - LLM responses
- **uv** - Dependency management

## Project Structure
```
DocuRAG/
├── data/
│   ├── PDF_files/          # Source PDFs
│   ├── text_files/         # Source text files
│   └── VectorStore/        # ChromaDB persistence (gitignored)
├── notebook/
│   ├── document.ipynb      # Text processing experiments
│   └── pdf_loader.ipynb    # PDF ingestion experiments
├── pyproject.toml
├── requirements.txt
├── uv.lock
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.10 or higher
- OpenAI API key

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/matiashonkasalo/rag-document-pipeline.git
cd rag-document-pipeline
```

2. **Install dependencies**

Using uv (recommended):
```bash
uv sync
```

Or with pip:
```bash
pip install -r requirements.txt
```

3. **Configure environment**

Set your OpenAI API key:
```bash
export rag_key="your_openai_api_key_here"
```

### Usage

1. **Add documents**

Place your documents in the data directory:
```
data/
├── PDF_files/
└── text_files/
```

2. **Run the pipeline**

The pipeline will:
- Load and parse documents
- Split text into semantic chunks
- Generate embeddings
- Store vectors in ChromaDB
- Enable question-answering

3. **Query your documents**

Example:
```python
query = "What is the attention mechanism?"
response = rag_pipeline.query(query)
print(response)
```

**Sample output:**
```
The attention mechanism is a technique in machine learning that allows models
to dynamically focus on relevant parts of input data when generating outputs...
```






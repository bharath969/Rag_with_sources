# RAG with Sources & Citations

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG)** pipeline that not only answers queries but also provides **source citations**. It works with **JSON** and **PDF** files as data sources, exploring different retrievers and their impact on retrieval quality and answer generation.

---

## Overview

Traditional RAG workflows often return answers without clear context. This project enhances RAG by:

- Using multiple retriever strategies: **Contextual Compression**, **Multi-Query**, and **Similarity/Ranking**
- Attaching **sources/citations** to responses for transparency
- Experimenting with how retrievers affect the relevance and completeness of answers

---

## Features

- Multiple retriever implementations:
  - Contextual Compression
  - Multi-Query
  - Similarity/Ranking
- Source citation and attribution
- Support for **JSON** and **PDF** data sources
- **LCEL chains** for efficient pipeline construction
- Interactive **Jupyter Notebook** for experimentation

---

## Installation

1. Create a virtual environment:

```bash
python -m venv venv
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Configure `.env` file with your API keys (e.g., OpenAI key)

---

## Usage

### Data Loading

- Load JSON/JSONL data (example: `wikidata_rag_demo.jsonl`) using `JSONLoader`
- Load PDF files using `unstructured` or `PyMuPDF`

### Embeddings

- Generate embeddings for text chunks
- Store embeddings in **vector stores** for fast retrieval

### Retrievers

- **Contextual Compression Retrieval**  
  Compresses documents before retrieval to keep only the most relevant context, reducing noise and speeding up RAG for long documents.

- **Multi-Query Retrieval**  
  Reformulates the user query into multiple queries and aggregates results to improve recall and retrieve different perspectives.

- **Similarity or Ranking-Based Retrieval**  
  Retrieves documents based on vector similarity or ranking scores, ideal for semantic search when exact keywords may not match the query.

### LCEL Chains

- **`src_rag_response_chain`**  
  Formats retrieved documents and combines them with the user question, sends the context + question to GPT-4o-mini using a RAG prompt template, and parses the output into a clean answer string.

- **`rag_chain_w_sources`**  
  Connects the retriever (e.g., similarity-based) to `src_rag_response_chain` and generates answers with **sources/citations** in a single pipeline.

---

## Running the Notebook

```bash
jupyter notebook
```

- Open the notebook to:
  - Load JSON and PDF data
  - Experiment with different retrievers
  - Observe how citations are included in answers

---

## Notes

- Ensure all dependencies in `requirements.txt` are installed
- `.env` file must contain API keys for GPT-4o access
- PDF extraction works best with **text-based PDFs**; scanned PDFs may require OCR

# Nexus

Nexus is an offline Retrieval-Augmented Generation (RAG) document assistant that enables users to interact with local documents using natural language. It combines semantic search with Microsoft's Phi language models to retrieve relevant information from indexed documents and generate accurate, context-aware responses.

Unlike cloud-based AI assistants, Nexus performs all document processing, indexing, retrieval, and inference locally, ensuring complete privacy without requiring API keys or external services.

Developed by **Soumyadeep Basu** as part of an undergraduate engineering curriculum.

<img width="1827" height="850" alt="Screenshot 2026-07-08 185324" src="https://github.com/user-attachments/assets/3d487373-c461-4d99-b3b7-d4f27db7c3bf" />

<img width="1838" height="676" alt="Screenshot 2026-07-08 185444" src="https://github.com/user-attachments/assets/03989ff5-7f25-4294-9fcb-1a77ef9b352f" />

<img width="1825" height="826" alt="image" src="https://github.com/user-attachments/assets/a9c77fb5-f1f3-4b50-bf35-9ad189345af0" />

<img width="1835" height="834" alt="Screenshot 2026-07-08 190024" src="https://github.com/user-attachments/assets/b7ca6ec7-ea20-4dad-bcb8-59db8356fd90" />

<img width="1835" height="507" alt="Screenshot 2026-07-08 190120" src="https://github.com/user-attachments/assets/7802c8e1-6b1f-4313-bea2-5fe0c2c208d9" />

<img width="1833" height="599" alt="Screenshot 2026-07-08 190218" src="https://github.com/user-attachments/assets/fedff282-aa2e-4d06-9488-f1f1b6854f2f" />

---

## Overview

Nexus allows users to ask questions about their documents using natural language. Documents are automatically indexed using semantic embeddings, enabling efficient retrieval of relevant information before generating responses with a locally hosted language model.

The application supports multiple document formats and continuously monitors the document directory for changes, automatically rebuilding the index whenever documents are added, modified, or removed.

---

## Features

- Offline document question answering
- Retrieval-Augmented Generation (RAG)
- Local inference using Microsoft Phi language models
- Semantic document search
- Automatic vector indexing
- Automatic document chunking
- Live file monitoring and index updates
- Multiple document format support
- GPU acceleration with CUDA (when available)
- Cross-platform compatibility
- No API keys required
- Fully local processing

---

## Supported File Formats

| Format | Supported |
|---------|-----------|
| TXT | Yes |
| PDF | Yes |
| DOCX | Yes |
| CSV | Yes |
| XLS | Yes |
| XLSX | Yes |

---

## System Architecture

```
                    User Query
                         │
                         ▼
                Document Collection
                         │
                         ▼
                  File Loaders
                         │
                         ▼
               Document Chunking
                         │
                         ▼
      Sentence Transformer Embeddings
                         │
                         ▼
               Vector Store Index
                         │
                         ▼
              Semantic Retrieval
                         │
                         ▼
          Microsoft Phi Language Model
                         │
                         ▼
                 Generated Response
```

---

## Technologies Used

- Python 3
- LlamaIndex
- Hugging Face Transformers
- Microsoft Phi
- Sentence Transformers
- LangChain
- PyTorch
- pandas
- PyMuPDF
- python-docx
- Watchdog
- Rich

---

## Project Structure

```
Nexus/
│
├── files/
│   ├── document.pdf
│   ├── notes.docx
│   ├── report.txt
│   └── dataset.xlsx
│
├── index_storage/
│
├── main.py
├── requirements.txt
└── README.md
```

---

## Installation

### Clone the Repository

```bash
git clone https://github.com/Soumyadxxp/Nexus.git

cd Nexus
```

### Create a Virtual Environment

**Windows**

```bash
python -m venv venv

venv\Scripts\activate
```

**Linux / macOS**

```bash
python3 -m venv venv

source venv/bin/activate
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

---

## Usage

Create a directory named `files` in the project root if it does not already exist.

Place the documents you want to analyze inside the `files` directory.

Run the application.

```bash
python main.py
```

During startup, Nexus will

1. Load the language model.
2. Initialize the embedding model.
3. Scan all supported documents.
4. Generate semantic embeddings.
5. Build the vector index.
6. Start monitoring the document directory.
7. Wait for user queries.

---

## Example Queries

General questions

```
What is this document about?

Summarize the report.

Explain the conclusion.

What are the key findings?

Who is the author?
```

File-specific questions

```
Summarize report.pdf

Explain notes.docx

What information is available in sales.xlsx?

What does resume.pdf contain?
```

---

## Built-in Commands

| Command | Description |
|----------|-------------|
| info | Display project information |
| cls | Clear the console |
| exit | Exit the application |
| quit | Exit the application |

---

## Processing Pipeline

### 1. Document Loading

Supported files are loaded using dedicated parsers.

### 2. Document Chunking

Documents are divided into overlapping chunks.

- Chunk Size: **128**
- Chunk Overlap: **20**

This improves semantic retrieval while maintaining contextual continuity.

### 3. Embedding Generation

Each document chunk is converted into a semantic vector using the Sentence Transformer embedding model.

### 4. Vector Indexing

Embeddings are stored in a LlamaIndex vector store for efficient similarity search.

### 5. Semantic Retrieval

When a query is received, the system retrieves the most relevant document chunks based on semantic similarity.

### 6. Response Generation

The retrieved context is passed to Microsoft's Phi language model, which generates an answer based solely on the indexed documents.

---

## Models Used

### Language Models

The application attempts to load the following models in order.

```
microsoft/phi-2

microsoft/phi-1_5

microsoft/phi-1
```

The first successfully initialized model is selected automatically.

### Embedding Model

```
sentence-transformers/all-mpnet-base-v2
```

---

## Automatic File Monitoring

Nexus continuously monitors the `files` directory.

Whenever a supported document is

- Added
- Modified
- Deleted

the application automatically rebuilds the vector index without requiring a restart.

---

## Privacy

Nexus is designed for complete local execution.

- No cloud services are used.
- No API keys are required.
- No document data is transmitted externally.
- All indexing and inference occur on the local machine.

---

## System Requirements

### Minimum

- Python 3.10 or later
- 8 GB RAM
- Multi-core processor

### Recommended

- 16 GB RAM or more
- NVIDIA GPU with CUDA support
- SSD storage

An internet connection is required only for downloading models during the first execution.

---

## Author

**Soumyadeep Basu**

This project was developed as part of an undergraduate engineering curriculum.

---

## Acknowledgements

This project is built upon the following open-source technologies.

- Microsoft Phi
- LlamaIndex
- Hugging Face Transformers
- Sentence Transformers
- LangChain
- PyTorch
- pandas
- PyMuPDF
- python-docx
- Watchdog
- Rich
  
---

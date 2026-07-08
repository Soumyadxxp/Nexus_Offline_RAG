# Nexus

> **An Offline Retrieval-Augmented Generation (RAG) Document Assistant Powered by Microsoft Phi**

Nexus is an offline Retrieval-Augmented Generation (RAG) document assistant that enables users to interact with local documents using natural language. It combines semantic search with Microsoft's Phi language models to retrieve relevant information from indexed documents and generate accurate, context-aware responses.

Unlike cloud-based AI assistants, Nexus performs all document processing, indexing, retrieval, and inference locally, ensuring complete privacy without requiring API keys or external services.

Developed by **Soumyadeep Basu** as part of an undergraduate engineering curriculum. 


<img width="1827" height="850" alt="Screenshot 2026-07-08 185324" src="https://github.com/user-attachments/assets/3d487373-c461-4d99-b3b7-d4f27db7c3bf" />

<img width="1838" height="676" alt="Screenshot 2026-07-08 185444" src="https://github.com/user-attachments/assets/03989ff5-7f25-4294-9fcb-1a77ef9b352f" />

<img width="1835" height="834" alt="Screenshot 2026-07-08 190024" src="https://github.com/user-attachments/assets/b7ca6ec7-ea20-4dad-bcb8-59db8356fd90" />

<img width="1835" height="507" alt="Screenshot 2026-07-08 190120" src="https://github.com/user-attachments/assets/7802c8e1-6b1f-4313-bea2-5fe0c2c208d9" />

<img width="1833" height="599" alt="Screenshot 2026-07-08 190218" src="https://github.com/user-attachments/assets/fedff282-aa2e-4d06-9488-f1f1b6854f2f" />

---

# Features

* Offline document question answering
* Retrieval-Augmented Generation (RAG)
* Local inference using Microsoft Phi language models
* Semantic document search
* Automatic document chunking
* Automatic vector indexing
* Real-time file monitoring
* Automatic index rebuilding when documents change
* Support for multiple document formats
* GPU acceleration with CUDA (when available)
* Cross-platform compatibility
* No API keys required
* Fully local and privacy-focused

---

# Supported File Formats

| Format | Supported |
| ------ | --------- |
| TXT    | ✅         |
| PDF    | ✅         |
| DOCX   | ✅         |
| CSV    | ✅         |
| XLS    | ✅         |
| XLSX   | ✅         |

---

# System Architecture

```text
                 User Query
                      │
                      ▼
            Document Collection
                      │
                      ▼
              Document Loaders
                      │
                      ▼
             Document Chunking
                      │
                      ▼
     Sentence Transformer Embeddings
                      │
                      ▼
           LlamaIndex Vector Store
                      │
                      ▼
         Semantic Similarity Search
                      │
                      ▼
       Retrieved Relevant Chunks
                      │
                      ▼
     Microsoft Phi Language Model
                      │
                      ▼
            Generated Response
```

---

# Technologies Used

* Python
* LlamaIndex
* Hugging Face Transformers
* Microsoft Phi
* Sentence Transformers
* LangChain
* PyTorch
* pandas
* PyMuPDF
* python-docx
* Watchdog
* Rich

---

# Project Structure

```text
Nexus/
│
├── files/                 # Place your documents here
├── index_storage/         # Automatically generated vector index
├── main.py
├── requirements.txt
└── README.md
```

---

# Installation

## 1. Clone the Repository

```bash
git clone https://github.com/Soumyadxxp/Nexus_Offline_RAG.git

cd Nexus
```

---

## 2. Create a Virtual Environment

### Windows

```bash
python -m venv venv

venv\Scripts\activate
```

### Linux / macOS

```bash
python3 -m venv venv

source venv/bin/activate
```

---

## 3. Install Dependencies

```bash
pip install -r requirements.txt
```

---

# First Run

During the first execution, Nexus automatically downloads the required language and embedding models from Hugging Face.

Depending on your internet connection, this may take several minutes.

Once downloaded, the models are cached locally and future launches do not require an internet connection.

---

# Usage

Run the application:

```bash
python main.py
```

If the `files` directory does not exist, Nexus creates it automatically.

Place your supported documents inside the `files` directory before asking questions.

During startup, Nexus will:

1. Load the Microsoft Phi language model.
2. Load the embedding model.
3. Scan supported documents.
4. Generate semantic embeddings.
5. Build the vector index.
6. Start monitoring the document directory.
7. Wait for user queries.

---

# Example Queries

## General Questions

```text
What is this document about?

Summarize the report.

Explain the conclusion.

What are the key findings?

Who is the author?
```

## File-Specific Questions

```text
Summarize report.pdf

Explain notes.docx

What information is available in sales.xlsx?

What does resume.pdf contain?
```

---

# Built-in Commands

| Command | Description                 |
| ------- | --------------------------- |
| `info`  | Display project information |
| `cls`   | Clear the terminal          |
| `exit`  | Exit the application        |
| `quit`  | Exit the application        |

---

# Retrieval-Augmented Generation Pipeline

### 1. Document Loading

Documents are loaded using dedicated parsers based on their file type.

### 2. Document Chunking

Documents are divided into overlapping chunks.

* **Chunk Size:** 128
* **Chunk Overlap:** 20

This improves semantic retrieval while maintaining contextual continuity.

### 3. Embedding Generation

Each document chunk is converted into a semantic vector using:

```text
sentence-transformers/all-mpnet-base-v2
```

### 4. Vector Indexing

Embeddings are stored inside a LlamaIndex Vector Store for efficient similarity search.

### 5. Semantic Retrieval

When a query is received, the system retrieves the most relevant document chunks using vector similarity.

### 6. Response Generation

The retrieved context is passed to Microsoft's Phi language model, which generates an answer based solely on the indexed documents.

---

# Models Used

## Language Models

Nexus attempts to load the following models in order:

```text
microsoft/phi-2

microsoft/phi-1_5
```

The first successfully initialized model is selected automatically.

## Embedding Model

```text
sentence-transformers/all-mpnet-base-v2
```

---

# Automatic File Monitoring

Nexus continuously monitors the `files` directory.

Whenever a supported document is:

* Added
* Modified
* Deleted

the application automatically reloads the documents and rebuilds the vector index without requiring a restart.

---

# Privacy

Nexus is designed for completely local execution.

* No cloud services
* No API keys
* No external inference
* No document uploads
* All indexing and inference remain on your computer

---

# GPU Support

If an NVIDIA GPU with CUDA is available, Nexus automatically performs inference on the GPU.

Otherwise, it seamlessly falls back to CPU execution.

---

# System Requirements

## Minimum

* Python 3.10 or later
* 8 GB RAM
* Multi-core processor

## Recommended

* Python 3.10 or later
* 16 GB RAM or more
* NVIDIA GPU with CUDA support
* SSD storage

An internet connection is required only during the first execution to download the required models.

---

# Limitations

* Supports text-based documents only.
* Scanned PDFs require OCR before processing.
* Images inside PDFs are not analyzed.
* Very large document collections may require additional memory.

---

# Acknowledgements

Nexus is built upon the following open-source technologies:

* Microsoft Phi
* LlamaIndex
* Hugging Face Transformers
* Sentence Transformers
* LangChain
* PyTorch
* pandas
* PyMuPDF
* python-docx
* Watchdog
* Rich

---

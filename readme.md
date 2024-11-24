
# Content Engine

## Overview
The **Content Engine** is a system designed to analyze and compare multiple PDF documents, specifically identifying and highlighting their differences. It uses **Retrieval Augmented Generation (RAG)** techniques to retrieve, assess, and generate insights. A chatbot interface built with Streamlit allows users to interact with the documents and gain comparative insights.

---

## Features
- **PDF Analysis**: Parse and process text from multiple PDF documents.
- **RAG System**: Utilize embeddings to retrieve relevant content.
- **Comparison Tool**: Highlight differences across documents.
- **Interactive Chatbot**: Provide answers to user queries via a conversational interface.
- **Privacy-Oriented**: Operates locally to ensure no data is sent to external APIs.

---

## Requirements

### Python Libraries
- `llama-index` or `langchain` (Choose one for retrieval)
- `streamlit`
- `chromadb` (or your chosen vector store library)
- `sentence-transformers` (for embedding models)
- `pdfminer.six` or `PyPDF2` (for PDF parsing)

### Local Language Model
- A locally hosted Large Language Model (e.g., GPT-J, LLaMA, etc.)

### Vector Store Options
- Supported vector stores: **ChromaDB**, **Pinecone**, **Faiss**, **Milvus**, **Weaviate**.

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/your-repo/content-engine.git
   cd content-engine
   ```

2. Install dependencies:
   ```bash
   pip install -r requirements.txt
   ```

3. Set up your embedding model:
   - Download and configure a local embedding model using `sentence-transformers`.

4. Configure your vector store:
   - Choose and install the library for your preferred vector store.

5. Set up a local LLM:
   - Install and run a local instance of a Large Language Model.

---

## Project Structure

```
Content-Engine/
│
├── app.py                 # Streamlit app for the chatbot interface
├── engine/
│   ├── document_parser.py  # Code for parsing PDFs
│   ├── vector_store.py     # Code for managing and querying embeddings
│   ├── query_engine.py     # Configuration of RAG-based retrieval system
│   ├── local_llm.py        # Integration with a local LLM
│   └── utils.py            # Utility functions
│
├── data/
│   ├── Alphabet_10K.pdf    # Input document
│   ├── Tesla_10K.pdf       # Input document
│   └── Uber_10K.pdf        # Input document
│
├── requirements.txt        # Python dependencies
└── README.md               # Project documentation
└── app.py
└── rest files
```

---

## Usage

### Step 1: Run the Streamlit App
```bash
streamlit run app.py
```

### Step 2: Interact with the Chatbot
- Access the web interface at `http://localhost:8501`.
- Use the chatbot to ask questions about the documents, such as:
  - "What are the risk factors associated with Google and Tesla?"
  - "What is the total revenue for Google Search?"
  - "What are the differences in the business of Tesla and Uber?"

---

## Example Code

### Document Parsing
```python
from pdfminer.high_level import extract_text

def parse_pdf(file_path):
    return extract_text(file_path)
```

### Generating Embeddings
```python
from sentence_transformers import SentenceTransformer

model = SentenceTransformer('all-MiniLM-L6-v2')

def generate_embeddings(text):
    return model.encode(text, show_progress_bar=True)
```

### Vector Store Integration
```python
from chromadb import Client

vector_store = Client()

def store_embeddings(doc_id, embeddings):
    vector_store.add(documents=[doc_id], embeddings=embeddings)
```

### Query Engine
```python
def query_engine(query, top_k=5):
    results = vector_store.query(query, top_k=top_k)
    return results
```

### Streamlit Chatbot
```python
import streamlit as st

st.title("Content Engine Chatbot")
query = st.text_input("Enter your question:")

if query:
    response = query_engine(query)
    st.write(response)
```

---


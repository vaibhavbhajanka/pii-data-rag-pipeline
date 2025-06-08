# Retrieval-Augmented Generation (RAG) Pipeline for Company Documents

## Overview

This project demonstrates a Retrieval-Augmented Generation (RAG) pipeline using GenAI techniques to analyze and answer questions about company documents, such as shipping orders, purchase orders, invoices, and inventory reports. The pipeline combines information retrieval from a document database with generative AI models to provide accurate, context-aware responses.

## What is RAG?
Retrieval-Augmented Generation (RAG) enhances the capabilities of large language models (LLMs) by first retrieving relevant information from a knowledge base and then generating responses based on that information. This approach improves the factual accuracy and relevance of generated answers.

## Features
- Loads and processes PDF company documents
- Embeds documents using HuggingFace sentence transformers
- Stores and retrieves document embeddings using Pinecone vector database
- Calculates semantic similarity between queries and documents
- Uses Groq's Llama 3.1 API for natural language generation
- Example queries and trends analysis on company data

## Setup & Installation

1. **Clone the repository**
2. **Install dependencies** (as used in the notebook):

```bash
pip install python-dotenv langchain langchain-community openai groq tiktoken pinecone-client langchain_pinecone unstructured pdfminer==20191125 pdfminer.six==20221105 pillow_heif unstructured_inference sentence-transformers
```

3. **Environment Variables**
   - Create a `.env` file in the project root with the following keys:
     - `PINECONE_API_KEY`
     - `OPENAI_API_KEY`
     - `GROQ_API_KEY`

4. **Dataset Download**
   - The notebook will attempt to automatically download the [Company Documents Dataset](https://www.kaggle.com/datasets/ayoubcherguelaine/company-documents-dataset) using the Kaggle CLI:
     ```python
     ! kaggle datasets download -d ayoubcherguelaine/company-documents-dataset
     ! unzip company-documents-dataset.zip
     ```
   - **Note:** The Kaggle CLI must be installed and authenticated on your system for this to work. If you encounter errors (e.g., `command not found: kaggle`), follow the troubleshooting steps below.

### Troubleshooting Dataset Download
- **Install the Kaggle CLI:**
  ```bash
  pip install kaggle
  ```
- **Authenticate the Kaggle CLI:**
  1. Go to your [Kaggle Account Settings](https://www.kaggle.com/account).
  2. Create a new API token. This will download a `kaggle.json` file.
  3. Place `kaggle.json` in the directory `~/.kaggle/` (create it if it doesn't exist).
  4. Set permissions: `chmod 600 ~/.kaggle/kaggle.json`
- **Manual Download:**
  - If you prefer, you can manually download and unzip the dataset from the [Kaggle dataset page](https://www.kaggle.com/datasets/ayoubcherguelaine/company-documents-dataset) and place it in the appropriate directory (e.g., `/content/CompanyDocuments`).

## Usage

Open and run the `RAG.ipynb` notebook. The main steps are:

1. **Install and import libraries**
2. **Load environment variables and API keys**
3. **Initialize embedding and vector store clients**
4. **Process and embed company documents**
5. **Insert document embeddings into Pinecone**
6. **Query the system with natural language questions**
7. **Retrieve relevant context and generate answers using Llama 3.1 via Groq**

### Example Queries
- "What are some common products bought by Mary Saveley?"
- "What are some trends with Ricardo Adocicados purchase orders?"

## Code Structure
- **Document Loading:** Uses `PyPDFLoader` to read PDFs
- **Embedding:** Uses HuggingFace's `all-MiniLM-L6-v2` model
- **Vector Store:** Pinecone for storing and retrieving embeddings
- **Similarity Search:** Cosine similarity for semantic search
- **LLM Generation:** Groq's Llama 3.1 API for answer generation

## Notes
- Ensure you have valid API keys for Pinecone, OpenAI, and Groq.
- The notebook is designed for educational and prototyping purposes.
- Some commands (e.g., Kaggle download) may require additional setup or authentication.

## References
- [LangChain Documentation](https://python.langchain.com/)
- [Pinecone Documentation](https://docs.pinecone.io/)
- [HuggingFace Sentence Transformers](https://www.sbert.net/)
- [Groq API](https://console.groq.com/docs)
- [Company Documents Dataset on Kaggle](https://www.kaggle.com/datasets/ayoubcherguelaine/company-documents-dataset)
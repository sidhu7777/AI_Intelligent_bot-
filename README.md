

# Intelligent Retrieval-Augmented Generation (RAG Model) Agent

This project implements a dynamic Retrieval-Augmented Generation (RAG) system combined with intelligent agent-level access control, graph-based expansion, and trigger-aware reranking.  
The assistant securely responds based only on the user's clearance level, using structured document embeddings and OpenAI's GPT models.

---

## Project Overview

The assistant flow is designed with multiple intelligent layers:

- **Environment Setup:** API keys and configurations are securely loaded using `.env` and `python-dotenv`.
- **Agent-Level Control:**  
  Users are prompted for their clearance level (Level-1 to Level-7+) at session start.
- **Hybrid Retrieval:**  
  Search for best-matching document chunks using a FAISS vector store plus metadata filtering.
- **Dynamic Graph Expansion:**  
  Expands the context dynamically based on graph-like relationships between chunks if needed.
- **Access Filtering:**  
  Only content authorized for the user's clearance level is passed to the model.
- **Trigger-Based Reranking:**  
  Boosts specific chunks if query matches known "triggers" in metadata.
- **Structured Context Formatting:**  
  Combines final chunks into a formatted prompt for the model.
- **OpenAI GPT-3.5 Turbo API Call:**  
  Final answer is generated based strictly on the allowed context.

If no authorized data is available for the query based on clearance, the assistant gracefully responds:  
> **"No authorized information available based on your clearance."**

---

## Features

- Intelligent access control based on agent level
- RAG system combining retrieval, expansion, and reranking
- Secure API key management via `.env`
- Structured context building with section-wise metadata
- Custom trigger detection for reranking important information
- Real-world operational feel with clearance-based restrictions
- FAISS-based local vector search for fast chunk retrieval
- OpenAI Chat Completion integration

---

## Folder Structure

```
INTELLIGENT_RAG/
│
├── RAG_datasets/                # Embedded documents and supporting data
│
├── .env                         # Environment variables (API keys)
├── .gitignore                   # Git ignore rules
├── LICENSE                      # Project license
├── README.md                    # Project documentation
├── RAG.ipynb                    # Full code (retrieval, access control, RAG loop)
│
├── chunk_metadata.json          # Metadata for each document chunk
├── embeddings.npy               # Numpy embeddings of chunks
├── faiss_index.bin              # FAISS index file for fast vector search
│
├── scraped_structured_data.txt  # Raw text data (optional)
├── structured_chunks.json       # Cleaned and chunked document pieces
├── structured_output.json       # Final JSON output used during retrieval
```

---

## How to Run

1. **Install dependencies:**

```bash
pip install openai python-dotenv faiss-cpu numpy pandas python-docx sentence-transformers  scipy  huggingface-hub rank-bm25


```

2. **Set up your `.env` file:**

```
OPENAI_API_KEY=your-openai-api-key
```

3. **Launch the RAG Assistant:**

Run the notebook or script:

```bash
python RAG.ipynb  # (inside Jupyter Notebook)
```

4. **Interact:**
- Enter your agent level (e.g., `Level-5`)
- Enter your query
- The assistant fetches allowed context, reranks, builds prompt, and responds.

---

## Example Output

```
Enter your agent level: Level-5

Greeting: The unseen hand moves, Whisper.

Enter your query: What are strategic asset relocation?

Assistant Response:
No authorized information available based on your clearance.
```

 The system smartly restricts data based on clearance levels.

---

## Requirements

- Python 3.8+
- Libraries:
  - `openai`
  - `python-dotenv`
  - `faiss-cpu`
  - `numpy`
  

---

## Future Improvements

- Switch to OpenAI Assistant API for memory and better state management
- Allow user authentication via tokens, not manual agent level
- Upgrade reranking logic with LLM-based relevance scoring
- Build UI interface using Streamlit or Gradio

---

## License

This project is licensed under the MIT License.

---


# EpsteinFiles-RAG
A RAG pipeline implementation built on the 'Epstein Files 20K' dataset from Hugging Face (Teyler).

![Recording 2026-02-10 230408](https://github.com/user-attachments/assets/e7378680-b113-442e-b112-7745197ade65)

Dataset source:  
👉 https://huggingface.co/datasets/teyler/epstein-files-20k

---

##  What This Project Does

This system:

- Downloads **2+ million raw document lines**
- Cleans and reconstructs documents by filename
- Chunks documents into semantically meaningful pieces
- Embeds them using Sentence Transformers
- Stores embeddings in **ChromaDB**
- Retrieves relevant context for a question
- Uses an LLM **only on retrieved context**
- Exposes a FastAPI backend
- Provides a Streamlit UI for querying

⚠️ **The model is not allowed to hallucinate.**  
If the answer is not present in the documents, it explicitly says so.

---

## Technical Architecture (High Level)

Raw Dataset
↓
Cleaning & Reconstruction
↓
Semantic Chunking
↓
Vector Embeddings
↓
Chroma Vector Database
↓
Retriever (MMR / similarity)
↓
LLM (Groq – LLaMA 3.3)
↓
Answer (Context-only)

## 🔄 Pipeline (Run in Order)

1. Download the dataset  
   Run:
   python ingest/download_dataset.py  
   → Saves raw data to `data/raw.json`

2. Clean and reconstruct documents  
   Run:
   python ingest/clean_dataset.py  
   → Removes junk rows and rebuilds documents by filename  
   → Output: `data/cleaned.json`

3. Chunk documents  
   Run:
   python ingest/chunk_dataset.py  
   → Splits documents into semantic chunks with metadata  
   → Output: `data/chunks.json`

4. Embed chunks into vector database  
   Run:
   python ingest/embed_chunks.py  
   → Stores embeddings in `chroma_db/`

5. Start the API server  
   Run:
   uvicorn api.main:app --reload  
   → API available at http://127.0.0.1:8000

6. Start the UI (new terminal)  
   Run:
   streamlit run app.py

## 🧰 Tech Stack

- Python 3.11
- Hugging Face Datasets
- LangChain (Core, HuggingFace, Chroma, Groq)
- ChromaDB (Vector Database)
- Sentence Transformers
- FastAPI + Uvicorn
- Streamlit
- Groq LLaMA 3.3 (70B)

---

## 👤 Author

Built by **Ankit Kumar Nayak**  
Full-Stack Developer | AI & RAG Systems

---

## 💬 Support

If you encounter issues or want to extend this project:
- Open an issue on the repository
- Suggest improvements or optimizations
- Fork and experiment responsibly

This project is built for **transparency, research, and learning**.



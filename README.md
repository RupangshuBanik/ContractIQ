# ContractIQ API

ContractIQ is a **Retrieval-Augmented Generation (RAG) API** built with **FastAPI**. It is designed to answer questions based on the content of a provided **PDF or DOCX document**.

The system uses a **hybrid retrieval approach**, combining sparse and dense search methods to find the most relevant passages before a language model generates a concise answer.

📌 **GitHub Link**: [ContractIQ](https://github.com/RupangshuBanik/ContractIQ)

---

## 🚀 Features
- **PDF/DOCX Processing**: Extracts text from both PDF and DOCX file formats.
- **Hybrid Retrieval**: Combines DPR (Dense Passage Retrieval) and Sentence-Transformers (dense) search.
- **Reciprocal Rank Fusion (RRF)**: Merges results from both retrieval methods.
- **Cross-Encoder Re-ranking**: Re-ranks passages using a cross-encoder model.
- **Extractive & Generative QA**: Supports extractive Q&A and LLM-based generative answers.
- **FastAPI Backend**: Production-ready API with a clean request/response structure.

---

## ⚙️ How It Works
1. **Document Ingestion**: The API fetches a PDF or DOCX file from a given URL.
2. **Text Extraction**: Extracts and cleans text from the document.
3. **Chunking**: Splits text into smaller passages.
4. **Indexing**:
   - Sparse index (**Whoosh**) for DPR keyword search.
   - Dense index (**Sentence-Transformers**) for semantic search.
5. **Hybrid Search**:
   - Sparse index retrieves keyword-relevant passages.
   - Dense index retrieves semantically relevant passages.
6. **Fusion & Re-ranking**:
   - Combines results using **RRF**.
   - Applies **cross-encoder re-ranking** to find the most relevant passages.
7. **Answer Generation**:
   - If `USE_LLM_READER=True` and `OPENAI_API_KEY` is available → uses **LLM** (e.g., GPT-4o-mini).
   - Otherwise → falls back to **extractive QA**.
8. **API Response**: Returns answers in **JSON** format.

---

## 📦 Tech Stack
- **FastAPI** (Backend)
- **Whoosh** (Sparse Retrieval)
- **Sentence-Transformers** (Dense Retrieval)
- **DPR** (Dense Passage Retrieval)
- **Cross-Encoder Models** (Re-ranking)
- **OpenAI GPT models** (Generative QA)

---

---

## 📬 API Response Format
```json
{
  "question": "What is ContractIQ?",
  "answer": "ContractIQ is a Retrieval-Augmented Generation API built with FastAPI to answer questions from PDF/DOCX files.",
  "context": ["ContractIQ is a RAG API built with FastAPI..."],
  "source": "https://example.com/document.pdf"
}
```

---

## 🔑 Environment Variables
```bash
USE_LLM_READER=True
OPENAI_API_KEY=your_api_key_here
```

---

## 🛠️ Installation & Setup
```bash
git clone https://github.com/RupangshuBanik/ContractIQ.git
cd ContractIQ
pip install -r requirements.txt
uvicorn app.main:app --reload
```

---

## 📖 Documentation
Once running, visit the interactive API docs at:

➡️ [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs)

---

## 🤝 Contributing
Contributions, issues, and feature requests are welcome! Feel free to check the [issues page](https://github.com/RupangshuBanik/ContractIQ/issues).

---

## 📜 License
This project is licensed under the **MIT License**.

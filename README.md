# 🧬 NEET Biology Concept Explainer  
### Retrieval-Augmented Generation (RAG) System using NCERT

---

## 📌 Project Overview

This project is a **NEET Biology Concept Explainer** built using a **Retrieval-Augmented Generation (RAG)** architecture.  
It answers Biology questions **strictly based on NCERT Class XI & XII Biology textbooks**, rewritten in **simple, student-friendly language** suitable for NEET preparation.

Unlike generic LLM chatbots, this system:
- Avoids hallucination *(by generating answers only from semantically retrieved NCERT content using Hugging Face embeddings and FAISS, with strict prompt constraints and no external knowledge access)*  
- Avoids out-of-syllabus content  
- Avoids copying NCERT sentences  
- Produces **original, exam-oriented explanations**

The application is implemented as a **full-stack AI system** using:
- **FastAPI** (backend + frontend serving)
- **FAISS** (vector similarity search)
- **Hugging Face Transformer encoders** (sentence embeddings)
- **LLaMA-3 via Ollama** (answer generation)

---

## 🎯 Problem Statement

NEET aspirants often face:
- Dense NCERT explanations  
- Online answers that go beyond syllabus  
- Hallucinated or plagiarized responses from LLMs  

This project solves the problem by:
- Grounding all answers strictly in NCERT PDFs  
- Using semantic retrieval instead of guessing  
- Rewriting concepts in **clear, NEET-focused language**

---

## 🧠 RAG SYSTEM – BUILD FLOW (Knowledge Base Construction)

This flow represents the **offline / one-time build process** of the RAG system.

Start
↓
Collect NCERT Biology PDFs
(Class XI & Class XII)
↓
PDF Document Loader
(Text Extraction)
↓
Text Cleaning & Normalization
↓
Text Chunking
(semantic, overlapping chunks)
↓
Hugging Face Transformer-based
Sentence Embeddings
(chunks → dense vectors)
↓
Vector Normalization
(for cosine similarity)
↓
FAISS Vector Index Creation
(Cosine Similarity Search)
↓
Persist Artifacts to Disk
(chunks.pkl, embeddings.npy, faiss.index)
↓
RAG Knowledge Base Ready
↓
End

✔ This pipeline runs **once during build time**, not during query time.

---

## 🧠 RAG QUERY-TIME FLOW (Runtime Inference)
User Question
↓
Query Embedding
(Hugging Face Transformer Encoder)
↓
FAISS Cosine Similarity Search
↓
Top-K Relevant NCERT Chunks
↓
Rule-Constrained Prompt Engineering
↓
LLaMA-3 (Transformer Decoder via Ollama)
↓
NEET-Style Concept Explanation


---

## 🧩 Core Techniques Used

### 1️⃣ Retrieval-Augmented Generation (RAG)
- Combines retrieval with generation  
- Keeps LLM responses grounded in NCERT content  
- Core mechanism for hallucination control  

### 2️⃣ NCERT PDF Processing
- Structured loading of NCERT Biology PDFs  
- Page-wise text extraction  
- NCERT used as the **single source of truth**  

### 3️⃣ Text Chunking Strategy
- Text split into **semantic overlapping chunks**  
- Preserves conceptual continuity  
- Optimized for biology concepts  

### 4️⃣ Hugging Face Transformer-based Sentence Embeddings
- Each NCERT chunk converted into dense vectors  
- Implemented using **Hugging Face Transformer encoder models**  
- Captures semantic meaning rather than keywords  
- Handles paraphrased and indirect questions  

### 5️⃣ Cosine Similarity Search using FAISS
- Embeddings normalized  
- FAISS performs **cosine similarity-based semantic retrieval**  
- Retrieves the most relevant NCERT chunks  

> Cosine similarity is used because it compares semantic direction rather than magnitude.

### 6️⃣ Prompt Engineering (Critical Design)
Strict constraints enforced:
- NCERT content used only for understanding  
- No sentence copying  
- Simple NEET-level language  
- 4–6 concise sentences  
- Focus on definition and key functions  

### 7️⃣ LLaMA-3 via Ollama (Transformer Decoder)
- Decoder-only Transformer model  
- Executed locally using **Ollama**  
- No Hugging Face inference pipeline used  
- Offline, cost-free inference  
- Used strictly for explanation and rewriting  

---

## 🚫 How the System Avoids Hallucination

- Answers are generated **only after retrieving semantically relevant NCERT chunks**
- Retrieval uses **Hugging Face embeddings + FAISS cosine similarity**
- The LLM never answers from its own knowledge
- No internet access or external tools during generation
- Prompt rules strictly limit scope and wording

---

## 🌐 Backend (FastAPI)

### Features
- FastAPI-based **HTTP inference endpoint**
- Serves frontend UI directly
- Handles long-running LLM inference
- Clear separation of build-time and query-time logic

### Endpoints

| Endpoint | Purpose |
|--------|--------|
| `/` | Frontend UI |
| `/concept` | POST – AI inference endpoint |
| `/docs` | Swagger UI (testing only) |
| `/health` | Health check |

---

## 🎨 Frontend
- HTML, CSS, JavaScript  
- Served directly by FastAPI  
- Uses Fetch API to communicate with backend  

---

## 🛠️ Tools & Technologies

### Programming & Frameworks
- Python  
- FastAPI  
- JavaScript  
- HTML, CSS  

### AI & NLP
- Hugging Face Transformer Encoder Models  
- Sentence Embeddings  
- FAISS  
- Cosine Similarity Search  
- Retrieval-Augmented Generation (RAG)  
- Prompt Engineering  
- LLaMA-3 (via Ollama – Transformer Decoder)  

### Data & Storage
- FAISS index  
- NumPy  
- Pickle  

---

## 🚀 How to Run

```bash
venv\Scripts\activate
python -m uvicorn backend.main:app --host 127.0.0.1 --port 8007

http://localhost:8007



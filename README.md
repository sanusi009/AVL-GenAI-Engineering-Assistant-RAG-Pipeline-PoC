# 🚗 AVL GenAI Engineering Assistant — RAG Pipeline PoC

> End-to-end Retrieval-Augmented Generation (RAG) pipeline for automotive  
> engineering knowledge — with vector search, evaluation metrics, and drift monitoring.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Gemini](https://img.shields.io/badge/LLM-Gemini%201.5%20Flash-orange?style=flat-square)
![FAISS](https://img.shields.io/badge/Vector%20Store-FAISS-purple?style=flat-square)
![Gradio](https://img.shields.io/badge/UI-Gradio-ff6b6b?style=flat-square)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Status](https://img.shields.io/badge/Status-PoC%20Complete-brightgreen?style=flat-square)

---

## 📌 Overview

A production-style **Retrieval-Augmented Generation (RAG)** pipeline built as a  
proof-of-concept aligned with the AVL List GmbH Working Student role in  
Generative AI & Data Engineering.

The assistant answers questions about AVL engineering topics (PUMA test systems,  
emission standards, data pipelines, GenAI policy) using **only verified documents**  
— no hallucination, fully grounded, every answer evaluated and logged.

---

## 🏗️ Pipeline Architecture

```
Documents (PDF / text / DB)
         │
         ▼
┌─────────────────────┐
│  1. INGESTION        │  Chunking with overlap (200 words, 40-word overlap)
│     & CHUNKING       │
└────────┬────────────┘
         ▼
┌─────────────────────┐
│  2. EMBEDDING        │  sentence-transformers/all-MiniLM-L6-v2 (local, free)
│     & INDEXING       │  → FAISS IndexFlatIP (cosine similarity)
└────────┬────────────┘
         ▼
┌─────────────────────┐
│  3. RETRIEVAL        │  Query embedding → top-k FAISS search
│     (RAG core)       │  Similarity-ranked chunks with source attribution
└────────┬────────────┘
         ▼
┌─────────────────────┐
│  4. GENERATION       │  Gemini 1.5 Flash + system prompt + retrieved context
│     (Grounded LLM)   │  Context-only answering — refuses if not in KB
└────────┬────────────┘
         ▼
┌─────────────────────┐
│  5. EVALUATION       │  Faithfulness · Relevance · Completeness scores
│     & MONITORING     │  Drift detection vs historical baseline
└────────┬────────────┘
         ▼
┌─────────────────────┐
│  6. LOGGING          │  CSV audit log: query, source, scores, response time
│     & ANALYTICS      │  Dashboard: score trends, source frequency, drift alerts
└─────────────────────┘
```

---

## 📚 Knowledge Base — AVL Engineering Documents

| Document | Topics Covered |
|---|---|
| AVL PUMA Test System Manual | Test automation, drive cycles, NEDC/WLTP/RDE |
| Emission Testing Guide | WLTP phases, RDE boundary conditions, PEMS |
| Data Engineering Pipeline | ETL, Kafka, Spark, Azure Data Lake, metadata |
| GenAI Integration Policy | RAG architecture, vector DBs, hallucination monitoring |
| Powertrain & EV Testing | HiL, BEV, FCEV, battery testing, NVH |
| ML for Engine Calibration | GPR, DoE, CAMEO, knock detection, federated learning |

---

## 📊 Evaluation Metrics

| Metric | Method | What it measures |
|---|---|---|
| **Faithfulness** | Answer-context keyword overlap | Is the answer grounded in retrieved docs? |
| **Relevance** | Query-chunk keyword match | Did retrieval find the right document? |
| **Completeness** | Answer length scoring | Is the answer substantive? |
| **Drift monitoring** | Score vs historical baseline | Is quality degrading over time? |

---



## 🛠️ Tech Stack

| Component | Technology | Cost |
|---|---|---|
| LLM | Gemini 1.5 Flash | Free tier |
| Embeddings | sentence-transformers (local) | Free |
| Vector store | FAISS (in-memory) | Free |
| UI | Gradio (public share link) | Free |
| Data | Pandas + CSV | Free |
| Visualization | Matplotlib | Free |

**Total cost: $0** ✅

---

## 🔮 Production Extensions

- [ ] Replace FAISS with **pgvector** or **Azure AI Search** for persistence
- [ ] Add **PDF ingestion** from SharePoint / Azure Blob Storage
- [ ] Connect to **Apache Kafka** stream for real-time document updates
- [ ] Deploy on **Azure Container Apps** with Azure OpenAI endpoint
- [ ] Add **LLM-based faithfulness scoring** (G-Eval / RAGAs framework)
- [ ] Implement **golden query monitoring** for automated quality regression

---

## 👤 Author

**Sanusi Isiaka Olatunji**  
M.Sc. Data Science — University of Leoben, Austria  
[LinkedIn](https://linkedin.com/in/sanusi-olatunji-43990198) 

*Built as a PoC aligned with AVL List GmbH — Working Student: Generative AI & Data Engineering*

# 🧠 LLM System Design Interview – Practice Questions

This document contains a curated list of mock LLM system design prompts tailored for interviews, including realistic use cases from Databricks customers.

---

## 🧪 Question 1: Real-Time Contract Clause Rewriting Assistant

> Design a system that helps legal professionals rewrite specific clauses in a contract using plain English, powered by an LLM.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Who are the users—lawyers, clients, paralegals?
- What contract types? (NDAs, licensing, employment)
- Definition of “real-time” latency?
- Should LLM explain or just rewrite?
- Is on-prem deployment required for data privacy?

### ✅ Functional Requirements
- Rewrite clauses on input.
- Highlight + explain transformation.
- Support multiple writing styles (plain, formal).

### ⚙️ Non-Functional Requirements
- p95 latency < 300ms.
- Privacy: All data stays on-prem.
- Support for 100 concurrent users.

### 🧩 Architecture
- Frontend: Rich text editor (e.g., SlateJS).
- Backend: FastAPI + vLLM (or Ollama).
- Retrieval: None, or clause similarity DB.
- Model: Quantized LLM via vLLM.

</details>

---

## 🧪 Question 2: Resume Ranking for Job Descriptions

> Build a system that scores and ranks resumes against a job description using LLM-based techniques.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Resume volume per job?
- Is latency or cost more important?
- Pre-computation allowed?
- Explainable matching needed?

### ✅ Functional Requirements
- Rank resumes by JD match.
- Include skill overlap, experience.

### ⚙️ Non-Functional Requirements
- 10k resumes ranked < 5s.
- Consistent scoring across runs.

### 🧩 Architecture
- Precompute resume embeddings.
- On-demand JD embedding.
- ANN search (FAISS/pgvector).
- Cross-encoder for top-100 reranking.

</details>

---

## 🧪 Question 3: Customer Support Answer Generator (RAG)

> Design a support system that generates LLM answers grounded in documentation, manuals, and past tickets.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Agent-facing or end-user chatbot?
- Multilingual support needed?
- Document freshness SLA?
- Citation required?

### ✅ Functional Requirements
- Retrieve docs.
- Generate grounded answers.
- Provide source references.

### 🧩 Architecture
- Embed + chunk docs via AutoLoader.
- Index in pgvector / Redis-Vector.
- RAG over retrieved context using vLLM/SGLang.
- Guardrails for hallucination monitoring.

</details>

---

## 🧪 Question 4: Industrial IoT Alert Summarizer (Manufacturing Client)

> Summarize alerts from machinery and suggest root causes based on historical logs.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Sensor alert frequency?
- Time window for summarization?
- Labeled RCA data availability?

### 🧩 Architecture
- Delta Live Tables + Spark for ingestion.
- FAISS for log similarity search.
- LLM for summarization + RCA generation.

</details>

---

## 🧪 Question 5: Financial News Insight Assistant (Hedge Fund)

> Build an LLM that extracts investment signals from real-time financial news.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Assets covered? (equities, crypto?)
- Generate summaries or structured outputs?
- Require attribution or audit?

### 🧩 Architecture
- Event extraction → Delta Lake.
- NLP pipeline → entity classification.
- RAG over internal analyst notes.
- LLM generates investment insight.

</details>

---

## 🧪 Question 6: Internal Retail Assistant (Global Retail Chain)

> Answer employee queries about policies, inventory rules, and workflows based on PDFs, Excel, and SharePoint docs.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- How often docs change?
- Permissions enforced?
- Support structured & unstructured data?

### 🧩 Architecture
- Ingest via AutoLoader.
- OCR + parsing → chunking → vector index.
- Use LlamaIndex or LangChain.
- Guardrails for citations + permissions.

</details>

---

## 🧪 Question 7: Email Routing and Summarization (Banking Client)

> Classify and summarize customer support emails, including urgency scoring.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Training data available?
- Multi-language needed?
- Is routing automated or human-reviewed?

### 🧩 Architecture
- Email ingestion into Delta.
- Classifier LLM for topic + urgency.
- Summarizer LLM (vLLM or Claude).
- Feedback loop into labeled store.

</details>

---

## 🧪 Question 8: Analyst Copilot for SQL + Dashboards (Databricks Internal)

> Let internal analysts use natural language to query dashboards, notebooks, and metrics.

<details>
<summary>🔍 Click to expand</summary>

### 🎯 Clarifying Questions
- Should copilot run SQL or just assist?
- Query execution or suggestion-only?
- Audit and permission control?

### 🧩 Architecture
- Unity Catalog metadata + query logs.
- Semantic search over dashboards.
- LLM agent to generate SQL / Python cells.
- Approval + audit logging.

</details>

---

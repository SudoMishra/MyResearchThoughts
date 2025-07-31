
# 🧠 LLM System Design Interview – Preparation Roadmap

> **Goal**: Prepare to solve open-ended LLM system design problems by practicing clarification, design articulation, trade-off analysis, and deployment best practices.

---

## 0️⃣ Frame the Interview

- **🎯 Understand expectations**
  - Panel gives a problem statement.
  - Your job: clarify **business value**, define **functional + non-functional requirements (F/NFRs)**, propose **architecture**, reason about **scaling**, **trade-offs**, and **monitoring**.

- **📝 Build a Prompt Sheet**
  - **Business Value**: Who are the users? What pain is being solved?
  - **Inputs/Outputs**: Size, rate, data shape, security?
  - **Quality Bar**: Latency, accuracy, cost, compliance?
  - **Lifecycle**: How frequently does model or data change?
  - **Failure Modes**: What breaks? How is success measured?

---

## 1️⃣ Core Concepts & Requirement Mapping

- [[Retrieval-Augmented Generation]], [[Fine-tuning vs Prompting]], [[Agentic Workflows]], [[Structured LLM Output]]

- **📋 NFR Mapping Table**


| NFR         | LLM Lever                   | Sample Interview Question         |
|-------------|-----------------------------|-----------------------------------|
| Latency     | KV caching, batching        | "Can we meet p95 < 300ms?"        |
| Cost        | Model routing, quantization | "Do we always need GPT-4?"        |
| Privacy     | On-prem, PII redaction      | "Can any data leave VPC?"         |
| Reliability | Replicas, retries           | "How tolerant to timeouts?"       |


- ✅ Deliverable: **One-pager requirement checklist** for interviews.

---

## 2️⃣ Architecture & Tech Stack Deep Dive

### Serving & Scheduling
- [[vLLM]], [[SGLang]], [[Triton-LLM]], [[Ray Serve]], [[Speculative Decoding]]

### Orchestration
- [[LangChain]], [[LlamaIndex]], [[BentoML]]

### Vector & Metadata Stores
- [[pgvector]], [[Redis-Vector]], [[Milvus]], [[Chroma]]

### Interfaces
- [[FastAPI]], [[gRPC]], streaming tokens (SSE / WebSocket)

### Security
- Token-level PII filters, [[Vault Secrets]], [[Policy Compliance]]

> 🎨 Deliverable: 2 annotated architecture diagrams (one real-time, one async batch pipeline)

---

## 3️⃣ Scaling Patterns & Trade-Offs

### ⚙️ Bottlenecks
- **Compute**: GPU mem, attention kernels → [[Flash Attention]], quantization
- **IO**: vector DB, cloud storage → caching, shard replicas
- **Concurrency**: spikes → [[Dynamic Batching]], [[Token Scheduling]]

### 🔄 Trade-Off Drill Table
| Option A | Option B | When to prefer |
|----------|----------|----------------|
| Huge model | MoE or small experts | When cost or latency is tight |
| In-house model | API call | If privacy or control is needed |
| CPU edge | GPU cloud | If latency isn't critical |

> 🧾 Deliverable: **2-page memo** on scaling a multilingual RAG system from 10 → 1000 QPS

---

## 4️⃣ Productionisation & Monitoring

### CI/CD for LLMs
- [[MLflow]], [[Model Registry]], Shadow deployments

### Guardrails & Safety
- Prompt filters, [[LLM Content Moderation]], [[Red teaming]]

### Observability Stack
- [[OpenTelemetry]], [[Prometheus]], [[Grafana]], [[Langfuse]]

### Eval Loops
- Synthetic + human-in-the-loop red teaming
- Daily RAG regression runs

### Incidents
- Monitor token budget, refusal rate, hallucination rate

> 🧪 Mini-lab: Deploy toy vLLM + FastAPI and add OTel traces to Grafana dashboard

---

## 5️⃣ Final Prep: Mock Interviews & Flashcards

- Simulate 3 design questions (e.g. “Design a real-time multilingual support agent”)
- Review checklist: Did you...
  - Clarify business value?
  - Identify F/NFRs?
  - Propose viable architecture?
  - Discuss scaling & bottlenecks?
  - Handle deployment and monitoring?

- 🔁 Create flashcards for:
  - Trade-offs (e.g. speculative decoding vs quantized inference)
  - Metrics (e.g. p95 latency, eval cost/token)
  - Framework features (e.g. vLLM batching strategies)

---

## 📚 Resources & Reading

| Topic | Resource |
|-------|----------|
| [[LLM Serving]] | vLLM 2025 release notes, Ray Serve docs |
| [[Scaling]] | Flash Attention, Speculative Decoding |
| [[Monitoring]] | OpenTelemetry + Langfuse integration |
| [[Benchmarks]] | vLLM vs SGLang throughput benchmarks |
| [[Framework Comparison]] | Adyog LLM serving blog (2025) |

---

> 💡 Tip: Everything you prepare should be **usable in the interview**. Diagrams, checklists, trade-off tables, and a prompt sheet = your toolkit.


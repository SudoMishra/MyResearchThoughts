
Use-case style ML problems where the system must:
1. **Retrieve** a set of candidate documents/passages/items.
2. **Rerank** them using a deeper model or a task-specific signal (relevance, intent match, semantic similarity, etc.)

---

## 1. Customer Support Answer Finder
**Question:**  
A user types: "How do I get a refund for a defective product?"  
You have a large set of support FAQs and documents.  
Build a retrieval + reranking pipeline to return the most relevant answer.

**Tags:** #retrieval #faq #support  
**Retriever:** BM25 / dense encoder  
**Reranker:** BERT (cross-encoder)  
**Extensions:** Add intent/urgency reranking

---

## 2. Academic Paper Recommendation
**Question:**  
Given a query like: *"papers on self-supervised contrastive learning in NLP"*,  
retrieve top-10 arXiv papers and rerank based on title + abstract + method section.

**Tags:** #retrieval #papers #semanticsearch  
**Retriever:** SPECTER / DPR  
**Reranker:** SciBERT cross-encoder  
**Extensions:** Citation graph reranking, freshness bias

---

## 3. Resume → Job Posting Matching
**Question:**  
A candidate submits a resume. Retrieve the most relevant job postings and rerank them based on role fit, skills match, and career level.

**Tags:** #retrieval #hrtech #ranking  
**Retriever:** FAISS / sparse + dense hybrid  
**Reranker:** BERT cross encoder with skill overlap  
**Extensions:** Learn-to-rank with click data, personalization

---

## 4. Query → Product Description Matching
**Question:**  
Query: "best wireless earbuds for gym with noise cancellation"  
Retrieve relevant products and rerank based on textual relevance and review features.

**Tags:** #ecommerce #retrieval #recommendation  
**Retriever:** BM25 + dense encoder  
**Reranker:** BERT w/ product specs and reviews  
**Extensions:** Use star ratings, price as rerank features

---

## 5. Query → Code Snippet Search
**Question:**  
Query: "how to read JSON file in Python using pathlib"  
Retrieve relevant code snippets from a codebase and rerank based on exact API usage and docstring similarity.

**Tags:** #retrieval #code #developersearch  
**Retriever:** CodeBERT embeddings  
**Reranker:** CrossEncoder w/ syntax-aware features  
**Extensions:** Use execution traces or function popularity

---

## 6. Legal Case Retrieval
**Question:**  
A legal assistant queries: "cases related to discrimination in hiring practices (post 2010)"  
Retrieve relevant legal cases and rerank based on jurisdiction, date, and factual similarity.

**Tags:** #legal #retrieval #caselaw  
**Retriever:** TF-IDF + dense hybrid  
**Reranker:** LegalBERT + metadata-aware reranker  
**Extensions:** Graph reranker using case citations

---

## 7. Research QA (Passage Reranking)
**Question:**  
Query: *"What is the impact of learning rate warm-up in Transformers?"*  
Retrieve candidate paragraphs from papers and rerank to extract most relevant passage.

**Tags:** #QA #retrieval #research  
**Retriever:** DPR or ColBERT  
**Reranker:** BERT with answer span supervision  
**Extensions:** Chain-of-thought-aware reranking

---

## 8. Tweet or Post Retrieval for Moderation
**Question:**  
Given a harmful text like: "This person should be silenced permanently."  
Retrieve similar past posts and rerank them by severity and potential violation type.

**Tags:** #contentmoderation #retrieval #ranking  
**Retriever:** Sentence embeddings (SBERT)  
**Reranker:** Content BERT + classification head  
**Extensions:** Include user history or topic modeling

---

## 9. Patent Search by Idea Description
**Question:**  
Inventor types: "A wearable device that tracks hydration using skin sensors."  
Retrieve similar patents and rerank based on similarity to claims/abstract sections.

**Tags:** #patents #retrieval #similarity  
**Retriever:** TF-IDF + BERT  
**Reranker:** LegalBERT w/ claim-section scoring  
**Extensions:** Embedding alignment with USPTO sections

---

## 10. Recipe Search by Ingredients
**Question:**  
Query: "chickpeas, garlic, lemon, olive oil"  
Retrieve matching recipes and rerank based on flavor profile similarity and number of matching ingredients.

**Tags:** #retrieval #recommendation #recipes  
**Retriever:** Ingredient vector match  
**Reranker:** TextBERT + cosine overlap  
**Extensions:** Incorporate dietary filters, taste preference models

---

## 🛠 Suggested Architecture Pattern


# 🔗 Matching + Dual Encoding - Problem Bank

These are use-case style problems where the objective is to match two entities using **dual encoders**:
- Text-to-text
- Text-to-graph
- Query-to-product
- Resume-to-job
- User-to-item

Dual encoders allow scalable, approximate retrieval or semantic matching using independent encoding and similarity computation.

---

## 1. Semantic Sentence Matching
**Question:**  
Given two sentences:
- A: *"What are the symptoms of COVID-19?"*  
- B: *"How can I tell if I have coronavirus?"*  
Train a model to predict whether they are semantically equivalent.

**Tags:** #dualencoder #semanticmatching #NLP  
**Dataset Ideas:** Quora Question Pairs, PAWS  
**Model Ideas:** SBERT, BERT + cosine  
**Extensions:** Add hard negatives (e.g., near-duplicates)

---

## 2. Resume → Job Description Matching
**Question:**  
Given a resume and a job posting, encode both and compute similarity to recommend jobs.

**Tags:** #resume #matching #dualencoder  
**Dataset Ideas:** Job2Resume, O*NET skill embeddings  
**Model Ideas:** BERT dual encoders  
**Extensions:** Skill embedding injection, job level conditioning

---

## 3. Product → Query Matching
**Question:**  
Query: *“noise-cancelling headphones for travel”*  
Product title: *“Bose QuietComfort 45 – Wireless ANC Headphones”*  
Build a dual encoder to compute relevance.

**Tags:** #ecommerce #dualencoder #retrieval  
**Dataset Ideas:** Amazon product corpus  
**Model Ideas:** DistilBERT dual encoders  
**Extensions:** Cross-modal features, titles + reviews + specs

---

## 4. Legal Clause → Precedent Case Matching
**Question:**  
Match a contract clause like *“termination for convenience”* to similar case summaries in legal precedent databases.

**Tags:** #legal #dualencoder #casematching  
**Dataset Ideas:** CUAD, case summaries  
**Model Ideas:** LegalBERT dual encoders  
**Extensions:** Use clause type embeddings

---

## 5. Tweet → News Headline Matching
**Question:**  
Given a viral tweet, retrieve the most related news headline using dual encoders.

**Tags:** #socialmedia #news #matching  
**Dataset Ideas:** TWEETNEWS, RumourEval  
**Model Ideas:** BERT dual encoders  
**Extensions:** Temporal filtering + fact match

---

## 6. Query → StackOverflow Post Retrieval
**Question:**  
Query: *"how to fix ValueError when parsing float in Python"*  
Retrieve relevant StackOverflow answers via dual encoding.

**Tags:** #developer #code #dualencoder  
**Dataset Ideas:** StackOverflow pairs  
**Model Ideas:** CodeBERT + TextBERT  
**Extensions:** Hybrid code + title+body encoders

---

## 7. FAQ → Customer Query Matching
**Question:**  
User query: *“Can I return a used blender?”*  
FAQ entry: *“Returns are accepted for used appliances within 30 days.”*  
Train a dual encoder to match customer queries to FAQs.

**Tags:** #support #faq #retrieval  
**Dataset Ideas:** Zendesk, open FAQs  
**Model Ideas:** SBERT  
**Extensions:** Response reranking, cluster-aware encoding

---

## 8. User Profile → Content Recommendation
**Question:**  
Match user embedding (interests, actions) with candidate content (e.g., articles, courses).

**Tags:** #recommendation #useritem #embedding  
**Dataset Ideas:** MovieLens, Coursera logs  
**Model Ideas:** Deep structured semantic models (DSSM), BERT  
**Extensions:** Time-aware encoders, personalization fine-tuning

---

## 9. Scientific Query → Method Section Matching
**Question:**  
Query: *"unsupervised pretraining for computer vision"*  
Method section: *“We use SimCLR for contrastive pretraining without labels…”*  
Build a dual encoder to match queries to relevant method snippets.

**Tags:** #papers #methodsearch #dualencoder  
**Dataset Ideas:** arXiv, S2ORC  
**Model Ideas:** SciBERT dual encoder  
**Extensions:** Paragraph-level pooling, citation reranking

---

## 10. Definition → Term Matching (Glossary Alignment)
**Question:**  
Given a definition: *“A type of neural network that uses attention mechanisms”*  
Match to: *“Transformer”*

**Tags:** #education #glossary #matching  
**Dataset Ideas:** Wiktionary, ConceptNet, education glossaries  
**Model Ideas:** BERT dual encoder with contrastive loss  
**Extensions:** Curriculum-aware filtering

---

## 🛠 Architecture Overview


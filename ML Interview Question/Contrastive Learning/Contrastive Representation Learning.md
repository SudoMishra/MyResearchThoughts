# 🧲 Contrastive Learning - Problem Bank

Use-case-style problems where models are trained to learn representations by bringing **similar examples closer** and **dissimilar ones apart** in embedding space. Contrastive learning is foundational to many self-supervised and few-shot learning tasks.

Each entry includes:
- **Objective**
- **Tags**
- **Positive / Negative Pair Ideas**
- **Downstream Tasks**
- **Extensions**

---

## 1. Sentence Similarity Embedding
**Objective:**  
Learn sentence embeddings where semantically similar sentences are close in vector space.

**Tags:** #nlp #sentenceembedding #contrastive  
**Positive Pairs:** Paraphrases (Quora, PAWS)  
**Negative Pairs:** In-batch negatives or random sentences  
**Downstream Tasks:** STS-B, FAQ matching, clustering  
**Extensions:** Use hard negatives via backtranslation

---

## 2. Resume Bullet Alignment via Contrastive Learning
**Objective:**  
Train an encoder where resume bullet points with similar functions (e.g., leadership, data analysis) are close.

**Tags:** #resume #skills #contrastive  
**Positive Pairs:** Bullets from same job function  
**Negative Pairs:** Bullets from unrelated fields  
**Downstream Tasks:** Skill classification, section segmentation  
**Extensions:** Add hierarchical labels (function → skill → tool)

---

## 3. Visual Similarity with Augmented Views
**Objective:**  
Learn robust visual features by making augmented versions of the same image close in embedding space.

**Tags:** #vision #selfsupervised #contrastive  
**Positive Pairs:** Two augmented crops of same image  
**Negative Pairs:** Other images in batch (SimCLR)  
**Downstream Tasks:** Classification, retrieval  
**Extensions:** Local patch-level contrast (DINO, SwAV)

---

## 4. Multimodal Image-Text Embedding
**Objective:**  
Align images and captions in a shared embedding space.

**Tags:** #multimodal #contrastive #retrieval  
**Positive Pairs:** Image + matching caption  
**Negative Pairs:** Other images/captions in batch  
**Downstream Tasks:** Image-to-text retrieval, zero-shot classification  
**Extensions:** Add object detection supervision

---

## 5. Graph Node Representation Contrast
**Objective:**  
Learn node embeddings by contrasting a node with positive/negative neighborhoods.

**Tags:** #graph #gnn #contrastive  
**Positive Pairs:** Node and augmented subgraph  
**Negative Pairs:** Node and subgraphs from other nodes  
**Downstream Tasks:** Node classification, link prediction  
**Extensions:** Use multiple graph views (GCA, GRACE)

---

## 6. Dialogue Response Contrastive Pretraining
**Objective:**  
Pretrain embeddings of dialogue utterances where responses to the same context are close.

**Tags:** #dialogue #nlp #contrastive  
**Positive Pairs:** Dialogue context-response pairs  
**Negative Pairs:** Random context-response mismatches  
**Downstream Tasks:** Response ranking, chatbot grounding  
**Extensions:** Add speaker role contrast (agent vs user)

---

## 7. Cross-Lingual Sentence Alignment
**Objective:**  
Learn embeddings where translated sentence pairs from different languages are close.

**Tags:** #multilingual #nlp #contrastive  
**Positive Pairs:** Translations (e.g., EN–FR)  
**Negative Pairs:** Random cross-language pairs  
**Downstream Tasks:** Cross-lingual retrieval, transfer learning  
**Extensions:** Align embeddings across 10+ languages

---

## 8. Code and Comment Embedding
**Objective:**  
Align code snippets with their corresponding docstrings or comments.

**Tags:** #code #nlp #contrastive  
**Positive Pairs:** Function code ↔ docstring  
**Negative Pairs:** Code and unrelated docstrings  
**Downstream Tasks:** Code search, documentation generation  
**Extensions:** Contrast API signature + body + comment

---

## 9. Audio Segment Contrast
**Objective:**  
Train on raw audio to create embeddings that are invariant to noise and time shifts.

**Tags:** #audio #speech #contrastive  
**Positive Pairs:** Augmented views of same audio (volume, tempo)  
**Negative Pairs:** Different utterances  
**Downstream Tasks:** Speaker ID, intent recognition  
**Extensions:** Learn multilingual acoustic embeddings

---

## 10. Skill Graph Embedding with Relation Contrast
**Objective:**  
Learn embeddings for skills such that relational edges (e.g., `used_with`, `subset_of`) guide similarity.

**Tags:** #skills #graph #contrastive  
**Positive Pairs:** Skills connected by `used_with` or `subset_of`  
**Negative Pairs:** Distant or unrelated skills  
**Downstream Tasks:** Skill suggestion, career path planning  
**Extensions:** Combine graph walk contrast + taxonomy hierarchy

---

## 🧠 Contrastive Learning Strategies

| Strategy           | Key Idea                                      |
|--------------------|-----------------------------------------------|
| In-Batch Contrast  | Use other examples in batch as negatives      |
| Hard Negative Mining | Select near-positives to increase difficulty |
| Data Augmentation  | Generate positive views via transforms        |
| Multi-view Learning| Contrast multiple semantic views              |
| Momentum Encoders  | Use momentum networks (MoCo, BYOL)            |

---

## ⚙️ Tools & Frameworks

- [SimCLR](https://github.com/google-research/simclr) (Vision)
- [SimCSE](https://github.com/princeton-nlp/SimCSE) (NLP)
- [SBERT](https://www.sbert.net/)
- [DGL / PyTorch Geometric] – for GraphCL
- [CLIP](https://openai.com/research/clip) – vision + language
- [HuggingFace Transformers] – contrastive loss customization

---

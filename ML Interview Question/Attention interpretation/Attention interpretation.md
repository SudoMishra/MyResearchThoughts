# 🎯 Attention Interpretation - Problem Bank

These use-case style problems focus on **interpreting, analyzing, and leveraging attention** in transformer-based models. Goals include improving interpretability, trust, performance, and error analysis.

Each problem includes:
- **Objective**
- **Tags**
- **Dataset Ideas**
- **Model Ideas**
- **Advanced Extensions**

---

## 1. Attention Highlighting for Sentiment
**Objective:**  
Given a sentence and its predicted sentiment, visualize which words the model attended to most when making the prediction.

**Example:**  
*"I love the screen but hate the battery life."*  
Model output:  
- `screen` → attention to "love"  
- `battery life` → attention to "hate"

**Tags:** #attention #sentiment #visualization  
**Dataset Ideas:** SemEval ABSA, IMDb  
**Model Ideas:** BERT + attention heatmaps  
**Extensions:** Token importance via gradient × attention

---

## 2. Attention-Based Error Diagnosis
**Objective:**  
Analyze attention weights in misclassified examples to detect spurious correlations or irrelevant focus.

**Example:**  
Model predicts "positive" sentiment for:  
*"The packaging was nice but the product broke in a day."*  
Attention focuses on "packaging" instead of "broke".

**Tags:** #debugging #attention #QA  
**Dataset Ideas:** SST-2, custom error buckets  
**Model Ideas:** BERT + attention rollout  
**Extensions:** Identify harmful heads or bias propagation

---

## 3. Multi-hop Reasoning Visualization
**Objective:**  
In multi-hop QA, visualize attention flow across hops to ensure the model is reasoning over multiple facts.

**Example:**  
Q: *"Where was the president of the company founded in Helsinki educated?"*  
Attention should first flow to “company → Helsinki” then to “president → education”.

**Tags:** #multihop #reasoning #attention  
**Dataset Ideas:** HotpotQA  
**Model Ideas:** Longformer, DeBERTa  
**Extensions:** Attention rollout graphs

---

## 4. Coreference-Aware Attention
**Objective:**  
Analyze how attention shifts between pronouns and antecedents in coreference chains.

**Example:**  
*"Sarah gave her dog a bath because she was dirty."*  
Should attend correctly from "she" to "dog".

**Tags:** #coreference #attention #interpretability  
**Dataset Ideas:** OntoNotes, GAP  
**Model Ideas:** BERT, SpanBERT  
**Extensions:** Visualize attention over mentions and entities

---

## 5. Causal vs Correlational Attention Heads
**Objective:**  
Identify heads that capture meaningful (causal) relationships vs those that latch onto surface forms.

**Example:**  
*"Inflation increased because oil prices surged."*  
Model should attend "inflation → oil prices".

**Tags:** #causality #attention #analysis  
**Dataset Ideas:** EventCausality, COPA  
**Model Ideas:** DeBERTa, GPT attention maps  
**Extensions:** Attention probing with causal masking

---

## 6. Attention for Named Entity Boundaries
**Objective:**  
Use attention visualization to understand how entity boundaries are learned.

**Example:**  
In: *“Barack Obama was born in Hawaii.”*  
Attention on "Obama" should extend to "Barack" in early layers.

**Tags:** #NER #attention #boundary  
**Dataset Ideas:** CoNLL-2003  
**Model Ideas:** BERT-CRF  
**Extensions:** Visualize head-specific boundary capture

---

## 7. Cross-Attention in Question Answering
**Objective:**  
In a QA model (e.g., T5), visualize cross-attention from decoder to encoder tokens to understand how answers are generated.

**Example:**  
Q: *"What is the capital of France?"*  
Decoder tokens "Paris" should attend to "capital" and "France".

**Tags:** #seq2seq #crossattention #QA  
**Dataset Ideas:** SQuAD, NaturalQuestions  
**Model Ideas:** T5, BART  
**Extensions:** Show token-to-token attention trajectory

---

## 8. Self-Attention Head Specialization
**Objective:**  
Detect if different heads specialize in different syntactic or semantic roles (e.g., subject, object, sentiment carrier).

**Tags:** #interpretability #headanalysis #attention  
**Dataset Ideas:** GLUE, syntactic treebanks  
**Model Ideas:** BERT  
**Extensions:** Use probing tasks per head

---

## 9. Attention Drift Over Layers
**Objective:**  
Track how attention to key tokens evolves across layers.

**Example:**  
In sentence classification, does early attention focus on syntax and later on semantics?

**Tags:** #layerwise #attentionflow  
**Dataset Ideas:** SST-2, MNLI  
**Model Ideas:** BERT, XLNet  
**Extensions:** Layer-head importance heatmaps

---

## 10. Attention-Based Token Importance for Explainability
**Objective:**  
Generate rationales by using high-attention tokens as justifications.

**Example:**  
*"The display is gorgeous but the touchpad is unresponsive."*  
Output:
- Positive rationale: "display", "gorgeous"
- Negative rationale: "touchpad", "unresponsive"

**Tags:** #explainability #rationale #attention  
**Dataset Ideas:** ERASER, Movie Reviews  
**Model Ideas:** Attention + LIME, SHAP  
**Extensions:** Faithfulness scoring for generated rationales

---

## 🔬 Tools for Visualization & Interpretation

- [BertViz](https://github.com/jessevig/bertviz)
- [exBERT](https://exbert.net/)
- [Captum (PyTorch)](https://captum.ai/)
- [Ecco (AllenNLP)](https://github.com/allenai/ecco)

---

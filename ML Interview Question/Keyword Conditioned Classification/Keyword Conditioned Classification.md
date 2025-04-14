
A curated collection of realistic, use-case style ML problems. Great for interview prep, case studies, or prototype thinking.

## ✅ Problem Format
Each problem follows:

- **Title**
- **Question**
- **Tags**: #classification #NLP #graph #retrieval etc.
- **Dataset Ideas**
- **Baseline Ideas**
- **Advanced Extensions**

---

## 1. Document-Aspect Sentiment Analysis
**Question:**  
"The battery lasts long and the display is crisp, but the phone heats up very quickly."  
Given aspects like `battery`, `display`, `heating`, build a model that predicts the sentiment toward each.

**Tags:** #NLP #sentiment #aspectbased #classification  
**Dataset Ideas:** SemEval 2014 Task 4  
**Baseline Ideas:** BERT + sentence-pair format, ATAE-LSTM  
**Advanced Extensions:** Multi-aspect attention, contrastive ABSA

---

## 2. User-Query Intent Disambiguation
**Question:**  
"How do I cancel my premium account and still keep playlists?"  
Classify intent into: `account management`, `payment`, `feature retention`.

**Tags:** #intent #NLU #classification  
**Dataset Ideas:** SNIPS, CLINC150  
**Baseline Ideas:** BiLSTM + softmax, intent classification with BERT  
**Advanced Extensions:** Multi-intent prediction, dialogue state tracking

---

## 3. Resume Skill Normalization
**Question:**  
"Skilled in PyTorch, TensorFlow, and building ML pipelines with Airflow."  
Extract and normalize skills to a taxonomy (e.g., `PyTorch → deep_learning_framework`).

**Tags:** #informationextraction #ontology #skills  
**Dataset Ideas:** StackOverflow tags, O*NET  
**Baseline Ideas:** spaCy NER, BERT + skill span classifier  
**Advanced Extensions:** Skill embeddings, soft skill clustering, synonym mapping

---

## 4. News Claim Stance Detection
**Question:**  
Headline: “Electric cars increase carbon footprint.”  
Body: “Battery production is improving, net emissions are down.”  
Predict stance: `supports`, `refutes`, `neutral`.

**Tags:** #stance #nli #NLP #classification  
**Dataset Ideas:** FNC-1, LIAR dataset  
**Baseline Ideas:** Sentence-pair classification with BERT  
**Advanced Extensions:** Long-context modeling with Longformer

---

## 5. Product Comparison Summarizer
**Question:**  
"While Kindle has a better screen, Kobo wins on battery life."  
Extract: `screen → Kindle > Kobo`, `battery → Kobo > Kindle`.

**Tags:** #comparison #relationextraction #NLP  
**Dataset Ideas:** Amazon reviews  
**Baseline Ideas:** Dependency parsing + rules, BERT + relation classifier  
**Advanced Extensions:** Graph construction, contrastive ranking

---

## 6. Query-to-Table Cell Matching
**Question:**  
"How many medals did India win in Tokyo 2020?"  
Given a table, return relevant cell(s) with the answer.

**Tags:** #retrieval #QA #tabular  
**Dataset Ideas:** WikiTableQuestions, TabFact  
**Baseline Ideas:** TableBERT, TAPAS  
**Advanced Extensions:** SQL generation, multi-modal retrieval

---

## 7. Email Response Prioritization
**Question:**  
“Our system has been down for 6 hours, and we can’t access orders.”  
Assign **urgency level** and suggest **response type**.

**Tags:** #classification #businessautomation #zeroshot  
**Dataset Ideas:** Helpdesk ticket datasets, Enron emails  
**Baseline Ideas:** FastText, BERT + classifier  
**Advanced Extensions:** Multi-label prediction, retrieval-augmented responses

---

## 8. Multi-turn Dialogue Task Classification
**Question:**  
> U: I’m not able to log in.  
> A: Can I get your email?  
> U: It’s john@gmail.com  
Classify task as: `login issue`, `account recovery`, etc.

**Tags:** #dialogue #multi-turn #classification  
**Dataset Ideas:** MultiWOZ, DSTC  
**Baseline Ideas:** BERT + RNN context encoder  
**Advanced Extensions:** Intent flow modeling, transformer over turns

---

## 9. Temporal Sentiment Tracking
**Question:**  
> Jan: "Growth in Q4 has been exceptional."  
> Mar: "We expect headwinds due to inflation."  
Track **sentiment trends over time** per company.

**Tags:** #timeseries #nlp #finance  
**Dataset Ideas:** Earnings call transcripts  
**Baseline Ideas:** BERT + time binning  
**Advanced Extensions:** Temporal GNNs, memory-based models

---

## 10. Point-of-View Modeling
**Question:**  
> “Sarah cried as she watched the dog run away. Her brother didn't seem to care.”  
Extract emotion events and assign to correct speaker.

**Tags:** #emotion #coreference #characterattribution  
**Dataset Ideas:** ROCStories, Empathetic Dialogues  
**Baseline Ideas:** Coref + rule-based attribution  
**Advanced Extensions:** Character graph modeling, narrative transformers

---

Let me know if you'd like the remaining 5–10 added to this or if you'd like this in a ZIP/Obsidian vault format!

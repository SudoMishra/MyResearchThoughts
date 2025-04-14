# 🧠 Multi-Task Learning (MTL) - Problem Bank

Use-case-style problem statements where **multiple related tasks are solved simultaneously** by a single model or shared representation. MTL enables better generalization, efficiency, and leveraging task synergies.

Each entry includes:
- **Objective**
- **Tags**
- **Dataset Ideas**
- **Model Ideas**
- **Advanced Extensions**

---

## 1. Joint Named Entity Recognition + Part-of-Speech Tagging
**Objective:**  
Given a sentence, predict both:
- POS tags (e.g., noun, verb)
- Named entities (e.g., PERSON, ORG)

**Tags:** #ner #pos #multitask  
**Dataset Ideas:** OntoNotes, CoNLL-2003  
**Model Ideas:** Shared BiLSTM/Transformer + two heads  
**Extensions:** Add dependency parsing as a third task

---

## 2. Emotion + Sentiment Classification
**Objective:**  
For social media text, jointly predict:
- Emotion (anger, joy, sadness, etc.)
- Sentiment (positive, negative, neutral)

**Tags:** #emotion #sentiment #multitask  
**Dataset Ideas:** GoEmotions, SemEval  
**Model Ideas:** BERT with multi-head classifiers  
**Extensions:** Multi-label emotion + intensity regression

---

## 3. Question Answering + Question Type Classification
**Objective:**  
For each QA pair:
- Classify the question type (factual, yes/no, procedural)
- Extract the answer span from the context

**Tags:** #QA #classification #spanextraction  
**Dataset Ideas:** SQuAD, NaturalQuestions  
**Model Ideas:** BERT with shared encoder  
**Extensions:** Add difficulty or confidence calibration as third task

---

## 4. Joint Intent Detection + Slot Filling
**Objective:**  
In a user utterance like:  
*"Book a flight to Tokyo tomorrow morning"*  
Predict:
- Intent: `book_flight`
- Slots: `location=Tokyo`, `date=tomorrow morning`

**Tags:** #nlu #dialogue #multitask  
**Dataset Ideas:** SNIPS, ATIS  
**Model Ideas:** Joint BERT tagging + classification  
**Extensions:** Add response generation or entity linking

---

## 5. Visual Question Answering + Visual Grounding
**Objective:**  
Given an image and question:
- Predict the answer
- Highlight the image region supporting the answer

**Tags:** #vqa #visionlanguage #multitask  
**Dataset Ideas:** GQA, VQA v2  
**Model Ideas:** ViLT, LXMERT with dual heads  
**Extensions:** Add reasoning type classification

---

## 6. Resume Parsing: Section Classification + Skill Extraction
**Objective:**  
For a resume:
- Label each section (e.g., experience, education)
- Extract skills mentioned within each section

**Tags:** #resume #extraction #multitask  
**Dataset Ideas:** Custom HR datasets  
**Model Ideas:** Shared transformer with span + token heads  
**Extensions:** Add career trajectory prediction

---

## 7. Fake News Detection + Factuality Scoring
**Objective:**  
Given a news article:
- Classify it as fake/real
- Score factual consistency with known claims (0–1)

**Tags:** #fakenews #factchecking #multitask  
**Dataset Ideas:** LIAR, FAKENEWSNET  
**Model Ideas:** BERT + regression + classification heads  
**Extensions:** Add claim extraction as a subtask

---

## 8. Translation + Named Entity Tagging
**Objective:**  
Translate a sentence from French to English while tagging named entities in the source sentence.

**Tags:** #translation #ner #multitask  
**Dataset Ideas:** WikiANN, WMT  
**Model Ideas:** mBART or mT5 with dual heads  
**Extensions:** Add word alignment supervision

---

## 9. Scene Understanding: Captioning + Object Detection
**Objective:**  
For a given image:
- Generate a natural language caption
- Detect bounding boxes for objects

**Tags:** #multimodal #captioning #detection  
**Dataset Ideas:** MS-COCO  
**Model Ideas:** Shared visual backbone (e.g., ResNet) + captioning and detection heads  
**Extensions:** Add object counting or segmentation

---

## 10. Speech: Speaker ID + Emotion Recognition
**Objective:**  
For each audio clip:
- Identify the speaker
- Predict emotional state

**Tags:** #speech #audio #multitask  
**Dataset Ideas:** IEMOCAP, VoxCeleb  
**Model Ideas:** Wav2Vec2 + multi-head classification  
**Extensions:** Add transcript generation (ASR) as third task

---

## 🧠 MTL Architecture Pattern


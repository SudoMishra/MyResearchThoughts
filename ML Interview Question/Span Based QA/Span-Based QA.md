
These are use-case style problems for training and evaluating models that extract answer spans from input contexts. Designed for interview prep, case work, and model experimentation.

Each entry includes:
- **Question**
- **Context**
- **Expected Answer Span**
- **Tags**: #QA #spanbased #NLP
- **Dataset Ideas**
- **Model Ideas**
- **Advanced Extensions**

---

## 1. Customer Support FAQ Matching
**Question:**  
"What is the return window for electronics?"  
**Context:**  
> "You can return electronics within 15 days of delivery, provided they are unused and in original packaging."  
**Answer:**  
`15 days of delivery`

**Tags:** #QA #ecommerce #spanbased  
**Dataset Ideas:** Amazon QA, eBay Help Pages  
**Model Ideas:** BERT QA, DistilBERT  
**Advanced Extensions:** Retrieval + QA over large docs

---

## 2. Legal Document Clause Finder
**Question:**  
"What is the minimum severance period under this agreement?"  
**Context:**  
> "In the event of termination, the company shall provide a severance notice period of no less than 45 days."  
**Answer:**  
`no less than 45 days`

**Tags:** #legal #contract #spanbased  
**Dataset Ideas:** CUAD, LexGLUE  
**Model Ideas:** LegalBERT, Longformer QA  
**Advanced Extensions:** Multi-span QA, clause ranking

---

## 3. Academic Paper QA (Literature Reading)
**Question:**  
"What optimizer was used in the experiments?"  
**Context:**  
> "We trained all models for 50 epochs using the Adam optimizer with an initial learning rate of 1e-4."  
**Answer:**  
`Adam optimizer`

**Tags:** #academic #spanbased #MLpapers  
**Dataset Ideas:** SciQ, PaperQA (custom)  
**Model Ideas:** SciBERT, BioBERT  
**Advanced Extensions:** Entity linking + QA

---

## 4. Movie Plot QA
**Question:**  
"Who saves Frodo in the end?"  
**Context:**  
> "After a long journey, Frodo is rescued by the eagles that arrive just in time."  
**Answer:**  
`the eagles`

**Tags:** #entertainment #qa #spanbased  
**Dataset Ideas:** MovieQA, NarrativeQA  
**Model Ideas:** BERT QA, GPT + span pointer  
**Advanced Extensions:** Coreference-aware QA

---

## 5. Financial Report Span Retrieval
**Question:**  
"What was the YoY revenue growth in Q2?"  
**Context:**  
> "The company reported a year-over-year revenue growth of 18% for the second quarter."  
**Answer:**  
`18%`

**Tags:** #finance #spanbased #qa  
**Dataset Ideas:** Earnings call transcripts  
**Model Ideas:** FinBERT, TAPAS  
**Advanced Extensions:** Table + text hybrid QA

---

## 6. Medical QA - Diagnosis
**Question:**  
"What symptoms did the patient report?"  
**Context:**  
> "The patient complained of fatigue, dizziness, and shortness of breath during exercise."  
**Answer:**  
`fatigue, dizziness, and shortness of breath`

**Tags:** #medical #clinical #spanbased  
**Dataset Ideas:** emrQA, MIMIC notes  
**Model Ideas:** ClinicalBERT  
**Advanced Extensions:** Entity linking + symptom QA

---

## 7. Resume Extraction QA
**Question:**  
"What tools does the candidate mention?"  
**Context:**  
> "Experienced in using Apache Spark, Airflow, and MLflow for building scalable pipelines."  
**Answer:**  
`Apache Spark, Airflow, and MLflow`

**Tags:** #resumes #HRtech #spanbased  
**Dataset Ideas:** Annotated resumes  
**Model Ideas:** BERT + QA head  
**Advanced Extensions:** Skill normalization

---

## 8. Cooking Recipe QA
**Question:**  
"What temperature should the oven be preheated to?"  
**Context:**  
> "Preheat the oven to 375°F before placing the tray inside."  
**Answer:**  
`375°F`

**Tags:** #spanbased #recipes #qa  
**Dataset Ideas:** RecipeQA  
**Model Ideas:** RoBERTa QA  
**Advanced Extensions:** Reasoning across steps

---

## 9. Policy Document QA
**Question:**  
"What is the cancellation fee?"  
**Context:**  
> "Cancellations made within 24 hours of the booking will incur a fee of $25."  
**Answer:**  
`$25`

**Tags:** #policy #travel #spanbased  
**Dataset Ideas:** Travel FAQs, internal policies  
**Model Ideas:** DistilBERT  
**Advanced Extensions:** Multi-span (conditions + value)

---

## 10. Scientific Fact QA
**Question:**  
"What is the boiling point of mercury?"  
**Context:**  
> "Mercury is a heavy metal with a boiling point of 356.7°C under standard pressure."  
**Answer:**  
`356.7°C`

**Tags:** #science #spanbased #qa  
**Dataset Ideas:** NaturalQuestions, SciQ  
**Model Ideas:** BERT, T5 QA  
**Advanced Extensions:** Unit normalization + QA

---

Would you like me to create an Obsidian vault with backlinks and templates for adding new problems? Or generate 10 more in this format?

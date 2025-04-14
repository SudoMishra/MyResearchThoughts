# 🔁 Continual Learning - Problem Bank

Use-case-driven problems where a model learns **sequentially** from a stream of tasks or domains. The goal is to retain previously learned knowledge while adapting to new data — avoiding **catastrophic forgetting**.

Each entry includes:
- **Objective**
- **Tags**
- **Dataset Ideas**
- **Model Ideas**
- **Advanced Extensions**

---

## 1. Language Model Adaptation Across Domains
**Objective:**  
Train a language model sequentially on:
- Scientific papers → Legal documents → News articles  
Ensure it retains earlier domain knowledge while adapting to new terminology.

**Tags:** #nlp #languagemodel #continuallearning  
**Dataset Ideas:** arXiv, Law360, Reuters  
**Model Ideas:** Adapter tuning, Elastic Weight Consolidation (EWC)  
**Extensions:** Add domain prediction or continual vocabulary adaptation

---

## 2. Visual Object Classification Across Tasks
**Objective:**  
Learn object classes in task order:  
`Task 1: cats & dogs`, `Task 2: cars & bikes`, `Task 3: birds & planes`  
Maintain accuracy on all tasks as new ones are introduced.

**Tags:** #cv #imageclassification #taskincremental  
**Dataset Ideas:** Split CIFAR-100, Split ImageNet  
**Model Ideas:** iCaRL, DER++, LwF  
**Extensions:** Use rehearsal-free CL

---

## 3. Incremental Skill Extraction from Resumes
**Objective:**  
First train a model to extract programming languages from resumes.  
Later train it on frameworks (e.g., TensorFlow, React), then soft skills.  
Avoid forgetting earlier skill categories.

**Tags:** #nlp #resume #entityextraction #continual  
**Dataset Ideas:** Resume datasets (custom or O*NET)  
**Model Ideas:** Memory-based BERT, AdapterFusion  
**Extensions:** Add task identity prediction as auxiliary output

---

## 4. Continual Emotion Recognition in Conversations
**Objective:**  
Train on emotion recognition across multiple datasets or demographics in sequence (e.g., IEMOCAP → MELD → DailyDialog).  
Retain performance across styles and domains.

**Tags:** #emotion #conversation #lifelong  
**Dataset Ideas:** IEMOCAP, MELD, DailyDialog  
**Model Ideas:** ContinualBERT, GEM++  
**Extensions:** Use task-specific adapters or meta-learning

---

## 5. Robotic Perception Across Environments
**Objective:**  
A vision model for a robot is trained first in lab environment, then a home, then outdoors.  
Maintain accuracy on earlier environments.

**Tags:** #robotics #continual #cv  
**Dataset Ideas:** RoboNet, Habitat datasets  
**Model Ideas:** Online rehearsal, dynamic memory networks  
**Extensions:** Domain-aware feature normalization

---

## 6. Continual Question Answering
**Objective:**  
Train a QA system on:
- Task 1: History questions  
- Task 2: Science questions  
- Task 3: Current events  
Without losing accuracy on prior topics.

**Tags:** #QA #lifelonglearning  
**Dataset Ideas:** TriviaQA, SciQ, NewsQA  
**Model Ideas:** Progressive Neural Networks, Memory Aware Synapses (MAS)  
**Extensions:** Use span retention scoring

---

## 7. Personalized Language Modeling
**Objective:**  
Fine-tune a language model for individual users in sequence (e.g., User A → B → C).  
Preserve prior personalization without storing their data.

**Tags:** #personalization #nlp #privacy #continual  
**Dataset Ideas:** Reddit per-user corpora, PersonaChat  
**Model Ideas:** FedCL (Federated CL), Prototypical memory networks  
**Extensions:** Add privacy-preserving constraints

---

## 8. Continual Toxicity Classification in Evolving Language
**Objective:**  
Train a toxicity classifier across different years of social media data as slang and hate terms evolve.  
Retain effectiveness on past and emerging terms.

**Tags:** #toxiclanguage #temporalshift #continual  
**Dataset Ideas:** Civil Comments, Reddit  
**Model Ideas:** Dynamic vocabulary adapters, BERT + replay  
**Extensions:** Few-shot adaptation to new slurs

---

## 9. Lifelong Recommendation Systems
**Objective:**  
A recommender system learns from user feedback over months, continuously updating preferences without forgetting prior signals.

**Tags:** #recommendation #continual #useradaptation  
**Dataset Ideas:** MovieLens temporal, streaming logs  
**Model Ideas:** Online meta-learning, Reservoir Sampling + fine-tuning  
**Extensions:** Catastrophic forgetting mitigation via user prototypes

---

## 10. Continual Multilingual Learning
**Objective:**  
Train a model on English → German → French → Swahili in sequence.  
Avoid forgetting English while learning new languages.

**Tags:** #multilingual #translation #continual  
**Dataset Ideas:** Tatoeba, FLORES  
**Model Ideas:** mBERT + language adapters, continual T5  
**Extensions:** Add task-free continual learning setup

---

## 🧠 Continual Learning Setup Types

- **Task-incremental**: Task identity known
- **Class-incremental**: New classes added over time
- **Domain-incremental**: Same task, new distribution
- **Task-free**: No explicit task boundaries

---

## 📦 Continual Learning Strategies

| Strategy           | Example Methods                  |
|--------------------|----------------------------------|
| Regularization     | EWC, MAS, SI                     |
| Rehearsal          | iCaRL, Experience Replay         |
| Dynamic Expansion  | ProgNN, Dynamically Expandable NN|
| Memory-based       | GEM, A-GEM                       |
| Adapter-based      | AdapterFusion, CL AdapterHub     |
| Replay-free        | DER++, LUCIR                     |

---

## 🛠 Libraries & Tools

- [Avalanche](https://avalanche.continualai.org/)
- [ContinualAI](https://www.continualai.org/)
- [Sequoia](https://github.com/lebrice/Sequoia)
- HuggingFace AdapterHub


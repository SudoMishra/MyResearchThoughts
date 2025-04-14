# 🧠 Graph-Based Inference - Problem Bank

These problems involve using **graph structures for inference**, classification, recommendation, clustering, reasoning or [[Graph Embedding]] creation. Nodes may represent entities (e.g., users, skills, proteins) and edges represent relations (semantic, temporal, co-occurrence, etc.).

Each task includes:
- **Objective**
- **Tags**
- **Dataset Ideas**
- **Model Ideas**
- **Advanced Extensions**

---

## 1. Skill Recommendation via Knowledge Graph
**Objective:**  
Given a knowledge graph of skills with edges like `used_with`, `required_for`, `subset_of`, predict the next most relevant skill to recommend to a learner.

**Tags:** #skills #recommendation #graph  
**Dataset Ideas:** O*NET, ESCO, SkillKG  
**Model Ideas:** GraphSAGE, R-GCN  
**Extensions:** Use temporal signals or skill levels

---

## 2. Fraud Detection in Financial Networks
**Objective:**  
Given a graph of transactions (nodes: accounts; edges: transfers), predict if a node is involved in fraudulent activity.

**Tags:** #fraud #graph #classification  
**Dataset Ideas:** Elliptic Dataset, AMLSim  
**Model Ideas:** GCN, Graph Attention Networks (GAT)  
**Extensions:** Heterogeneous graphs (users + merchants + IPs)

---

## 3. Drug-Drug Interaction Prediction
**Objective:**  
Given a biomedical knowledge graph with drugs, proteins, and diseases as nodes, predict if two drugs interact adversely.

**Tags:** #biomedical #linkprediction #graph  
**Dataset Ideas:** BioKG, DrugBank  
**Model Ideas:** ComplEx, RotatE, R-GCN  
**Extensions:** Add textual node features + multi-modal fusion

---

## 4. Document Entity Relationship Prediction
**Objective:**  
Given a document converted into a graph of entities (people, places, events), predict semantic links like `works_at`, `located_in`.

**Tags:** #IE #entitygraph #inference  
**Dataset Ideas:** DocRED, TACRED  
**Model Ideas:** Relational GNNs, HeteroGNN  
**Extensions:** Use document layout (DocGNN), coreference links

---

## 5. Community Detection in Social Networks
**Objective:**  
Given a user-user interaction graph, detect latent communities based on message frequency and topics of discussion.

**Tags:** #socialgraph #communitydetection  
**Dataset Ideas:** Reddit graphs, Twitter followers  
**Model Ideas:** Louvain algorithm, DeepWalk + clustering  
**Extensions:** Dynamic community detection (time-evolving)

---

## 6. Question Answering over Knowledge Graph
**Objective:**  
Answer questions like *“What movies has Christopher Nolan directed after 2010?”* using a KG of movies, directors, and dates.

**Tags:** #QA #KGQA #graph  
**Dataset Ideas:** WebQuestionsSP, Freebase, WikiData  
**Model Ideas:** GraftNet, PullNet, STAGG  
**Extensions:** Natural language-to-subgraph mapping

---

## 7. Citation Influence Prediction
**Objective:**  
In a paper citation graph, predict which papers will become highly cited within 5 years based on structure and semantics.

**Tags:** #citation #temporalgraph #influence  
**Dataset Ideas:** OpenCitations, MAG  
**Model Ideas:** Temporal GNNs (TGAT, TGN)  
**Extensions:** Textual node attributes + co-authorship

---

## 8. Node Classification in Academic Graph
**Objective:**  
Given a graph of authors, papers, and venues, predict the topic category of an author (e.g., NLP, CV, Bioinformatics).

**Tags:** #classification #graph #academic  
**Dataset Ideas:** OGB-arxiv, AMiner  
**Model Ideas:** GraphSAGE, Heterogeneous GNN  
**Extensions:** Use publication sequences as temporal signals

---

## 9. Supply Chain Risk Inference
**Objective:**  
Given a supplier → product → manufacturer graph, predict disruptions due to natural disasters, delays, or failures.

**Tags:** #supplychain #risk #graphreasoning  
**Dataset Ideas:** Synthetic or enterprise data  
**Model Ideas:** GAT + message passing  
**Extensions:** Geo-temporal node features (weather, location)

---

## 10. Commonsense Reasoning on Concept Graphs
**Objective:**  
Given a graph like ConceptNet, infer missing edges like:
> *“knife → used_for → cutting”*

**Tags:** #commonsense #graphcompletion  
**Dataset Ideas:** ConceptNet, ATOMIC  
**Model Ideas:** TransE, ConvE, KG-BERT  
**Extensions:** Combine text with graph walk-based embeddings

---

## 🧠 Architecture Concepts


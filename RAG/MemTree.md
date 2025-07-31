
### MemTree — dynamic tree memory for LLMs (ICLR 2025 poster)

|||
|---|---|
|**Citation**|Rezazadeh, Li, Wei & Bao, “_From Isolated Conversations to Hierarchical Schemas: Dynamic Tree Memory Representation for LLMs_,” poster, ICLR 2025. ([OpenReview](https://openreview.net/forum?id=moXtEmCleY "From Isolated Conversations to Hierarchical Schemas: Dynamic Tree Memory Representation for LLMs \| OpenReview"))|
|**Status**|First pre-print Oct 2024, accepted Jan 2025; code promised but not yet released.|
|**Goal**|Give agentic LLMs a _schema-like_ external memory that grows online, stays logarithmic to update, and retrieves multi-granular context better than flat RAG or MemGPT.|

---

## 1 Core data structure

- **Dynamic M-ary tree** T = (V,E).  
    Each node _v_ stores the tuple ⟨**text summary c**ᵥ, **embedding e**ᵥ, **depth d**ᵥ, parent pᵥ, children C(v)⟩.
    
- **Similarity-gated insertion.**  
    New chunk → embed → start at root → at each level choose the child whose embedding-cosine > θ(d). θ grows exponentially with depth (θ₀ e^{λd}) so deeper nodes are “tighter”. If no child passes, open a new leaf. Insertion ≈ O(log N) if the thresholds keep the tree balanced.
    
- **Parent aggregation.**  
    After inserting, walk back up and ask an LLM to _re-summarise_ the parent’s content, conditioning on number of descendants to keep upper levels compact.
    
- **Collapsed-tree retrieval.**  
    At query-time flatten V, cosine-rank all nodes, discard scores < θᵣ, return top-k nodes (mixture of summaries and leaves) to the generator prompt. This bypasses step-wise traversal latency.
    

---

## 2 Results worth knowing

|Benchmark|Setting|Flat --> Best competing|**MemTree**|
|---|---|---|---|
|**MSC (15-turn dialogues)**|GPT-4o + query-only retrieval|MemGPT 70.4 / 68.6 MemoryStream 84.4 / 79.1|**84.8 / 79.9** accuracy / ROUGE-L|
|**MSC-E (200 turns)**|GPT-4o|Full-history 78.0|**82.5** (beats MemoryStream 80.7)|
|**MultiHop-RAG**|Inference / Comparison / Temporal Qs|MemoryStream overall 74.7|**79.4** (closes gap to offline RAPTOR 81.0)|

Take-aways:

- Tree wins once the context blows past a few hundred turns; naïve “just stuff GPT-4o” degrades fast.
    
- Biggest gains are on **comparison** (+9 pts) and **temporal** (+6 pts) queries—hierarchy seems to preserve relational structure.
    

Latency isn’t quantitatively reported, but authors note one extra OpenAI call for parent aggregation during updates and a single embed-cosine pass at retrieval (sub-second in their 30 k-node experiments).

---

## 3 Strengths

|✔|Why it matters|
|---|---|
|**Online + logarithmic insert**|Lets an always-on agent keep growing memory without clustering the whole corpus each night.|
|**Hierarchical abstraction**|Parent summaries compress old context; token cost for retrieval stays roughly constant.|
|**Schema emergence**|Visualisations show semantically coherent branches (e.g., “US politics” vs “Tech earnings”). Helps interpretability.|

---

## 4 Pain points / open questions

|✘|Consequence|Possible fix|
|---|---|---|
|_Summary drift_|Early-level mis-summary propagates down the tree, mis-routing future inserts and retrieval|Periodic offline re-summarisation with a larger model; child-voting checks|
|_Recency bias_|Insert path is chronological, so recent leaves dominate similar topics (seen in MSC-E)|Decay-weighted thresholds or rotate leaves into internal nodes after _m_ days|
|*Collapsed retrieval is O(|V|)*|
|_No skip-edges_|Query that should jump across sub-trees must rely on embedding alone|Your HNSW-with-summaries idea would add logarithmic shortcuts|

---

## 5 How it differs from prior memories

|System|Topology|Update cost|Retrieval strategy|Notes|
|---|---|---|---|---|
|**MemoryStream**|Append-only list|O(1)|Recency-+-salience score|Flat; no abstraction|
|**MemGPT**|Flat DB + LLM paging|O(1)|LLM decides what to read/write|Two-tier RAM/Disk metaphor|
|**HAT**|Perfect M-ary tree|O(depth)|LLM navigates step-wise|No ANN; latency per move|
|**MemTree**|_Dynamic_ M-ary, adaptive thresholds|**O(log N)**|One flattened similarity pass|Online, schema-like|

---

## 6 Implications for your HNSW-plus-summary proposal

MemTree confirms that **hierarchical summaries** beat flat vectors, _but_ it still linearly scans all nodes at retrieval and lacks long-range hops. Replacing the flat cosine pass with HNSW layers (each node already has an embedding) would:

1. Drop retrieval to O(log N) _and_
    
2. Give you cross-branch routing that trees alone miss.
    

Add lightweight hybrid scoring (α · vector + β · text Relevance) and you may push past RAPTOR even on comparison/temporal tasks. In short, MemTree supplies the **tree mechanics**; you supply the **graph geometry**.

---

### TL;DR

MemTree is the first _online_ hierarchical-memory system that stays logarithmic to update and demonstrably outperforms MemGPT/MemoryStream when dialogues hit hundreds of turns. Its main bottleneck is linear retrieval and susceptibility to summary drift—exactly the gaps an HNSW-style, vector-guided hierarchy could fill.
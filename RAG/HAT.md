### HAT in depth — _“Enhancing Long-Term Memory using Hierarchical Aggregate Tree for Retrieval-Augmented Generation”_ (Jun 2024, arXiv 2406.06124)

|||
|---|---|
|**Authors / venue**|A. Aadhithya, S. Kumar, K. P. Soman — Amrita School of AI. Released 10 Jun 2024.|
|**Motivation**|LLMs forget everything outside the fixed window; flat RAG wastes tokens and can still miss deep context. The authors want a memory structure that (i) gives _coarse-to-fine_ access, (ii) recompresses older dialogue, and (iii) lets an agent pick just enough detail to answer.|
|**Core contribution**|A _data structure_ — **Hierarchical Aggregate Tree (HAT)** — plus a simple traversal agent. Unlike MemGPT’s flat vector store, each internal node holds a **summary** of its children, so resolution increases as you descend.|

---

#### 1 Data structure mechanics

- **Topology:** Perfect M-ary tree, depth grows ⌈logₘ N⌉. Child index _i_ lives under parent ⌊i / M⌋, preserving chronological order horizontally (left → right) and abstraction vertically (root → leaves).
    
- **Aggregator A(·):** any function that maps the children’s texts to a _shorter_ text. In the paper they just call GPT-3.5 with a “summarise salient persona+facts” prompt and cache the result.
    
- **Update rule:** insert a new leaf ⇒ propagate `update_text()` up to the root so summaries stay consistent. Complexity: O(depth).
    

**Nice property:** “resolution retention” — newest turns are always present as raw leaves at the rightmost fringe; older ones bubble up as summaries, so the memory footprint grows sub-linearly.

---

#### 2 Query-time traversal = an MDP

They model navigation as an action set **A = {U,D,L,R,S,O,U}** (Up/Down/Left/Right/Reset/OK/Unclear). A GPT-4-style “memory agent” receives the current node’s text + the user query and chooses the next move until it emits **O** (context sufficient) or gives up.

> _Why an MDP?_ Because optimal traversal is a sequential decision problem with sparse reward: response quality after generation.

No RL training here — the agent is _prompted_, not learned. That keeps the system model-agnostic but inflates latency.

---

#### 3 Empirical evidence

Dataset: **Multi-Session-Chat** (five sessions per episode; ≈ 17 k episodes train+val).

|Metric|BFS|DFS|**GPTAgent (HAT)**|
|---|---|---|---|
|BLEU-1 / BLEU-2|0.652 / 0.532|0.624 / 0.501|**0.721 / 0.612**|
|DISTINCT-1 / DISTINCT-2|0.072 / 0.064|0.064 / 0.058|**0.092 / 0.084**|

Against baselines that feed **All context**, **Current-session only**, or **Gold memory**, the GPTAgent still tops BLEU and diversity while using fewer tokens.

Latency isn’t rigorously benchmarked, but authors note an extra few seconds per turn from repeated OpenAI calls. Memory blow-up is linear in #leaves; they flag this as future work.

---

#### 4 Strengths

- **Granular control ≈ log N tokens** — the agent can stop at a high-level summary if that suffices.
    
- **Model independence** — any LLM with function-calling can serve as both aggregator and navigator.
    
- **Deterministic updates** — summaries are cached; no drift unless children change.
    

#### 5 Weaknesses & open questions

|Issue|Consequence|Possible fix|
|---|---|---|
|_Summary drift_|Early-level error misroutes every future query.|Periodic re-summarisation with a stronger model; child “voting” checks.|
|_Traversal latency_|Multiple GPT calls → seconds per step.|Heuristic or Monte-Carlo tree search hinted by authors; could pre-train a lightweight policy net.|
|_Unbounded growth_|Leaves grow with conversation; tree eventually huge.|“Coupled-HAT” idea: parallel vector HAT for ANN + text HAT for summaries; prune with TTL.|
|_No vector skip-edges_|Search is Θ(depth) not log N across siblings.|Your proposal of HNSW overlay would add logarithmic long-range hops.|

---

#### 6 How it compares to **your HNSW+hierarchical-summary** concept

||HAT|Your idea|
|---|---|---|
|**Geometry**|Pure tree; only parent/child links.|HNSW graph with cross-layer _short-cuts_ for ANN search.|
|**Routing**|LLM hill-climbs via summaries.|First-layer ANN narrows to a region, then LLM drill-downs.|
|**Token budget**|Upper-bounded by tree depth.|Potentially _lower_: skip directly to deep nodes that score highly in vector space before reading summaries.|
|**Failure mode**|Wrong summary → wrong path.|Vector/summary hybrid could mitigate this (score = α vec + β text).|

In short, HAT shows the **value of embedding summaries into the structure itself**, but it stops one abstraction level short of your graph-plus-skip-edge vision. That leaves a clear systems angle for a paper: fuse HNSW’s _log-arithmic search cost_ with HAT-style summarisation and measure ∆tokens / ∆latency / ∆accuracy.

---

### 7 If you want to prototype

```bash
pip install networkx openai
# build a bare-bones HAT with M=4 and GPT aggregator
# then swap BFS with your HNSW-guided descent
```

_Start small_: 1 k chat turns, compare (i) flat RAG, (ii) vanilla HAT, (iii) HNSW-HAT fusion. Log prompt tokens and BLEU-1. If fusion wins by ≥10 % tokens at equal BLEU the idea is ready for a workshop submission.

---

**Bottom line:** HAT validates the hierarchical-summary thesis but leaves optimisation headroom. Grafting HNSW geometry and hybrid scoring on top is still unexplored territory — worth a focused, empirical paper.
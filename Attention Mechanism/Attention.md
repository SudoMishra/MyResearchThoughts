Below is an overview of several key “flavours” of attention mechanisms that have been proposed over the years. Note that the landscape is continually evolving, and many of these mechanisms build on the basic ideas of “vanilla” attention to improve efficiency, scalability, or model inductive biases. Here’s a list with brief descriptions:

1. **[[Vanilla Attention]]**  
   - **Description:** This is the classic form of attention (often called “dot-product” or “scaled dot-product” attention) introduced in early sequence-to-sequence models and later popularized in the Transformer architecture. It computes full pairwise interactions between all queries and keys.  
   - **Characteristics:** High expressivity but with quadratic time and memory complexity.

1. **[[Multi-Head Attention]]**  
   - **Description:** Rather than using a single attention operation, the input is projected into multiple “heads” which each perform attention in parallel. The outputs are then concatenated and combined.  
   - **Characteristics:** Allows the model to capture information from different representation subspaces, enriching the learned representations.

1. **[[Sparse Attention]]**  
   - **Description:** In sparse attention, the full attention matrix is replaced with one that is only computed over a subset of positions. The idea is to drop many of the pairwise computations by using a fixed or learned sparsity pattern.  
   - **Characteristics:** Reduces computational load and memory footprint, making it feasible to apply attention to longer sequences. Examples include variants like block-sparse or strided patterns.

1. **[[Local Attention]]**  
   - **Description:** A special case of sparse attention where each query attends only to a local window of keys (e.g., tokens near it in the sequence).  
   - **Characteristics:** Particularly useful in tasks where local context is most relevant, and it often forms the basis for more complex sparse patterns.

1. **[[Grouped Query Attention]]**  
   - **Description:** This mechanism groups similar queries together and shares some computations among them. Instead of computing independent attention scores for every single query, queries are clustered (or “grouped”) and a shared attention context is computed per group.  
   - **Characteristics:** This grouping can lead to computational savings, especially when many queries are similar or when redundancies exist in the input.

1. **[[Radix Attention]]**  
   - **Description:** Radix attention typically refers to approaches that introduce a hierarchical or multi-scale structure into the attention mechanism. For example, by grouping keys and queries into clusters at different “scales” or levels (akin to radix sorting or hierarchical clustering), the mechanism approximates full attention with reduced complexity.  
   - **Characteristics:** Aims to capture long-range dependencies while reducing the cost of computing all pairwise interactions.

1. **[[Ring Attention]]**  
   - **Description:** Ring attention is designed with distributed or parallel computation in mind. In settings where the model’s computation is spread over multiple devices or nodes, the attention mechanism is organized in a ring-like topology where each node passes partial information around the ring.  
   - **Characteristics:** Facilitates efficient distributed computation, reducing the communication overhead typically associated with global attention mechanisms.

8. **Additional Variants (for broader context):**  
   - **[[Axial Attention]]:** Decomposes multi-dimensional attention (e.g., in images) by sequentially attending along each axis (rows, then columns) instead of a full 2D attention map.  
   - **[[Linearized or Low-Rank Attention]]:** Techniques that approximate the full attention matrix using low-rank factorizations or kernel-based methods to achieve linear rather than quadratic complexity.  
   - **[[Memory-Compressed or Summarized Attention]]:** Approaches that first compress or pool parts of the sequence to generate a summary representation, which is then used in the attention computation.

Each of these variants is tailored to address specific challenges—whether it’s the computational cost of full attention, the need for scalability to longer sequences, or the efficiency of distributed computation. Researchers continue to innovate in this area, often combining multiple ideas (such as sparsity with grouping) to push the limits of what attention-based models can achieve.

This list provides a high-level overview, and you may encounter additional specialized variants in recent literature that further refine or combine these ideas.

- **[[Sliding Window Attention (SWA)]]**  
    A type of local attention that “slides” over the input sequence—each token attends to a window of previous tokens. This is used in models like Mistral 7B to handle longer contexts without quadratic scaling.  
    [​[huggingface.co](https://huggingface.co/docs/transformers/en/model_doc/mistral)]
    
- **[[Flash Attention]]**  
    An implementation improvement that computes attention in smaller “chunks” to reduce memory usage and increase speed during inference. Models such as Mistral 7B leverage Flash Attention (or its newer versions) for faster processing.
    
- **[[Native Sparse Attention (NSA)]]**  
    A variant where sparsity is learned during training rather than imposed as a post-processing design. It further organizes tokens into efficient chunks, which is particularly useful for very long contexts.
- **[[Multi-Query Attention (MQA)]]**  
	Shares key and value matrices across all attention heads (only queries remain head-specific), reducing memory overhead while incurring a small performance drop. This technique is used in models like PaLM and Falcon.
    
- **[[Grouped Query Attention (GQA)]]**  
    Groups similar queries so that a subset of heads share the same key-value matrices. This retains much of the modeling capacity of full multi-head attention but with reduced memory and computation. It’s employed in models such as Mistral 7B and Llama 2.
- **[[Multi-Head Latent Attention (MLA)]]**  
	Used notably in DeepSeek models, this approach compresses the key-value pairs into a lower-dimensional (latent) representation. By performing a low-rank joint compression, MLA drastically reduces the memory required for KV caching during inference.
- **[[Dual Chunk Attention (DCA) & Dynamic Sparse Attention with Context Memory]]**  
	Found in models like Qwen, these techniques break the long context into chunks, process them with sparse attention, and dynamically adjust which parts of the context to focus on—thus extending context lengths (up to millions of tokens) while keeping computation manageable.  
	[inferless.com](https://www.inferless.com/learn/the-ultimate-guide-to-qwen-model)
-  **[[PageAttention]]**  
    This technique organizes the Key-Value (KV) cache into “pages” (i.e., fixed-size blocks) that are managed and reused during inference. By breaking down the KV cache into smaller pages, the system can:
    
    - **Reduce Memory Footprint:** Only a subset of pages may need to be loaded or updated at each decoding step.
        
    - **Improve Parallelization:** Page-level operations can be scheduled more efficiently on modern hardware.
        
    - **Facilitate Dynamic Batching:** Serving frameworks can more flexibly reuse cached pages across similar inference requests.
        
- **[[Page-Based KV Caching in vLLM and SGLang]]**  
    Modern serving frameworks like **vLLM** and **SGLang** implement variants of PageAttention. These frameworks slice the KV cache into manageable pages or blocks to maximize throughput and minimize latency. They often incorporate additional optimizations such as:
    
    - **Rotating Buffer KV Cache:** Maintaining a fixed-size window (or “page”) of recent tokens to avoid re-computation.
        
    - **Dynamic Cache Reorganization:** Adjusting page allocations based on current workload to ensure balanced resource use.
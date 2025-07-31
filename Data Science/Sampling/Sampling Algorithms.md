## Common Sampling Algorithms

- **[[Fisher-Yates Shuffle]]**: Used for shuffling arrays before sampling
    
- [[**Reservoir Sampling Algorithm]] (Vitter's Algorithm R)**: Uniform sampling from streams
    
- **[[Poisson Sampling]]**: Each element is selected with fixed probability
    
- **[[Multinomial Sampling]]**: Sampling from a categorical distribution
    
- **[[Weighted Random Sampling]]**: Items are sampled proportionally to their assigned weights
    
- **Gibbs Sampling / [[MCMC]]**: Used in Bayesian inference for drawing samples from complex distributions
    
- **[[Thompson Sampling]]**: Used in reinforcement learning for exploration-exploitation tradeoff
    
- **[[Rejection Sampling]]**: Generate samples from a distribution using a simpler proposal distribution
    

---

## Sampling in Different ML Paradigms

### Supervised Learning

- **Stratified Sampling**: To maintain class balance in classification
    
- **SMOTE / Oversampling**: To address class imbalance
    
- **Bootstrap Sampling**: For bagging methods (Random Forests)
    

### Unsupervised Learning

- **Random Sampling**: For clustering or dimensionality reduction tasks
    
- **Reservoir Sampling**: In large-scale k-means
    
- **Active Sampling**: For labeling few representative points to initialize semi-supervised learning
    

### Reinforcement Learning

- **Importance Sampling**: For off-policy learning
    
- **Adaptive Sampling**: In exploration strategies
    
- **[[Prioritized Experience Replay]]**: Sample important transitions more frequently
    
- **Thompson Sampling**: In contextual bandits and Bayesian RL
    

---

## Sampling by Dataset Type

### NLP Datasets

- **Stratified Sampling**: To preserve label/token distribution
    
- **Undersampling/Oversampling**: For low-resource intent classification
    
- **Active Sampling**: To reduce annotation cost in entity recognition
    

### Computer Vision Datasets

- **Image Augmentation + Oversampling**: For data diversity and balance
    
- **[[Class-balanced Sampling]]**: For imbalanced detection datasets
    
- **[[Patch-wise Sampling]]**: In segmentation tasks
    

### Audio and Speech Datasets

- **[[Sliding Window Sampling]]**: To capture temporal features
    
- **[[Random Crop Sampling]]**: For spectrograms and audio chunks
    
- **SMOTE**: For under-represented classes in classification
    

### Multi-Modal Datasets

- **[[Joint Sampling]]**: Ensuring paired inputs (image + text, audio + text)
    
- **[[Modal-Aware Sampling]]**: Sample based on dominant modality importance
    

---

Each method is linked to a detailed explanation:

Let me know if you'd like me to add visualization aids, algorithm pseudocode, or performance considerations for each method!
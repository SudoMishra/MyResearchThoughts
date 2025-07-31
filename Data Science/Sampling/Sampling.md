# Sampling Methods in Data Science and Machine Learning

Sampling is a foundational concept in data science and machine learning. It refers to selecting a subset of data from a larger population or dataset. The goal is to efficiently estimate population characteristics, reduce computational load, improve model generalizability, or balance data for learning algorithms.

Different sampling strategies are suited for different types of data—structured, unstructured, imbalanced, streaming, etc. Below is a detailed exploration of sampling methods, categorized by technique and dataset type, with links to individual strategy descriptions.

---

## Overview of Sampling Strategies

|Sampling Method|Dataset Type|Purpose|Link|
|---|---|---|---|
|Simple Random Sampling|Structured, Tabular|Unbiased subset selection|[[Simple Random Sampling]]|
|Stratified Sampling|Structured, Tabular|Ensure representation across key subgroups|[[Stratified Sampling]]|
|Systematic Sampling|Structured, Time Series|Evenly spaced selection|[[Systematic Sampling]]|
|Cluster Sampling|Structured, Tabular|Reduce cost, cluster-level insights|[[Cluster Sampling]]|
|Reservoir Sampling|Streaming, Large-scale|Fixed-size sample from data streams|[[Reservoir Sampling]]|
|Importance Sampling|Probabilistic, Monte Carlo|Estimate rare events, reduce variance|[[Importance Sampling]]|
|Bootstrap Sampling|Model Evaluation, Resampling|Uncertainty estimation, ensemble methods|[[Bootstrap Sampling]]|
|Undersampling|Imbalanced Classification|Balance dataset by removing majority class|[[Undersampling]]|
|Oversampling|Imbalanced Classification|Balance dataset by duplicating minority class|[[Oversampling]]|
|SMOTE|Imbalanced Classification|Synthetic data generation for minority class|[[SMOTE]]|
|Active Sampling|Annotation / Human-in-the-loop|Choose most informative samples|[[Active Sampling]]|
|Adaptive Sampling|Online / RL, Time Series|Focus on high-variance or informative regions|[[Adaptive Sampling]]|

---

Each method is linked to a detailed explanation:

## [[Simple Random Sampling]]

- **Definition**: Each data point has an equal chance of being selected.
    
- **Use Case**: General purpose, unbiased exploration.
    
- **Pros**:
    
    - Easy to implement
        
    - Unbiased estimate of population
        
- **Cons**:
    
    - May miss important subgroups
        
    - Inefficient for rare class problems
        

## [[Stratified Sampling]]

- **Definition**: Population is divided into strata (groups) and sampled proportionally or equally within each.
    
- **Use Case**: Ensuring representation across demographic or class categories.
    
- **Pros**:
    
    - Guarantees group-level representation
        
    - Reduces variance in estimates
        
- **Cons**:
    
    - Requires prior knowledge of strata
        
    - Complexity increases with number of strata
        

## [[Systematic Sampling]]

- **Definition**: Select every k-th element from a sorted population.
    
- **Use Case**: Time series, evenly spaced logs.
    
- **Pros**:
    
    - Simple to implement
        
    - Ensures spread across dataset
        
- **Cons**:
    
    - Risk of periodicity bias
        
    - Not truly random
        

## [[Cluster Sampling]]

- **Definition**: Randomly select groups (clusters), then sample all or some within each.
    
- **Use Case**: Distributed or geographically organized datasets.
    
- **Pros**:
    
    - Reduces cost
        
    - Useful for hierarchical structures
        
- **Cons**:
    
    - Higher sampling error than stratified sampling
        
    - Assumes intra-cluster similarity
        

## [[Reservoir Sampling]]

- **Definition**: Maintain a reservoir of size k while streaming over large or unknown dataset.
    
- **Use Case**: Online learning, log data sampling.
    
- **Pros**:
    
    - Memory-efficient
        
    - Suitable for streaming data
        
- **Cons**:
    
    - Approximate (non-deterministic)
        
    - Slight overhead per sample update
        

## [[Importance Sampling]]

- **Definition**: Sample more frequently from regions of high importance (probability-weighted).
    
- **Use Case**: Rare event modeling, Monte Carlo estimates.
    
- **Pros**:
    
    - Reduces variance of estimates
        
    - Focuses computation on important regions
        
- **Cons**:
    
    - Requires good knowledge of importance distribution
        
    - Can be unstable if weights are poorly chosen
        

## [[Bootstrap Sampling]]

- **Definition**: Sample with replacement to generate multiple datasets.
    
- **Use Case**: Confidence intervals, bagging, model evaluation.
    
- **Pros**:
    
    - No distribution assumptions
        
    - Great for small datasets
        
- **Cons**:
    
    - May replicate noise or outliers
        
    - Slower for large datasets
        

## [[Undersampling]]

- **Definition**: Reduce majority class to match minority size.
    
- **Use Case**: Class imbalance problems.
    
- **Pros**:
    
    - Reduces class imbalance
        
    - Faster training
        
- **Cons**:
    
    - Discards potentially useful data
        
    - Risk of underfitting
        

## [[Oversampling]]

- **Definition**: Duplicate or synthetically generate minority class samples.
    
- **Use Case**: Class imbalance.
    
- **Pros**:
    
    - Retains all data
        
    - Improves class balance
        
- **Cons**:
    
    - Overfitting on duplicated samples
        
    - Higher computational cost
        

## [[SMOTE]]

- **Definition**: Synthetic Minority Over-sampling Technique; interpolates between nearby minority points.
    
- **Use Case**: Structured imbalanced datasets.
    
- **Pros**:
    
    - More realistic than naive oversampling
        
    - Works well with classifiers
        
- **Cons**:
    
    - Can generate noise
        
    - Assumes minority class is continuous
        

## [[Active Sampling]]

- **Definition**: Model or human selects next sample based on uncertainty or informativeness.
    
- **Use Case**: Labeling budgets, active learning.
    
- **Pros**:
    
    - More efficient labeling
        
    - Focuses on ambiguous data
        
- **Cons**:
    
    - Needs a model or acquisition function
        
    - Hard to parallelize
        

## [[Adaptive Sampling]]

- **Definition**: Adjust sampling strategy dynamically based on model feedback or environment.
    
- **Use Case**: Reinforcement learning, sequential decision problems.
    
- **Pros**:
    
    - Prioritizes learning from hard or informative regions
        
    - Reduces wasteful samples
        
- **Cons**:
    
    - High complexity
        
    - Requires continuous monitoring
        

---

[[Sampling Algorithms]]

# ✅ Evaluation Methods for ML, Deep Learning & Generative Models

A comprehensive table of evaluation metrics and methods across supervised, unsupervised, generative, and retrieval-based problems in machine learning. Each method is linked using Obsidian `[[Backlinks]]`.

| **Category**                    | **Evaluation Method**                               | **Use Case / Description**                                                    |
| ------------------------------- | --------------------------------------------------- | ----------------------------------------------------------------------------- |
| [[Classification Metrics]]      | [[Accuracy]]                                        | Proportion of correctly classified samples                                    |
|                                 | [[Precision]]                                       | TP / (TP + FP); How many predicted positives are correct                      |
|                                 | [[Recall]] / [[Sensitivity]]                        | TP / (TP + FN); How many actual positives are retrieved                       |
|                                 | [[F1 Score]]                                        | Harmonic mean of precision and recall                                         |
|                                 | [[ROC-AUC Score]]                                   | Area under the ROC curve; threshold-independent binary classifier performance |
|                                 | [[PR-AUC Score]]                                    | Area under Precision-Recall curve (especially useful for imbalanced classes)  |
| [[Regression Metrics]]          | [[Mean Absolute Error (MAE)]]                       | Average absolute difference between predictions and ground truth              |
|                                 | [[Mean Squared Error (MSE)]]                        | Average of squared errors; penalizes large errors more                        |
|                                 | [[Root Mean Squared Error (RMSE)]]                  | Square root of MSE for interpretability                                       |
|                                 | [[R-squared (R²) Score]]                            | Proportion of variance explained by the model                                 |
| [[Ranking / Retrieval Metrics]] | [[Precision@K]]                                     | Precision among the top-K retrieved items                                     |
|                                 | [[Recall@K]]                                        | Recall among the top-K retrieved items                                        |
|                                 | [[MAP (Mean Averaged Precision)]]                   |                                                                               |
|                                 | [[NDCG (Normalized Discounted Cumulative Gain)]]    | Measures ranking quality; accounts for position and relevance                 |
|                                 | [[MRR (Mean Reciprocal Rank)]]                      | Average inverse rank of first relevant item                                   |
| [[Clustering Metrics]]          | [[Silhouette Score]]                                | Measures how similar an object is to its own cluster vs. others               |
|                                 | [[Davies-Bouldin Index]]                            | Evaluates intra-cluster similarity and inter-cluster separation               |
|                                 | [[Adjusted Rand Index (ARI)]]                       | Compares clustering with ground truth labels                                  |
|                                 | [[Normalized Mutual Information (NMI)]]             | Shared information between predicted and true clusters                        |
| [[Generative Model Metrics]]    | [[Inception Score (IS)]]                            | Measures image quality and diversity for GANs                                 |
|                                 | [[Fréchet Inception Distance (FID)]]                | Compares feature distributions of real vs generated images                    |
|                                 | [[Perplexity]]                                      | Evaluates language models: lower = better                                     |
|                                 | [[BLEU Score]]                                      | N-gram precision for text generation (MT, summarization)                      |
|                                 | [[ROUGE Score]]                                     | Recall-based metric for summarization / translation                           |
|                                 | [[METEOR Score]]                                    | Harmonic mean of precision and recall with stemming and synonym matching      |
|                                 | [[Self-BLEU]]                                       | Measures diversity of generations in text generation                          |
| [[Calibration Metrics]]         | [[Brier Score]]                                     | Measures the accuracy of probabilistic predictions                            |
|                                 | [[Expected Calibration Error (ECE)]]                | Difference between predicted probability and actual accuracy                  |
| [[Fairness Metrics]]            | [[Equal Opportunity Difference]]                    | Difference in TPR across groups                                               |
|                                 | [[Demographic Parity]]                              | Compares prediction rates across demographic groups                           |
|                                 | [[Disparate Impact]]                                | Ratio of favorable outcomes for different groups                              |
| [[Uncertainty Estimation]]      | [[Prediction Interval Coverage Probability (PICP)]] | Fraction of true values within predicted intervals                            |
|                                 | [[Expected Calibration Error (ECE)]]                | Also used here for model confidence calibration                               |
| [[Human Evaluation]]            | [[Likert Scale Rating]]                             | 1–5 or 1–10 scale human scoring (used in text/image generation)               |
|                                 | [[Pairwise Preference]]                             | Which of two outputs is preferred? Used in RLHF, summarization                |
|                                 | [[Human-in-the-loop Evaluation]]                    | Evaluation in production or subjective feedback loops                         |

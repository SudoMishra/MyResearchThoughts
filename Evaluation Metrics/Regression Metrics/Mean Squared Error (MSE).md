# [[Mean Squared Error (MSE) in Regression]]

Mean Squared Error (MSE) is one of the most fundamental loss functions in regression analysis. It measures the average of the **squared differences between the actual and predicted values**.

---

## 🔢 How is MSE Calculated?

Given:
- $y_i$: actual value
- $\hat{y}_i$: predicted value
- $n$: number of observations

### Formula:

$$
\text{MSE} = \frac{1}{n} \sum_{i=1}^{n} (y_i - \hat{y}_i)^2
$$

### Components:
- $(y_i - \hat{y}_i)$ = residual (error)
- Squaring penalizes larger errors more heavily.
- Averaging over $n$ ensures scale consistency.

---

## 📊 What Does MSE Represent?

- MSE is a **measure of prediction error** for regression models.
- It tells us **how far off, on average,** our predictions are from the actual values **in squared units**.
- It places **greater penalty on large errors** (due to squaring), making it sensitive to outliers.

---

## 🧠 Statistical Interpretation

### 1. [[Connection to Variance]]
- MSE has units of the square of the response variable (e.g., \$^2 if predicting salary).
- In **unbiased models**, MSE approaches the **variance of the error term** $\varepsilon$ in:
  $$
  y = X\beta + \varepsilon
  $$

### 2. [[Bias-Variance Decomposition]]
For a given point $x$:
$$
\text{MSE}(x) = \text{Bias}^2(\hat{y}) + \text{Var}(\hat{y}) + \sigma^2
$$

Where:
- $\text{Bias}^2$: squared difference between expected prediction and true value.
- $\text{Var}$: variability of the model prediction.
- $\sigma^2$: irreducible error (noise in the data).

This decomposition is central to understanding **model performance vs generalization**.

---

## ✅ When to Use MSE

- **Standard choice** in linear regression and most continuous prediction tasks.
- Preferred when **larger errors are exponentially worse** than smaller ones.
- Used in **closed-form optimization** of Ordinary Least Squares:
  $$
  \beta = (X^T X)^{-1} X^T Y
  $$

---

## ⚠️ Limitations

| Issue                      | Explanation |
|---------------------------|-------------|
| **Sensitive to Outliers** | Squaring errors inflates large residuals. |
| **Interpretation**        | Hard to interpret due to squared units (e.g., predicting height → MSE in cm²). |
| **Scale Dependency**      | Not normalized—values can't be directly compared across datasets with different scales. |

For these reasons, you may also compute:
- **Root Mean Squared Error (RMSE)**: $\text{RMSE} = \sqrt{\text{MSE}}$
- **Mean Absolute Error (MAE)**: avoids squaring, treats all errors equally.

---

## 📌 Example

Suppose your model predicts:
- Actual: $[3, 5, 2.5, 7]$
- Predicted: $[2.5, 5, 4, 8]$


$$\text{MSE} = \frac{1}{4} \left[ (3 - 2.5)^2 + (5 - 5)^2 + (2.5 - 4)^2 + (7 - 8)^2 \right] = \frac{1}{4} (0.25 + 0 + 2.25 + 1) = 0.875$$


---

## 🧪 In the Context of Model Training

- Used as the **loss function** during training to update model weights (especially in regression-based deep learning).
- Smooth and differentiable → suitable for **gradient-based optimization** like SGD, Adam, etc.

---

## 🔁 MSE vs Other Metrics

| Metric       | Penalizes Outliers | Differentiable | Interpretability | Common Use Case |
|--------------|--------------------|----------------|------------------|-----------------|
| MSE          | Yes                | Yes            | Squared units    | Regression training |
| RMSE         | Yes                | Yes            | Same units as $y$| Final performance report |
| MAE          | No (Linear)        | No (at 0)      | Absolute units   | Robust regression |

---

## 🧠 Summary

- MSE measures **average squared error**.
- Optimizing MSE = **maximizing likelihood** under the assumption of **Gaussian errors**.
- Core metric for evaluating and training regression models.

[[Loss Functions in Regression]] · [[Bias-Variance Tradeoff]] · [[RMSE vs MAE]]

# What MSE Tells You About a Model

Mean Squared Error (MSE) gives you a **quantitative measure** of your model's **average prediction error**. But interpreting MSE **in isolation** has limitations.

---

## ✅ What You *Can* Infer from MSE

### 1. **Absolute Error Magnitude (in squared units)**
- Lower MSE = better fit (fewer large errors).
- A high MSE indicates your predictions deviate significantly from true values.

> Example: If MSE = 16 while predicting house prices (in $1000s), your average squared error is \$16,000² = \$256M off → large deviations exist.

---

### 2. **Outlier Sensitivity**
- If MSE is **unexpectedly high**, your model may be overreacting to **outliers**.
- Helps decide whether to:
  - Use a **robust loss** (like MAE or Huber).
  - Clean or transform the data.

---

### 3. **Relative Improvement (Model A vs Model B)**
- Use MSE to compare models **on the same dataset**.
- A significantly lower MSE suggests a **better approximation** to the underlying function.

> But this only holds true if **scale, sample size, and target units** are consistent.

---

### 4. **Bias-Variance Clues**
- **High MSE** can result from:
  - **High bias**: underfitting → too simple
  - **High variance**: overfitting → too complex
- If you track MSE on **train and validation sets**, you can infer:
  - Train MSE ≪ Val MSE → High variance
  - Both MSEs are high → High bias

---

## ⚠️ What MSE *Doesn’t* Tell You

| It doesn’t reveal...        | Why? |
|-----------------------------|------|
| Whether all predictors are useful | Doesn’t assess feature importance |
| Whether model assumptions hold | Residual plots, diagnostics required |
| Statistical significance of fit | Need F-statistic, t-tests |
| Comparative strength of relationships | Need coefficient analysis |
| Whether model generalizes | Need cross-validation / test error |

---

## 📌 Summary

| MSE Helps You Understand         | MSE Alone Cannot Tell You     |
|----------------------------------|-------------------------------|
| Magnitude of average squared error | Causality or correlation     |
| Model performance relative to others | Model interpretability       |
| Error sensitivity to outliers     | Statistical reliability       |
| Train vs validation behavior      | Feature relevance             |

> **MSE is a crucial metric, but never sufficient alone. Always pair it with residual analysis, $R^2$, validation error, and interpretability tools.**

[[Model Evaluation]] · [[Bias-Variance Tradeoff]] · [[Overfitting vs Underfitting]]

# MSE and Statistical Theory

Mean Squared Error (MSE) is more than just a prediction error metric—it is deeply grounded in **statistical theory**, particularly in **estimation**, **likelihood**, and the **bias-variance tradeoff**.

---

## 📐 1. MSE as an Estimator Quality Metric

In classical statistics, MSE is a metric for evaluating the **quality of an estimator** $\hat{\theta}$ of a true parameter $\theta$.

### Formula:
\[
$$\text{MSE}(\hat{\theta}) = \mathbb{E}\left[(\hat{\theta} - \theta)^2\right]$$
\]

This expression captures both **bias** and **variance** of the estimator:

### [[Bias-Variance Decomposition]]:
\[
$$\text{MSE}(\hat{\theta}) = \underbrace{\left( \mathbb{E}[\hat{\theta}] - \theta \right)^2}_{\text{Bias}^2} + \underbrace{\text{Var}(\hat{\theta})}_{\text{Variance}}$$
\]

- **Bias**: error due to systematic assumptions in the model.
- **Variance**: error due to model sensitivity to training data.
- An **ideal estimator** has **low bias and low variance**.

---

## 📈 2. MSE in Linear Regression = Maximum Likelihood Estimation

When we assume the noise term $\varepsilon$ in a linear regression model is normally distributed:

\[
$$y = X\beta + \varepsilon, \quad \varepsilon \sim \mathcal{N}(0, \sigma^2 I)$$
\]

then minimizing the MSE is **equivalent to maximizing the likelihood** of observing the data under the normal error model.

### Log-likelihood of the Gaussian:
\[
$$\log \mathcal{L}(\beta) = -\frac{n}{2} \log(2\pi\sigma^2) - \frac{1}{2\sigma^2} \sum_{i=1}^n (y_i - \hat{y}_i)^2$$
\]

Maximizing this is the same as **minimizing** the sum of squared errors (i.e., MSE), since the rest are constants.

> This connects MSE to **Maximum Likelihood Estimation (MLE)** and gives it a **statistical justification**.

---

## 🧠 3. MSE as a Risk Function in Decision Theory

In **Bayesian and frequentist decision theory**, the MSE is a **loss function** that quantifies risk:

- If the loss function is:
  \[
$$  L(\theta, \hat{\theta}) = (\theta - \hat{\theta})^2$$
  \]
  then the **expected loss** is the MSE.

This makes MSE a **natural choice for point estimation** in regression and other inference problems.

---

## 📊 4. MSE and Gauss-Markov Theorem

In classical linear regression:

> The **Gauss-Markov Theorem** states that the **Ordinary Least Squares (OLS)** estimator is the **Best Linear Unbiased Estimator (BLUE)** under the assumptions:
- Linearity
- Independence
- Homoscedasticity
- No perfect multicollinearity

This implies:
- The OLS estimator **minimizes the MSE** among all unbiased linear estimators.

---

## 🧪 5. MSE and Hypothesis Testing

- Although MSE itself is not a test statistic, it is closely tied to:
  - **Standard Error (SE)** of the coefficients
  - **t-tests** and **F-tests** in regression

> These tests rely on estimates of $\sigma^2$ derived from the **Residual Sum of Squares (RSS)**, which is a scaled version of MSE:
\[
$$\hat{\sigma}^2 = \frac{SS_{\text{res}}}{n - k - 1}$$
\]

Thus, MSE feeds directly into inferential procedures.

---

## 📌 Summary: MSE's Statistical Role

| Area                     | Role of MSE                                                  |
|--------------------------|--------------------------------------------------------------|
| Estimation Theory        | Measures estimator quality (bias + variance)                 |
| Maximum Likelihood       | Equivalent to MLE in Gaussian noise models                   |
| Decision Theory          | Expected loss under quadratic loss function                  |
| Linear Regression        | Core optimization target for OLS                            |
| Inferential Statistics   | Used to estimate error variance in $t$ and $F$ tests         |
| Model Selection          | A building block for AIC, BIC, and cross-validation metrics  |

> **MSE is not just a performance metric—it's a fundamental tool that bridges regression, inference, estimation, and decision theory.**

[[Bias-Variance Tradeoff]] · [[Maximum Likelihood Estimation]] · [[Gauss-Markov Theorem]] · [[Risk and Loss Functions]]


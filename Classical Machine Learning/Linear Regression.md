# Objective Problem Statement

For linear regression, our problem is essentially: given some numerical data about a problem, we need to predict a continuous target value. To do this we need to have a set of X (our features or predictor/independent variables) and Y (our output/dependent variables). The output in itself is a continuous value that we need. 

## Simple Linear Regression:
Simple Linear Regression models the relationship between a single predictor X and a continuous response Y. Key points include:

- **Model Equation**  
  $$ y = \beta_0 + \beta_1 x + \varepsilon $$ 
  where $\beta_0$ is the intercept, $\beta_1$ the slope coefficient, and $\varepsilon$ the error term. [[Model Equation]]

- **Objective (Loss Function)**  
  Minimize the Mean Squared Error (MSE):  
  $$
    \text{MSE} = \frac{1}{n}\sum_{i=1}^n (y_i - \hat y_i)^2
	$$
  typically via Ordinary Least Squares. [[Ordinary Least Squares]]

- **Parameter Estimation**  
  - **Closed‑form** via the Normal Equation:  
    $$ \displaystyle \beta = (X^T X)^{-1} X^T Y $$  
  - **Iterative** via [[Gradient Descent]] when \(n\) or feature count is large.

- **Assumptions**  
  1. **Linearity**: true relationship between X and Y is linear. [[Assumptions of Linear Regression]]  
  2. **Independence** of errors.  
  3. **Homoscedasticity**: constant variance of errors.  
  4. **Normality** of error terms.  
  5. **No influential outliers**.

- **Interpretation**  
  $\beta_1$ represents the average change in Y for a one‑unit increase in X. Its sign indicates direction, magnitude indicates strength.

- **Diagnostics**  
  - **Residual analysis**: check linearity & homoscedasticity via plots. [[Residual Analysis]]  
  - **Goodness‑of‑fit**: $R^2$, $adjusted R^2$.  
  - **Statistical tests**: t‑tests on $\beta$-coefficients for significance.

## Multi Linear Regression
Multi Linear Regression extends simple linear regression to multiple inputs and, optionally, multiple outputs.

- **Single‑output (Multiple Predictors)**  
  $$
    \hat y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \dots + \beta_n x_n + \varepsilon
    $$  
  where $x_1,\dots,x_n$ are predictors. [[Multiple Regression]]

- **Matrix Formulation**  
  $$
    Y = X\beta + \varepsilon
    $$
  
  with $Y$ as $n\times1$, $X$ as $n\times(p+1)$ (including intercept column), and $\beta$ as $(p+1)\times1$. [[Matrix Algebra in Regression]]

- **Parameter Estimation**  
  - **Normal Equation**:  $$\beta = (X^T X)^{-1} X^T Y$$  
  - **Gradient Descent** for large‑scale data.

- **Multivariate Output (M outputs)**  
  When predicting \(M\) correlated targets, \(Y\) is \(n\times M\) and \(\beta\) is \((p+1)\times M\). Estimate via  
  $$
    \hat{\beta} = (X^T X)^{-1} X^T Y$$
    
  [[Multivariate Regression]]

- **Additional Assumptions & Challenges**  
  - **No perfect multicollinearity** among predictors. [[Multicollinearity]]  
  - Adequate sample size $(n \gg p)$ to avoid overfitting.

- **Diagnostics & Evaluation**  
  - **Variance Inflation Factor (VIF)** to detect multicollinearity.  
  - **Joint F‑test** for overall model significance.  
  - Residual checks for each output dimension.

- **Interpretation**  
  Each coefficient $\beta_j$ measures the marginal effect of $x_j$ on the response, holding other predictors constant. In the multivariate case, each column of $\beta$ maps predictors to a specific output.


# [[Why MSE is preferred over MAE in Linear Regression]]

In linear regression, the **Mean Squared Error (MSE)** is commonly used as the loss function rather than **Mean Absolute Error (MAE)**. Below are the key reasons:

---

## 1. [[Mathematical Differentiability]]

- MSE is **differentiable everywhere**, including at 0.  
- MAE is **not differentiable at 0** due to the absolute value function. This creates issues for optimization algorithms like [[Gradient Descent]] which rely on computing gradients.
- The derivative of MSE:
  $$
  \frac{d}{d\theta} \text{MSE} = \frac{2}{n} \sum_i (y_i - \hat{y}_i)(-x_i)
  $$
  is smooth and continuous, making it easier to solve with standard optimization tools.

---

## 2. [[Closed-form Solution]]

- Using MSE leads to a **closed-form solution** for Ordinary Least Squares (OLS):  
  $$
  \beta = (X^T X)^{-1} X^T Y
  $$
- MAE does **not** have a closed-form solution and requires **iterative optimization** like Linear Programming or advanced techniques such as coordinate descent.

---

## 3. [[Statistical Interpretation]]

- Minimizing MSE is equivalent to **Maximum Likelihood Estimation (MLE)** under the assumption that errors are **normally distributed**.  
  - If $\varepsilon \sim \mathcal{N}(0, \sigma^2)$, the likelihood is maximized by minimizing MSE.

- MAE corresponds to assuming errors follow a **Laplace distribution**, which is less common in real-world noise models.

---

## 4. [[Error Sensitivity and Penalization]]

- MSE **penalizes larger errors more** than smaller ones due to the squaring effect.
  - Good when you want to heavily penalize outliers or large deviations.
- MAE treats all errors **linearly**, making it more **robust to outliers** but less sensitive to large deviations.

---

## 5. [[Computational Efficiency]]

- Since MSE leads to convex and smooth optimization landscapes, **convergence is faster and more stable** in gradient-based methods.
- MAE's piecewise nature can lead to **slower convergence** and unstable gradients near non-differentiable points.

---

## Summary: MSE vs MAE

| Criterion               | MSE                        | MAE                       |
|------------------------|----------------------------|---------------------------|
| Differentiable         | Yes                        | No (at 0)                 |
| Closed-form solution   | Yes (via OLS)              | No                        |
| Statistical basis      | Normal distribution (MLE)  | Laplace distribution      |
| Outlier sensitivity    | High                       | Low                       |
| Optimization landscape | Smooth, convex             | Piecewise, less smooth    |

---

## When to Use MAE?

- In **robust regression**, when the dataset contains **many outliers**, MAE or Huber loss is preferable.  
- MAE is also used when minimizing **median** error is more meaningful than minimizing **mean** error.

For hybrid approaches, consider [[Huber Loss]] which combines the benefits of MSE and MAE.

# [[Minimizing Median Error over Mean Error]]

In certain scenarios, minimizing the **median error** (via [[Median Absolute Error]] or quantile loss) is preferred over minimizing the **mean error** (via [[Mean Squared Error]] or [[Mean Absolute Error]]).

---

## 🎯 When is Minimizing Median Error Appropriate?

### 1. [[Robustness to Outliers]]
- **Median** is robust to extreme values and skewed distributions.
- If the target variable or error distribution is **heavy-tailed** or contains **outliers**, using the median ensures that the model doesn't get skewed by those extreme values.

> Example: Predicting housing prices in a region where a few luxury houses inflate the average price. Minimizing mean error will overfit to these rare expensive homes, while median keeps predictions realistic.

---

### 2. [[Skewed Target Distributions]]
- When the target variable is **not symmetrically distributed**, the **mean is not representative** of central tendency.
- **Median** better captures the central tendency in such cases.

> Example: Income prediction, where a small fraction of people earn significantly more than the rest. Median income is a better indicator than mean.

---

### 3. [[Fairness and Equity-Oriented Objectives]]
- In fairness-sensitive domains (like healthcare or public services), focusing on the **median error** can ensure **equity** in predictions for the majority population rather than a few high-error individuals.

---

## ⚙️ How is Median Error Minimized?

### 1. **Median Absolute Error (MedAE)**

Defined as:

$$
\text{MedAE} = \text{median}(|y_i - \hat{y}_i|)
$$

This loss function is **not differentiable**, so **standard gradient descent cannot be applied** directly.

#### Optimization:
- Requires **non-gradient methods**, such as:
  - Linear programming
  - Subgradient methods
  - Specialized algorithms for quantile regression

---

### 2. **Quantile Regression** (Generalization of Median Minimization)

Median is a special case of quantile regression with quantile \(q = 0.5\)

#### Quantile Loss Function:

$$
L_q(y, \hat y) = 
\begin{cases}
q \cdot (y - \hat y) & \text{if } y \geq \hat y \\
(1 - q) \cdot (\hat y - y) & \text{if } y < \hat y
\end{cases}
$$

For $q = 0.5$, this becomes the **check function for the median**:

$$
L_{0.5}(y, \hat y) = 
\begin{cases}
0.5 \cdot |y - \hat y| & \text{if } y \geq \hat y \\
0.5 \cdot |y - \hat y| & \text{if } y < \hat y
\end{cases}
= 0.5 \cdot |y - \hat y|
$$

This is equivalent to minimizing **Median Absolute Error** under quantile regression.

---

## 🧠 Summary: Median vs Mean

| Aspect                        | Min Mean Error (MSE/MAE)    | Min Median Error (MedAE)       |
|------------------------------|------------------------------|-------------------------------|
| Sensitivity to Outliers      | High                         | Low                            |
| Assumes Symmetric Noise      | Yes                          | No                             |
| Differentiability            | Yes (MSE), No (MAE)          | No                             |
| Closed-form Solution         | Only for MSE                 | No                             |
| Use Case                     | General regression           | Robust or skewed data         |

---

## ✅ When to Use

- Use **MSE**: When data is clean, and large errors must be penalized more.
- Use **MAE**: When you want equal treatment of all errors, and some outliers may exist.
- Use **MedAE**: When fairness and robustness to outliers is crucial.
- Use **Quantile Loss**: When you want to estimate specific percentiles (not just mean or median).

[[Robust Regression]] · [[Quantile Regression]] · [[Fairness in ML]]

# [[Evaluating Linear Regression Models]]

Once a linear regression model has been fitted, it’s important to evaluate its **goodness of fit**, **statistical validity**, and the **relationship between independent and dependent variables**.

---

## 📊 Model Evaluation Metrics

### 1. [[R-squared & Adjusted R-squared]]
- Measures the proportion of variance in the dependent variable explained by the model.
- Ranges from 0 to 1 (higher is better).
- Formula:
  $$
  R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}
  $$

 **Adjusted R-squared**
- Penalizes for the number of predictors to avoid overfitting.
- Use this when comparing models with different numbers of features.

### 3. [[Mean Squared Error (MSE)]]
- Average of the squared prediction errors. Lower indicates better fit.

### 4. [[Mean Absolute Error (MAE)]]
- Average of absolute errors. More interpretable but less sensitive to outliers than MSE.

### 5. [[F-statistic and ANOVA]]
- Tests whether at least one regression coefficient is significantly different from zero.
- High F-value and low p-value indicate the model as a whole is significant.

---

## 📈 Diagnostic Checks

### 1. [[Residual Analysis]]
- Plot residuals vs fitted values:
  - Should look like random scatter (indicates good model fit).
- Non-random patterns suggest model misspecification (e.g., non-linearity, heteroscedasticity).

### 2. [[QQ Plot of Residuals]]
- Tests for normality of residuals.
- Deviations from diagonal indicate violation of normality assumption.

### 3. [[Variance Inflation Factor (VIF)]]
- Measures multicollinearity among independent variables.
- VIF > 5 or 10 suggests high collinearity → may inflate standard errors.

---

## 🧠 Inference from Coefficients

### 1. [[Unstandardized Coefficients]]
- Represent the change in the dependent variable for a **one-unit change** in the independent variable.
- Directly interpretable in original units.

### 2. [[Standardized Coefficients]]
- Represent the effect size **in standard deviation units**.
- Useful for comparing the relative importance of predictors.

### 3. [[Significance Testing of Coefficients]]
- Use **t-tests** to check whether each coefficient is significantly different from zero.
- Low p-value (< 0.05) implies statistically significant relationship.

### 4. [[Confidence Intervals]]
- Gives a range within which the true coefficient is likely to lie.
- If 0 lies within the interval → predictor may not be significant.

---

## ✅ What You Can Infer

- **Direction** of relationship (positive or negative) from the sign of the coefficient.
- **Magnitude** of effect from the size of the coefficient.
- **Importance** from standardized coefficients or p-values.
- **Multicollinearity** from VIF values.
- **Overall model quality** from $R^2$, adjusted $R^2$, F-statistic.

---

## 📌 Example Interpretation

> Suppose you fit the model:
> $$
> \hat{y} = 5 + 2.3x_1 - 1.5x_2
> $$
> - For every 1-unit increase in $x_1$, $y$ increases by 2.3 units (holding $x_2$ constant).
> - For every 1-unit increase in $x_2$, $y$ decreases by 1.5 units.
> - If $x_2$ has a p-value > 0.05, its effect might not be statistically significant.

[[Model Diagnostics]] · [[Interpreting Coefficients]] · [[Model Fit Evaluation]]

# R Squared and Adjusted R Squared in Linear Regression

$R^2$ and Adjusted $R^2$ are fundamental metrics used to evaluate the fit of a regression model. They quantify how well the independent variables explain the variance in the dependent variable.

---

## 📐 What is $R^2$?

Also known as the **coefficient of determination**, $R^2$ measures the **proportion of variance in the dependent variable ($y$)** that is **explained by the model**.

### 🔢 Formula:

Let:
- $SS_{\text{tot}}$ = Total Sum of Squares  from the observed mean 
  $$SS_{\text{tot}} = \sum_{i=1}^n (y_i - \bar{y})^2$$
- $SS_{\text{res}}$ = Residual Sum of Squares (Squared Error between predicted and observed)
  $$SS_{\text{res}} = \sum_{i=1}^n (y_i - \hat{y}_i)^2$$

Then:

$$R^2 = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}$$


- $R^2 = 0$: model explains none of the variance
- $R^2 = 1$: model perfectly explains all variance
- $R^2 < 0$: model performs worse than the mean

---

## 🧠 What Does $R^2$ Represent?

- **Explained variance**: Measures the proportion of variance captured by the model.
- **Goodness of fit**: Indicates how well the regression line approximates real data.
- $R^2$ answers: *“How much better is the model compared to simply using the mean of $y$?”*

---

## ⚠️ Limitations of $R^2$

- **Monotonically increases** with more predictors—even if they are irrelevant.
- Doesn’t penalize **model complexity** or overfitting.
- Not a reliable metric for comparing models with different numbers of predictors.

---

## 🧮 Adjusted $R^2$

### Why Adjust?

To account for the number of predictors and penalize for adding variables that do not improve the model.

### Formula:

Let:
- $n$ = number of observations
- $k$ = number of predictors (excluding the intercept)

Then:

$$R^2_{\text{adj}} = 1 - \left( \frac{SS_{\text{res}} / (n - k - 1)}{SS_{\text{tot}} / (n - 1)} \right)$$


Alternatively:

$$R^2_{\text{adj}} = 1 - (1 - R^2) \cdot \frac{n - 1}{n - k - 1}$$

### 🔍 Interpretation:

- Adjusted $R^2$ **increases only** if the new predictor improves the model more than would be expected by chance.
- Can **decrease** when an irrelevant variable is added.
- More conservative than $R^2$ → better for **model selection**.

---

## 🎓 Statistical Interpretation

## 🎓 Statistical Interpretation (Expanded)

In linear regression, **ANOVA decomposition** breaks down the total variability in the outcome variable into parts explained and unexplained by the model.

### Total Sum of Squares ($SS_{\text{tot}}$)
- Measures **total variance** in the dependent variable $y$.
- Formula:
  $$
  SS_{\text{tot}} = \sum_{i=1}^n (y_i - \bar{y})^2
  $$
- Think of it as the error you'd make if you **only used the mean $\bar{y}$** to predict every $y_i$.

---

### Residual Sum of Squares ($SS_{\text{res}}$)
- Measures the **error left** after fitting the regression model.
- Formula:
  $$
  SS_{\text{res}} = \sum_{i=1}^n (y_i - \hat{y}_i)^2
  $$
- These are the **residuals** (difference between actual and predicted values).

---

### Regression Sum of Squares ($SS_{\text{reg}}$)
- Measures the **explained variance**—the part of $y$ explained by the model.
- Formula:
  $$
  SS_{\text{reg}} = \sum_{i=1}^n (\hat{y}_i - \bar{y})^2
  $$
- It captures how far the model predictions $\hat{y}_i$ are from the overall mean $\bar{y}$.

---

### ANOVA Identity:

$$SS_{\text{tot}} = SS_{\text{reg}} + SS_{\text{res}}$$


This tells us that the total variability in $y$ is made up of:
- The part explained by the regression line ($SS_{\text{reg}}$),
- Plus the part that's still unexplained ($SS_{\text{res}}$).

---

### Final $R^2$ Interpretation:
$$R^2 = \frac{SS_{\text{reg}}}{SS_{\text{tot}}} = 1 - \frac{SS_{\text{res}}}{SS_{\text{tot}}}$$
This means:
- **$R^2$ is the proportion of total variance that is explained by the model**.
- The closer $R^2$ is to 1, the better your model explains the data.

---

### Adjusted $R^2$ (Recap)
- Adjusted $R^2$ corrects $R^2$ for the number of predictors used.
- It serves as a **more reliable indicator** of the model's ability to generalize, especially when comparing models with different numbers of predictors.

- $R^2$ is the **squared correlation** between observed $y$ and predicted $\hat{y}$.
- In the context of the **ANOVA decomposition**:
 
$$  SS_{\text{tot}} = SS_{\text{reg}} + SS_{\text{res}}$$
  $R^2$ reflects the proportion:  
$$  R^2 = \frac{SS_{\text{reg}}}{SS_{\text{tot}}}$$
- Adjusted $R^2$ can be seen as a **bias-adjusted estimator** of the population $R^2$, improving generalization.

---

## 🧪 Practical Implications

| Metric           | Use For                       | Behavior with More Features | Best When                     |
|------------------|-------------------------------|------------------------------|-------------------------------|
| $R^2$             | Explaining variance            | Increases or stays the same  | Exploratory analysis          |
| Adjusted $R^2$    | Model comparison               | May increase or decrease     | Feature selection, small $n$  |

---

## ✅ When to Use Which?

- Use **$R^2$**:
  - When you want a quick idea of fit
  - When all models have the **same number of predictors**

- Use **Adjusted $R^2$**:
  - When comparing models with **different numbers of predictors**
  - When avoiding **overfitting**
  - When working with **small datasets**

---

## 📌 Example

> Suppose we have a model:
$$ y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \varepsilon$$
> - $R^2 = 0.80$: The model explains 80% of the variance in $y$.
> - Adjusted $R^2 = 0.75$: After penalizing for two predictors, the true explanatory power is 75%.

[[Goodness of Fit]] · [[Model Selection Criteria]] · [[Variance Explained]]

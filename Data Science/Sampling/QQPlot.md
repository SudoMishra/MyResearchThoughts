# [[QQ Plot]]

A **QQ Plot** (Quantile-Quantile Plot) is a graphical tool used to compare the **quantiles** of a dataset with the **quantiles of a theoretical distribution** (often a normal distribution). It helps assess whether the data follows a particular distribution.

---

## 🧠 Intuition

If the data comes from the theoretical distribution:
- The points will lie approximately **on a straight line**.

If the data deviates from that distribution:
- The points will **curve away** from the line.

---

## 🧪 Use Cases

- **Check normality** of residuals in regression models
- **Assess assumptions** in hypothesis testing
- **Visual diagnostics** in exploratory data analysis (EDA)

---

## 📊 How it Works

1. Sort the data sample → empirical quantiles
2. Compute theoretical quantiles from desired distribution (e.g., Normal)
3. Plot empirical quantiles vs theoretical quantiles
4. Compare against the reference line \( y = x \)

---

## ✅ Interpretation

| Shape/Trend | Interpretation |
|-------------|----------------|
| Straight Line | Good match with the distribution |
| S-curve | Skewness in the data |
| Points diverge at ends | Heavy or light tails (kurtosis issues) |
| Curved upwards or downwards | Systematic deviation from the model |

---

## 🧑‍🔬 Example: Normality Check in Python

```python
import scipy.stats as stats
import matplotlib.pyplot as plt

data = [12, 13, 15, 16, 18, 20, 25]
stats.probplot(data, dist="norm", plot=plt)
plt.title("QQ Plot - Normal Distribution")
plt.show()

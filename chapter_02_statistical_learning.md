# Chapter 2: Statistical Learning

## Summary

In any ML problem, the first step is deciding whether the goal is to **predict** unseen data or to **understand** the underlying relationship between variables.

- **Prediction:** Accurately estimating outcomes for new data, prioritizing performance over interpretation.
- **Inference:** Understanding how and why variables are related, focusing on interpreting each predictor's effect on the outcome.

**Reducible vs. Irreducible Error** — No model can eliminate all error. Reducible error can be lowered by choosing a better method; irreducible error comes from unmeasured variables or inherent randomness and cannot be removed no matter how good the model is.

**The Bias-Variance Trade-off** — Simply choosing the most complex model usually fails. As flexibility increases, bias drops but variance rises. At some point, variance spikes faster than bias falls, and test error increases.

## Model Types

| Type | Examples | Best When |
|------|----------|-----------|
| **Restrictive (Parametric)** | Linear Regression | Goal is *inference*, or sample size is small |
| **Flexible (Non-parametric)** | K-Nearest Neighbors | Goal is pure *prediction*, interpretability is not needed, and data is abundant |

Flexible models fail when data is limited or noisy — they memorize the noise (overfitting).

## Important Notes

- Parametric methods assume a specific shape for f (e.g., a straight line). If this assumption is wrong, the model will have high bias and miss the true pattern.
- A common mistake is selecting a model based on the lowest *training* error. A low training error does **not** guarantee a low test error.
- **Overlooked detail:** In KNN, an overly small K (e.g., K = 1) creates a highly flexible model with low bias but massive variance — very jumpy and prone to overfitting.

## Questions to Keep in Mind

- **Why might a less flexible method be preferred over a highly flexible one?**

  Less flexible models are more interpretable (better for inference) and less prone to overfitting when the true relationship is simple or data is limited.

**How should you choose a model?**

Prefer a simpler model when the dataset is small or noisy (complex models overfit). Also prefer simpler models when interpretability matters, such as in medical or financial decisions where understanding variable effects is more important than marginal accuracy gains.

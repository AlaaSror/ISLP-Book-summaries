# Chapter 5: Resampling Methods

## Summary

We need resampling because calculating true test error requires a large dedicated test set, which is rarely available. A simple validation set approach (one 50/50 split) overestimates test error since models perform worse when trained on fewer observations. Using training error as a proxy is also flawed — it usually drastically *underestimates* test error.

## Two Core Methods

**1. Cross-Validation (CV)**
Used to estimate **test error** for model assessment (how well a model generalizes) and model selection (choosing the right level of flexibility). It simulates unseen data by intentionally holding out subsets of data during training.

**2. Bootstrap**
Repeatedly samples *with replacement* from the training data and refits the model to estimate the **uncertainty** (standard error, confidence intervals) of a statistic. It measures *variability*, not performance. The Bootstrap was introduced because many complex estimators lack simple formulas for their standard deviation — the Bootstrap simulates new samples computationally to measure this variance.

## Important Notes

- **k-Fold CV:** The standard tool for choosing tuning parameters (e.g., K in KNN, polynomial degree). Computationally efficient and provides a reliable test error estimate.
- **The Bootstrap:** Use when you need a confidence interval or standard error for a custom metric where statistical software doesn't output standard errors automatically (e.g., optimizing an asset allocation fraction).
- **LOOCV** becomes prohibitively slow when the model is complex and the dataset is large, as it requires fitting the model n times.
- **Common misunderstanding:** LOOCV is not always the best CV method despite training on the most data. Because its training sets are nearly identical, the resulting estimates are highly correlated — averaging highly correlated quantities produces *higher* variance than k-fold CV.

## Questions to Keep in Mind

- **What are the main drawbacks of the single validation set approach?**

  The test error estimate is highly variable depending on which observations end up in which set, and it tends to overestimate test error because the model is trained on a smaller dataset.

- **Why does 5-fold or 10-fold CV often outperform LOOCV?**

  Bias-variance trade-off: while LOOCV has less bias, its training sets are almost identical, making outputs highly positively correlated. Averaging highly correlated quantities yields higher variance than averaging the less-correlated outputs of k-fold CV.

- **How does the Bootstrap generate new datasets without collecting new data?**

  It creates distinct datasets by repeatedly sampling observations *with replacement* from the original dataset, meaning the same observation can appear multiple times in a single bootstrap sample.

**What is the difference between model assessment and model selection?**

**Model assessment** evaluates a model's overall generalization performance. **Model selection** chooses the appropriate level of flexibility.

**Can LOOCV ever be computationally cheap?**

Yes. For least squares linear or polynomial regression, LOOCV can be computed using a mathematical shortcut based on observation leverage, requiring the model to be fit only once.

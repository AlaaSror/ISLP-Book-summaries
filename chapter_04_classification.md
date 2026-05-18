# Chapter 4: Classification

## Summary

**Why not linear regression?** It can predict probabilities below 0 or above 1, and it imposes a false ordering between distinct categories. Different numeric codings of the same categories produce entirely different models — an unacceptable property.

## Methods Overview

**Logistic Regression** — Best for binary classification when interpretability is paramount (e.g., understanding the log-odds of a customer defaulting). The log-odds (logit) is linear in X; β₁ captures the change in log-odds per unit increase in X, not the change in probability. Coefficients are estimated via maximum likelihood.

**Generative Models (LDA / QDA)** — Introduced because logistic regression can become unstable when classes are perfectly separated or when sample size is small. All generative methods model the distribution of X within each class and apply Bayes' theorem to recover posterior probabilities.

| Method | Key Assumption | Best When |
|--------|---------------|-----------|
| **LDA** | Shared covariance matrix across classes | Classes are well-separated, n is small, predictors are roughly normal |
| **QDA** | Each class has its own covariance matrix | Different covariance structures, moderately non-linear boundary, large n |
| **Naive Bayes** | Predictors are independent within each class | Many features relative to dataset size |
| **KNN** | None | Highly non-linear boundaries with n >> p |

**Naive Bayes** reduces a hard p-dimensional density problem to p simple 1D problems. Even though independence is almost always false, it trades bias for a large variance reduction, making it robust to overfitting. Interestingly, LDA is a special case of Naive Bayes when the covariance matrix is diagonal with equal variances.

## Important Notes

- **Thresholds and the ROC Curve:** Using a rigid 0.5 threshold is a common mistake. In the Default dataset, LDA at 0.5 correctly identifies only 24.3% of actual defaulters. Lowering the threshold to 0.2 raises detection to 58.6% at a modest total error cost (2.75% → 3.73%). The ROC curve visualizes the sensitivity/specificity trade-off across all thresholds; the AUC summarizes it (0.5 = random, 1.0 = perfect). The right threshold requires domain knowledge about the relative cost of each error type.

- **Confounding** can completely reverse logistic regression results. In the Default data, student status appears to *increase* default risk in simple logistic regression but *decreases* it in multiple regression once balance is included — because students carry higher balances, and balance is the true driver of risk. Confounding occurs when the apparent relationship between a predictor and the response changes significantly once correlated predictors are added.

- **Comparing all methods:** LDA and logistic regression perform similarly when the true decision boundary is linear. QDA and Naive Bayes handle moderate non-linearity. KNN handles highly non-linear boundaries but requires n >> p, cannot identify which predictors matter, and is very sensitive to K — even on genuinely non-linear problems, K = 1 can give the worst results. No single method dominates; the right choice depends on boundary shape, n, p, and the bias-variance trade-off.

- **Generalized Linear Models (GLMs):** When Y is a count, neither regression nor classification applies directly. Poisson regression models log(E(Y)) as linear in predictors, ensuring non-negative fitted values. A key property: under the Poisson distribution, mean equals variance, so variability scales naturally with the count. Linear, logistic, and Poisson regression are all GLMs — each pairs a distributional assumption with a link function that makes the transformed mean linear in the predictors.

## Questions to Keep in Mind

- **Why is linear regression inappropriate for predicting a qualitative response with three classes?**

  It forces an arbitrary numeric ordering and spacing between classes; different codings of the same categories produce fundamentally different models and predictions.

- **When would you choose QDA over LDA?**

  When class-specific covariance matrices clearly differ, when the decision boundary is moderately non-linear, or when n is large enough to absorb the extra parameters.

**What is confounding in logistic regression?**

When the relationship between a predictor and the response changes or reverses once other correlated predictors are added. Missing confounders leads to misleading conclusions about individual predictors.

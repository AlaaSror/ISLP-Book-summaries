# Chapter 3: Linear Regression

## Summary

Linear regression is a simple, interpretable baseline for supervised learning with quantitative responses. It is ideal for **baseline modeling** and **inference** (e.g., deciding how to allocate a budget across TV vs. Radio advertising).

**When it struggles:** Linear regression performs poorly when the true relationship is highly non-linear or when there are more predictors than observations. It strictly assumes the relationship is *additive* (predictors don't interact) and *linear* (constant slope), and that error terms are uncorrelated with constant variance.

**Interaction Terms** should be used when the effect of one predictor on the response depends on the value of another (a "synergy" effect). The **F-statistic** is necessary to address the multiple testing problem: examining individual p-values across many predictors guarantees false associations by pure chance.

## Important Notes

- **Common misunderstanding:** A variable isn't necessarily unimportant just because its individual p-value is high. In multiple regression, collinearity (highly correlated predictors) can inflate standard errors and mask a variable's true importance.
- **High leverage points** (unusual predictor values) can distort the regression line far more than standard outliers (unusual response values). Not all "weird" data points affect the model the same way.

## Questions to Keep in Mind

- **What does the F-statistic test in multiple linear regression?**

  It answers: "Does this set of variables, taken together, actually explain anything about the outcome?" The F-statistic checks whether your regression model is meaningfully better than a model with no predictors at all.

  - **Large F-value** → model explains a lot relative to noise → likely significant
  - **Small F-value** → model not much better than guessing the mean → not significant
  - Always pair the F-value with its p-value — never judge it in isolation.

- **How do interaction terms address the additive assumption?**

  They allow the effect of one predictor on the response to vary depending on the value of another predictor, relaxing the assumption that predictors act independently.

- **Why is the F-statistic better than looking at individual p-values when you have many predictors?**

  The F-statistic adjusts for the number of predictors. Examining only individual p-values leads to false discoveries (Type I errors) simply by chance.

**What is collinearity and why does it damage a linear model?**

Collinearity occurs when two or more predictors are highly correlated, making it difficult to separate their individual effects. This inflates standard errors and reduces the power to detect significant variables. Stepwise selection or regularization can help by dropping redundant predictors.

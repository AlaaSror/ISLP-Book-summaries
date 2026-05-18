# Chapter 8: Tree-Based Methods

## Summary

Tree-based methods model complex, non-linear relationships and interactions without requiring the rigid assumptions of linear models. They recursively partition the predictor space into non-overlapping regions and predict using the mean (regression) or majority class (classification) of observations in each region.

A **single decision tree** is highly interpretable but suffers from high variance — small changes in training data can produce entirely different tree structures. **Ensemble methods** overcome this instability.

## Ensemble Methods

| Method | Core Idea | Key Benefit |
|--------|-----------|-------------|
| **Bagging** | Train many trees on bootstrapped samples; average predictions | Reduces sensitivity to any single dataset |
| **Random Forests** | Like bagging, but also randomizes the predictor subset at each split | Reduces correlation between trees, lowers variance further |
| **Boosting** | Build trees sequentially, each correcting previous errors | Gradually improves accuracy with controlled flexibility |
| **BART** | Sum of many small trees with Bayesian regularization | Quantifies uncertainty; controls overfitting probabilistically |

## Important Notes

- **Single Decision Trees:** Best when explainability is paramount, or when dealing with qualitative predictors where creating dummy variables is undesirable.
- **Random Forests:** Use when you have many correlated predictors — forcing random predictor subsets prevents a few strong variables from dominating every tree.
- **Boosting:** Use when you want a highly accurate model built gradually. Shallow trees (depth-1 "stumps") create a highly interpretable additive model.
- **Axis-parallel splits:** Trees partition using axis-aligned splits, creating rectangular regions. This means trees may struggle with diagonal, smoothly varying, or globally linear relationships, often requiring many splits to approximate what simpler models capture directly.
- **Node impurity metrics:** In classification trees, classification error rate is *not* used to grow trees — it is insufficiently sensitive. Gini index or entropy are preferred as they better measure node purity.
- **Interpretability trade-off:** Ensemble methods substantially improve accuracy but sacrifice the interpretability of a single tree. Variable Importance measures how much each predictor contributes to reducing impurity across the ensemble.

## Questions to Keep in Mind

- **Why is recursive binary splitting considered a 'greedy' algorithm?**

  It makes the locally best split at each step to immediately minimize error, without looking ahead to consider whether a sub-optimal split now might lead to a much better tree overall.

- **How does Cost Complexity Pruning (weakest link pruning) find the right tree size?**

  It introduces a tuning parameter α that penalizes the tree for having too many terminal nodes, creating a sequence of subtrees that balance training fit against complexity. The optimal subtree is selected via cross-validation.

**What is Out-of-Bag (OOB) error estimation?**

A way to estimate test error for a bagged model without cross-validation. Each observation is predicted using only the subset of trees (~1/3) that did not use that observation in their bootstrap training set.

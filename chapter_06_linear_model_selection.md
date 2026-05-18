# Chapter 6: Linear Model Selection and Regularization

## Summary

When the number of predictors (*p*) is large relative to observations (*n*), least squares estimates have high variance and overfit. When p > n, OLS fails entirely — there are infinitely many solutions that perfectly fit the training data. **Shrinkage and selection methods** solve this by intentionally introducing a small amount of bias in exchange for a large reduction in variance, yielding lower overall test error.

## Selection Methods

| Method | Approach | Models Considered |
|--------|----------|-------------------|
| **Best Subset** | Fits every possible predictor combination | 2ᵖ (exhaustive but expensive) |
| **Forward Stepwise** | Greedily adds the single best predictor one at a time | ~p(p+1)/2 |
| **Backward Stepwise** | Starts with full model, removes least useful predictor iteratively | ~p(p+1)/2 (requires n > p) |

## Shrinkage Methods

- **Lasso** — Use when interpretability matters and you suspect only a few predictors drive the response. Lasso performs variable selection by forcing some coefficients exactly to zero (sparse model).
- **Ridge Regression** — Use when prediction accuracy is the priority and most variables are useful (small, roughly equal effects). Does not zero out coefficients.
- **Principal Components Regression (PCR)** — Use when predictors are highly correlated and a few underlying linear combinations capture most of the variation.

## Important Notes

- **Standardization is critical:** Ridge and Lasso depend heavily on predictor scale. If predictors are not standardized (zero mean, unit standard deviation), the penalty will unfairly shrink variables measured on smaller scales.
- **High R² ≠ good model:** In high-dimensional settings (p ≫ n), a model can reach R² ≈ 1.0 by fitting noise in the training data, causing severe overfitting and poor test performance.

## Questions to Keep in Mind

- **Why does Lasso produce sparse models (coefficients exactly zero), but Ridge does not?**

  Lasso uses an L1 penalty whose constraint region has sharp corners (like a diamond). The elliptical RSS contours frequently intersect these corners directly on the axes, forcing coefficients to zero. Ridge uses an L2 (circular) penalty, which has no sharp corners and therefore never sets coefficients exactly to zero.

- **Why must predictors be standardized before Ridge or Lasso?**

  The shrinkage penalty treats all coefficients equally. If variables are on different scales (e.g., distance in inches vs. miles), the penalty disproportionately affects variables based on measurement units rather than true predictive power.

**How does Partial Least Squares (PLS) improve upon PCR?**

PCR is unsupervised — it identifies dimensions that maximize variance in X without considering Y. PLS is supervised; it places the highest weight on variables most strongly related to Y when constructing new dimensions.

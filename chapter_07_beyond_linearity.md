# Chapter 7: Moving Beyond Linearity

## Summary

Linear regression is often a poor approximation of reality, but fully non-parametric approaches can be uninterpretable and data-hungry. Methods like splines and GAMs find a middle ground — they allow flexible, smooth non-linear curves without imposing a rigid global structure, while keeping the effects of distinct predictors interpretable.

**Regression Splines** create a flexible curve by dividing the predictor range into regions using **knots**, fitting separate low-degree polynomials in each region, and constraining them to join smoothly at the knots. Knot locations are typically placed at uniform quantiles of the data as a pragmatic default.

**Generalized Additive Models (GAMs)** extend linear regression by allowing each predictor's relationship with the response to be **non-linear**, while keeping the overall model additive and interpretable. Each predictor gets its own smooth functional form that can be visualized independently.

**Key advantage of splines over polynomials:** High-degree polynomials impose a single global shape — a small change in one region distorts the entire fit. Splines use piecewise local polynomials between knots, adapting smoothly to local structure without global distortion.

## Important Notes

- **Regression / Natural Splines:** Preferred for smooth non-linear relationships in a single predictor. Natural splines enforce linear behavior at the boundaries, reducing the risk of unstable predictions at the extremes of the data.
- **Step Functions:** Useful when a continuous variable has discrete interval-based effects or when domain knowledge suggests natural groupings (e.g., age groups). Simple but can create abrupt, unrealistic changes at bin boundaries.
- **GAMs:** Best when multiple predictors likely have non-linear effects but interpretability still matters. Each predictor's effect can be analyzed independently.
- **GAM limitation:** GAMs assume *additivity* — the effect of X₁ on Y does not depend on X₂. If important interactions exist, they will be missed unless manually added.
- **Common mistake:** Using a high-degree polynomial (e.g., d = 15) for flexibility. Polynomials enforce a global structure that distorts the fit at boundaries. Splines are preferred for their local flexibility.

## Questions to Keep in Mind

- **Why are Natural Cubic Splines generally preferred over standard Cubic Splines?**

  Standard splines can show wild, high-variance behavior at the outer ranges of the predictors. Natural splines force the function to be linear past the extreme knots, giving much more stable boundary estimates.

- **How does a Smoothing Spline differ from a Regression Spline?**

  Regression splines require manually selecting the number and placement of knots. A smoothing spline conceptually places a knot at every training observation and controls flexibility via a roughness penalty governed by a smoothing parameter λ, which balances fit against smoothness automatically.

- **What is the major limitation of a GAM?**

  The model is strictly additive. It cannot automatically capture interactions between variables unless the user manually builds interaction terms into the model.

**What happens if you make the span (s) very large in Local Regression?**

A very large s means almost all points are used to compute the fit, resulting in a smooth, global fit (essentially standard least squares). A very small s produces a highly localized, wiggly fit prone to overfitting.

# Chapter 10: Deep Learning

## Summary

Deep learning uses neural networks with many layers to model highly complex, non-linear relationships directly from raw data. Unlike traditional statistical learning, **deep learning automatically learns useful representations** from the data itself through layered transformations — no manual feature engineering required.

The foundation is the **feed-forward neural network**: inputs pass through hidden layers of linear combinations followed by **non-linear activation functions**. Activation functions are essential — without them, the entire network collapses into a single linear model regardless of depth.

## Architecture Guide

| Architecture | Designed For | Key Mechanism |
|-------------|-------------|---------------|
| **Feed-Forward (Dense)** | General tabular/structured data | Fully connected layers with activation functions |
| **CNN** | Image / spatial data | Local convolution filters + pooling for spatial patterns |
| **RNN** | Sequential data (text, time-series) | Hidden state updated sequentially; captures temporal dependencies |

**Why CNNs for images:** Standard dense networks destroy spatial structure when pixels are flattened. CNNs apply convolution filters locally, preserving spatial relationships and sharing weights across positions, dramatically reducing parameters.

**Why RNNs for sequences:** RNNs maintain a hidden state that carries context from earlier inputs to future predictions, enabling the model to capture temporal dependencies and variable-length sequences efficiently via weight sharing.

## Important Notes

- Non-linear activation functions are non-negotiable — without them, stacking layers is mathematically identical to a single linear transformation.
- Deep learning models are often heavily **over-parameterized** and require aggressive regularization: **dropout** (randomly disabling neurons during training) and **data augmentation** (realistic transformations of training examples).
- Despite over-parameterization, deep learning can still generalize well when combined with proper regularization.
- **The "double descent" phenomenon:** Test error can decrease *again* after the model becomes complex enough to perfectly interpolate the training data.
- For standard tabular datasets, simpler methods (linear regression, random forests, gradient boosting) often achieve comparable performance with far greater interpretability and much lower computational cost.

## Questions to Keep in Mind

- **Why are non-linear activation functions necessary in neural networks?**

  Without them, the network collapses into a single linear model regardless of how many hidden layers are added.

- **Why are CNNs better suited for image data than standard feed-forward networks?**

  CNNs preserve spatial structure by applying local convolution filters and weight sharing, allowing nearby pixels to be processed together rather than independently.

- **What is the purpose of pooling layers in CNNs?**

  Pooling layers reduce the dimensionality of feature maps while preserving the most important information, improving computational efficiency and location invariance.

- **Why are RNNs considered suitable for sequential data?**

  RNNs maintain a hidden state that allows previous observations to influence future predictions, capturing temporal dependencies and contextual meaning.

- **Why is deep learning often unnecessary for standard tabular datasets?**

  Simpler models such as linear regression, random forests, or gradient boosting often achieve similar performance while being faster to train, easier to tune, and more interpretable.

**What is the double descent phenomenon?**

Test error initially follows the classical bias-variance trade-off curve, but then decreases *again* after the model becomes complex enough to perfectly fit the training data.

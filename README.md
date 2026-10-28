# Transmitter Weight Modulation (TWM)

## Abstract

Artificial neural networks (ANNs) typically use backpropagation to compute gradients for directly updating their weights and biases. However, improving learning performance, adaptability, and robustness under changing data distributions remains an important challenge. This motivates exploring whether biologically inspired learning rules can provide alternative mechanisms for training ANNs.

We introduce a learning rule, Transmitter Weight Modulation (TWM), derived from a neurophysiological model of transmitter dynamics. This rule uses latent weights and biases, together with trainable modulation parameters, to generate the emitted weights and biases used during forward propagation. Our approach provides an alternative mechanism for training ANNs by optimizing the trainable parameters within the rule, thereby indirectly updating the emitted weights and biases. The rule also provides a biologically inspired interpretation based on transmitter recovery and activity-dependent depletion.

Preliminary experiments comparing TWM with conventional direct weight and bias learning using the same underlying neural network architectures suggest improvements in learning performance when training from scratch, as well as adaptability and robustness under continual learning with changing data distributions. These findings indicate the potential of TWM as a general learning rule for ANN training.

## Preliminary results

See [the retained preliminary results](docs/preliminary-results.md) for image-classification tables, their observation dates, and comparison limitations.

The abstract reproduces the author-designated manuscript wording. The public tables provide partial evidence and do not independently establish every claim in the abstract.

This repository currently shares the manuscript abstract and preliminary results. Code and checkpoints are not included.

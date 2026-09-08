# Transmitter Weight Modulation

Most neural networks are trained using backpropagation to compute gradients and an optimizer to update their weights and biases directly. **Transmitter Weight Modulation (TWM)** explores a different approach: using a transmitter update rule to adapt weights and biases indirectly, while retaining backpropagation for learning.

Our pilot results show that this approach can support learning in both convolutional networks and vision transformers. We report preliminary image-classification results on CIFAR-100 and partial results on ImageNet-1K. These findings motivate further investigation, with matched comparisons needed to establish whether the approach offers an advantage over conventional training.

## CIFAR-100

Validation accuracy (%). Multi-seed values are mean ± sample standard deviation.

| Model | Method | Epochs | Seeds | Best | Final |
| --- | --- | ---: | --- | ---: | ---: |
| ResNet-50 | Plain reference | 200 | 42, 43, 44 | 79.64 ± 0.23 | 79.44 ± 0.27 |
| ResNet-50 | TWM (ReLU) | 200 | 42, 43, 44 | 80.76 ± 0.34 | 80.63 ± 0.32 |
| ViT-B/16 | Plain reference | 300 | 42 | 71.30 | 71.08 |
| ViT-B/16 | TWM (ReLU) | 300 | 42, 43, 44 | 74.91 ± 0.21 | 74.81 ± 0.18 |
| ConvNeXt-Small | Plain, historical | 300 | 42 | 67.87 | 67.85 |
| ConvNeXt-Small | TWM, historical | 300 | 42 | 69.70 | 69.60 |

Plain references differ in configuration or seed coverage. ConvNeXt values are historical reports; original artifacts are unavailable. These are preliminary comparisons, not confirmed performance gains.

## ImageNet-1K: ResNet-50 (incomplete)

| Method | Seed | Completed epochs | Best Top-1 (%) |
| --- | ---: | ---: | ---: |
| Plain | 42 | 149 / 300 | 62.08 |
| TWM (ReLU) | 42 | 109 / 300 | 73.38 |

Latest retained records checked on 2026-09-08; different epoch counts prevent a matched comparison.

Results only; code and checkpoints are not included.

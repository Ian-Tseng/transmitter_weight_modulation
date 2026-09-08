# Transmitter Weight Modulation

Conventional neural network training uses backpropagation to compute gradients and an optimizer to update the weights and biases used directly in the forward pass. **Transmitter Weight Modulation (TWM)** explores an alternative parameter-update approach: a transmitter update rule generates the effective weights and biases from trainable latent parameters and a recurrent state derived from previous effective parameters. Backpropagation and the optimizer remain part of training, while the weights and biases used by the network evolve indirectly through this rule.

Our pilot results show that this approach can train both a convolutional network and a vision transformer on CIFAR-100. Across three seeds, the ReLU persistent-state variant reached a mean best validation accuracy of **80.76% with ResNet-50** and **74.91% with ViT-B/16**. Additional ConvNeXt-Small results are reported below with their experimental settings and evidence status. These findings support further investigation of transmitter-based parameter updates. Establishing an advantage over conventional training requires matched baseline experiments and broader validation.

## Completed ReLU persistent-state pilots

These CIFAR-100 results use the **ReLU persistent-state variant**, recorded as `TX-persistent-S-transform` with `tx_s_anchor_transform=relu`. They describe this specific variant, rather than every TWM configuration.

| Architecture | Epochs per seed | Seeds | Best validation accuracy | Final validation accuracy |
| --- | ---: | --- | ---: | ---: |
| ResNet-50 | 200 | 42, 43, 44 | 80.76% ± 0.34% | 80.63% ± 0.32% |
| ViT-B/16 | 300 | 42, 43, 44 | 74.91% ± 0.21% | 74.81% ± 0.18% |

Values are mean ± sample standard deviation across seeds. Best is each seed's highest recorded validation accuracy; final is its accuracy at the last completed epoch. Both experiments used FP32 with AMP disabled.

These are completed pilot screens, not yet eligible for the project's formal paper tables. They do not establish a matched baseline benefit, stability advantage, or general scaling result. In this variant, validation is recurrent: effective parameters evolve across validation batches without gradient or optimizer updates, and the saved training state is restored afterward.

## ImageNet-1K: ResNet-50 progress (incomplete)

| Method | Seed | Completed epochs | Best validation Top-1 accuracy so far |
| --- | ---: | ---: | ---: |
| TWM, ReLU persistent-state | 42 | 109 / 300 | 73.38% |
| Conventional training (Plain) | 42 | 149 / 300 | 62.08% |

These are the latest retained completed-epoch records checked on 2026-09-08. They are incomplete single-seed results at different epoch counts, not a final or matched performance comparison.

## ConvNeXt-Small: historical 300-epoch results

The project result register preserves the following CIFAR-100 values for seed 42. The original checkpoint/log sources are no longer available, so these historical reported values cannot currently be reverified from the original artifacts. The TX row has a historical configuration; it is not identified as the ReLU persistent-state variant above.

| Architecture | Method | Epochs reported | Seed | Best validation accuracy | Final validation accuracy |
| --- | --- | ---: | ---: | ---: | ---: |
| ConvNeXt-Small | Conventional training (Plain) | 300 | 42 | 67.87% | 67.85% |
| ConvNeXt-Small | Historical TX | 300 | 42 | 69.70% | 69.60% |

These values provide historical context, not a verified matched comparison or a three-seed aggregate.

## Retained source-policy experiment

A separate 64-epoch CIFAR-100 screen compared two sources for transmitter modulation: parameter/state-derived (`existing_weight`) and activation-derived (`activation`). All rows use seed 42 and a historical validation protocol. They are distinct from the ReLU persistent-state pilots and the 300-epoch ConvNeXt-Small experiment.

| Architecture | Source policy | Best validation accuracy | Final validation accuracy |
| --- | --- | ---: | ---: |
| ViT-B/16 | Parameter/state-derived | 71.72% | 71.53% |
| ViT-B/16 | Activation-derived | 70.92% | 70.85% |
| ConvNeXt-Small | Parameter/state-derived | 62.54% | 62.53% |
| ConvNeXt-Small | Activation-derived | 62.89% | 62.71% |

The retained report validates all four 64-epoch metric histories. Checkpoint and completion artifacts are incomplete. The different preferred sources across architectures are a screening observation requiring multi-seed confirmation.

## Results files

- [Per-seed ReLU pilot results](results/pilot_results.csv)
- [Historical ConvNeXt-Small results](results/convnext_historical.csv)
- [Source-policy screening results](results/source_policy_screen.csv)
- [ImageNet-1K progress](results/imagenet1k_progress.csv)
- [Result provenance and experiment identities](results/provenance.json)

This repository shares the project introduction and pilot-result summaries only. Training code, datasets, model weights, and checkpoints are not included.

# Preliminary results

Most neural networks are trained using backpropagation to compute gradients and an optimizer to update their weights and biases directly. **Transmitter Weight Modulation (TWM)** explores a different approach: using a transmitter update rule to adapt weights and biases indirectly, while retaining backpropagation for learning.

Our pilot results show that this approach can support learning in both convolutional networks and vision transformers. We report preliminary image-classification results on CIFAR-100 and partial results on ImageNet-1K. These findings motivate further investigation, with matched comparisons needed to establish whether the approach offers an advantage over conventional training.

## CIFAR-100

Validation accuracy (%). Multi-seed values are mean ± sample standard deviation.

| Model | Method | Epochs | Seeds | Best | Final |
| --- | --- | ---: | --- | ---: | ---: |
| ResNet-50 | Plain reference | 200 | 42, 43, 44 | 79.64 ± 0.23 | 79.44 ± 0.27 |
| ResNet-50 | TWM (ReLU) | 200 | 42, 43, 44 | **80.76 ± 0.34** | **80.63 ± 0.32** |
| ViT-B/16 | Plain reference | 300 | 42 | 71.30 | 71.08 |
| ViT-B/16 | TWM (ReLU) | 300 | 42, 43, 44 | **74.91 ± 0.21** | **74.81 ± 0.18** |
| ConvNeXt-Small | Plain (repeat x3) | 300 | 42, 43, 44 | 68.68 ? 0.47 | 68.49 ? 0.46 |
| ConvNeXt-Small | TWM (ReLU, repeat x3) | 300 | 42, 43, 44 | 68.77 ? 0.93 | 68.57 ? 1.01 |

Plain references differ in configuration or seed coverage. These are preliminary comparisons, not confirmed performance gains. ConvNeXt-Small now uses the retained three-seed histories imported on 2026-09-28 and rechecked on 2026-10-28; its previous single-seed values are superseded in this table.

## ConvNeXt-Small: updated preliminary evidence

CIFAR-100, 300 epochs, FP32, repeated augmentation x3. All six saved histories contain 300 validation entries; best and final values were recomputed from those arrays. Summary values above are mean ? sample standard deviation across seeds 42/43/44.

| Seed | Plain best (%) | TWM best (%) | Plain final (%) | TWM final (%) |
| --- | ---: | ---: | ---: | ---: |
| 42 | 69.01 | 69.83 | 68.88 | 69.73 |
| 43 | 68.14 | 68.14 | 67.98 | 67.90 |
| 44 | 68.90 | 68.33 | 68.62 | 68.09 |

The mean TWM-minus-Plain differences are +0.083 percentage points for best accuracy and +0.080 for final accuracy. Results vary by seed and do not establish a consistent advantage.

Provenance: retained `cifar100_convnext_small_plain_tx_relu_persistent_s42-44_e300_fp32_v1` run group. [Per-seed summary](convnext-small-cifar100.csv). Dataset fingerprints were not recorded, copied trainer hashes differ across seeds, and source-equivalence review remains pending. Checkpoints were integrity-hashed during import but were not reopened for this publication update. These results remain preliminary and are not pooled with no-repeat runs.

The earlier seed-42 report-only values (Plain best/final 67.87/67.85%; TWM 69.70/69.60%) describe a separate historical run whose original artifacts are unavailable. They are not part of the three-seed aggregate above.

## ImageNet-1K: ResNet-50 (incomplete)

| Method | Seed | Completed epochs | Best Top-1 (%) |
| --- | ---: | ---: | ---: |
| Plain | 42 | 149 / 300 | 62.08 |
| TWM (persistent ReLU) | 42 | 109 / 300 | **73.38** |

Retained checkpoint audit dated 2026-10-07 records Plain 62.078% at epoch149 and TWM 73.384% at epoch109 (rounded above). Different epoch counts and weight decay prevent a matched comparison. Both the ResNet-50 and ViT-B/16 TWM rows use persistent raw-S ReLU; their Plain references do not.

## ImageNet-1K: ViT-B/16 (incomplete)

| Method | Seed | Completed epochs | Best Top-1 (%) | Latest completed Top-1 (%) |
| --- | ---: | ---: | ---: | ---: |
| Plain | 42 | 61 / 300 | 64.430 | 64.430 |
| TWM (persistent ReLU) | 42 | 43 / 300 | 71.206 | 71.206 |

Retained checkpoint metadata and validation histories were reopened on CPU on 2026-10-28. Best values occur at epochs 61 and 43, respectively. Partial training batches are excluded. These are incomplete single-seed results, not final 300-epoch outcomes.

The runs have unequal epoch budgets and different weight decay (Plain 0.05; TWM 0.0), and use a historical legacy-padding configuration. The +6.776 percentage-point best-accuracy difference is descriptive, not evidence of an equal-budget or matched-recipe advantage. Seeds 43/44 have no results in this snapshot. This update checked stored scalar/history consistency; it did not rerun evaluation or scan every checkpoint tensor. Do not pool these values with canonical padding-0 experiments.

Results only; code and checkpoints are not included.

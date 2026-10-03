# Preliminary Experiment Results

These are my first results for the SPE3R pretraining experiment.

I trained Model A and Model B on one GPU with a physical batch size of 2. The intended setup uses a batch size of 16, so this first run made around eight times more optimizer updates per epoch.

Because of that, I do not consider this a fair final comparison and I decided to repeat the experiments with the same setup.

## Models

- **Official SPNv2:** checkpoint released by the SPNv2 authors
- **Model A:** ImageNet -> SPEED+ Tango
- **Model B:** ImageNet -> SPE3R -> SPEED+ Tango
- **Random seed:** 2021
- **Evaluation:** frozen testing on SPEED+ Lightbox and Sunlamp

## Results

| Model | Test domain | Orientation error | Translation error | Final pose score |
|---|---|---:|---:|---:|
| Official SPNv2 | Lightbox | 6.442 deg | 0.175 m | 0.141 |
| Official SPNv2 | Sunlamp | 10.878 deg | 0.225 m | 0.227 |
| Model A | Lightbox | about 13.0 deg | 0.392 m | 0.287 |
| Model A | Sunlamp | about 19.0 deg | 0.327 m | 0.389 |
| Model B | Lightbox | about 15.6 deg | 0.465 m | 0.343 |
| Model B | Sunlamp | about 30.3 deg | 0.545 m | 0.618 |

Lower is better for all three metrics.

## What I found

The official SPNv2 checkpoint gave strong results using the same local evaluation pipeline. This helped confirm that the dataset, labels, evaluation code and metrics were working correctly.

Model A did not reproduce the official checkpoint performance.

Model B was worse than Model A in this first setup, but I do not want to make a conclusion about SPE3R pretraining from this run because the training setup was not controlled correctly.

I also recalibrated the BatchNorm statistics of Model A using synthetic Tango images without changing the learned weights.

The Lightbox pose score improved from about **0.287 to 0.257**, but it was still worse than the official SPNv2 result of **0.141**.

This suggests that BatchNorm statistics were part of the problem, but not the only reason for the performance gap.

## Next experiment

I will repeat Model A and Model B with the same controlled setup:

- 1 NVIDIA A100 80GB
- Target batch size 16
- No DistributedDataParallel
- No SyncBatchNorm
- Same optimization and Tango training settings for both models
- Frozen Lightbox and Sunlamp evaluation after training

The large per-image raw logs from the first runs are not included in this public repository. I kept the aggregate results here instead.

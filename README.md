# SPNv2 + SPE3R Pretraining Research

I am using this repository for my research on spacecraft pose estimation.

I started from the original SPNv2 implementation by Tae Ha Park and the SLAB Group, and I extended it to study whether pretraining on SPE3R can help before training on SPEED+.

Original SPNv2 repository: https://github.com/tpark94/spnv2

## What I added

- SPE3R dataset support
- SPE3R pretraining pipeline
- A rotation loss for the SPE3R setup
- Changes to the training and inference code
- A tool to transfer the SPE3R-trained EfficientNet and BiFPN weights into the Tango SPNv2 model
- Style augmentation generation for SPEED+ training images
- Experiment configurations for Model A and Model B
- Frozen Lightbox and Sunlamp evaluation
- Preliminary result tracking

## Experiment idea

I compare two training pipelines:

**Model A:** ImageNet -> SPEED+ Tango

**Model B:** ImageNet -> SPE3R -> SPEED+ Tango

The goal is to check whether SPE3R pretraining improves the final spacecraft pose estimation performance.

## Current results

The first single-GPU experiments were not a fair final comparison because I used a physical batch size of 2 instead of the intended batch size of 16. This caused many more optimizer updates per epoch.

Because of that, I am treating these results as preliminary and I decided to repeat the experiments using the same controlled setup for both models.

The current results and notes are in:

```text
results/README.md
```

## Main research files

```text
core/dataset/SPE3RDataset.py
core/engine/trainer.py
core/nets/loss/rotation_loss.py
tools/create_spe3r_tango_init.py
tools/generate_speedplus_styles.py
experiments/
results/
```

## Installation

Install PyTorch first, then:

```bash
pip install -r requirements.txt
```

The project uses the original SPNv2 codebase, so the SPEED+ setup and the original model requirements still apply.

## Credit

This work is based on the original SPNv2 implementation by Tae Ha Park and the Space Rendezvous Laboratory (SLAB), Stanford University.

SPNv2 paper:

Tae Ha Park and Simone D'Amico, "Robust multi-task learning and online refinement for spacecraft pose estimation across domain gap", Advances in Space Research, 2023.

I kept the original MIT license and copyright notice in `LICENSE.md`.

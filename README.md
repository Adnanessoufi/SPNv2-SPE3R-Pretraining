# SPNv2 + SPE3R Pretraining Research

I am using this repository for my research on spacecraft pose estimation.

I started from the original SPNv2 implementation and I extended it to study if SPE3R pretraining can help before training on SPEED+.

Original SPNv2 repository: https://github.com/tpark94/spnv2

## What I added

- SPE3R dataset support
- SPE3R pretraining
- Rotation loss for the SPE3R setup
- Changes in the training and inference pipeline
- A tool to transfer the SPE3R-trained EfficientNet and BiFPN weights into SPNv2
- Style augmentation generation for SPEED+ images
- Experiment files for the different training setups
- Lightbox and Sunlamp evaluation
- Preliminary result tracking

## What I am comparing

I am comparing two main models:

**Model A:** ImageNet -> SPEED+ Tango

**Model B:** ImageNet -> SPE3R -> SPEED+ Tango

The main question is whether SPE3R pretraining can improve the final spacecraft pose estimation results.

## Current status

I already ran preliminary experiments, but the first setup used a physical batch size of 2 instead of the intended batch size of 16.

Because of that, I do not consider those results a fair final comparison. I am repeating the experiments with the same controlled setup for both models.

The current results and notes are here:

```text
results/README.md
```

## Main files I added or changed

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

The original SPNv2 code uses `tangoPoints.mat`. I keep a note under `core/utils/models/` with the upstream link for that file.

## Credit

This work is based on the original SPNv2 implementation by Tae Ha Park and the Space Rendezvous Laboratory (SLAB), Stanford University.

Original paper:

Tae Ha Park and Simone D'Amico, "Robust multi-task learning and online refinement for spacecraft pose estimation across domain gap", Advances in Space Research, 2023.

The original MIT license and copyright notice are kept in `LICENSE.md`.

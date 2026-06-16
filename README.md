# FlowFake: Liquid Networks for Audio Deepfake Detection

[![Status](https://img.shields.io/badge/Status-Accepted-success)](#)
[![Venue](https://img.shields.io/badge/ICML%202026-ML4Audio%20Workshop-blue)](#)
[![Task](https://img.shields.io/badge/Task-Audio%20Deepfake%20Detection-orange)](#)
[![Model Size](https://img.shields.io/badge/Parameters-~34K-purple)](#)

FlowFake is a lightweight audio deepfake detector built on **Liquid Time-Constant (LTC)** networks.
It is designed to generalize across datasets by learning **temporal speech dynamics** rather than dataset-specific spectral fingerprints.

> **Paper:** *FlowFake: Liquid Networks for Audio Deepfake Detection*  
> **Status:** Accepted at the **ICML 2026 ML4Audio Workshop**

---

## Project Overview

Existing audio deepfake detectors often degrade under cross-dataset evaluation because they overfit to spectral artifacts tied to specific datasets.

FlowFake addresses this by modeling synthetic speech as **multi-timescale trajectory anomalies** in continuous-time hidden dynamics:

- frame-level spectral discontinuities
- prosodic inconsistencies
- abnormal temporal evolution

Instead of relying only on fixed-context transformers or CNNs, FlowFake uses a **continuous-time neural ODE** with adaptive per-neuron time constants.

---

## Core Idea

Natural speech follows physical articulatory dynamics, while synthetic speech frequently violates those dynamics.

FlowFake captures these violations through LTC dynamics:

- **Fast neurons** capture short-timescale artifacts (~10–100 ms)
- **Slow neurons** capture long-timescale prosodic cues (~100 ms–2 s)

This separation allows robust spoof detection under distribution shift.

---

## Architecture

### Pipeline

```text
Audio Waveform
→ Log-Mel Spectrogram
→ Conv1D Feature Extractor
→ LTC-ODE Temporal Module
→ RK4 Solver
→ Classifier
→ Bonafide / Spoof
```

### LTC Cell Dynamics

The LTC cell combines:

- external input current (**I_ext**)
- recurrent synaptic current (**I_syn**)
- leak current (**I_leak**)

ODE integration is performed with **RK4** using **two unfolds per frame**.

### Architecture Figure

> Replace this placeholder with the final model diagram.

![FlowFake Architecture Placeholder](https://placehold.co/1200x420?text=FlowFake+Architecture+Figure+Placeholder)

---

## Repository Structure

```text
FlowFake/
├── ASV19/
├── FOR/
├── ITW/
└── MLAADv1/
```

These folders contain dataset-specific training/evaluation scripts and logs for cross-dataset deepfake detection experiments.

---

## Citation

If you use FlowFake in your research, please cite:

```bibtex
@inproceedings{flowfake2026,
  title     = {FlowFake: Liquid Networks for Audio Deepfake Detection},
  author    = {Anonymous},
  booktitle = {ICML 2026 Workshop on Machine Learning for Audio (ML4Audio)},
  year      = {2026}
}
```

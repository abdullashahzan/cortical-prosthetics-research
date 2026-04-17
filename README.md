# Cortical Visual Prosthetics Research — Abdulla Shahzan

> **Building the encoding pipeline that lets blind people see.**
> This repository is an index of my independent research in cortical visual prosthetics.
> Each paper below is a self-contained contribution to a single end-to-end system:
> from biological simulation → transfer learning → learned stimulus optimisation.

---

## About This Research

I am a Computer Engineering student at King Khalid University (Abha, Saudi Arabia) working independently on **cortical visual prosthetics** — devices that restore partial sight by electrically stimulating the primary visual cortex (V1).

The central problem I am trying to solve is the **encoding problem**: given a camera frame and a fixed electrode array implanted in V1, which activation pattern produces the most useful visual percept for the patient?

Every paper in this series builds one piece of that pipeline:

```
Camera frame
     │
     ▼
[ Encoder Network ]   ← Paper 3: learned, end-to-end optimised
     │
     ▼
[ Phosphene Simulator ]   ← Paper 2: differentiable, biologically plausible
     │
     ▼
[ Phosphene Images ]
     │
     ▼
[ Recognition / Oracle ]   ← Paper 1: transfer learning baseline
     │
     ▼
Perceived phosphene pattern
```

The papers are designed to be read in order, each building directly on the previous one.

---

## Published Papers

### Paper 3 — Adaptive Phosphene Encoding via Learned Stimulus Optimisation
**The encoder that replaces brightness mapping with a learned convolutional network.**

> *Cortical Visual Prosthetics · End-to-End Optimisation · Stimulus Encoding*

- Introduces a two-phase training framework: oracle domain alignment (Phase 1) followed by encoder training through the frozen simulator-oracle pipeline (Phase 2)
- Lightweight convolutional encoder (217,636 parameters) trained end-to-end through the frozen V1 simulator and a phosphene-aware EfficientNet oracle
- Achieves **61.0% classification accuracy** on CIFAR-10 versus **46.4% for brightness mapping** (+14.6 percentage points)
- Electrode budget experiment: adaptive encoder at **50 electrodes outperforms brightness mapping at 200 electrodes** by 46 points — direct clinical implication for surgical risk
- Sparsity regulariser reduces mean electrode activation by **~40%**, lowering charge injection independently of recognition performance

📄 **[Read Paper 3 →](https://github.com/abdullashahzan/phosphene-encoder)**

---

### Paper 2 — Biologically Plausible Differentiable Phosphene Simulation for Cortical Visual Prostheses
**The simulator: the first fully differentiable PyTorch phosphene simulator.**

> *Phosphene Simulation · Cortical Magnification · Differentiable Rendering*

- Models **cortical magnification** via differentiable spatial warping using the Schwartz (1980) log-polar retinotopic map — the first simulator to do this in a differentiable framework
- Models **temporal phosphene decay** (τ = 0.5 s) consistent with psychophysical measurements of phosphene fade
- Variable phosphene morphology across three Gaussian shape templates (circular, horizontal ellipse, vertical ellipse)
- **10% stochastic electrode dropout** modelling real-world electrode-tissue interface degradation
- Fully end-to-end differentiable — gradients flow back through the entire simulator to any upstream encoder network
- Runs at **~15 ms per image** on GPU, supporting real-time video applications

📄 **[Read Paper 2 →](https://github.com/abdullashahzan/phosphene-simulation-bionic-eye)**

---

### Paper 1 — Transfer Learning for Phosphene-Based Object Recognition in Cortical Visual Prostheses
**The recognition baseline: do ImageNet features survive phosphene degradation?**

> *Transfer Learning · EfficientNet · Phosphene Recognition · CIFAR-10*

- Designs a six-stage phosphene simulation pipeline (grayscale → blur → downsample → threshold → noise → RGB) applied to CIFAR-10
- Compares EfficientNet-B0 fine-tuned from ImageNet weights against random initialisation under identical conditions
- **ImageNet pretrained: 69.21%** vs. **random init: 62.31%** — a 6.90 pp final gap
- The **epoch-1 gap of 20.67 points** (before significant fine-tuning) demonstrates that ImageNet edge detectors survive phosphene degradation
- Establishes the recognition oracle used as the reward signal in Paper 3

📄 **[Read Paper 1 →](https://github.com/abdullashahzan/phosphene-transfer-learning-bionic-eye)**

---

## Research Roadmap

| Paper | Status | Contribution |
|-------|--------|--------------|
| Paper 1 — Transfer Learning Baseline | ✅ Published | Phosphene recognition oracle |
| Paper 2 — Differentiable Simulator | ✅ Published | Biologically plausible V1 simulation |
| Paper 3 — Adaptive Encoder | ✅ Published | End-to-end learned stimulus optimisation |
| Paper 4 — Temporal Dynamics *(planned)* | 🔬 In progress | Temporal phosphene differential equation model |


## Contact

**Abdulla Shahzan**
Department of Computer Engineering, King Khalid University, Abha, Saudi Arabia
📧 abdullashahzan@gmail.com
🐙 [github.com/abdullashahzan](https://github.com/abdullashahzan)

---

*This research is dedicated to every patient waiting for cortical prosthetics to cross the threshold from proof-of-concept to clinical utility.*

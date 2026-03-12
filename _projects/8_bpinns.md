---
layout: page
title: "Bayesian Physics-Informed Neural Networks"
description: From-scratch implementation of Bayesian PINNs with HMC sampling for uncertainty quantification in PDE solving.
img: assets/projects/BPINNs/cover-pic.png
importance: 3
category: academic projects
github: https://github.com/rubenifrah/B-PINNs
tags: [Bayesian, deep-learning, Research]
---

End-of-semester research project for the **Bayesian Machine Learning** course of the **M2 IASD** program. A from-scratch implementation and extension of **B-PINNs** (*Yang et al., 2020*), built entirely in PyTorch — including a custom **Hamiltonian Monte Carlo (HMC)** sampler and Bayesian neural network architectures.

[Read the original article (PDF)](/assets/projects/BPINNs/Bayesian-PINNs.pdf) &nbsp;·&nbsp; [Read our report (PDF)](/assets/projects/BPINNs/report.pdf) &nbsp;·&nbsp; [View presentation (PDF)](/assets/projects/BPINNs/presentation-slides.pdf)

<div class="row justify-content-center">
  <div class="col-md-10 mt-3">
    {% include figure.liquid loading="eager" path="assets/projects/BPINNs/bpinn_unknown_noise_10000_2000_0.0005_50_-2.3_80.png" title="Hierarchical B-PINN result" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  Hierarchical B-PINN with inferred noise level. The model jointly learns the PDE solution and the noise parameter, yielding calibrated ±2σ uncertainty bands even under significant observational noise.
</div>

---

## Motivation

Standard PINNs solve PDEs by enforcing physics as a soft loss constraint, but produce **point estimates** with no sense of uncertainty — they overfit badly under noisy sensor data. B-PINNs extend this into a Bayesian framework: network weights are treated as random variables, yielding a **distribution of solutions** with calibrated confidence intervals.

## What We Built

- **HMC sampler** implemented from scratch for posterior sampling over neural network weights.
- **Standard B-PINN** replicating Yang et al. on the 1D Poisson equation and damped harmonic oscillator.
- **Hierarchical B-PINN** that jointly infers the noise level — acting as an adaptive regularizer in high-noise regimes.
- **Physics-Informed Gaussian Processes (PI-GPs)** as an infinite-width analytical baseline, derived via the NNGP correspondence.

## Key Findings

- In **high-noise regimes**, standard PINNs overfit the noise; B-PINNs and Hierarchical B-PINNs maintain robust uncertainty bands.
- In **low-noise regimes**, standard PINNs converge cleanly; B-PINNs maintain full coverage (100% PICP) but navigate a sharper posterior.
- **PI-GPs** are mathematically elegant but over-smooth complex dynamics — confirming that finite-width B-PINNs with active representation learning are empirically essential.

*With **Anouk Ruer** and **Pénélope Forcioli**.*

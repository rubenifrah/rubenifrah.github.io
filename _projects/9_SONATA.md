---
layout: page
title: Reproducibility and Critical Analysis of SONATA
description: An empirical evaluation of the geometric shortcut in 3D self-supervised learning, analyzing dense point representations of the Sonata architecture.
img: assets/projects/sonata/sonata_picture.png
importance: 3
category: academic projects
github: https://github.com/rubenifrah/SONATA-project
tags: [Computer Vision, deep learning]
---

This project is a reproducibility study and critical analysis of the CVPR 2025 paper *Sonata: Self-Supervised Learning of Reliable Point Representations*. It addresses a fundamental issue in 3D computer vision:

> Do dense, point-level features in 3D self-supervised models genuinely learn abstract semantics, or do they secretly memorize absolute spatial coordinates?

This work was carried out as a research project for the **Perception** course in the **M2 IASD** program at Dauphine-PSL, by **Ruben Ifrah**.

[Read the full report (PDF)](/assets/projects/sonata/report.pdf)

[Read the original paper (PDF)](https://arxiv.org/pdf/2503.16429)

---

## Motivation

3D self-supervised learning (SSL) often suffers from the **geometric shortcut**, where networks heavily encode low-level spatial coordinates rather than learning high-level, meaningful semantics. Because point clouds are sparse, 3D operators must directly ingest $(x, y, z)$ coordinates, making it incredibly difficult to mask out spatial information during pre-training.

Sonata proposes to fix this by stripping away the traditional U-Net decoder and using a parameter-free "feature up-casting" mechanism combined with DINOv2-style self-distillation. This project empirically evaluates whether this architecture truly breaks the shortcut at the final dense representation stage.

## Experimental Methodology

To test Sonata's claims, we built a rigorous probing pipeline on the MesoNET (Juliet) computing cluster:

### 1. The Synthetic Sanity Check
Before testing Sonata, we validated our evaluation metrics on a synthetic 12,000-point cloud. We proved that a linear regression probe ($R^2$) and correlation metrics (Pearson/Spearman) could successfully distinguish between a "lazy" network that memorized geometry and a "smart" network structured around semantic clusters.

### 2. Real-World Feature Extraction
We ran an unseen indoor scan (`indoor_scan.ply`, 273,530 points) through the pre-trained 108M-parameter Sonata backbone (PointTransformerV3) on an NVIDIA A100 GPU to extract the dense, 1088-dimensional features.

### 3. Geometric Probing
We attempted to linearly reconstruct the absolute $(x, y, z)$ coordinates strictly from Sonata's final up-casted feature vectors.

## Visual Evidence: The PCA Gradient

<div class="row justify-content-center">
  <div class="col-sm-6 mt-3">
    <img src="/assets/projects/sonata/cc_indoor_scan.png" alt="Original Indoor Scan" class="img-fluid rounded z-depth-1">
  </div>
  <div class="col-sm-6 mt-3">
    <img src="/assets/projects/sonata/cc_indoor_scan_pca.png" alt="PCA Projection of Dense Features" class="img-fluid rounded z-depth-1">
  </div>
</div>
<div class="caption">
  Left: The original indoor point cloud. Right: A 6-component Zero-Shot PCA projection of Sonata's dense up-casted features. <em>Notice how the colors form continuous spatial gradients across the room rather than grouping into discrete semantic object clusters.</em>
</div>

## Key Results

- **High Predictability Remains:** A simple linear probe on Sonata's dense features predicted absolute spatial coordinates with **$R^2 = 0.988$**. The final representations remain highly predictive of raw geometry.
- **Distributed Leakage:** While no single feature dimension directly copied the coordinates (indicated by a low maximum Pearson correlation of 0.219), the linear combination of the 1088-dimensional ensemble perfectly reconstructed physical space.
- **Architectural Insight:** The results are consistent with the hypothesis that Sonata's **parameter-free feature up-casting** mechanism—which relies on inverse pooling indices defined by local geometric proximity—preserves or reintroduces substantial low-level spatial dependence. 
- **Conclusion:** While Sonata's latent coarse features may be highly semantic, dense feature construction pipelines in 3D SSL require careful evaluation to ensure they do not collapse back into the geometric shortcut.
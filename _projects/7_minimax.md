---
layout: page
title: Minimax Estimation of Distances on a Manifold
description: A computational study of minimax-optimal geodesic distance estimation on smooth manifolds, comparing ISOMAP, TDC, and Offset methods.
img: assets/projects/minimax/geodesic_path_knot.png
importance: 7
category: academic projects
github: https://github.com/rubenifrah/minimax-manifold-learning
tags: [Maths, Research]
---

This project is a computational study of the paper *Minimax Estimation of Distances on a Surface and Minimax Manifold Learning in the Isometric-to-Convex Setting*. It addresses a fundamental question in manifold learning:

> Given only sampled points on a smooth manifold, how should one estimate intrinsic geodesic distances?

This work was carried out as a research project for the **Dimension Reduction and Manifold Learning** course taught by **Eddie Aamari** in the **M2 IASD** program, with **Pierre Cornilleau**, **Abel Douzal**, and **Ruben Ifrah**.

[Read the article (PDF)](/assets/projects/minimax/Minimax Estimation of Distances on a Surface and Minimax Manifold Learning in the Isometric-to-Convex Setting.pdf)

[View the presentation slides (PDF)](/assets/projects/minimax/presentation.pdf)

---

## Motivation

Graph-based geodesic estimates (like ISOMAP) are **not minimax-optimal** in the isometric-to-convex setting. The key issue is *short-circuiting*: when distant regions of a manifold are close in ambient Euclidean space, a discrete graph can create spurious shortcuts that distort estimated distances. This project studies when and why this happens — and what methods can provably do better.

The Tangential Delaunay Complex (TDC) achieves the minimax-optimal `O(ε²)` relative distortion regime by reconstructing the surface before computing geodesics, avoiding the shortcut problem entirely.

## Three Paradigms Compared

### 1. ISOMAP — Graph Geodesics

Shortest paths on a weighted k-nearest-neighbor graph. Fast and simple, but vulnerable to short-circuiting when manifold branches are close in ambient space.

### 2. TDC — Tangential Delaunay Complex

The manifold is first reconstructed as a triangulated surface. Geodesics are then computed on the reconstructed mesh. This is the method most aligned with the minimax theory — consistent with the optimal distortion bound.

### 3. Offset — Volumetric Geodesics

The manifold is thickened into a continuous ambient volume, and geodesics are approximated inside that offset region. Motivated by geometric robustness ideas, but more sensitive to voxel resolution and offset radius.

## The Knot Example

The tubular knot is the most striking illustration of the problem. Different branches of the tube can be close in ambient space, causing ISOMAP to "jump" between branches — while TDC, constrained to the reconstructed 2-manifold surface, stays on the correct branch.

<div class="row justify-content-center">
  <div class="col-md-8 mt-3">
    {% include figure.liquid loading="lazy" path="assets/projects/minimax/geodesic_path_knot.gif" title="Knot geodesic comparison" class="img-fluid rounded z-depth-1" %}
  </div>
</div>
<div class="caption">
  ISOMAP vs. TDC vs. Offset geodesics on a tubular knot. Notice how the graph path (ISOMAP) short-circuits across branches, while TDC stays on the correct surface path.
</div>

### Interactive 3D Visualization

Explore the geodesic paths interactively on 5 different knot geometries — rotate, zoom, and compare ISOMAP vs. TDC directly in your browser:

<div class="row justify-content-center">
  <div class="col-12 mt-3">
    <iframe src="/assets/projects/minimax/5_knots_geodesics.html"
            width="100%" height="650px"
            style="border: none; border-radius: 8px;"
            loading="lazy">
    </iframe>
  </div>
</div>

## Key Results

- **ISOMAP** is fast but provably suboptimal — and fails visually on the knot.
- **TDC** achieves the minimax-optimal distortion regime and produces geometrically faithful geodesics. Yet a lot of heuristics are needed to make it work in practice. It doesn't scale with the dimension of the manifold.
- **Offset** is a theoretically motivated alternative but is sensitive to hyperparameters and computationally very expensive (voxel resolution, offset radius).
- The **sphere** provides an analytic ground truth for controlled comparisons, validating the distortion bounds empirically.

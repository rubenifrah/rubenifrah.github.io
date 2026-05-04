---
layout: page
title: MCTS for Equation Discovery
description: A hybrid architecture combining MCTS and SINDy for physical equation discovery.
img: assets/projects/MCTS-SINDy/MCTS_pp.jpeg
importance: 1
category: academic projects
github: https://github.com/gabriellafrds/MCTS_Equation_Discovery
giscus_comments: true
tags: [RL, Research]
---

Discovering governing physical equations from noisy trajectory data is a famously difficult combinatorial problem. This project explores a novel hybrid architecture for symbolic regression by combining the search capabilities of **Monte Carlo Tree Search (MCTS)** with the robust mathematical guarantees of **Sparse Identification of Nonlinear Dynamical Systems (SINDy)**.

Developed as a final course project under Pr. Tristan Cazenave for the M2 IASD Master's program.

## The Problem with pure Symbolic Regression

Traditional sparse regression methods (like PySINDy) rely heavily on pre-built structural libraries (such as polynomials up to degree N). When dealing with deeply nested non-linearities, these libraries either explode in dimensionality or catastrophically overfit in the presence of noise. 
Conversely, pure symbolic mathematics models suffer from massive computational overhead because they attempt to optimize continuous physical constants simultaneously while randomly exploring discrete mathematical syntax.

## Core Architecture: MCTS-SINDy

This project bridges that gap by decoupling the structural search from the parameter optimization:

1. **Discrete Grammar Search**: MCTS constructs mathematical grammar trees sequentially as a discrete Markov Decision Process. 
2. **Continuous Parameter Optimization**: Instead of guessing coefficients during the search, the MCTS sequence is compiled into a sparse feature matrix. SINDy then analytically solves for the optimal continuous coefficients using orthogonal matching pursuit logic.
3. **Parsimony Enforcement**: The tree is rewarded using a Bayesian Information Criterion (BIC), enforcing strict Occam's Razor discipline to punish deeply nested structures that do not offer massive predictive improvements.

## Benchmarks & Results

The architecture was benchmarked against systems of increasing difficulty using synthetic data with injected Gaussian noise (up to 5%):

*   **Damped Harmonic Oscillator:** MCTS-SINDy perfectly bounds parsimony at 2 features across all noise tiers, whereas baseline algorithms degrade and overfit.
*   **Colpitts Chaos Oscillator:** This acted as the rigorous architecture test because the target equations contain explicitly nested parameters alongside strict constant offsets. The MCTS completely solves this nested dynamic by decoupling structure generation from parameters.
*   **Deep Nested Bound:** The model successfully evaluates systems requiring nested sine dependencies reaching depth thresholds standard dictionaries cannot populate.

## Tech Stack
*   **Concepts**: Symbolic Regression, Monte Carlo Tree Search (MCTS), SINDy, Markov Decision Processes
*   **Languages**: Python

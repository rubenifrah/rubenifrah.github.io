---
layout: page
title: Deep RL F1 Racing
description: Autonomous F1 racing agent using PPO and DQN
img: assets/img/f1_env.png
importance: 1
category: personal projects
github: https://github.com/rubenifrah/deep-rl
related_publications: false
---

This project involves developing and training a Deep Reinforcement Learning agent to autonomously drive an F1 car in a custom Gym environment.

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/demo_f1.gif" title="F1 Agent in Action" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The agent navigating the track after training.
</div>

## Project Overview

The goal of this project is to create a robust agent capable of navigating complex tracks at high speeds.

### Key Features
*   **Custom Environment**: Built on top of OpenAI Gym, simulating F1 physics and track dynamics.
*   **Algorithms**: Implemented and compared **Proximal Policy Optimization (PPO)** and **Deep Q-Networks (DQN)**.
*   **Reward System**: Designed a progress-based reward function to encourage speed and track completion, replacing a simple speed-based metric to improve stability.
*   **Track Generation**: Developed tools for automatic and manual track generation using spline interpolation (Catmull-Rom, Hermite, Bezier).

### Technical Details
The agent observes the environment through ray-casting sensors (Lidar-like) and vehicle telemetry (speed, steering angle). The model is trained to output continuous control actions (steering, acceleration/braking).

We tackled challenges such as:
*   **Training Stability**: Implemented gradient clipping and hyperparameter tuning to stabilize learning.
*   **Generalization**: Trained on multiple procedurally generated tracks to ensure the agent can adapt to unseen circuits.

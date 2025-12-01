# Deep Reinforcement Learning Playground

Hi! I'm Ruben, a 24 year old student at école Polytechnique and M2 IASD at Dauphine University, and this repository is my personal playground for exploring and implementing Deep Reinforcement Learning algorithms.

Recently I've been more than interested in Deep Reinforcement Learning and I've been reading a lot of papers and articles about it. I've been reading papers about DQN, Double DQN, Dueling DDQN, and more. So motivated by the idea of going further than the course I'm taking, I decided to build a custom environment and implement these algorithms.

The idea was also to build a custom environment that was more complex than CartPole but less computationally heavy than 3D simulators. So I decided to build a custom F1 environment using Pygame and Box2D concepts to simulate a car controlled by LIDAR sensors. I also wanted to implement a custom track generator using Harmonic Noise, which is a method of generating procedurally generated tracks.

## Project Overview

This project features a unified training pipeline that allows for easy experimentation with different agents and environments. A key highlight is the **custom F1 Racing Environment**, which I built using Pygame and Box2D concepts to simulate a car controlled by LIDAR sensors.

### Key Features

*   **Modular Architecture**: A single `train.py` script dynamically loads agents and environments, making it easy to plug in new algorithms or tasks without rewriting the training loop.
*   **Algorithms Implemented**:
    *   **DQN** (Deep Q-Network) with Experience Replay.
    *   **DDQN** (Double DQN) to reduce overestimation bias.
    *   **Dueling DDQN** to separately estimate state value and advantage.
*   **Custom F1 Environment**:
    *   **LIDAR Perception**: The agent "sees" the track using ray-casting, similar to real-world autonomous robots.
    *   **Procedural Generation**: Tracks are generated algorithmically using Harmonic Noise (sum of sines), ensuring the agent learns to generalize rather than memorize a single layout.
    *   **Physics**: Custom 2D physics engine with friction, acceleration, and collision detection.

## The F1 Environment

I wanted a challenge that was more complex than CartPole but less computationally heavy than 3D simulators. The F1 environment provides a continuous state space (LIDAR distances) and a discrete action space (Steer Left/Right, Gas, Brake).

<p align="center">
  <img src="/assets/f1_env.png" alt="F1 Environment" />
  <br>
  <em>F1 car, LIDAR rays (green=safe, red=close), and procedurally generated track.</em>
</p>

### Procedural Track Generation
To prevent overfitting, I implemented a track generator based on **Harmonic Noise**. By summing multiple sine waves with random phases and frequencies, I can generate infinite variations of organic, winding tracks.

```bash
# Generate a complex track with high curvature
python create_track.py --output tracks/complex.json --complexity 10 --distortion 200
```

### Example of a run with Dueling DDQN

<p align="center">
  <img src="/assets/demo_f1.gif" alt="F1 Environment" />
  <br>
  <em>Dueling DDQN training on F1 environment for a total of 1000 episodes.</em>
</p>

## Getting Started

If you want to run this code or use it as a base for your own experiments, here is how to get set up.

### Installation

```bash
git clone https://github.com/yourusername/deep-rl.git
cd deep-rl
pip install gymnasium[box2d] pygame numpy torch matplotlib
```

### Training an Agent

You can train any agent on any supported environment using the command line.

**Train Dueling DDQN on the F1 Environment:**
```bash
python train.py --env F1Env --agent DuelingDDQN --num_episodes 1000 --render_last 10
```

**Train DQN on CartPole (Sanity Check):**
```bash
python train.py --env CartPole-v1 --agent DQN
```

### Visualizing Results

I included a script to plot training metrics (Reward and Loss) to analyze stability and convergence.

```bash
python plot_results.py --file results.json
```

## Structure

*   `agents/`: Implementation of RL agents (DQN, DDQN, DuelingDDQN).
*   `envs/`: Custom environments (`f1_gym_env.py`).
*   `utils/`: Utility scripts (`replay_buffer.py`).
*   `tracks/`: JSON files defining F1 tracks.
*   `train.py`: The main training loop and argument parser.
*   `create_track.py`: Procedural track generator.
*   `visualize_track.py`: Tool to inspect generated tracks.
*   `plot_results.py`: Training results plotter.

---

*This project has been developed by Ruben Ifrah, contact me for any questions or suggestions:*

mail : ruben.ifrah@dauphine.eu \
linkedin : [ruben-ifrah](https://www.linkedin.com/in/ruben-ifrah-245496253/) \
github : [ruben-ifrah](https://github.com/rubenifrah)
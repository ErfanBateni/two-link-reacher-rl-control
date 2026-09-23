# two-link-reacher-rl-control
Control and Reinforcement Learning (DDPG, SARSA, PID) for a 2-DOF Planar Robotic Arm using OpenAI Gymnasium.
# 2-DOF Planar Reacher: Control vs. Reinforcement Learning

This repository contains the implementation and comparative analysis of classical control techniques and modern Reinforcement Learning (RL) algorithms for a 2-DOF planar robotic arm (Two-Link Reacher). The objective is to drive the end-effector to static and dynamically moving target points within the continuous-time dynamics space.

This project was developed for the **Reinforcement Learning** course.

---

## 📌 Project Overview
The core challenge involves navigating the nonlinear dynamics of a multi-link robotic arm, accounting for inertia, Coriolis forces, and joint damping. We built a custom simulation environment adhering to the **OpenAI Gymnasium API** and evaluated multiple baseline controllers against state-of-the-art RL agents.

---

## 🤖 Implemented Control Strategies

### 1. Continuous Control with DDPG
*   **Deep Deterministic Policy Gradient (DDPG):** An off-policy, continuous-action actor-critic algorithm. Through hyperparameter tuning and appropriate exploration noise, DDPG successfully learned continuous control policies, producing smoother torque profiles and demonstrating energy efficiency compared to discrete methods. The agent is trained to minimize the distance between the end-effector and the target position.

---

## 🧪 Experiments & Ablation Studies

1.  **Exploration Noise Analysis:** Compared Gaussian noise against temporally correlated **Ornstein-Uhlenbeck (OU) noise**. The OU process significantly improved DDPG stability and learning by injecting smooth, inertia-friendly exploration into the torque actions. The performance is evaluated based on the mean tracking error and success rate across multiple seeds.
2.  **State Representation Ablation:** Implemented a state wrapper (`DDPGStateWrapper`) to augment the minimal state observation. Providing the agent with explicit end-effector coordinates ($x_{end}, y_{end}$) alongside joint angles ($x_{t}, y_{t}, \theta_{1}, \theta_{2}, \dot{\theta}_{1}, \dot{\theta}_{2}$) is crucial for improving learning efficiency and tracking accuracy.

---

## 📊 Results Summary
*   The DDPG agent demonstrates the capability to learn complex, continuous-time dynamics without explicit knowledge of the system model.
*   However, the learning process exhibits high variance and instability, as evidenced by the highly irregular return and error curves.
*   The agent occasionally achieves very low errors and returns close to zero, indicating it has learned useful control behaviors, but fails to apply them consistently across episodes.
*   This instability is characteristic of DDPG trained with a limited number of steps (15,000 steps across 100 episodes) on a task with randomly changing targets, highlighting the limitations of the current training setup in achieving full convergence and generalization.

---

## 🛠️ Tools & Technologies
*   **Python, NumPy, PyTorch** (Deep Learning implementations)
*   **OpenAI Gymnasium** (Custom environment architecture)
*   **Pygame** (Rendering and human-in-the-loop interactive control)
*   **Matplotlib** (Plotting learning curves and performance metrics)

---

## 📂 Repository Structure
*   `Part 1-4.ipynb`: Jupyter Notebook containing the custom Gymnasium environment implementation, classical baselines (Task-Space PID, IK+PD), and the discrete-action RL agent (N-Step SARSA).
*   `Part 5-9.ipynb`: Jupyter Notebook focusing on continuous control. It includes the DDPG agent implementation (Actor/Critic networks, Replay Buffer, Gaussian/OU noise models), state wrappers, training loops, and ablation study results.
*   `Report.pdf`: The comprehensive technical report covering mathematical modeling, standardized metrics (Mean Tracking Error, Success Rate, Control Energy), and training curves.
*   `Report.pdf`: The comprehensive technical report covering mathematical modeling, standardized metrics (Mean Tracking Error, Success Rate, Control Energy), and training curves.

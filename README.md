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

### 1. Classical Baselines
*   **Task-Space PID:** A model-free classical controller calculating corrective torques directly from Cartesian position errors using the Jacobian transpose.
*   **Inverse Kinematics + Joint-Space PID (IK + PD):** Utilizes geometric inverse kinematics to compute desired joint angles, followed by PD control in the joint space. This method served as the upper-bound baseline, providing the highest accuracy and stability.

### 2. Reinforcement Learning Agents
*   **N-Step SARSA (Discrete RL):** An on-policy algorithm with a discretized action space (torque levels). Due to the continuous nature of the robotic dynamics, this method struggled to converge to an optimal policy.
*   **Deep Deterministic Policy Gradient (DDPG):** An off-policy, continuous-action actor-critic algorithm. Through hyperparameter tuning and appropriate exploration noise, DDPG successfully learned continuous control policies, producing smoother torque profiles and demonstrating energy efficiency compared to discrete methods.

---

## 🧪 Experiments & Ablation Studies

1.  **Exploration Noise Analysis:** Compared Gaussian noise against temporally correlated **Ornstein-Uhlenbeck (OU) noise**. The OU process significantly improved DDPG stability and learning by injecting smooth, inertia-friendly exploration into the torque actions.
2.  **Generalization (Distribution Shift):** Tested the RL agent's robustness against unseen trajectories (e.g., changing target velocity, radius, or navigating complex Lissajous curves).
3.  **State Representation Ablation:** Evaluated minimal state definitions versus augmented states. Providing the agent with explicit end-effector coordinates ($x_{end}, y_{end}$) alongside joint angles drastically improved learning efficiency and tracking accuracy.

---

## 📊 Results Summary
Based on the comprehensive final report:
*   **Classical controllers (especially IK + PD)** remain highly reliable and precise when the system's exact mathematical model is known.
*   **DDPG** demonstrated a strong capacity to learn complex, continuous-time dynamics without explicit knowledge of the system model. While it yielded smooth, low-energy trajectories, it requires significant data and hyperparameter tuning to match the strict tracking accuracy of classical IK methods.

---

## 🛠️ Tools & Technologies
*   **Python, NumPy, PyTorch** (Deep Learning implementations)
*   **OpenAI Gymnasium** (Custom environment architecture)
*   **Pygame** (Rendering and human-in-the-loop interactive control)

---

## 📂 Repository Structure
*   `reacher_env.py`: Custom continuous-time dynamics Gymnasium environment.
*   `/Notebooks`: Jupyter notebooks containing PID, SARSA, and DDPG training loops, evaluation metrics, and ablation studies.
*   `play_pygame.py`: Interactive script to control the robotic arm via keyboard.
*   `Report.pdf`: The comprehensive technical report covering mathematical modeling, standardized metrics (Mean Tracking Error, Success Rate, Control Energy), and training curves.

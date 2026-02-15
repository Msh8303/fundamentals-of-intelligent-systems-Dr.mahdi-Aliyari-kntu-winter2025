# 🏭 Hybrid Intelligent Control System for Steel Defect Detection
### Integrating Computer Vision, Fuzzy Logic, and Reinforcement Learning

![Project Banner](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.9%2B-blue?style=for-the-badge&logo=python)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0-EE4C2C?style=for-the-badge&logo=pytorch)
![YOLOv8](https://img.shields.io/badge/YOLO-v8%2Fv11-00FFFF?style=for-the-badge)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

> **Course:** Fundamentals of Intelligent Systems  
> **Instructor:** Dr. Mahdi Aliyari  
> **University:** K. N. Toosi University of Technology  
> **Semester:** Winter 2025 - Spring 2026

---

## 📖 Table of Contents
- [Abstract](#-abstract)
- [System Architecture](#-system-architecture)
- [Key Features](#-key-features)
- [Methodology](#-methodology)
  - [1. Computer Vision (YOLOv8n-Improved)](#1-computer-vision-yolov8n-improved)
  - [2. Fuzzy Logic Controller](#2-fuzzy-logic-controller)
  - [3. Reinforcement Learning (Q-Learning)](#3-reinforcement-learning-q-learning)
- [Experimental Results](#-experimental-results)


---

## 📝 Abstract

In the steel manufacturing industry, balancing **production speed** and **inspection accuracy** is a critical challenge. High conveyor speeds increase productivity but introduce *motion blur*, degrading defect detection performance.

This project proposes a **Closed-Loop Hybrid Intelligent System** that dynamically adjusts the conveyor belt speed based on real-time defect analysis. The system integrates:
1.  **YOLOv8n-Improved:** For real-time surface defect detection with attention mechanisms.
2.  **Fuzzy Logic:** As a safety supervisor to handle uncertainty and provide expert-based guidance.
3.  **Reinforcement Learning (Q-Learning):** An adaptive agent that learns the optimal speed-safety trade-off over time.

---

## 🏗 System Architecture

The system operates in a continuous loop:
1.  **Perception:** Camera captures frames; YOLO detects defects.
2.  **Risk Assessment:** Defects are weighted by type (e.g., *Crazing* > *Scratches*) to calculate a `Risk Score`.
3.  **Decision Making:**
    * **Fuzzy System:** Outputs a suggested speed change based on predefined rules.
    * **RL Agent:** Takes the Fuzzy suggestion and Current Speed as state, outputs the optimal action.
4.  **Action:** Conveyor speed is adjusted, affecting the motion blur of subsequent frames.

<div align="center">
  <img src="assets/architecture_diagram.png" alt="System Architecture" width="80%">
  <br>
  <em>Figure 1: High-level block diagram of the Hybrid Control Loop.</em>
</div>

---

## 🚀 Key Features

| Feature | Description |
| :--- | :--- |
| **Custom YOLO Backbone** | Replaced standard Conv blocks with **GSConv** for lightweight processing and added **GAM Attention** for better feature extraction. |
| **Advanced Loss Function** | Implemented **PIoU v2** to improve bounding box regression for elongated defects (e.g., cracks). |
| **Dynamic Simulation** | Realistic **Motion Blur** simulation linked to conveyor speed to test system robustness. |
| **Hybrid Control** | Novel combination of **Fuzzy Logic** (for cold-start guidance) and **RL** (for long-term optimization). |
| **Multi-Objective Reward** | Reward function balances Efficiency ($+Speed$) vs. Safety ($-Risk \times Speed$). |

---

## 🔬 Methodology

### 1. Computer Vision (YOLOv8n-Improved)
We enhanced the YOLOv8-Nano architecture to handle the specific challenges of steel defects:
* **Backbone:** `GSConv` blocks for efficiency.
* **Neck:** `GAM` (Global Attention Mechanism) to capture both channel and spatial information.
* **Head:** `PIoU v2 Loss` for better localization of high-aspect-ratio defects.


### 2. Fuzzy Logic Controller
A Mamdani inference system with **9 Rules** acts as a safety supervisor.
* **Inputs:** `Risk Score` (Low, Medium, High) & `Confidence` (Low, Medium, High).
* **Output:** `Speed Change` (Brake, Maintain, Accelerate).

### 3. Reinforcement Learning (Q-Learning)
The agent interacts with the environment to maximize the long-term reward.
* **State Space (3x3):** `{Fuzzy_Suggestion} × {Current_Speed}`
* **Action Space:** `{-0.1, 0, +0.1}`
* **Policy:** $\epsilon$-Greedy with decay.

---

## 📊 Experimental Results

### Detection Performance
Our improved model outperforms the baseline YOLOv8n and YOLOv11m in balancing speed and accuracy.

| Model | mAP@0.5 | Inference Time | Parameters |
| :--- | :---: | :---: | :---: |
| YOLOv8n (Base) | 62.4% | **4.1 ms** | 3.2 M |
| YOLOv11m | 65.1% | 12.8 ms | 20.1 M |
| **YOLOv8n-Imp (Ours)** | **67.7%** | 5.3 ms | **3.5 M** |



---

├── run_simulation.py        # Main control loop
├── requirements.txt         # Dependencies
└── README.md

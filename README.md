# 🚗 Lane Keeping Assist (LKA) using Pure Pursuit Control

> Implementation of lateral vehicle control for ADAS using a geometric Pure Pursuit controller.

---

## 📌 Overview

This project implements a **Lane Keeping Assist (LKA)** system using a **kinematic bicycle model** and a **Pure Pursuit controller**.

The goal is to simulate lateral vehicle control and analyze how a vehicle can **stably converge to the lane center** from a large initial offset.
This project complements Adaptive Cruise Control (ACC) by addressing **lateral control**, forming a core component of modern ADAS systems.

---

## 🎯 Motivation

Lane keeping is a fundamental function in Advanced Driver Assistance Systems (ADAS).
Understanding how a controller behaves under different conditions is critical for real-world deployment.

This project focuses on:

* Implementing a **geometric lateral controller**
* Analyzing **convergence behavior**
* Investigating **stability vs responsiveness trade-offs**

---

## 🧠 System Architecture

```text
Lane Center (Reference Path)
        ↓
Target Point Selection (Lookahead)
        ↓
Pure Pursuit Controller (Steering Angle)
        ↓
Vehicle Model (Kinematic Bicycle Model)
        ↓
State Update (x, y, yaw)
```

---

## ⚙️ Mathematical Model

### Vehicle Model (Kinematic Bicycle Model)

[
\dot{x} = v \cos(\psi), \quad
\dot{y} = v \sin(\psi), \quad
\dot{\psi} = \frac{v}{L} \tan(\delta)
]

### Pure Pursuit Control Law

[
\delta = \tan^{-1}\left(\frac{2L \sin(\alpha)}{L_d}\right)
]

### Lookahead Distance

[
L_d = k \cdot v + L_{min}
]

---

## 🎬 Simulation

![LKA Simulation](LKA_simulation.gif)

---

## 📊 Results & Analysis

* Initial lateral offset: **y = -30 m**
* Vehicle converges to lane center (**y ≈ 0**) within approximately **120 m**
* Smooth trajectory achieved without oscillation
* Stable tracking behavior observed after convergence

### Key Insight

The convergence behavior is strongly influenced by the lookahead distance:

* Larger lookahead → faster but aggressive convergence
* Smaller lookahead → smoother but slower response

This demonstrates the **trade-off between responsiveness and stability** in geometric controllers.

---

## Challenges & Solutions

### 1. Target Point Jump Issue

**Problem:**
The lookahead-based target selection caused sudden jumps in the target point, resulting in unrealistic motion in the simulation.

**Solution:**

* Introduced a **monotonically increasing target index**
* Limited the maximum index increment per timestep

→ Result: Smooth and continuous target movement

---

### 2. Excessively Fast Convergence

**Problem:**
The vehicle converged to the lane center too quickly, reducing interpretability of controller behavior.

**Solution:**

* Tuned lookahead parameters (`k`, `L_min`)
* Applied **steering angle constraints**

→ Result: Gradual and realistic convergence over distance

---

### 3. Visualization Issues

**Problem:**
Initial plots did not clearly show convergence behavior due to improper scaling.

**Solution:**

* Adjusted axis ranges
* Added GIF-based animation for dynamic visualization

→ Result: Improved interpretability of system behavior

---

## Implementation Details

* **Language:** Python
* **Environment:** Google Colab
* **Libraries:** NumPy, Matplotlib

### Code Structure

* `Vehicle` class → kinematic bicycle model
* `find_target()` → lookahead-based target selection
* `pure_pursuit()` → steering computation
* Simulation loop → state update & logging
* Visualization → trajectory plot + GIF animation

---

## Limitations

* Pure Pursuit is a **geometric controller** and does not explicitly consider vehicle dynamics
* Performance may degrade at **high speeds or sharp curvature**
* No **sensor noise or disturbance** modeling
* Assumes a perfectly known reference path

---

## 💡 Key Takeaways

* Developed a complete lateral control simulation from scratch
* Gained insight into controller tuning and system behavior
* Identified practical limitations of geometric control methods
* Strengthened ability to analyze and debug dynamic systems


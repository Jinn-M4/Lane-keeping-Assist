# 🚗 Lane Keeping Assist (LKA) using Pure Pursuit Control

## 📌 Overview

This project implements a **Lane Keeping Assist (LKA)** system using a **kinematic bicycle model** and a **Pure Pursuit controller**.
The objective is to simulate lateral vehicle control and demonstrate how a vehicle can **converge smoothly to the lane center** from an initial offset.

This project complements Adaptive Cruise Control (ACC) by covering **lateral control**, forming a fundamental component of modern ADAS systems.

---

## 🎯 Key Features

* Kinematic bicycle model for vehicle motion
* Pure Pursuit algorithm for lateral control
* Speed-dependent lookahead distance
* Smooth convergence from large lateral offset
* Real-time simulation with trajectory visualization
* GIF-based animation for intuitive understanding

---

## 🧠 System Architecture

```
Path (Lane Center)
        ↓
Target Point Selection (Lookahead)
        ↓
Pure Pursuit Controller (Steering Angle)
        ↓
Vehicle Model (Bicycle Model)
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

## 📊 Results & Insights

* The vehicle starts with a **large lateral offset (y = -30 m)**.
* It gradually converges to the lane center (**y = 0**) over distance.
* The convergence rate is controlled by:

  * Lookahead distance tuning
  * Steering angle constraints
* A smooth and stable trajectory is achieved without oscillation.

---

## 🚀 Key Engineering Decisions

### 1. Stable Target Point Selection

To prevent sudden jumps in the lookahead point:

* Maintained a **monotonically increasing target index**
* Limited index increment per timestep

### 2. Smooth Convergence Behavior

* Tuned lookahead parameters to control convergence rate
* Applied steering angle constraints for realistic motion

### 3. Visualization for Interpretability

* Added trajectory plots and GIF animation
* Enabled intuitive understanding of controller behavior

---

## 💡 What I Learned

* Implementation of lateral control using geometric methods
* Trade-offs between responsiveness and stability in control systems
* Importance of parameter tuning in real-world vehicle dynamics
* Visualization as a tool for system validation

---




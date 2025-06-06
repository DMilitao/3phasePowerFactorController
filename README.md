# Control of a Three-Phase PFC Rectifier

## 📝 Overview

This project presents the design, simulation, and comparison of control systems for a three-phase Power Factor Correction (PFC) rectifier. The primary goal is to improve the circuit's power factor by forcing the AC-side currents to be sinusoidal and in phase with the voltages, thereby reducing the Total Harmonic Distortion (THD).

The project explores and contrasts two distinct control design philosophies: a classical **frequency-domain approach** and a modern **time-domain (optimal control) approach**. The entire system is modeled, and all controllers are designed and validated within a **MATLAB & Simulink** simulation environment.

---

## 🚀 Control Strategies & Implementations

Two main control architectures were developed and tested:

### 1. Frequency-Domain Approach
This method uses a cascaded control structure with discrete-time controllers designed via pole placement.
* **Outer Voltage Loop:** A discrete PID controller with a low-pass filter and an anti-windup mechanism regulates the DC bus voltage (`Udc`).
* **Inner Current Loops:** Two discrete PI controllers manage the d-axis and q-axis currents (`id`, `iq`).
* **Decoupling:** A feedforward mechanism is used to decouple the cross-coupling effects between the d-q axes.

### 2. Time-Domain (Optimal Control) Approach
This method is based on the state-space representation of the system and uses a Linear Quadratic Regulator (LQR) to compute the controller gains.
* **Initial LQR Controller:** An LQR controller was first designed for the system. While it provided good setpoint tracking (servoing), it showed poor performance in rejecting disturbances, such as sudden changes in load (regulation).
* **Extended State Feedback (LQR + Integral Action):** To solve the regulation issue, the design was enhanced by implementing an extended state feedback controller. This adds an integral action to the LQR framework, successfully eliminating steady-state errors after load variations.

---

## 🏆 Key Findings & Comparison

Both control methodologies successfully achieved the main goal of making the rectifier draw sinusoidal currents, which significantly improves the power factor. However, their performance and design characteristics differed:

* The **Frequency-Domain Approach** was effective but showed some discrepancies between the desired and the achieved system dynamics. This is due to the mathematical approximations and simplifications made during the design process.

* The initial **Time-Domain (LQR) Approach** was simpler to implement (requiring only a state-feedback gain matrix) but was not robust against load changes.

* The final **Extended State Feedback Controller** delivered the best overall performance. It demonstrated faster and more robust dynamics than the frequency-domain method, especially in its ability to quickly handle sudden load variations and eliminate steady-state voltage errors.

---

## 🛠️ Technologies Used

MATLAB/Simulink

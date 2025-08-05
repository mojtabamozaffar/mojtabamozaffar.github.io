---
title: "Self-Balancing Cube: Design, Build and Control Strategies"
tags: ["robotics", "control systems", "3D printing", "embedded electronics", "reinforcement learning"]
date: 2025-01-04
description: "A deep dive into the design, electronics, and control strategies of my self-balancing cube project."
summary: "I engineered a self-balancing cube—mechanically, electronically, and in software—exploring LQR, quaternion-based nonlinear control, and reinforcement learning."
cover:
    image: "cubli.png"
    alt: "Self-Balancing Cube resting on its corner"
    relative: false
---

<img src="/cubli.png" width="800">

Balancing on a corner or edge may seem trivial for a person, but for a rigid cube it demands precise actuation, state estimation, and clever control laws. Here’s how I tackled each aspect of this project.

---

## Mechanical Design & Fabrication  
I began by iterating on a CAD model of a 10 cm³ cube equipped with three reaction wheels arranged orthogonally inside its faces. My design is heavily inspired by the original paper and the design [here](https://github.com/remrc/Self-Balancing-Cube). Key considerations included:

- **Mass distribution**: Hollowing out non-structural regions reduced the cube’s moment of inertia while maintaining rigidity.  
- **Print orientation**: Each face was oriented to minimize support material, leveraging PETG for durability.  
- **Assembly tolerances**: Press-fit housings for the wheel motors ensured concentric spinning without bearings.

After multiple prototypes, the final 3D-printed frame achieved sub-millimeter accuracy, letting the reaction wheels deliver smooth motion.

I also designed a custom PCB that reads the IMU and controls the 3 motors.

<img src="/cubli_kicad.png" width="800">

---

## Control Strategies  

### Linear Quadratic Regulator (LQR)  
By linearizing the cube’s dynamics around its perfectly balanced corner, I derived a 6-state model (angle, angular velocity, wheel speed). Solving the Riccati equation yielded feedback gains that stabilize small-angle deviations (around under ±5°).  

The LQR approach served as a reliable benchmark for more advanced schemes.

### Quaternion-Based Nonlinear Control  
To handle large disturbances—such as a gentle push that tips the cube onto its face—I adopted a quaternion attitude controller from Bobrow et al. (2021). Key benefits:

- **No gimbal lock**: Attitude errors computed directly on \(\mathbb{S}^3\).  
- **Global attractiveness**: A Lyapunov-based torque law ensures convergence from any orientation.  

In practice, this controller recovered balance from much more steep angles and outperforming LQR in robustness.

### Reinforcement Learning with Drake  
Finally, I built a high-fidelity simulation in Drake, modeling friction, motor saturations, and sensor noise. Using proximal policy optimization (PPO), the agent learned to:

- Balance from random initial angles.  
- Optimize wheel speed to minimize energy consumption over a 5 s horizon.  

After training and solve system identification to match simulation with real cube I was able to run the policy on the hardware and achieve roughly similar performance as the nonlinear.

<img src="/cubli_2.jpg" width="800">

---

### References

- Gajamohan, Mohanarajah, et al. “The Cubli: A cube that can jump up and balance.” *2012 IEEE/RSJ International Conference on Intelligent Robots and Systems*, IEEE, 2012.  
- Bobrow, Fabio, et al. “The Cubli: modeling and nonlinear attitude control utilizing quaternions.” *IEEE Access* 9 (2021): 122425–122442.  
- REMRC Self-Balancing Cube repository: https://github.com/remrc/Self-Balancing-Cube  

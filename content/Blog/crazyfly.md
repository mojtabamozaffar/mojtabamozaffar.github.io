---
title: "Controlling Crazyflie Mico-Dones via Radio in Android"
tags: ["drones", "Crazyflie", "Android", "robotics", "RF communication"]
date: 2024-08-01
description: "An introduction to the Crazyflie nano-quadcopter platform and my work developing an Android application to control it over a 2.4 GHz radio link."
summary: "I have been working with Crazyflie drones which are tiny open-source drones from Bitcraze. Here I describe my experience with it and how I built an Android app that sends real-time commands over radio, enabling intuitive remote flight control and telemetry monitoring."
cover:
    image: "crazyflie.png"
    alt: "crazyflie"
    relative: false
---

<img src="/crazyflie.png" width="800">

The **Crazyflie** is an ultra-lightweight (≈27 g) open-source nano-quadcopter developed by [Bitcraze](https://www.bitcraze.io/). Despite its small size, it boasts:
1. **Modular Hardware**  
   Swappable decks for IMU, LiDAR, cameras, and radio modules.
2. **Open-Source Firmware & SDKs**  
   Extensible C / Python codebase for custom flight controllers and companion computers.
3. **2.4 GHz Long-Range Radio**  
   Reliable bidirectional link supporting telemetry and control up to hundreds of meters.
4. **Rich Ecosystem**  
   Community-driven extensions for swarm flights, SLAM, and autonomous behaviors.

My recent project centers on building an **Android application** to harness the Crazyflie’s radio link and deliver real-time remote control:

1. **Intuitive UI & Command Mapping**  
   Designed a touch-based joystick interface that translates user gestures into pitch, roll, yaw, and thrust commands.
2. **2.4 GHz Radio Integration**  
   Leveraged Bitcraze’s Android SDK to open and manage the Crazyradio USB dongle, establish a secure link, and handle packet framing.
3. **Telemetry & Feedback**  
   Display live IMU data, battery voltage, and link quality directly on the phone—enabling situational awareness during flight.
4. **Flight Modes & Safety**  
   Implemented configurable rate and angle modes, plus an emergency cut-off feature to halt the propellers instantly if needed.
5. **Extensibility**  
   Structured the app for easy addition of new decks (e.g., optical flow, LiDAR) and custom flight behaviors.

Through this work, I’ve demonstrated how mobile platforms can become powerful ground stations for lightweight drones, opening doors for rapid prototyping of indoor navigation, swarm research, and educational robotics using the Crazyflie platform.

I intent to open-source the software, but need a bit more time for that... Will update this post!


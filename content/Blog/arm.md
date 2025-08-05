---
title: "Building and Teleoperating a DIY 6-DOF Robot Arm"
tags: ["robotics", "teleoperation", "DIY", "3D printing", "embedded systems", "human-robot interaction"]
date: 2025-04-20
description: "A deep dive into replicating the Arctos 6-DOF arm from scratch and crafting a scaled potentiometer-based master arm for real-time teleoperation."
summary: "I built the open-source Arctos 6-DOF robot arm—3D-printing every link, wiring up an Arduino-based control stack, and adding a miniature potentiometer ‘master’ to drive the full-scale arm with low latency. It was quite an experience and I want to share it here."
cover:
    image: "arm.jpg"
    alt: "Manipulation at Amazon Robotics"
    relative: false
---

<img src="/arm.jpg" width="800">


These days I work quite often with industrial robot arms and really wanted to give it try to build one from scratch myself. I didn quite a bit of research about what are existing open-source project and found some very interesting ones. From [MOTUS](https://www.instructables.com/MOTUS-Open-Source-3D-Printed-Robotic-Arm/) to [BCN3D](https://www.thingiverse.com/thing:1693444), and [AR4](https://www.anninrobotics.com/), they all seem fantastic projects, but I ended up going with [Arctos](https://arctosrobotics.com) because of a combination of cost, learning opportunity of printing almost all of it including gearboxes, and aesthetics. While I mostly re-created the design that Artcos community created, I found the experience very valuable and was able to add a few tweaks and featurs to it at the end.


## Mechanical Design,  3D Printing, and Electronics

Arctos’s six revolute joints give ~600 mm of workspace—enough to reach across a standard 24″ desk—and a rated ~1 kg payload. I used ASA for functional parts that required strength like gearbox parts and PLA for the rest. All non-printing parts are standard and can be bought according to the project [BOM](https://docs.google.com/spreadsheets/d/1vieItTpYDkgyDhjjvzrczWXugibwgaBKGWtBCbKjsf0/edit?gid=385089357#gid=385089357). I opted for the open-loop variation of the design, but love to upgrade it to the close-loop at some point.

I mirrored the official Arctos wiring harness: motors, drivers, endstops, fans with:
  - Core: Arduino Mega 2560  
  - Motor Drivers: TMC2209 (silent, micro-step to 256) on a CNC Shield V3  
  - Power: 24 V, 6A SLA supply  
  - Homing: Magnetic Hall sensor at each axis
  - Communication: A bluetooth module to receive commmands

## Software

<img src="/arm_2.jpg" width="800">

I wrote my own software to calibration and control the robot arm. At the startup, the robot goes into a calibration mode until it triggers all the hall sensors. I also developed a miniature version of the robot arm with potentiometers that reads the position of each joint and sends a smoothened version of it over bluetooth to the main robot board. This was an interesting process and took some trial and error to get it to work with low latency.

## 5. Challenges & Lessons Learned

- **Cable Routing:** has definitely been a major challenge to keep the robot clean-looking, and that's the main reason that I want to migrate to CAN communication. 
- **Thermals:** The motor drivers can get hot after some use and it took some adjusting to find the right balance between driver and motors heating up and arm performance.
- **Backlash Management:** One of cyclic gearboxes shows noticable backlash that I haven't been able to fully resolve.


## 6. What’s Next?

- **Closed-Loop Control:** Upgrade to a Closed-loop stepper motor drive for better performance and cable management.
- **ROS2 Bridge:** Use ROS2 for easy integration with SLAM and vision stacks.  
- **Haptic Feedback:** Upgrade the End-of-arm tooling (EOAT) to a design that can grab bigger objects.

---

Building—then teleoperating—this DIY Arctos arm taught me that open-source robotics can be both accessible and deeply rewarding. If you’re itching to try your own hand at six axes of motion (and maybe a tiny master arm of your own) all highly recommand the Arctos project!

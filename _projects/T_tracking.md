---
layout: page
title: Person-Following for Indoor Robots
description: ROS-based real-time person tracking pipeline fusing RGB-D and LiDAR — deployed on Jetson-class hardware at COGA Robotics.
# img: assets/img/projects/T_tracking/cover.jpg
importance: 5
category: tech
tags: [ROS, Python, Deep SORT, LiDAR, Edge Deployment]
proj_role: "Intern Researcher"
proj_dates: "Dec 2022–Feb 2023"
giscus_comments: true
---
{% include project_header.liquid %}


**Outcome.** Built a real-time person-following system for indoor mobile robots — fusing RGB-D and LiDAR in ROS with Deep SORT tracking, validated under real-world lighting and occlusion conditions on Jetson-class edge hardware.

**Role**: Intern Researcher · **Dates**: Dec 2022 – Feb 2023 · **Context**: COGA Robotics · **Stack**: Python, ROS, Deep SORT

---

### Overview

Indoor person-following demands reliable tracking across varied lighting, partial occlusion, and constrained compute. The system fuses complementary sensor modalities — RGB-D for visual identity, LiDAR for depth geometry — to maintain stable trajectories where either sensor alone would fail.

### Highlights

- Implemented **ROS nodes** with RGB-D/LiDAR calibration for accurate cross-sensor alignment
- Integrated **Deep SORT** tracker leveraging fused sensor signals for continuous trajectory estimation
- Conducted **lighting and occlusion stress tests** to surface failure modes and validate recovery behavior
- Profiled and optimized runtime on **Jetson-class devices** for real-time edge deployment
- Designed **modular node interfaces** and launch files for maintainable, production-ready deployment

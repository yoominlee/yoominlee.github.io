---
layout: page
title: Lens — Sensor-Aware Image Acquisition under Shift
description: Stabilized recognition accuracy under natural distribution shift via adaptive sensor control — validated across multiple backbones.
# img: assets/img/projects/T_lens/cover.jpg
importance: 6
category: tech
# tags: [Computer Vision, Domain Shift, PyTorch, OpenCV]
tags: [Computer Vision, Domain Shift, PyTorch]
proj_role: "Research member"
proj_dates: "Mar–Dec 2024"
# proj_question: "What if the camera, not the model, was the problem?"
# alt questions:
# "Can you stabilize recognition accuracy before the image is even taken?"
# "What does a sensor 'know' about where it is — and can that knowledge help?"
# "How much accuracy is lost before the image reaches the model?"
# "Is domain shift a model problem or a capture problem?"
giscus_comments: true
---
{% include project_header.liquid %}


Prototyped a *sensor-control loop* that tunes capture parameters to scene/domain shift, yielding **more stable accuracy** on natural shift sets.

**Role**: Research member · **Dates**: Mar–Dec 2024 · **Stack**: Python, PyTorch, OpenCV, ImageMagick  
**Context**: AIoT Group @ SNU

### Highlights
- Designed **offline→online eval parity** on real natural-shift datasets; tracked QoQ regressions with **regression-safe comparisons**.
- Authored a **data collection protocol** to expose failure modes across illumination/ISO/exposure; automated labeling + metadata.
- Demonstrated **accuracy stability gains** vs. fixed capture baselines across multiple backbones (CLIP-like and CNN).

{% include figure.liquid path="assets/img/projects/T_lens/diagram.jpg" title="System overview" class="img-fluid rounded z-depth-1" %}

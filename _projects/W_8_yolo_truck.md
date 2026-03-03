---
layout: page
title: Truck Detection under Camera-Angle Domain Shift
description: Adapting YOLO-based truck detection to stay robust across cameras at different positions and angles — tackling geometric domain shift.
img: assets/img/projects/W_3_yolo_truck/cover.jpg
importance: 8
category: work
tags: [YOLO, Object Detection, Domain Adaptation, PyTorch]
status: active
giscus_comments: true
---

{% include figure.liquid path="assets/img/projects/W_3_yolo_truck/detection.jpg" title="Detection results across camera angles" class="img-fluid rounded z-depth-1" %}

**Status: In Progress** &nbsp;·&nbsp; 2025

**The core problem:** A YOLO detector trained on one camera position degrades when deployed on cameras at different angles and locations — even on the same trucks, same road, same scene.

---

### Why Camera-Angle Shift Is Hard

Most domain shift work focuses on appearance changes: weather, lighting, time of day. Camera-angle shift is different and more fundamental.

{% include figure.liquid path="assets/img/projects/W_3_yolo_truck/shift-diagram.jpg" title="Same truck, different camera positions" class="img-fluid rounded z-depth-1" %}

When the camera moves:
- **Geometry changes** — aspect ratio, visible surfaces, and perspective distortion all shift
- **Occlusion patterns change** — a truck seen from the side hides the front, and vice versa
- **Scale varies** — the same object occupies a different pixel area depending on angle and distance

A model trained on camera A learns these geometric priors implicitly. On camera B, those priors break.

---

### Approach

*(To be updated as the project progresses.)*

---

### Current Status

Active development. Detection results, ablations, and methodology will be documented here as the project matures.

---

**Role**: Individual (lab-affiliated) · **Dates**: 2025–present · **Stack**: YOLO, PyTorch, Python

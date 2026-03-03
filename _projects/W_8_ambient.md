---
layout: page
title: On-Device Real-Time Blurring (SNU Ambient AI — 1st Prize)
description: Real-time privacy blurring at target FPS on-device under thermal and power constraints — 1st Prize, SNU Ambient AI Competition.
img: assets/img/projects/W_2_ambient/cover.jpg
importance: 8
category: work
tags: [On-Device ML, PyTorch Mobile, Android, OpenCV]
award: "1st Prize"
giscus_comments: true
---

**Outcome.** Built a mobile blurring pipeline achieving **real-time FPS** with consistent quality under battery and thermal limits; won **1st prize**.

**Role**: Team member (4) · **Dates**: Aug–Sep 2024 · **Stack**: PyTorch-Mobile / NNAPI, Android, OpenCV

### Highlights
- Explored **model/runtime trade-offs** (quantization, input scaling) with a deterministic harness for **latency & quality**.
- Implemented **graceful degradation** policies to sustain FPS under thermal throttling.
- Delivered **demo app** and benchmark report; coordinated split workstreams (model, runtime, UX).

{% include figure.liquid path="assets/img/projects/W_2_ambient/app.jpg" title="Demo app" class="img-fluid rounded z-depth-1" %}

<!-- {% include video.liquid path="https://www.youtube.com/embed/1xL6tBFlIoY" class="img-fluid rounded z-depth-1" %} -->
<div style="position:relative; padding-bottom:56.25%; height:0; overflow:hidden; border-radius:6px;">
  <iframe
    src="https://www.youtube.com/embed/1xL6tBFlIoY"
    style="position:absolute; top:0; left:0; width:100%; height:100%;"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>
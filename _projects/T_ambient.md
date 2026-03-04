---
layout: page
title: On-Device Real-Time Blurring
description: Real-time privacy blurring at target FPS on-device under thermal and power constraints — 1st Prize, SNU Ambient AI Competition.
img: assets/img/projects/T_ambient/cover.jpg
importance: 8
category: tech
tags: [On-Device ML, PyTorch Mobile, Android, YOLO]
award: "1st Prize — SNU Ambient AI"
proj_role: "Team of 5"
proj_dates: "Aug–Sep 2024"
proj_stack: "PyTorch Mobile · Android · YOLO"
tldr: "Built a mobile privacy-blurring pipeline that hits target FPS on-device under real battery and thermal constraints — won 1st prize at the SNU Ambient AI Competition."
links:
  - label: "Demo Video"
    url: "https://www.youtube.com/watch?v=1xL6tBFlIoY"
giscus_comments: true
---

{% include project_header.liquid %}



<div class="row mt-3">
  <div class="col-md-6">
    {% include figure.liquid path="assets/img/projects/T_ambient/cover.jpg" title="Demo app" class="img-fluid rounded z-depth-1" %}
  </div>
  <div class="col-md-6">
    {% include figure.liquid path="assets/img/projects/T_ambient/demo2.jpg" title="Demo app" class="img-fluid rounded z-depth-1" %}
  </div>
</div>

---

### Problem

Privacy-sensitive blurring (faces, license plates) must run **on-device** — no cloud round-trips. The hard constraint: hitting a target FPS on a mid-range Android phone while the battery drains and the SoC throttles.

Most approaches optimize for accuracy in isolation. We had to co-optimize **model size, runtime backend, and degradation policy** simultaneously.

---

### Approach
{% include figure.liquid path="assets/img/projects/T_ambient/model_light.jpg" title="App UI" class="img-fluid rounded z-depth-1" %}
<div class="row mt-3">
  <div class="col-md-6">
    <p><strong>Runtime</strong></p>
    <ul>
      <li>Evaluated PyTorch Mobile vs NNAPI backend across thermal states</li>
      <li>Implemented graceful degradation — reduced resolution at high thermal load to sustain FPS</li>
    </ul>
  </div>
  <div class="col-md-6">
    <p><strong>Model optimization</strong></p>
    <ul>
      <li>Explored quantization strategies (INT8, FP16) and input scaling trade-offs</li>
      <li>Built a deterministic latency + quality harness for controlled comparison</li>
    </ul>
    
  </div>
</div>

---

### Results

| Config | FPS (normal) | FPS (throttled) | Quality |
|---|---|---|---|
| Baseline (FP32) | target | drops | high |
| INT8 quantized | ✅ target | ✅ target | acceptable |
| + degradation policy | ✅ target | ✅ sustained | adaptive |

Delivered a demo app and benchmark report. Coordinated split workstreams across model, runtime, and UX subteams.

---

### Demo

<div style="position:relative; padding-bottom:56.25%; height:0; overflow:hidden; border-radius:6px;">
  <iframe
    src="https://www.youtube.com/embed/1xL6tBFlIoY"
    style="position:absolute; top:0; left:0; width:100%; height:100%;"
    frameborder="0"
    allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
    allowfullscreen>
  </iframe>
</div>

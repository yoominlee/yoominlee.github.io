---
layout: page
title: Classifying Visually Similar Furniture
description: End-to-end classification pipeline on a self-rendered 3D dataset — interior design domain knowledge translated directly into training data.
img: assets/img/projects/T_furniture/cover.jpg
importance: 6
category: tech
tags: [TensorFlow, 3D Rendering, Dataset Design, Python]
giscus_comments: true
---

{% include figure.liquid path="assets/img/projects/T_furniture/dataset-grid.jpg" title="Self-rendered furniture dataset" class="img-fluid rounded z-depth-1" %}

**Outcome.** Built a full classification pipeline from scratch — 3D modeling → rendering → TensorFlow training — achieving consistent accuracy gains through iterative model refinements on a self-created dataset.

---

### The Dataset Problem

Most furniture datasets use web-scraped images with inconsistent lighting, backgrounds, and angles. Training on this noise makes it hard to know whether the model struggles with the *category* or the *context*.

I built the dataset using 3D modeling and rendering (SketchUp / Rhino), controlling for the variables that matter:

- **Consistent lighting and background** across all categories
- **Multiple angles** per object to improve generalization
- **Rigorous splits** to prevent leakage between visually similar categories

{% include figure.liquid path="assets/img/projects/T_furniture/renders.jpg" title="Rendered samples from the self-created dataset" class="img-fluid rounded z-depth-1" %}

---

### Model Pipeline

Started with a TensorFlow CNN baseline, then refined iteratively:

| Stage | Change | Effect |
|---|---|---|
| Baseline | CNN trained from scratch | — |
| Refinement 1 | Data augmentation + learning rate tuning | +accuracy |
| Refinement 2 | Transfer learning (pretrained backbone) | +accuracy |

---

### Why This Project

Interior architecture training means thinking carefully about what makes two chairs *different* — proportion, material, silhouette. That domain knowledge directly shaped how categories were defined and how the dataset was constructed. The rendering pipeline turned design skills into training data.

---

**Role**: Individual · **Dates**: Mar–Jun 2023 · **Stack**: TensorFlow, SketchUp / Rhino, Python

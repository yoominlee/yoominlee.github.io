---
layout: page
title: Fine-Grained Furniture Classification
description: From self-rendered 3D dataset and CNN baseline to CLIP-based few-shot fine-grained recognition with context conditioning.
img: assets/img/projects/T_furniture/cover.jpg
importance: 6
category: tech
tags: [TensorFlow, PyTorch, CLIP, Few-Shot Learning, 3D Rendering, HuggingFace, Python]
proj_role: "Individual → Undergraduate researcher"
proj_dates: "Mar 2023–Jan 2024"
giscus_comments: true
---
{% include project_header.liquid %}


{% include figure.liquid path="assets/img/projects/T_furniture/dataset-grid.jpg" title="Self-rendered furniture dataset" class="img-fluid rounded z-depth-1" %}

Two-phase project: first building a controlled 3D rendered dataset and CNN baseline, then extending to CLIP-based few-shot fine-grained classification with context conditioning.

---

## Phase 1 — Dataset & CNN Baseline

**Role**: Individual · **Dates**: Mar–Jun 2023 · **Stack**: TensorFlow, SketchUp / Rhino, Python

### The Dataset Problem

Most furniture datasets use web-scraped images with inconsistent lighting, backgrounds, and angles. Training on this noise makes it hard to know whether the model struggles with the *category* or the *context*.

I built the dataset using 3D modeling and rendering (SketchUp / Enscape), controlling for the variables that matter:

- **Consistent lighting and background** across all categories
- **Multiple angles** per object to improve generalization
- **Rigorous splits** to prevent leakage between visually similar categories


### Model Pipeline

Started with a TensorFlow CNN baseline, then refined iteratively:

| Stage | Change | Effect |
|---|---|---|
| Baseline | CNN trained from scratch | — |
| Refinement 1 | Data augmentation + learning rate tuning | +accuracy |
| Refinement 2 | Transfer learning (pretrained backbone) | +accuracy |

Interior architecture training means thinking carefully about what makes two chairs *different* — proportion, material, silhouette. That domain knowledge directly shaped how categories were defined and how the dataset was constructed.

---

## Phase 2 — CLIP-Based Few-Shot Extension

**Role**: Undergraduate researcher · **Dates**: Oct 2023–Jan 2024 · **Stack**: PyTorch, HuggingFace, Pandas

### Motivation

The CNN baseline required substantial labeled data per category. Fine-grained furniture recognition is a natural few-shot problem — categories are visually similar and labels are expensive. CLIP's vision-language alignment offered a better prior.

### Approach

Added lightweight **context conditioning** to a CLIP-style baseline:

- Engineered **geographic and language priors** as auxiliary inputs
- Built **fusion heads** to blend visual and contextual signals
- Ablated conditioning strength and prompt variants systematically
- Built **stratified few-shot splits** with seeded runs for full reproducibility


<!-- **Outcome:** Consistent accuracy gains in few-shot regimes without sacrificing inference speed. -->

---

**Role**: Individual (Phase 1) → Undergraduate researcher (Phase 2) · **Dates**: Mar 2023–Jan 2024

---
layout: page
title: About Me
permalink: /about/
nav: true
nav_order: 1

_styles: >
  .about-bio-wrap {
    display: grid;
    grid-template-columns: 1fr 280px;
    gap: 3rem;
    align-items: start;
    margin-top: 2rem;
  }
  @media (max-width: 720px) {
    .about-bio-wrap {
      grid-template-columns: 1fr;
    }
    .about-bio-photo {
      order: -1;
    }
  }
  .about-bio-photo img {
    width: 100%;
    display: block;
    border-radius: 2px;
  }
  .about-bio-text {
    font-weight: 300;
    line-height: 1.8;
    font-size: 1rem;
  }
  .about-bio-text p {
    margin-bottom: 1.2rem;
  }
  .about-bio-text a {
    color: var(--global-text-color);
    font-weight: 700;
    text-decoration: none;
    border-radius: 2px;
    padding: 0 2px;
    transition: background 0.15s ease;
  }
  .about-bio-text a:hover {
    background: rgba(0,0,0,0.06);
  }
  .about-bio-links {
    display: flex;
    flex-wrap: wrap;
    gap: 1.2rem;
    margin-top: 2rem;
    font-size: 0.78rem;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    border-top: 1px solid var(--global-divider-color);
    padding-top: 1.2rem;
  }
  .about-bio-links a {
    color: var(--global-text-color);
    text-decoration: none;
    border-bottom: 1px solid var(--global-text-color);
    padding-bottom: 1px;
    font-weight: 500;
    transition: color 0.15s ease, border-color 0.15s ease;
  }
  .about-bio-links a:hover {
    color: var(--global-theme-color);
    border-color: var(--global-theme-color);
  }
  .post-header .post-title { display: none; }
  .about-bio-display-title {
    font-size: clamp(1.8rem, 4vw, 2.8rem);
    font-weight: 300;
    letter-spacing: 0.02em;
    margin-bottom: 2rem;
    color: var(--global-text-color);
  }
  .about-bio-caption {
    margin-top: 0.6rem;
    line-height: 1.65;
  }
  .caption-name {
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--global-text-color);
  }
  .caption-location,
  .caption-weather {
    font-size: 0.72rem;
    letter-spacing: 0.04em;
    color: var(--global-text-color-light);
  }
---

<!--
<div class="about-bio-wrap">
  <div class="about-bio-text">
    <p><strong>M.S. student in Computer Science (AI)</strong> at the <a href="https://www.cs.usc.edu/">University of Southern California</a>, working in <strong>computer vision</strong> and <strong>applied machine learning</strong> - focus on measurable quality/robustness and reliable, reproducible deployment. Especially interested in evaluation under distribution shift. </p>

    <p>Previously, a research member in the AIoT Group at <a href="https://en.snu.ac.kr/index.html">Seoul National University</a>, and an undergraduate researcher in the Multimodal AI Lab at <a href="https://www.hanyang.ac.kr/web/eng">Hanyang University</a>. Earlier, worked at <a href="https://en.coga-robotics.com/">COGA Robotics</a>'s advanced R&D center. Projects have spanned sensor–model co-design for robust recognition, dataset design and protocol building, and hardening ML pipelines for real-world use.</p>

    <p>Received a B.S. in <strong>Computer Science & Interior Architecture Design</strong> from Hanyang University. The design background sharpened my spatial intuition and human-centered judgement, which carries into building clear, reproducible ML baselines and fast demos.</p>

    <p>If you'd like to discuss practical ML or vision systems, feel free to reach out.</p>

    <div class="about-bio-links">
      <a href="mailto:yoomin0104@gmail.com">Email</a>
      <a href="https://github.com/yoominlee" target="_blank">GitHub</a>
      <a href="https://www.linkedin.com/in/yoominlee1" target="_blank">LinkedIn</a>
      <a href="/cv/">CV</a>
    </div>
  </div>

  <div class="about-bio-photo">
    <img src="{{ '/assets/img/ym3.jpg' | relative_url }}" alt="Yoomin Lee">
    <p class="about-bio-caption">Yoomin Lee — Los Angeles, CA</p>
  </div>
</div>
-->

<h1 class="about-bio-display-title">Yoomin (Elaine) Lee</h1>

<div class="about-bio-wrap">
  <div class="about-bio-text">
    <p>Hello! My name is Yoomin Lee — I also go by Elaine. I'm currently an M.S. student in Computer Science (AI) at the <a href="https://www.cs.usc.edu/">University of Southern California</a>, where my research focuses on <strong>computer vision</strong> and <strong>applied machine learning</strong> — particularly building systems that are reliable and measurable in the real world.</p>

    <p>Previously, I was a researcher in the AIoT Group at <a href="https://en.snu.ac.kr/index.html">Seoul National University</a> and an undergraduate researcher in the Multimodal AI Lab at <a href="https://www.hanyang.ac.kr/web/eng">Hanyang University</a>. Earlier, I interned at <a href="https://en.coga-robotics.com/">COGA Robotics</a>'s advanced R&D center. My projects have spanned sensor–model co-design for robust recognition, dataset design and protocol building, and hardening ML pipelines for real-world use.</p>

    <p>I hold a B.S. in <strong>Computer Science</strong> and <strong>Interior Architecture Design</strong> from Hanyang University — a combination that might seem unusual, but the design side genuinely shaped how I think about spatial problems and human-centered systems, and it's something I carry into my ML work every day.</p>

    <p>When I'm not working, you'll probably find me outside running, on the golf course, or planning the next trip. I really enjoy stepping into unfamiliar environments — whether that's a new city or a new problem — and I find that the clearest thinking often happens away from the screen!</p>

    <div class="about-bio-links">
      <a href="mailto:yoomin0104@gmail.com">Email</a>
      <a href="https://github.com/yoominlee" target="_blank">GitHub</a>
      <a href="https://www.linkedin.com/in/yoominlee1" target="_blank">LinkedIn</a>
      <a href="/cv/">CV</a>
    </div>
  </div>

  <div class="about-bio-photo">
    <img src="{{ '/assets/img/ym3.jpg' | relative_url }}" alt="Yoomin Lee">
    <div class="about-bio-caption">
      <div class="caption-name">Yoomin Lee</div>
      <div class="caption-location">@ Los Angeles, CA</div>
      <div class="caption-weather" id="weather-line">· —</div>
    </div>
  </div>
</div>

{% include weather_widget.liquid %}

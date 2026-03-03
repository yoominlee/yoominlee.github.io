---
layout: page
title: Projects
permalink: /projects/
nav: true
nav_order: 4
display_categories: [tech, design]
horizontal: false

_styles: >
  .project-overlay-card {
    border-radius: 6px;
    overflow: hidden;
    cursor: pointer;
  }
  .project-overlay-img {
    position: relative;
    overflow: hidden;
  }
  .project-overlay-img figure,
  .project-cover-placeholder {
    margin: 0;
    display: block;
  }
  .project-overlay-img img,
  .project-cover-placeholder {
    width: 100%;
    aspect-ratio: 3 / 2;
    object-fit: cover;
    display: block;
    transition: transform 0.4s ease;
  }
  .project-cover-placeholder {
    background: var(--global-code-bg-color);
  }
  .project-overlay-card:hover .project-overlay-img img {
    transform: scale(1.04);
  }
  .project-overlay {
    position: absolute;
    inset: 0;
    background: linear-gradient(transparent 20%, rgba(0,0,0,0.78) 62%);
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    padding: 0.9rem;
  }
  .project-overlay-title {
    color: #fff;
    font-size: 0.9rem;
    font-weight: 600;
    margin: 0 0 0.25rem;
    line-height: 1.3;
  }
  .project-overlay-desc {
    color: rgba(255,255,255,0.85);
    font-size: 0.76rem;
    line-height: 1.4;
    margin: 0 0 0.45rem;
    overflow: hidden;
    max-height: 0;
    opacity: 0;
    transition: max-height 0.35s ease, opacity 0.3s ease;
  }
  .project-overlay-card:hover .project-overlay-desc {
    max-height: 5rem;
    opacity: 1;
  }
  .project-overlay-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.3rem;
    overflow: hidden;
    max-height: 0;
    opacity: 0;
    transition: max-height 0.35s ease 0.05s, opacity 0.3s ease 0.05s;
  }
  .project-overlay-card:hover .project-overlay-tags {
    max-height: 3rem;
    opacity: 1;
  }
  .project-tag {
    background: rgba(255,255,255,0.18);
    color: #fff;
    padding: 0.1rem 0.5rem;
    border-radius: 2rem;
    font-size: 0.68rem;
    border: 1px solid rgba(255,255,255,0.3);
  }
  .project-badge {
    position: absolute;
    top: 0.6rem;
    padding: 0.15rem 0.6rem;
    border-radius: 2rem;
    font-size: 0.68rem;
    font-weight: 600;
    z-index: 1;
  }
  .project-badge-award {
    right: 0.6rem;
    background: var(--global-theme-color);
    color: #fff;
  }
  .project-badge-active {
    left: 0.6rem;
    background: rgba(255,255,255,0.15);
    color: #fff;
    border: 1px solid rgba(255,255,255,0.4);
  }
  .projects h2.category {
    font-size: 0.72rem;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: var(--global-text-color-light);
    border-bottom: 1px solid var(--global-divider-color);
    text-align: left;
    padding-bottom: 0.4rem;
    margin-top: 2.5rem;
    margin-bottom: 1.25rem;
    font-weight: 500;
  }
---

<div class="projects">
{% if site.enable_project_categories and page.display_categories %}
  {% for category in page.display_categories %}
  <a id="{{ category }}" href=".#{{ category }}">
    <h2 class="category">{{ category }}</h2>
  </a>
  {% assign categorized_projects = site.projects | where: "category", category %}
  {% assign sorted_projects = categorized_projects | sort: "importance" | reverse %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects_overlay.liquid %}
    {% endfor %}
  </div>
  {% endfor %}
{% else %}
  {% assign sorted_projects = site.projects | sort: "importance" | reverse %}
  <div class="row row-cols-1 row-cols-md-3">
    {% for project in sorted_projects %}
      {% include projects_overlay.liquid %}
    {% endfor %}
  </div>
{% endif %}
</div>

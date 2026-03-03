---
layout: page
title: Gallery
permalink: /gallery/
nav: true
nav_order: 6
description: A collection of moments from research, places, and life.

_styles: >
  .gallery-filters {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
  }
  .gallery-filter-btn {
    padding: 0.3rem 1rem;
    border: 1px solid var(--global-theme-color);
    border-radius: 2rem;
    background: transparent;
    color: var(--global-theme-color);
    cursor: pointer;
    font-size: 0.85rem;
    transition: background 0.2s, color 0.2s;
  }
  .gallery-filter-btn.active,
  .gallery-filter-btn:hover {
    background: var(--global-theme-color);
    color: #fff;
  }
  .gallery-grid {
    column-count: 3;
    column-gap: 1rem;
  }
  @media (max-width: 768px) { .gallery-grid { column-count: 2; } }
  @media (max-width: 480px) { .gallery-grid { column-count: 1; } }
  .gallery-item {
    position: relative;
    overflow: hidden;
    break-inside: avoid;
    margin-bottom: 1rem;
    border-radius: 6px;
    cursor: pointer;
  }
  .gallery-item img {
    width: 100%;
    aspect-ratio: 3 / 4;
    object-fit: cover;
    display: block;
    transition: transform 0.3s ease;
  }
  .gallery-item:hover img {
    transform: scale(1.04);
  }
  .gallery-caption {
    position: absolute;
    bottom: 0; left: 0; right: 0;
    background: linear-gradient(transparent, rgba(0,0,0,0.65));
    color: #fff;
    padding: 1.5rem 0.75rem 0.6rem;
    font-size: 0.82rem;
    line-height: 1.3;
    opacity: 0;
    transition: opacity 0.3s ease;
  }
  .gallery-item:hover .gallery-caption { opacity: 1; }
  .gallery-empty {
    column-span: all;
    text-align: center;
    padding: 4rem 0;
    color: var(--global-text-color-light);
    font-size: 0.95rem;
  }
---

{% assign gallery = site.data.gallery %}

<div class="gallery-filters">
  {% for cat in gallery.categories %}
    <button class="gallery-filter-btn {% if forloop.first %}active{% endif %}"
            data-filter="{{ cat.id }}">
      {{ cat.label }}
    </button>
  {% endfor %}
</div>

<div class="gallery-grid">
  {% if gallery.photos and gallery.photos.size > 0 %}
    {% for photo in gallery.photos %}
      <div class="gallery-item" data-category="{{ photo.category }}">
        <img src="{{ photo.file | prepend: 'assets/img/' | relative_url }}"
             alt="{{ photo.alt }}"
             loading="lazy"
             data-zoomable />
        {% if photo.caption %}
          <div class="gallery-caption">{{ photo.caption }}</div>
        {% endif %}
      </div>
    {% endfor %}
  {% else %}
    <div class="gallery-empty">Photos coming soon.</div>
  {% endif %}
</div>

<div style="text-align:center; margin-top: 3rem;">
  <a href="https://mapmyvisitors.com/web/1lGdALiaWil_FJ8UFkuPgJt9ZhrAAFsWKSxg74_8Jws" title="Visit tracker">
    <img src="https://mapmyvisitors.com/map.png?d=1lGdALiaWil_FJ8UFkuPgJt9ZhrAAFsWKSxg74_8Jws&cl=f5ede2&w=300&t=n&co=a6c0bf&cmo=a07d40&cmn=376275&ct=ffffff" alt="Visitor map" style="max-width:300px;" />
  </a>
</div>

<script>
  (function () {
    var btns = document.querySelectorAll('.gallery-filter-btn');
    var items = document.querySelectorAll('.gallery-item');
    btns.forEach(function (btn) {
      btn.addEventListener('click', function () {
        btns.forEach(function (b) { b.classList.remove('active'); });
        btn.classList.add('active');
        var filter = btn.dataset.filter;
        items.forEach(function (item) {
          item.style.display =
            (filter === 'all' || item.dataset.category === filter) ? 'block' : 'none';
        });
      });
    });
  })();
</script>

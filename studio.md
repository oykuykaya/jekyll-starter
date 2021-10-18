---
layout: page
title: Studio
permalink: /studio/
images:
  - image_path: /images/landing_page.jpg
    title: Landing Page
  - image_path: /images/ecs_concept.png
    title: ECS Overview
---

<ul class="photo-gallery">
  {% for image in page.images %}
    <li><img src="{{ image.image_path }}" alt="{{ image.title}}"/></li>
  {% endfor %}
</ul>
---
layout: page
title: Studio
permalink: /studio/
images:
  - image_path: /images/landing_page.jpg
    title: Landing Page
    link: /images/ecs_concept.png
  - image_path: /images/ecs_concept.png
    title: ECS Overview
    link: /images/ecs_concept.png
---

<ul class="photo-gallery">
  {% for image in page.images %}
    <li>
      <a href="{{ image.link }}">
        <img src="{{ image.image_path }}" alt="{{ image.title}}"/>
      </a>
    </li>
  {% endfor %}
</ul>
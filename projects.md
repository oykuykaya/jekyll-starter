---
layout: page
title: Projects
permalink: /projects/
images:
  - image_path: /images/landing_page.jpg
    title: Landing Page
  - image_path: /images/ecs_concept.png
    title: ECS Overview
---

[![TypeScript](https://img.shields.io/badge/--3178C6?logo=typescript&logoColor=ffffff)](https://www.typescriptlang.org/)

[![JavaScript](https://img.shields.io/badge/--F7DF1E?logo=javascript&logoColor=000)](https://www.javascript.com/)

[![Made withJupyter](https://img.shields.io/badge/Made%20with-Jupyter-orange?style=for-the-badge&logo=Jupyter)](https://jupyter.org/try)

[![made-with-python](https://img.shields.io/badge/Made%20with-Python-1f425f.svg)](https://www.python.org/)



<ul>
  {% for repository in site.github.public_repositories %}
    <li>
      <a href="{{ repository.name }}">{{ repository.name }}</a>
      {{ repository.description }}
      
    </li>
  {% endfor %}
</ul>


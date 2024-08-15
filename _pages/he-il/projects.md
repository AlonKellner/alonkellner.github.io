---
page_id: projects
layout: page
title: פרויקטים
permalink: /projects/
description: הפרויקטים שלי, בדרך כלל טכנולוגיים ונלווה אליהם קוד-פתוח ב-GitHub Repository.
nav: true
nav_order: 3
display_categories: [open-source]
horizontal: false
---

<!-- pages/projects.md -->
<div class="projects">
  {% if site.enable_categories and page.display_categories %}
    <!-- Display categorized projects -->
    {% for category in page.display_categories %}
      <a id="{{ site.data[site.active_lang].strings.categories.projects[category] }}" href=".#{{ site.data[site.active_lang].strings.categories.projects[category] }}">
        <h2 class="category">{{ site.data[site.active_lang].strings.categories.projects[category] }}</h2>
      </a>
      {% assign categorized_projects = site.projects | where: "category", category | reverse %}
      {% assign sorted_projects = categorized_projects | sort: "importance" %}
      <!-- Generate cards for each project -->
      {% if page.horizontal %}
        <div class="container">
          <div class="row row-cols-1 row-cols-md-2">
            {% for project in sorted_projects %}
              {% include projects_horizontal.liquid %}
            {% endfor %}
          </div>
        </div>
      {% else %}
        <div class="row row-cols-1 row-cols-md-3">
          {% for project in sorted_projects %}
            {% include projects.liquid %}
          {% endfor %}
        </div>
      {% endif %}
    {% endfor %}
  {% else %}
    <!-- Display projects without categories -->
    {% assign sorted_projects = site.projects | sort: "importance" %}
    <!-- Generate cards for each project -->
    {% if page.horizontal %}
      <div class="container">
        <div class="row row-cols-1 row-cols-md-2">
          {% for project in sorted_projects %}
            {% include projects_horizontal.liquid %}
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="row row-cols-1 row-cols-md-3">
        {% for project in sorted_projects %}
          {% include projects.liquid %}
        {% endfor %}
      </div>
    {% endif %}
  {% endif %}
</div>

---
page_id: drawer
layout: page
title: המגירה
permalink: /drawer/
description: המגירה היצירתית שלי. אני כותב בעיקר בעברית.
nav: true
nav_order: 7
display_categories: [poetry, stories]
horizontal: false
---

<!-- pages/drawer.md -->
<div class="drawer">
  {% if site.enable_categories and page.display_categories %}
    <!-- Display categorized drawer -->
    {% for category in page.display_categories %}
      <a id="{{ site.data[site.active_lang].strings.categories.drawer[category] }}" href=".#{{ site.data[site.active_lang].strings.categories.drawer[category] }}">
        <h2 class="category">{{ site.data[site.active_lang].strings.categories.drawer[category] }}</h2>
      </a>
      {% assign categorized_drawer = site.drawer | where: "category", category | reverse %}
      {% assign sorted_drawer = categorized_drawer | sort: "importance" %}
      <!-- Generate cards for each draw -->
      {% if page.horizontal %}
        <div class="container">
          <div class="row row-cols-1 row-cols-md-2">
            {% for page in sorted_drawer %}
              {% include drawer_horizontal.liquid %}
            {% endfor %}
          </div>
        </div>
      {% else %}
        <div class="row row-cols-1 row-cols-md-3">
          {% for draw in sorted_drawer %}
            {% include drawer.liquid %}
          {% endfor %}
        </div>
      {% endif %}
    {% endfor %}
  {% else %}
    <!-- Display drawer without categories -->
    {% assign sorted_drawer = site.drawer | sort: "importance" %}
    <!-- Generate cards for each draw -->
    {% if page.horizontal %}
      <div class="container">
        <div class="row row-cols-1 row-cols-md-2">
          {% for draw in sorted_drawer %}
            {% include drawer_horizontal.liquid %}
          {% endfor %}
        </div>
      </div>
    {% else %}
      <div class="row row-cols-1 row-cols-md-3">
        {% for draw in sorted_drawer %}
          {% include drawer.liquid %}
        {% endfor %}
      </div>
    {% endif %}
  {% endif %}
</div>

---
page_id: story_2021-03-26_a-divine-error_ep7-comfort-zone
date: 2021-03-26
layout: page
title: "A Divine Error, Episode 7: Comfort Zone"
description: An episodical comedy about philosophy, the military, life and everything in between.
img: /assets/img/divine-apple-worm.jpeg
importance: 1
category: stories
---

Currently there is no English version of this story, you can view [the Hebrew version]({{site.baseurl}}/he-il{{page.url}}) instead.

---

<!-- pages/drawer.md -->
<div class="drawer">
<!-- Generate cards for each draw -->
{% if page.horizontal %}
    <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_ep6-'" %}
        {% include drawer_horizontal.liquid %}
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_index'" %}
        {% include drawer_horizontal.liquid %}
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_ep8-'" %}
        {% include drawer_horizontal.liquid %}
    </div>
    </div>
{% else %}
    <div class="row row-cols-1 row-cols-md-3">
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_ep6-'" %}
        {% include drawer.liquid %}
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_index'" %}
        {% include drawer.liquid %}
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains '_a-divine-error_ep8-'" %}
        {% include drawer.liquid %}
    </div>
{% endif %}
</div>

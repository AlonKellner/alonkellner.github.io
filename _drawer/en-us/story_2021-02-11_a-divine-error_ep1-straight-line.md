---
page_id: story_2021-02-11_a-divine-error_ep1-straight-line
date: 2021-02-11
layout: page
title: "A Divine Error, Episode 1: Straight Line"
description: An episodical comedy about philosophy, the military, life and everything in between.
img: /assets/img/angry-bus-driver.jpeg
importance: 1
category: stories
---

Currently there is no English version of this story, you can view [the Hebrew version]({{site.baseurl}}/he-il{{page.url}}) instead.

---

<!-- pages/drawer.md -->
<div class="drawer">
<!-- Display drawer without categories -->
{% assign sorted_drawer = site.drawer | sort: "importance" | where_exp: "draw", "draw.page_id contains '_a-divine-error_ep'" %}
<!-- Generate cards for each draw -->
{% if page.horizontal %}
    <div class="container">
    <div class="row row-cols-1 row-cols-md-2">
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains 'story_2021-02-10_a-divine-error_index'" %}
        {% include drawer_horizontal.liquid %}
    </div>
    </div>
{% else %}
    <div class="row row-cols-1 row-cols-md-3">
        {% assign draw = site.drawer | find_exp: "draw", "draw.page_id contains 'story_2021-02-10_a-divine-error_index'" %}
        {% include drawer.liquid %}
    </div>
{% endif %}
</div>

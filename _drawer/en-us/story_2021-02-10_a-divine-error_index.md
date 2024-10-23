---
page_id: story_2021-02-10_a-divine-error_index
date: 2021-02-10
layout: page
title: A Divine Error
description: An episodical comedy about philosophy, the military, life and everything in between.
img: /assets/img/divine-apple-worm.jpeg
og_image: /assets/img/divine-apple-worm.jpeg
importance: 1
category: stories
---

What would you do if you would have found an error in the fabric of creation?  
Something that proves that everything was planned, that everything is built of complex and wonderful layers that hide a single critical mistake in their core that exposes the hand that made it.

When a strange collection of people in a top secret military compound in the middle of the israeli desert found a security vulnerability in the very laws of nature itself - each of them had a different idea in mind.

---

<!-- pages/drawer.md -->
<div class="drawer">
<!-- Display drawer without categories -->
{% assign sorted_drawer = site.drawer | sort: "importance" | where_exp: "draw", "draw.page_id contains '_a-divine-error_ep'" %}
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
</div>

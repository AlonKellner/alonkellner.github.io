---
page_id: story_2021-02-10_a-divine-error_index
date: 2021-02-10
layout: page
title: טעות אלוהית, תוכן עניינים
description: סיפור קומדיה בהמשכים על פילוסופיה, צבא, החיים ומה שביניהם.
img: /assets/img/divine-apple-worm.jpeg
og_image: /assets/img/divine-apple-worm.jpeg
importance: 1
category: stories
---

מה הייתם עושים אם הייתם מוצאים טעות במרקם הבריאה?  
משהו שמוכיח שהכול תוכנן, שהכול בנוי מרבדים סבוכים ומופלאים שבלב ליבם שגיאה אחת קטנה חושפת את היד שמאחור.

כשחבורה מוזרה של אנשים במתקן צבאי מסווג ביותר בדרום הרחוק גילו פרצת אבטחה בחוקי הפיזיקה של העולם עצמו -לכל אחד מהם היה רעיון משלו.

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

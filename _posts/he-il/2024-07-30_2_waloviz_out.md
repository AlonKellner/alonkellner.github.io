---
layout: post
title: הוצאתי את WaloViz!
date: 2024-07-30
description: חבילת הקוד-פתוח החדשה שלי, WaloViz
tags: waloviz open-source python github
categories: software research open-source
thumbnail: /assets/img/waloviz-logo-horizontal.png
---

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-horizontal.png" title="הלוגו של WaloViz" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    תעיפו מבט ב<a href="https://waloviz.com">אתר הרשמי של WaloViz!</a>
</div>

### Quick Links

[האתר של WaloViz :globe_with_meridians:](https://waloviz.com)  
[ה-Github Repo :octocat:](https://github.com/AlonKellner/waloviz/)
[דף הפרויקט בפורטפוליו :bust_in_silhouette:](../projects/open-source_2024-07-25_waloviz)

## שמע + Jupyter == :tired_face:

בכל פרויקט מחקר שמע נתקלתי באותה בעיה שוב ושוב - לעבוד עם שמע במחברות Jupyter זה קשה מדי!

ספציפית, לבחון מקטע שמע לעומק זה קשה באופן מפתיע, זה דורש גם להקשיב וגם להסתכל במשהו שנקרא ספקטרוגרמה (תעיפו מבט בהסבר שלי [מה זו ספקטרוגרמה?](../projects/open-source_2024-07-25_waloviz/#whats-a-spectrogram)).  
זה בדיוק למה יצרתי את WaloViz, כדי לעבוד עם שמע במחברות Jupyter בצורה הבאה:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/waloviz/tldr.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

נסו ללחוץ על הספקטרוגרמה מעל, המנגינה תתחיל להתנגן :)
כדי ללמוד עוד על איך להשתמש ב-WaloViz, קראו ב[אתר התיעוד של WaloViz!](https://waloviz.com)

## פרויקט הקוד-פתוח הראשון שלי!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-github-top.png" title="ה-GitHub Repo שלנו!" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    אם אתם רוצים לעזור לפרויקט, בואו ל-<a href="https://github.com/AlonKellner/waloviz/">GitHub Repo שלנו!</a> תסתכלו מה יש שם ותאמרו שלום, אנחנו נחמדים :)
</div>

זו הפעם הראשונה שאני הבעלים של פרויקט קוד-פתוח, אני ממש נרגש לבנות את הקהילה.  
אם אהבתם את WaloViz, תשקלו לתת לנו :star2: ב-[Github Repo שלנו](https://github.com/AlonKellner/waloviz/)!

אם אתם רוצים לעזור - **WaloViz הוא פרויקט ידידותי למתחילים!**  
אנחנו מזמינים כל אחד לעזור, ללא קשר לרמת הנסיון בתחום.  
הנה שלוש סיבות למה WaloViz היא טובה למתחילים:

1. **כמות הקוד הטנה** - אין הרבה מה ללמוד כדי להתחיל לעבוד
2. **הכול מתועד** - הסטנדרט שלנו הוא לתעד על פונקציה, מתודה ומחלקה
3. **להכל יש אוטומציה** - מה סטנדרט הקוד שלנו? אוטומציות של בדיקות (testing, formatting, linting, type-checking) יעזרו לכם עם זה :)

רוצים לנסות? תתחילו ב-[README](https://github.com/AlonKellner/waloviz/) שלנו ואז עברו ל[מדריך העזרה](https://github.com/AlonKellner/waloviz/blob/main/CONTRIBUTING.md) שלנו, אתם מסוגלים!

שימו לב ש-WaloViz בגרסת אלפא, אבל אנחנו מתכננים להוציא גרסת בטא עוד חודש ומאוחר יותר השנה - גרסת `1.0` רשמית!

זהו לבינתיים ל-WaloViz, אפרסם עדכונים כשהבטא תגיע חודש הבא, ובתקווה עוד פרויקטי קוד-פתוח מגיעים בקרוב, אז צפו לחדשות בשבועות הקרובים :wink:

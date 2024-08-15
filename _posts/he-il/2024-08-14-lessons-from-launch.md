---
layout: post
title: תובנות מהשקת קוד-פתוח
date: 2024-08-14 13:00:00
description: למדתי המון מלהשיק את WaloViz, הפוסט הזה עוסק בחוויה שלי, מסקנותיי ותוכניותיי.
tags: software research open-source
categories: professional
thumbnail: /assets/img/waloviz-star-history-2024-08-14.svg
---

[:globe_with_meridians: האתר של WaloViz :globe_with_meridians:](https://waloviz.com), [:star: ה-GitHub Repo :star:](https://github.com/AlonKellner/waloviz/), [:arrow_forward: דמו ב-Google Colab :arrow_forward:](https://colab.research.google.com/drive/1euQCxaNlTg0pGvXz6d7RSoDhM3B1k7dy), [:bust_in_silhouette: דף הפרויקט בפורטפוליו :bust_in_silhouette:](../../../projects/open-source_2024-07-25_waloviz)

<br/>
<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-star-history-2024-08-14.svg" title="היסטוריית הכוכבים של WaloViz, 14.08.2024" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 תראו את <a href="https://star-history.com/#AlonKellner/waloviz&Date">היסטוריית הכוכבים העדכנית שלנו!</a>
</div>

לפני שבועיים בדיוק השקתי את פרויקט הקוד הפתוח הראשון שלי, WaloViz.

**וואו**.

השקת קוד-פתוח היא מסע, רק התחלתי את שלי ואני כבר המום ממה שקרה, מה שלמדתי ומה שאני עוד לומד בדרך.

אבל זה המקום שבו אני נמצא עכשיו, היום, עדיף שאתחיל בהתחלה.

בפוסט הזה אשתף אתכם בתהליך שעברתי, אם אתם מתכננים להקים או להשיק פרויקט קוד-פתוח - זה הפוסט בשבילכם :)

> אם אתם לא יודעים מה זה WaloViz, קראו את [דף הפרויקט של WaloViz](../../../projects/open-source_2024-07-25_waloviz) או את [הבלוג פוסט של השקת WaloViz](../waloviz-out).

## הכנות

WaloViz היא היורשת של הגרסה המקורית שנקראה WaViz, זה לא היה קוד-פתוח, רק כלי פנימי שידעתי שיכול להיות שימושי עבור אנשים נוספים.  
כשהתחלתי לעבוד על WaloViz כבר ידעתי אילו פיטצ'רים נחוצים ואילו אתגרים טכניים עומדים לפני, כך שהפיתוח התקדם חלק.

ובכל זאת, עבדתי קשה על דברים אחרים וקריטיים יותר.  
שלושה במיוחד:

### "קוד-פתוח"יות

ניסיתי לעקוב אחרי עקרונות קוד-פתוח, קראו את [opensource.guide](https://opensource.guide/), למדתי ממנו הרבה.  
כמו כן, השקעתי זמן רב בשילוב כלי אוטומציה ופיתוח כדי להקל על ה-contributor המתחיל והמזדמן להצטרף:

1. [Github Actions](https://docs.github.com/en/actions) - פתרון CI\CD רב תכליתי עם קהילה ענקית, עבור תהליכי CI\CD אוטומטיים, WaloViz משתמשת בו כדי להפוך יצירת דוקומנטציה לאוטומטית, פרסום חבילות , בדיקות CI וכדו'.
2. [VSCode Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers) - סביבת פיתוח מקומית מבוססת Docker, ל-On-Boarding קל ו-Setup לסביבת הפיתוח, אתה פשוט פותח את ה-repo וזה עושה זאת כל השאר בשבילך.
3. [pre-commit](https://pre-commit.com/) - תשתית לניהול ה-pre-commit hooks, היא מריצה ולידציות ותיקונים של Pyright, Ruff, Prettier ועוד אוטומציות על כל הקוד בכל commit, כמו גם בכל push בעזרת Github Actions.
4. [Pyright](https://microsoft.github.io/pyright/#/) - עושה Static Typing ל-Python, זה חושף מלא באגים פוטנציאליים, שווה את המאמץ.
5. [Ruff](https://docs.astral.sh/ruff/) - עושה Python Formatting & Linting, זה מהיר ועצבני, הקוד שלכם ייראה וירגיש הרבה יותר טוב.
6. [Prettier](https://prettier.io/docs/en/) - עושהּ Formatting ל-Markdown, YAML ו-JSON, פשוט הופך דברים ליפים יותר :)

בקרוב אצור Github Template עבור חבילת קוד-פתוח מודרנית בפייתון עם כל אלה כלולים, אני אפרסם פוסט על זה אז הישארו מעודכנים!

### דוקומנטציה טובה

ידעתי (וקיוויתי) שאנשים יקשרו את WaloViz ל-[HoloViz ecosystem](https://holoviz.org/), אחד מסימני ההיכר של כל פרויקט HoloViz הוא תיעוד אינטראקטיבי מרשים ומושקע.  
כדי ליצור את אותו המראה והתחושה הלכתי על שימוש ב-[NBSite](https://nbsite.holoviz.org/), שהיא תשתית הדוקומנטציה של HoloViz.

**אני לא ממליץ להשתמש ב-NBSite.**  
NBSite מבוסס על [Sphinx](https://www.sphinx-doc.org/en/master/), ואם אתם לא מכוונים להיות שיבוט של פרויקט HoloViz, אתם יכולים פשוט להשתמש ב-Sphinx ישירות, זה אפילו יותר גמיש.

בכל אופן, NBSite אכן הגיעה עם extension-ים ופיטצ'רים שימושיים של Sphinx פשוט Out-of-the-Box, כמו הטמעה חלקה של output-ים של מחברות אינטראקטיביות בדוקומנטציה, כמו ממש בתחילת [דף ה-Introduction של WaloViz](https://waloviz.com).

כמו כן, השקעתי הרבה בתיעוד inline מקיף שהומר אוטומטית ל-[API Reference Manual](https://waloviz.com/en/stable/reference-manual/index.html), זה טוב גם למשתמשים שצריכים לצלול פנימה, וגם ל-contributor-ים מתחילים שרק החלו לטבול את בהונותיהם.

הדוקומנטציה של WaloViz קיבלה משוב חיובי גורף, אבל אני מקדים את עצמי :)

### מציאת קהילות יעד

רציתי שההשקה תהיה משמעותית ותמשוך את הקהלים הנכונים, לכל פרויקט יש קהילה פוטנציאלית ייחודית, כך היעדים שלי להשקה לא יהיו שלכם.  
ובכל זאת, אלה עשויים לתת לכם מושג לגבי מהן נקודות התחלה טובות ודפוסים טובים:

**קהילות אישיות**  
פוסט אישי בפייסבוק, קבוצות וואטסאפ, הודעות פרטיות, את אלו החברים והעמיתים שלכם יראו.  
הייתה לי רשימה של כ-15 הודעות פרטיות לאנשים ספציפיים, 3 קבוצות ווטסאפ רלוונטיות של חברים ופוסט אישי אחד בפייסבוק.  
החברים והעמיתים שלכם חשובים, זה אולי מרגיש שטחי לבקש עזרה מקהל שבוי אבל רק ככה אתם תתחילו את החיכוך שלכם.

אני ממליץ לבקש מהם לתמוך בפוסטים שלכם בקהילות המיינסטרים, אלו החשובות באמת.

**קהילות מיינסטרים**  
ציוץ X, פוסט ב-LinkedIn, קבוצת פייסבוק ספציפית, אלה יתנו לכם חשיפה לקהל הרחב, לאנשים שאתם לא מכירים, למשתמשים האמיתיים הראשונים שלכם. הייתה לי רשימה של 3 קבוצות וואטסאפ מיינסטרים, 2 קבוצות בפייסבוק וערוץ דיסקורד אחד.

יש רק בעיה אחת, כדי לקבל תשומת לב כלשהי - צריך **מסה קריטית** של תשומת לב ראשונית.  
תשומת לב היא כמו כסף, ברגע שיש לך קצת מהם - ניתן לייצר מהם עוד.  
כדי להגיע למסה הקריטית של לייקים או מה שזה לא יהיה תרתמו את החברים והעמיתים לעזרתכם, זה עובד :)

במקרה שלי [קהילת MDLI](https://www.facebook.com/groups/MDLI1/) הייתה היעד המרכזי שלי, זו קהילת למידה עמוקה ישראלית, להצלחה שם הייתה משמעות רבה עבור WaloViz.  
החברים שלי הביאו אותי ל-30 לייקים, בסופו של דבר בסך הכל קיבלתי 80 לייקים. **מסה קריטית**.

בדיעבד הייתי צריך להשקיע יותר בקהילות מיינסטרים בינלאומיות, ארחיב בהמשך.

**קהילות מומחים**  
זה לא מה שאתם חושבים, זו לא הקבוצה הטובה הזאת שיש לה פוסטים באיכות גבוהה מאוד, או הקבוצה הסופר נישתית עם המומחים האמיתיים בתעשייה.  
לא, כל אלה הם פשוט קהילות מיינסטרים קטנות יותר.

קהילות מומחים אינן אלה עם מומחי דומיין - אלא אלה עם מומחי קוד-פתוח.

מצאו את אלה שיכולים להזדהות אתכם, אלה שיודעים מה זה להתחיל פרויקט קוד-פתוח כי הם היו שם.

הייתה לי בראש רק קהילת מומחים אחת, ערוץ הדיסקורד של [Panel (חלק מה-HoloViz ecosystem)](https://panel.holoviz.org/).  
אם הייתי יודע מה הולך לקרות - הייתי משקיע יותר בלמצוא קהילות מומחים נוספות.

## התחלה חזקה

פרסמתי הכל, בכל מקום בבת אחת.  
ליום אחד - הרגשתי שהסרט הזה היה החיים שלי.

רצף האירועים הוביל לזינוק מדהים של עניין ב-1 באוגוסט, כפי שניתן לראות בניתוח המשתמשים הן עבור [אתר הפורטפוליו הזה ממש](https://alonkellner.com) והן עבור [הדוקומנטציה של WaloViz](https://waloviz.com):

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/portfolio-google-analytics-2024-08-14.png" title="משתמשים לאורך זמן, Google Analytics" class="img-fluid rounded z -עומק-1" %}
 </div>
</div>
<div class="caption">
 נוצר עם <a href="https://analytics.google.com/analytics">Google Analytics</a> עבור <a href="https://alonkellner.com">alonkellner.com</a>
</div>

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-cloudflare-analytics-2024-08-14.png" title="משתמשים לאורך זמן, Cloudflare Analytics" class="img-fluid rounded z -עומק-1" %}
 </div>
</div>
<div class="caption">
 נוצר עם <a href="https://www.cloudflare.com/">CloudFlare</a> עבור <a href="https://waloviz.com">waloviz.com</a>
</div>

וב[תחילת הבלוג פוסט הזה ממש](#lessons-from-launching-an-open-source) תוכלו לראות את העלייה המדהימה במספר הכוכבים [ב-WaloViz Github Repo](https://github.com/AlonKellner/waloviz/).

לרוע המזל, ההייפ הסתיים בפתאומיות, הזינוק הראשוני יצר מעט מאוד עניין מתמשך.  
לא השגתי מסה קריטית אמיתית עבור WaloViz, בה המשתמשים פשוט מוצאים אותה מכל מקום שבו הם נמצאים ללא התערבות פעילה.

אבל זה למאוחר יותר, עכשיו בואו נעבור על כמה מהפוסטים והריפוסטים האהובים עלי שאפשרו ל-WaloViz להגיע ל-50 כוכבי Github.

### MDLI

כפי שאמרתי, MDLI הייתה קהילת המיינסטרים שבראש סדר העדיפויות שלי, הנה הפוסט עצמו:

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-mdli-post.png" title="הפוסט ב-MDLI" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 ראו <a href="https://www.facebook.com/share/p/mYQtVEadLh4SJdHg/">את הפוסט ב-MDLI</a>
</div>

80 הלייקים ו-20 התגובות האלו היו ממש נחמדות ונתנו ל-WaloViz הרבה חשיפה, רבים שיבחו את איכות הדוקומנטציה, וכמו שאמרתי החברים והעמיתים תרמו את חלקם באופן מופלא, תודה חברים :)

### ה-Discord של Panel

בכנות, לא ציפיתי להרבה מהקהילה הזו, זה ערוץ קטן מלא באנשים שמעולם לא פגשתי, אבל עמדתי להיות מאוד מופתע:

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-panel-discord-post.png" title="הודעת ה-discord ב-Panel" class="img-fluid rounded z-depth-1 " %}
 </div>
</div>
<div class="caption">
 ראו את <a href="https://discordapp.com/channels/1075331058024861767/1088148883655364698/1268494576851746826">הודעת ה-discord ב-Panel</a>
</div>

כמה ממנהיגי הקהילה שלהם התחילו לדבר איתי, חלק מהם פשוט התעניינו והתחילו לנבור בקוד שלי כדי להבין איך הוא עובד, חלק פתחו PR-ים כדי לשפר את WaloViz, וחלק... ובכן, חלק היו אדיבים מספיק כדי לעזור להפיץ את הבשורה :)

### Panel - הפצת הבשורה

הדבר הראשון שקרה היה שהפוסט הראשון שלי ב-LinkedIn על WaloViz קיבל ריפוסט מ-Panel:

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-repost.png" title="הריפוסט המקורי של Panel" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 ראו את <a href="https://www.linkedin.com/posts/alonkellner_alon-kellner-waloviz-is-out-activity-7224700653732855808-m_yb?utm_source=share&utm_medium=member_desktop">הפוסט המקורי ב-LinkedIn</a>
</div>

אז Panel פרסמו שני פוסטים שונים על WaloViz:

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-first-post.png" title="הפוסט הראשון של Panel" class="img-fluid rounded z-depth- 1" %}
 </div>
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-second-post.png" title="הפוסט השני של Panel" class="img-fluid rounded z-depth- 1" %}
 </div>
</div>
<div class="caption">
 ראו את <a href="https://www.linkedin.com/company/panel-org/posts/">הדף של Panel ב-LinkedIn</a>
</div>

השבתי עם פוסט משלי ואני הצגתי את Panel הפעם:

<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-i-feature-panel.png" title="הצגתי את Panel!" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 ראו את <a href="https://www.linkedin.com/posts/alonkellner_audio-dataviz-datascience-activity-7225925608675921920-FExs?utm_source=share&utm_medium=member_desktop">הפוסט המקורי ב-LinkedIn</a>
</div>

כפי שאתם יכולים לראות אף אחד מהם לא קיבל הרבה לייקים, אז למה אני מתרגש מהם?

ובכן, שתי סיבות עיקריות, ראשית זו לא סדרה של פוסטים, זו תחילתה של שותפות, סימן של אמון וכוונות טובות ביני לבין ראשי קהילת Panel, בהכרזה הגדולה הבאה שלי אולי הם יעשו זאת שוב.  
שנית, זו הקהילה הבינלאומית הראשונה ש-WaloViz נחשפה אליה, זה נהדר, מכיוון שלא התמקדתי הרבה בקהילות בינלאומיות, למרות שבדיעבד הייתי צריך.

האינטראקציה הזו נתנה boost ל-WaloViz, גיוונה את הקהל שלי, התחילה שותפות וחיממה לי את הלב, תודה Panel!

## הצד השטוח של המגלשה (לא עובד כמו באנגלית)

כפי שציינתי בסעיף [התחלה חזקה](#התחלה-חזקה), ההייפ הגיע והלך מהר מאוד.

עכשיו, WaloViz לא גדלה בפופולריות, היא בסטטוס סטטי, עקומה שטוחה.  
זוהי עקומה גרועה עבור פרויקט קוד-פתוח.

פרויקטי קוד-פתוח צריכים קו אלכסוני ישר, עלייה מתמדת בכוכבים, הורדות או כל דבר אחר.  
כדי שזה יקרה אני חייב לעשות ארבעה דברים:

1. **לעבוד על WaloViz** - להתקדם ב-Roadmap של WaloViz, לתקן בעיות, לשפר את המהימנות, השימושיות והקריאות.
2. **להמשיך להפיץ** - להמשיך לפרסם עדכונים בבלוג הזה ובפלטפורמות אחרות, לפרסם פיטצ'ים והכרזות כמו גרסת הבטא.
3. **ליצור משפכים** - לשים את WaloViz בתוצאות החיפוש, בין אם ישירות כמו כתבת Medium, או בעקיפין כמו תשובה לשאלה רלבנטית ב-stackoverflow.
4. **לחזק שותפויות** - ליצור PR-ים לפרויקטים שכנים ולתקשר עם קהילות, כמו Panel או [AudioSample](https://github.com/deepdub-ai/audiosample) החדשה והמרגשת (היא נראית מדהים, נסו אותה!)

אלו משימות לא קלות, הן דורשות זמן, סבלנות, נחישות ומשמעת.  
לפחות עשיתי את הפוסט הזה, וזו הפצה נחמדה ;)

זהו לעת עתה, עוד בקרוב, הישארו מעודכנים :wink:

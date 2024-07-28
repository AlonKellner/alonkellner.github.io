---
page_id: open-source_2024-07-25_waloviz
layout: page
title: WaloViz
description: חבילת קוד-פתוח פייתונית של נגן שמע אינטראקטיבי עם ספקטרוגרמה מובנית.
img: /assets/img/waloviz-thumbnail.png
importance: 1
category: open-source
---

## TL;DR

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/waloviz/tldr.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

נסו ללחוץ על הספקטרוגרמה מעל, המנגינה תתחיל להתנגן :)

## מה זה WaloViz?

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-horizontal.png" title="The WaloViz logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    תעיפו מבט על  <a href="https://waloviz.com">האתר הרשמי של WaloViz!</a>
</div>

הפרויקט WaloViz הוא ספריית [קוד-פתוח](https://github.com/AlonKellner/waloviz) פייתונית למחקר שמע מבוסס מחברות Jupyter, היא יוצרת נגן שמע אינטראקטיבי עם ספקטרוגרמה מובנית ([מה זה ספקטרוגרמה?](#מה-זה-ספקטרוגרמה)).

היא עובדת עם קבצי `wav` או כל פורמט קבצי שמע אחר הודות ל-`torchaudio` ו-`ffmpeg`, והנוחות האינטראקטיבית היא הודות לגמישות ויכולת ההתאמתיות המתקדמת של ה-[HoloViz ecosystem](https://holoviz.org/), לכן השם - `wav + HoloViz = WaloViz`.

יצרתי את WaloViz עם שלושה עקרונות מכווינים:

1. היא צריכה להיות **קלה** - נדרשות רק שלוש שורות קוד כדי להתחיל להשתמש
2. היא צריכה להיות **חזקה** - יש הרבה יכולות מתקדמות, כגון ייצוא קובץ HTML או הצגת נתונים משלכם מעל הספקטרוגרמה
3. היא צריכה להיות **פתוחה** - קוד-פתוח זו הדרך הנכונה בשביל WaloViz, תעיפו מבט על [ה-GitHub Repo שלנו](https://github.com/AlonKellner/waloviz), ואם אהבתם - תשקלו לתת לנו :star2: :)

## למה התחלתי את WaloViz

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-spectrogram.png" title="WaloViz recursion!" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    כדי לראות את הדוגמא האינטראקטיבית המלאה לכו ל<a href="https://waloviz.com">אתר התיעוד של WaloViz!</a>
</div>

כשאני עובד על מחקר שמע אני תמיד צריך להקשיב לשמעים ולראות את הספקטרוגרמות שלהם ([מה זה ספקטרוגרמה?](#מה-זה-ספקטרוגרמה)), יש המון כלים ייעודיים וטובים במיוחד כדי לעשות את זה, למשל:

1. [Adobe Audition](https://www.adobe.com/il_en/products/audition.html)
2. [Audacity](https://www.audacityteam.org/)
3. [Ocenaudio](https://www.ocenaudio.com/)

הם דוגמאות טובות.  
אבל לכולם יש את אותה החולשה - הם כלי Desktop שצריכים את קובץ השמע לוקלית - בעוד המחקר שלי הוא במחברת Jupyter.

יש שיאמרו "זה לא כזו בעיה קשה, פשוט צור קובץ ואז תוריד אותו", אבל זה תהליך שנהיה יותר ויותר מציק ככל שה-Setup יותר מורכב ויש יותר קבצי שמע, מהר מאוד זה נהיה בלגן מעמיס.

הגעתי למצב שיצרתי לעצמי כל מיני ויזואליזציות מעפנות שיעזרו לי לשמוע את השמע ולהציג את הספקטרוגרמה בתוך מחברת ה-Jupyter שלי, נדהמתי לגלות שהרבה מחברי למחקר והעבודה עשו בדיוק את אותו הדבר בהרבה דרכים שונות במקרים שונים.

דברים כאלו משגעים אותי!  
אז עשיתי את הדבר ההגיוני היחידי - יצרתי עוד נגן שמע אחד שישלוט בכולם!

## מה זה ספקטרוגרמה?

> גם אם אתם יודעים מהן ספקטרוגרמות - דוגמת הספקטרוגרמה של "Twinkle" מציגה כמה יכולות מתקדמות שאולי תרצו לראות, אם לא - תרגישו בנוח [לקפוץ קדימה](#לקפוץ-קדימה) :)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/spectrogram-tomroelandts.jpg" title="A typical Spectrogram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    תמונה מתום רולנד (Tom Roeland), מהפוסט שלו <a href="https://tomroelandts.com/articles/what-is-a-spectrogram">What is a Spectrogram?</a>
</div>

ספקטרוגרמה זו מילה גדולה, פירושה הישיר הוא "תמונה של ספקטרום", או במילים אחרות זו ויזואליזציה של תדרים.

בואו ננסה לחשוב על זה במונחים מוזיקליים, לכל תו מוזיקלי יש תדר בסיס שתואם לו, זה אומר שלהשתמש בתדרים זה מאוד דומה לשימוש בתווים מוזיקליים, במובן הזה ספקטרוגרמה היא מאוד דומה לדף תווים!

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/waloviz/twinkle.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twinkle-music-sheet.png" title="Twinkle Twinkle little Star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    חלק מדף התווים של Twinkle Twinkle little Star, נלקח מ-<a href="https://commons.wikimedia.org/wiki/File:Pitch_axis_inversion.png">Wikimedia Commons</a>
</div>

ככל שמתקדמים משמאל לימין מתקדמים בזמן, וככל שעולים מלמטה למעלה עולים בגובה הצליל (התדר).

בדף תווים הרקע לבן, הכתמים השחורים אומרים שהתו ההוא מתנגן באותו הרגע.  
בספקטרוגרמה הרקע הוא שחור, וכתם צהוב בהיר אומר שהתדר ההוא מתנגן באותו הרגע.

הבדל מהותי אחד הוא שבספקטרוגרמה ככל שהכתם בהיר יותר - הצליל יהיה רועש יותר, ויש מעבר חלק בין מאוד שקט (כהה) למאוד רועש (בהיר).  
עוד הבדל הוא שבמקום סוגים שונים של כתמים, כדי לציין את משך הצליל מותחים את הכתם אופקית לקו. אורך הקו הוא משך הצליל!

לראות את התדרים של שמע בצורה ויזואלית זה מאוד חשוב, מומחה שמע יכול להבין כל מיני דברים רק מלהסתכל על הספקטרוגרמה, באופן דומה לאיך שמוזיקאי יכול להבין הרבה רק מלקרוא את דף התווים.

## יכולות מתקדמות

היכולת הראשונה שחוקרים אוהבים להשתמש בה היא הצגת עקומות מחושבות על הספקטרוגרמה.  
דוגמא מאוד פשוטה תהיה להציג את ה-Waveform או מניפולציות שלו, זה יכול להיעשות בהרבה דרכים, הנה אחת מהן:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/waloviz/overlay.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

בדוגמא מעל יש 3 עקומות מוצגות על הספקטרוגרמה:

1. ה-`waveform`, זה משתמש ב-callback כדי להשיג את ה-waveform ולהחזיר אותו כעקומה
2. ה-`envelope`, זה גם משתמש ב-callback, אבל הפעם מחשב מתוך ה-waveform את ה-envelope
3. עקומה `random`, פשוט מועברת כעקומה מחושבת מראש שצריך להציג מעל הספקטרוגרמה

מהדוגמא הפשוטה הזו אפשר לראות כמה היכולת הזו חזקה כדי להציג נתונים של משימות מורכבות כמו SAD (Speech Activity Detection), דיאריזציה, ועוד הרבה משימות שמע דומות.

יש ל-WaloViz עוד הרבה יכולות, לכו ל[אתר התיעוד של WaloViz](https://waloviz.com) כדי ללמוד עוד :)

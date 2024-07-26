---
page_id: open-source_2024-07-25_waloviz
layout: page
title: WaloViz
description: An open-source python package of an interactive audio player with a spectrogram built-in.
img: /assets/img/waloviz-thumbnail.png
importance: 1
category: open-source
related_publications: true
---

## TL;DR

{::nomarkdown}
{% assign jupyter_path = '/waloviz-tldr.ipynb' | prepend: site.active_lang | prepend: 'assets/jupyter/' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

Try clicking the spectrogram above, it will start playing :)

## What is WaloViz?

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-horizontal.png" title="The WaloViz logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Take a look at the [official WaloViz website!](https://waloviz.com)
</div>

WaloViz is an [open-source](https://github.com/AlonKellner/waloviz) python package for interactive Jupyter notebook based audio research, it creates an interactive audio player with a spectrogram built-in ([What's a Spectrogram?](#What's-a-Spectrogram?)).

It works with `wav` files or any other audio format thanks to `torchaudio` and `ffmpeg`, and it is comfortably interactive thanks to the high customizability of the [HoloViz ecosystem](https://holoviz.org/), hence the name - `wav + HoloViz = WaloViz`.

I made WaloViz with three main things in mind:

1. **It should be EASY** - starting to use it requires 3 lines of code
2. **It should be POWERFUL** - there are many advanced features, such as exporting to an HTML file and overlaying custom data
3. **It should be OPEN** - open-source is the right place for WaloViz to exist, take a look at [our GitHub Repo](https://github.com/AlonKellner/waloviz), and consider giving us a :star2:!

## Why I started WaloViz

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-spectrogram.png" title="WaloViz recursion!" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    For the full interactive example go to [the WaloViz documentation website!](https://waloviz.com)
</div>

When I am doing audio research I constantly need to hear audio files and see their spectrograms ([What's a Spectrogram?](#What's-a-Spectrogram?)), for that there are many good dedicated tools that do just that:

1. [Adobe Audition](https://www.adobe.com/il_en/products/audition.html)
2. [Audacity](https://www.audacityteam.org/)
3. [Ocenaudio](https://www.ocenaudio.com/)

But they all suffer from the same problem - they are desktop tools that need the audio file locally - while my research is in a Jupyter notebook.

Some might say "that's not that big of an issue, just create a file and download it", but that becomes more and more annoying with more elaborate setups which have more audio files, very quickly it becomes a laboursome mess.

I found myself creating all sorts of ragtag visualizations to help me both play the audio and view it's spectrogram, I was shocked when I learned that many of my colleagues did the exact same thing in many different ways occasions.

Things like that drive me nuts!  
So I did the only sensible thing anyone would do - I created yet another audio player to rule them all :)

## What's a Spectrogram?

Even if you know what Spectrograms are - the "Twinkle" spectrogram example will show you some advanced features you might like to know, or just feel free to [skip ahead](#Advanced-Features) :)

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/spectrogram-tomroelandts.jpg" title="A typical Spectrogram" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Image by Tom Roeland, from [his post "What is a Spectrogram?"](https://tomroelandts.com/articles/what-is-a-spectrogram)
</div>

A Spectrogram is a big word, it literally means "A Picture of a Spectrum", or in other words it's a visualization of frequencies.

Let's try to think of in musical terms, each musical note has a base frequency associated with it, meaning that using frequencies is very similar to using musical notes, in that sense a Spectrogram is very similar to a musical sheet!

{::nomarkdown}
{% assign jupyter_path = '/waloviz-twinkle.ipynb' | prepend: site.active_lang | prepend: 'assets/jupyter/' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/twinkle-music-sheet.png" title="Twinkle Twinkle little Star" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    A portion of the musical sheet of "Twinkle Twinkle little Star", from [Wikimedia Commons](https://commons.wikimedia.org/wiki/File:Pitch_axis_inversion.png)
</div>

As you go from left to right you go forward in time, and as you go from bottom to top you go higher in pitch (frequency).

In a musical sheet the background is white, and a black spot means that note is played at that moment.  
In a Spectrogram the background is black, and a bright yellow spot means that a frequency is played at that moment.

One important difference is that on a Spectrogram the brighter the spot - the louder the sound, and it's a smooth transition from very quiet (dark) to very loud (bright).  
Another difference is that instead of different kinds of spots, to specify the length of the note the spot is stretched horizontally into a line. The length of the line is the length of the note!

## Advanced Features

The first feature that researchers really like is overlaying curves over the spectrogram.  
A very simple example of that would be to overlay the waveform itself or manipulations over it, it can be done in many ways, here is one of them:

{::nomarkdown}
{% assign jupyter_path = '/waloviz-overlay.ipynb' | prepend: site.active_lang | prepend: 'assets/jupyter/' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

In the above example there are 3 overlaid curves:

1. The `waveform`, it uses a callback to read the waveform and calculate the curve from it
2. The `envelope`, it also uses a callback, but this time does a calculation over the waveform to create the curve
3. A `random` curve, it is just passed as a precalculated curve to be displayed over the spectrogram

From this simple example you can see how powerful this feature is for visualizing cases like SAD (Speech Activity Detection), Diarization, and many other audio related tasks.

There are many more features, go to the [WaloViz documentation website](https://waloviz.com) to learn more :)

---
layout: post
title: WaloViz is Out!
date: 2024-07-30 14:00:00
description: My newest open-source project, WaloViz
tags: software research open-source
categories: professional
thumbnail: /assets/img/waloviz-logo-vertical-2-3-ratio.png
---

[:globe_with_meridians: WaloViz Website :globe_with_meridians:](https://waloviz.com), [:star: GitHub Repo :star:](https://github.com/AlonKellner/waloviz/), [:arrow_forward: Google Colab Demo :arrow_forward:](https://colab.research.google.com/drive/1euQCxaNlTg0pGvXz6d7RSoDhM3B1k7dy), [:bust_in_silhouette: Portfolio Project Page :bust_in_silhouette:](../../../projects/open-source_2024-07-25_waloviz)

<br/>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-logo-horizontal.png" title="The WaloViz logo" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Take a look at the <a href="https://waloviz.com">official WaloViz website!</a>
</div>

## Audio + Jupyter == :tired_face:

On every single audio research project I got into I faced the same problem again and again - working with audio in Jupyter notebooks is too difficult!

Specifically, inspecting an audio snippet in depth is a surprisingly difficult task, it requires both listening and viewing something called a spectrogram (see my explanation about [What's a Spectrogram?](../../../projects/open-source_2024-07-25_waloviz/#whats-a-spectrogram)).  
That is precisely what I made WaloViz for, working with audio in Jupyter notebooks, like so:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/waloviz/tldr.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

Try clicking the spectrogram above, it will start playing :)  
To learn more about how to use WaloViz go to the [WaloViz Documentation Website!](https://waloviz.com)

## My First Open-Source Project!

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-github-top.png" title="Our GitHub Repo!" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    If you want to contribute, come to our <a href="https://github.com/AlonKellner/waloviz/">GitHub Repo!</a> Take a look around and say hi, we're friendly :)
</div>

WaloViz is the first open-source project that I own, I am really excited to get to build an open-source community.  
If you like it, consider giving us a :star2: on our [GitHub Repo](https://github.com/AlonKellner/waloviz/)!

If you want to contribute - **WaloViz is a Beginner Friendly project!**  
We welcome anyone to contribute, no matter your experience level.  
Here are three things that make WaloViz great for beginners:

1. **Our codebase is SMALL** - there is not much to learn to start working
2. **Everything is DOCUMENTED** - our standard is to document inline each and every single function, method or class
3. **Standards are AUTOMATED** - what are our code standards? Automated testing, formatting, linting and type-checking will help you with that :)

Want to give it a go? Start by reading our [README](https://github.com/AlonKellner/waloviz/) and then read our [Contributing Guide](https://github.com/AlonKellner/waloviz/blob/main/CONTRIBUTING.md), you can do it!

WaloViz is in early-alpha, but we plan to go Beta in a month, and later this year - an official `1.0` version!

That's it for WaloViz for now, I will publish updates when the Beta arrives next month, and hopefully more open-source projects are coming soon, so stay tuned :wink:

---
layout: post
title: Lessons from Launching an Open-Source
date: 2024-08-14 13:00:00
description: Launching WaloViz taught me a lot, this post is about my experience, conclusions and plans.
tags: software research open-source
categories: professional
thumbnail: /assets/img/waloviz-star-history-2024-08-14.svg
---

[:globe_with_meridians: WaloViz Website :globe_with_meridians:](https://waloviz.com), [:star: GitHub Repo :star:](https://github.com/AlonKellner/waloviz/), [:arrow_forward: Google Colab Demo :arrow_forward:](https://colab.research.google.com/drive/1euQCxaNlTg0pGvXz6d7RSoDhM3B1k7dy), [:bust_in_silhouette: Portfolio Project Page :bust_in_silhouette:](../../../projects/open-source_2024-07-25_waloviz)

<br/>
<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-star-history-2024-08-14.svg" title="WaloViz star history, 14.08.2024" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See our <a href="https://star-history.com/#AlonKellner/waloviz&Date">current Star History!</a>
</div>

Exactly two weeks ago I launched my first open-source project, WaloViz.

**WOW**.

Launching an open-source is a journey, I just started mine and I'm already blown away by what happened, and what I learned and am learning along the way.

But that's where I am now, the present day, I should start from the beginning.

In this post I'll share with you my process, if you're planning on starting or launching an open-source project - this is the post for you :)

> If you don't know what's WaloViz, read [the WaloViz Project Page](../../../projects/open-source_2024-07-25_waloviz) or [the WaloViz Launch blog post](../waloviz-out).

## Preparations

WaloViz is the successor of the earlier version called WaViz, it wasn't open-source, just an internal tool that I knew could be useful for other people.  
When I started working on WaloViz I already knew what features are needed and what technical challenges lie ahead, so development went smoothly.

Still, I worked hard on other more crucial things.  
Three in particular:

### Open-Sourcability

I tried following open-source principles, read the [opensource.guide](https://opensource.guide/), I learned a lot from it.  
I also invested a lot of time in integrating automation and development tools to make it easy for the casual beginner contributor to join in:

1. [Github Actions](https://docs.github.com/en/actions) - A versatile CI\CD solution with a huge community, for automated CI\CD pipelines, WaloViz uses it to automate docs creation, package publishing, CI validations etc.
2. [VSCode Dev Containers](https://code.visualstudio.com/docs/devcontainers/containers) - A Docker based local development environment, for easy on-boarding and development setup, you literally just open the repo and it does all of the rest for you.
3. [pre-commit](https://pre-commit.com/) - A framework for managing pre-commit hooks, it integrates Pyright, Ruff, Prettier and more automatic validations and fixes, and applies them over the entire codebase on every single commit, as well as on every push with Github Actions.
4. [Pyright](https://microsoft.github.io/pyright/#/) - Python Static Typing, It uncovers tons of potential bugs, worth the effort.
5. [Ruff](https://docs.astral.sh/ruff/) - Python Formatting & Linting, it is fast and furious, your code will look and feel much better.
6. [Prettier](https://prettier.io/docs/en/) - Markdown, YAML and JSON Formatting, things are just prettier with it :)

Soon I'll create a Github Template for a modern open-source python package with all of these included, I'll make a post about it so stay tuned!

### Good Docs

I knew (and hoped) that WaloViz was going to be associated with the [HoloViz ecosystem](https://holoviz.org/), one of the hallmarks of every single HoloViz project is great interactive documentation.  
In order to have the same look and feel I went for using [NBSite](https://nbsite.holoviz.org/), which is HoloViz's docs framework.

**I do not recommend using NBSite.**  
NBSite is based on [Sphinx](https://www.sphinx-doc.org/en/master/), and if you are not going for being a HoloViz clone, you can just use Sphinx directly, it's even more customizable.

Nevertheless, NBSite did come with handy Sphinx extensions and features out-of-the-box, such as seamlessly embedding interactive notebooks outputs in your docs, like on the very start of the [Introduction Page of WaloViz](https://waloviz.com).

Also, I invested a lot in comprehensive inline documentation which got automatically converted into the [API Reference Manual](https://waloviz.com/en/stable/reference-manual/index.html), it's good both for users that need to dive-in, and for beginner contributors that are just starting to dip their toes.

The docs of WaloViz got tons of positive feedback, but I'm getting ahead of myself :)

### Finding Target Communities

I wanted the launch to be impactful and attract the right audiences, each project has a unique potential community, so my targets for the launch will not be yours.  
Still, these might give you an idea as to what are good starting points and patterns:

**Personal Communities**  
 Personal Facebook post, Whatsapp groups, DMs, these are the ones which your friends and colleagues will see.  
 I had a list of about 15 DMs for specific people, 3 relevant whatsapp groups of friends, and 1 personal post on Facebook.  
 Your friends and colleagues are important, it might seem superficial to ask for help from a captive audience but that's how you're gonna get traction.

I really recommend asking them to support your Mainstream Communities posts, these are the real important ones.

**Mainstream Communities**  
X tweet, LinkedIn post, Specific Facebook group, these will get you exposure to the crowd, people you don't know, your first real users. I had a list of 3 mainstream whatsapp groups, 2 facebook groups and 1 discord channel.

There is only one problem, to get any attention - you need a CRITICAL MASS of initial attention.  
Attention is like money, once you have some of it - it can make you more.  
To get to your critical mass of likes or whatever get you friends and colleagues involved, it works :)

In my case the [MDLI community](https://www.facebook.com/groups/MDLI1/) was my top target mainstream, it's an Israeli Deep-Learning community, success there meant a lot for WaloViz.  
My friends got me to 30 likes, eventually overall I got 80 likes. CRITICAL MASS.

In retrospect I should have invested more in international mainstream communities, more on that later.

**Expert Communities**  
These are not what you think, it's not that real good group that has very high quality posts, or that super niche group with real industry experts.  
No, those are just smaller Mainstream Communities.

Expert Communities are not those with Domain Experts - but those with Open-Source Experts.

Find those that can relate to you, those that know what it's like to be a new open-source because they've been there.

I had only 1 Expert Community in mind, the [Panel (part of the HoloViz ecosystem)](https://panel.holoviz.org/) discord channel.  
If I had known what was going to happen next - I would've tried harder to find more Expert Communities.

## A Strong Start

I posted everything, everywhere all at once.  
And for a single day - I felt like that movie was my life.

The aftermath resulted in an incredible spike of interest on the 1st of August, as indicated by the user analytics for both [this very Portfolio Website](https://alonkellner.com) and the [WaloViz Docs](https://waloviz.com):

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/portfolio-google-analytics-2024-08-14.png" title="Users over time, Google Analytics" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Generated with <a href="https://analytics.google.com/analytics">Google Analytics</a> for <a href="https://alonkellner.com">alonkellner.com</a>
</div>

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-cloudflare-analytics-2024-08-14.png" title="Users over time, Cloudflare Analytics" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    Generated with <a href="https://www.cloudflare.com/">CloudFlare</a> for <a href="https://waloviz.com">waloviz.com</a>
</div>

And on [the top of this post](#lessons-from-launching-an-open-source) you can see the incredible increase in stars in [the WaloViz Github Repo](https://github.com/AlonKellner/waloviz/).

Unfortunately the hype ends abruptly, the initial spike created very little lasting interest.  
I did not achieve true CRITICAL MASS for WaloViz, where users just find it wherever they are without active intervention.

But that is for later, now let's go over some of my favorite posts and reposts that got WaloViz to reach 50 Github stars.

### MDLI

As I said, MDLI was my top priority Mainstream Community, here's the post itself:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-mdli-post.png" title="The Hebrew MDLI post" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See <a href="https://www.facebook.com/share/p/mYQtVEadLh4SJdHg/">the post on MDLI</a>
</div>

Obviously the post is in Hebrew because it's an Israeli community, but it pretty much translates to:

> To all Speech folks - For the longest time I needed a good visualization library with interactive spectrograms in notebooks, I got frustrated and made one!
>
> You're more than welcome to try it or pass it on to whoever you think can use it.
>
> It's open-source as well, so do a Mitzvah and give a tiny star on GitHub ;)

Those 80 likes and 20 comments were really nice and got WaloViz a lot of traction, many praised the quality of the docs, and as I said my friends an colleagues did they're part wonderfully, thanks guys :)

### The Panel Discord channel

Honestly, at first I didn't expect much from this community, it's a small channel full of people that I never met, but I was about to be very surprised:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-panel-discord-post.png" title="The Panel discord message" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See <a href="https://discordapp.com/channels/1075331058024861767/1088148883655364698/1268494576851746826">the message on the Panel discord</a>
</div>

A few of their community leaders started engaging with me, some of them just got interested and started digging through my codebase to understand how it works, some opened PRs to make WaloViz better, and some... well, some were kind enough to help spread the word :)

### Panel - Spreading the Word

The first thing that happened was that my first LinkedIn post about WaloViz got reposted by Panel:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-repost.png" title="Panel original repost" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See <a href="https://www.linkedin.com/posts/alonkellner_alon-kellner-waloviz-is-out-activity-7224700653732855808-m_yb?utm_source=share&utm_medium=member_desktop">the original post on LinkedIn</a>
</div>

To be later followed with two different posts by Panel that feature WaloViz:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-first-post.png" title="Panel first post" class="img-fluid rounded z-depth-1" %}
    </div>
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-panel-second-post.png" title="Panel second post" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See <a href="https://www.linkedin.com/company/panel-org/posts/">the Panel page on LinkedIn</a>
</div>

I replied with my own repost and I featured Panel this time:

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/waloviz-launch-linkedin-i-feature-panel.png" title="I featured Panel!" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    See <a href="https://www.linkedin.com/posts/alonkellner_audio-dataviz-datascience-activity-7225925608675921920-FExs?utm_source=share&utm_medium=member_desktop">the original post on LinkedIn</a>
</div>

As you can see none of these got many likes, so why am I getting all excited about them?

Well, two main reasons, firstly it's not a series of posts, it's the beginning of a collaboration, a sign of good faith between me and the Panel community leaders, on my next big announcement they might do it again.  
Secondly, this is the first international community that WaloViz got exposed to, this is great, since I did not put a lot of focus on international communities, although in retrospect I should have.

This interaction gave WaloViz a boost, diversified my audience, started a collaboration and warmed my heart, thanks Panel!

## The Flat Side of the Slide

As I mentioned in the [Strong Start section](#a-strong-start), the hype arrived and left very quickly.

Now, WaloViz is not increasing in popularity, it's in a static status, a flat curve.  
This is a bad curve for an open-source project.

Open-Source projects need a straight diagonal line, a constant increase in stars, downloads or whatever.  
To make it happen I must do four things:

1. **Work on WaloViz** - Advance on the WaloViz roadmap, fix issues, improve reliability, usability and readability.
2. **Keep Nudging** - Keep posting updates on this blog and other platforms, share features and announcements such as the Beta version.
3. **Create Funnels** - Put WaloViz in search results, either directly like a Medium article, or indirectly like an answer to a relevant stackoverflow question.
4. **Collaborate** - Create PRs for neighboring projects and engage with communities, such as Panel or the new and exciting [AudioSample](https://github.com/deepdub-ai/audiosample) (it looks amazing, check them out!)

These are not easy tasks, they require time, patience, determination and discipline.  
At least I got this post done, which is a nice nudge ;)

That's it for now, more is coming soon, stay tuned :wink:

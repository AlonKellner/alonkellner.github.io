---
layout: post
title: A Deep Dive into my "Weighter" talk in DefenseML
date: 2024-11-26 13:00:00
description: An in depth explanation of a fascinating research effort called "Weighter" which I presented on MDLI's DefenseML conference.
tags: research
categories: professional
thumbnail: /assets/img/defenseml-banner.png
---

<br/>
<div class="row">
 <div class="col-sm mt-3 mt-md-0">
 {% include figure.liquid loading="eager" path="assets/img/defenseml/en-us/01.png" title="Opening Slide" class="img-fluid rounded z-depth-1" %}
 </div>
</div>
<div class="caption">
 Watch <a href="https://machinelearning.co.il/lp-events/defenseml/">the recording of me presenting!</a> You may also view <a href="https://docs.google.com/presentation/d/173AjB0vz8pdrKIiAR8JdxvhF1KGvq_SESwpL-LW-G78/edit?usp=sharing">the original presentation</a> :)
</div>

The DefenseML conference was fascinating and meaningful. I had the pleasure of speaking alongside talented speakers and talented organizers who invested in a conference of a very high standard.

After the lecture, I got to talk to some of the conference guests. I received many compliments, but there were also criticisms and difficulties.  
The first criticism I was told was that the LinkedIn slide was only at the beginning of the presentation - before they knew I was worth anything.  
Fortunately, this is a criticism that was easy to correct. The more general criticism that was not explicitly stated but was clear to me - is that it is difficult to understand from the lecture how things really work.

This is a criticism that I expected, in 20 minutes it is impossible to summarize all the details of a complete and extensive research effort. I tried to give a taste, intuitions, directions, but I could not provide understanding.  
In this post, I will try to answer some of the questions I was asked, clarify points that confused some people, and expand on some of the ideas presented in the lecture.

To understand this blog post you need to be familiar with the lecture itself, the kind organizers of the conference uploaded [the full lecture on their Youtube channel](https://youtu.be/wxMQJ3vXngg), you are welcome to watch it there :)

{% include video.liquid path="https://www.youtube.com/embed/wxMQJ3vXngg?si=zpaFWi3r2d1Xb541" class="img-fluid rounded z-depth-1" %}

In addition, you are welcome to go through [my presentation](https://docs.google.com/presentation/d/173AjB0vz8pdrKIiAR8JdxvhF1KGvq_SESwpL-LW-G78/edit?usp=sharing) yourself and at your own pace, regardless of the recording itself.

There are 2 parts in this blog post, the first is [Q & A](#q--a) where I'll answer some of the questions I was asked after the lecture, most of them are clarifications about the details of our research and method.  
The second part is [Deep dive & Enrichment](#deep-dive--enrichment) which will expand on subjects which I didn't have the time to get into in the lecture.

Let's start :)

## Q & A

1. **What does your model output?**  
   During training, the model has a classification head, meaning its output is N vectors of logits the size of the number of classes (the number of speakers in the train-set, in our case 856).  
   During inference, we do not use the classification head, so instead of getting N vectors of logits we get N vectors of Embeddings (in our case 256 dimensions).

2. **What does the model even learn if a "like" does not distinguish the file? What is the supervision here?**  
   The model learns to produce for each file a set of Embeddings, a subset of those Embeddings should represent the "likes" that were tagged on the file.  
   In other words, the model learns to produce Embeddings that are similar to files that have the same "like", the very fact that there should be some common Embeddings is the supervision.

3. **You talked about clustering and that it is not differentiable, but there are ways to extract differentiable weightings from clustering algorithms, have you tried them?**  
   Short answer - we didn't try, it wasn't accessible enough and we had intuitions that it wouldn't work well.  
   In a little more detail - as I elaborate later in the post about [The Simulation](#the-simulation), we had evidence that the time dimension is very significant, and a learning algorithm could do a lot that a clustering algorithm that ignores the time dimension could never do.  
   (P.S: A clustering algorithm that takes into account the time dimension is a whole complication of its own, in our literature review we didn't find anything suitable).

4. **How ​​are the layers of your "Weighter" module structured?**  
   As I elaborate later this post in [Layers from `torchaudio`](#layers-from-torchaudio), we used torchaudio's implementation of the WavLM Encoder block, basically a cute block with self-attention and positional-embeddings and of course lots of built-in hyperparameters.  
   There is nothing sophisticated in the core part. It's a Transformer.  
   But we did some interesting things around it, first we used two convolution layers to reduce the number of dimensions in channels by a factor of 12 and in time by a factor of 15, this saved a lot of VRAM and almost did not change performance, it even made training a little easier and improved performance (at least during the first few epochs).  
   Then at the output we tried to do a convolution to restore the reduced time dimension, in the end the best option was to duplicate the weightings 15 times (repeat interleave), convolutions were worse.

## Deep dive & Enrichment

Here I’ve chosen a few specific subjects from our research that I particularly liked but didn’t have time to go into detail about during the lecture.  
If you're looking to enrich your understanding of the nature of the research we conducted and how we arrived at our innovations – this section is for you :)

### Layers from `torchaudio`

We invested very little in the layers of the model; we didn’t try to create something very sophisticated. We wanted something accessible and effective with a lot of hyperparameters.  
The typical approach nowadays would be to take a layer from some model in `transformers`, but we saw that there is a decent implementation of WavLM blocks in a library we were already using – `torchaudio`.

Here’s our `import`:

```python
from torchaudio.models.wav2vec2.components import _get_wavlm_encoder, FeatureProjection
```

The function `_get_wavlm_encoder` creates a Transformer block with built-in positional embeddings, etc. It takes a sequence of vectors and outputs a sequence of the same size with self-attention, exactly what we were looking for.

The class `FeatureProjection` is just a simple transformation with layer-norm and dropout that needs to be applied before feeding the input into the encoder.

This saved us the dependency on `transformers`, and maybe it can help you too :)

### The Simulation

Before we started working with real data, we started by asking ourselves a question: what are the advantages of a diarization algorithm that learns over a clustering approach?  
Apart from it being differentiable and not engineered, we had one unique advantage – clustering ignores the time dimension.

Here’s an example that will illustrate why the time dimension is essential:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/weighter/simulation/stereo_envelope.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

This is a sample conversation from the well-known CALLHOME dataset, a typical phone call between family members.  
The envelope of each channel is displayed over the spectrogram.  
Let’s try to do what diarization does – let’s try to determine which channel is speaking at any given moment:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/weighter/simulation/loud_channel.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

The first graph above shows a very trivial calculation to determine the speaking channel - where the envelope is stronger.  
But you can see that "Real" looks very different from "Pure random", so what's different?

Note that channel switching is less common in "Real", in "Pure random" each frame has a 50% chance of switching channels, while in "Real" the chances are much lower, meaning that in "Real" the time dimension has significance.

One way to model randomness that takes the time dimension into account is a "Random walk", we used a simple calculation that creates a "Random walk" bounded between 0 and 1, as shown in the second graph.  
In the third graph we use the "Random walk" to randomly select a channel per frame with time-dependent randomness, and you can see that the two graphs look much more similar.

Based on this idea, we created a simulation of vectors that switch depending on time, and we saw that a learning model is able to separate vectors with noise four times larger than what clustering, which ignores time, could achieve.

### Confidence

Our definition of Confidence is non-trivial, as presented in this presentation, using the following formula:

$$ C(\mathbf{X}) =\frac{\sum _{j=1}^{T} X_{j}^{2}}{\sum _{i=1}^{T} X_{i}} $$

Where C is the formula for calculating Confidence, and **X** is the output of the weighting layer, T is the length of the time dimension of **X**, and X_i is the value at time i out of T in the timeline, all X_i values ​​are between 0 and 1.

To get to this, we went through a multi-step process. I will share the concepts we explored and how we progressed from one to another until we arrived at this formula.  
I think this is a classic example of iterative research based on experience, and maybe it will inspire you :)

When we started the project, we wondered how we could make the model output fewer than N vectors in a learnable way. We considered the DETR approach, which created a class called "no-class," meaning it is not a real object.  
We had to deal with the problem that, during inference, we would not have Logits but Embeddings, so we couldn’t apply the same approach as DETR.

In DETR, the training approach is similar to what we ended up using. However, initially, we decided to separate the outputs. One output of the model would be the weightings, and the second output would be the confidences.  
For example, if N = 3, we would design the model to output 6 dimensions: the first three, normalized over time, represent the weightings, and the averages over time of the last three represent the confidences.

We call the output of the weightings **X**, and the output of the confidences **Y**:

<!-- prettier-ignore -->
$$ C(\mathbf{Y}) =\frac{\sum _{j=1}^{T} Y_{j}}{T} $$

<!-- prettier-ignore -->
$$ W_{j}(\mathbf{X}) =\frac{X_{j}}{\sum _{i=1}^{T} X_{i}} $$

Note that to make Y a confidence, we averaged it since it should be a single number, while to get the weightings, we normalized X by its sum, so that it sums to one, as is appropriate for the definition of weightings.

We tried this, but we observed a strange phenomenon. It seemed that the confidence didn’t work very well. Since we did a global average, we basically forced each token to look at as much global context as possible in order to understand for each of the weightings whether it is real, even if it is 0 at that moment, meaning it is a completely different speaker.

What we decided to do was calculate the Confidence not as an average of Y, but as a weighted average of Y based on X:

<!-- prettier-ignore -->
$$ C(\mathbf{X}, \mathbf{Y}) = \sum _{j=1}^{T} Y_{j} \cdot W_{j}(\mathbf{X}) $$

<!-- prettier-ignore -->
$$ W_{j}(\mathbf{X}) = \frac{X_{j}}{\sum _{i=1}^{T} X_{i}} $$

Our rationale was that this way, the tokens at each moment in time could focus on the current moment and whether it was a real speaker, without necessarily considering the global context.  
This approach showed significant improvement.

At this point, we were quite satisfied. But when we looked at **X** and **Y**, one thing stood out to us – they were very similar.  
At that level, we asked ourselves: why have **Y** at all? If they are the same, we can just replace **Y** with **X**:

<!-- prettier-ignore -->
$$ C(\mathbf{X}) = \sum _{j=1}^{T} X_{j} \cdot W_{j}(\mathbf{X}) $$

<!-- prettier-ignore -->
$$ W_{j}(\mathbf{X}) = \frac{X_{j}}{\sum _{i=1}^{T} X_{i}} $$

When we did this, it worked even better than before.  
A simple development will show that this form is equivalent to the final formula we arrived at:

<!-- prettier-ignore -->
$$ C(\mathbf{X}) = \sum _{j=1}^{T} X_{j} \cdot W_{j}(\mathbf{X}) = \sum _{j=1}^{T} X_{j} \cdot \frac{X_{j}}{\sum _{i=1}^{T} X_{i}} = \frac{\sum _{j=1}^{T} X_{j}^{2}}{\sum _{i=1}^{T} X_{i}} $$

But then we arrived at a very strange definition. Our confidence is **X** weighted by **X**. What?!

Our intuition behind this is that it is a kind of average where the larger the value, the more important it is.  
Zero is not important at all, while 100 is twice as important as 50.  
An example of a case where such a calculation would be necessary is in the context of the coronavirus. When trying to estimate how many people a confirmed infected patient could have been around, for example, if it was at a gathering of 100 people, they could infect 100 people, and if it was at a gathering of 200 people, they could infect 200 people.  
But what is the probability of them being at a gathering of 100 people versus 200 people?  
The answer is that they are twice as likely to have been at a gathering of 200 people than a gathering of 100 people.  
If we count all the gatherings, the probability of the confirmed person being at each one, and multiply by the number of people in each gathering, and call the distribution of quantities **X**, we get exactly **X** weighted by **X**.

In our case, we assume that if the weight was 0 at a certain time, it doesn’t mean much about that person, because it's likely they didn’t speak there at all.  
On the other hand, if the weight is 1, it says a lot – because it's almost certain they were there.  
If the model is not confident, it will output lower numbers without changing the weightings.

In fact, just as the magnitude is independent of the direction of a vector, the information of the confidence is also independent of the weightings, meaning the model can change each of them without affecting the other.

This is a non-obvious solution, an elegant one, and also the best one we tested. That's as good as they get in my opinion :)

### The wBCE Formula

<!-- prettier-ignore -->
$$ wBCE(y,\hat{y})=-y⋅\ln(\hat{y})+\hat{y} $$

wBCE is a very neat result - it's a very simple formula, but not an obvious one, which improves results while maintaining important properties of BCE.

I will now explain its development.

First, let's recall the definition of BCE:

<!-- prettier-ignore -->
$$ BCE(y,\hat{y})=-y⋅\ln(\hat{y})-(1-y)⋅\ln(1-\hat{y}) $$

In our development, we began with the question: can we replace the part that penalizes errors when y is 0 with something else that will maintain the minimum point of BCE in one dimension?

<!-- prettier-ignore -->
$$ wBCE(y,\hat{y})=-y⋅\ln(\hat{y})+f(y, \hat{y}) $$

<!-- prettier-ignore -->
$$ min(wBCE(y,\hat{y}))=min(BCE(y,\hat{y})) $$

I won’t elaborate on this here, but I’ll mention that the minimum of BCE is simply y:

<!-- prettier-ignore -->
$$ min(BCE(y,\hat{y}))=y $$

<!-- prettier-ignore -->
$$ min(wBCE(y,\hat{y}))=y $$

Let’s try to understand the desired properties for f to satisfy this condition.

<!-- prettier-ignore -->
$$ \frac{d}{d\hat{y}} wBCE(y,\hat{y})=-\frac{y}{\hat{y}}+\frac{d}{d\hat{y}}f(y, \hat{y}) $$

We know that when y_hat = y, it is the minimum point, meaning the derivative equals 0:

<!-- prettier-ignore -->
$$ -\frac{y}{y}+\frac{d}{d\hat{y}}f(y, \hat{y})=0 $$

<!-- prettier-ignore -->
$$ \frac{d}{d\hat{y}}f(y, \hat{y})=1 $$

(The case where y = 0 is important but will not be explained here, the desired properties remain)

That is, the derivative of f when y_hat = y is 1.  
Of course, there are infinitely many solutions to this problem, but we want a solution that is more moderate than ln, so a simple approach would be to aim for a linear formula like this:

<!-- prettier-ignore -->
$$ f(y, \hat{y})=m\hat{y}+n $$

Based on what we already know, we can conclude that m must be equal to 1, and we can choose n without affecting the minimum point.

The simplest solution would be:

<!-- prettier-ignore -->
$$ f(y, \hat{y})=\hat{y} $$

If we substitute this back into the formula we started with, we get the final formula for wBCE:

<!-- prettier-ignore -->
$$ wBCE(y,\hat{y})=-y⋅\ln(\hat{y})+f(y, \hat{y})=-y⋅\ln(\hat{y})+\hat{y} $$

To get more intuition about the differences, I’ll present some simple visualizations comparing BCE and wBCE:

{::nomarkdown}
{% assign jupyter_path = 'assets/jupyter/weighter/wBCE.ipynb' | relative_url %}
{% jupyter_notebook jupyter_path %}
{:/nomarkdown}

In the first set of graphs, you can see that the minimum point for both BCE and wBCE appears to align, exactly when y_hat = y.

In the second set of graphs, I numerically compute the derivatives (gradients) of both and show them. It is clear that both derivatives cross 0 at the same point, or in other words, the sign of the gradient of BCE always matches the sign of the gradient of wBCE.  
Additionally, you can see that BCE contains both large positive and negative gradients near the asymptotes, whereas wBCE contains only one asymptote near 0. This means wBCE has large negative gradients but its positive gradients are at most 1.

As can be understood, wBCE does its job; it bounds the gradient size possible during a labeling error when y = 0.

The improvement from BCE to wBCE is not dramatic, but it was necessary for us to meet our objectives.

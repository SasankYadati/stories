---
toc: false
layout: post
description: Let us evaluate the capabilities of Deep Learning.
categories: [Deep Learning]
title: Deep Learning can only do so much
image: images/2018-04-18-Deep-Learning-can-only-do-so-much/deep_learning.jpeg
---

## Prologue
Deep Learning has revolutionized machine capabilities by leveraging the advancements in computing power and rise in amounts of data available. From object recognition to recommendation engines and from translation systems to fraud detection, we have witnessed state-of-the-art performances using Deep Learning.

Consequently, Deep Learning powered applications have become a reality in no time. Apps on your smartphone are probably running Deep Learning algorithms locally while getting better with time and usage. Obviously, there is so much hype around Deep Leaning thanks to the various tech companies and media. In fact, most of the hype is justified given its impact. However, I believe it is vital to understand what Deep Learning can and cannot do.

## So, what is Deep Learning anyway?
Deep Learning is essentially a statistical technique used to identify patterns given data. This is achieved using neural networks which are nothing but stacks of layers of neurons. Each neuron is a function whose parameters are to be determined by the optimization process.
So essentially, each layer computes a transformation on the input and passes it forward onto the next layer.

![]({{ site.baseurl }}/images/2018-04-18-Deep-Learning-can-only-do-so-much/deep_learning.jpeg "A Deep Neural Network. Source: FreeCodeCamp")

To sum it up, you have a large bunch of examples including the input and the output. You feed the input, compute the output by performing transformations at each layer, compare this output with the actual output and depending on the difference we adjust the parameters of neurons in different layers. This process repeats until we achieve desired performance.

Although I have obscured many details, it still is a simple idea. Yet, unbelievably effective. Theoretically, Deep Learning is powerful enough to represent any deterministic mapping between a set of inputs and outputs. But, you probably shouldn’t read too much into it, as many other factors come into play in practice.

## Limitations of Deep Learning
### Data hungry
Deep Learning models work well only when they have large amounts of data available to them.

> Give me a X, Give me a Y, Give me a lot of them!

In fact, the more complex transformations you want it to learn (assuming it can), the bigger the network has to be and more the data it requires so as to not fit on some irrelevant relationships and patterns. This is mostly in contrast with how humans learn. A child doesn’t need millions of examples to classify a hot dog from not a hot dog.

### Adversarial examples hurt the performance
Using the idea of gradient ascend, it is very easy to trick the model to predict really high probabilities for incorrect classes. This is as simple as taking an image of class A and adding to it the gradient of image of class B. Although it almost has no visual difference to us, deep learning models fail to classify them.
![]({{ site.baseurl }}/images/2018-04-18-Deep-Learning-can-only-do-so-much/adv_images.png "Fooling the model by adding gradient of a different class. Source: blog.keras.io")
Many strategies have been proposed to prevent adversarial attacks, but almost all of them defend only some subset of these attacks.

### Generalization capabilities are limited
Deep Learning performs well on test data only if the test data distribution resembles that of the training data. Any deviation in the test input thrown at it will result in poor performance.
To quote Francois Chollet,

> …our models can only perform local generalization, adapting to new situations that must stay very close from past data, while human cognition is capable of extreme generalization, quickly adapting to radically novel situations, or planning very for long-term future situations.

I could not put that in better words. Deep Learning can only generalize to something new given it is similar to the data it has seen. Humans, on the other hand, are adaptive to novel situations.

### Restrictions on transformations it can use
We have learnt that each layer in a neural network applies a geometric transformation to the input and passes it forward to the next layer.
Deep Learning uses gradient based optimizations to learn the right values for the parameters of the transformations. This imposes a restriction on what kind of transformations we could use. Since, the transformations need to be differentiable, they need to be smooth and continuous as well. This is quite a strong restriction.

### Trouble with Hierarchical Structure
There is no way for a Deep Learning model to deal with hierarchical structure. It only learns correlations among features that are flat and considered equal.
This is a serious problem, considering what Noam Chomsky believes: natural languages have hierarchical structures, where large structures are recursively made out of smaller ones.

![]({{ site.baseurl }}/images/2018-04-18-Deep-Learning-can-only-do-so-much/eng_sentence.gif "Hierarchical Structure of an English Sentence. Source: Grammarpedia English Grammar Resource.")

This is why RNNs have trouble extending what they have learnt to unfamiliar examples. They assume natural languages to be nothing but a set of sequences and thereby perform poorly when they come across complex sentences.

<hr>

In this post, I have covered some of the limitations of Deep Learning. I believe it is important for somebody who wants to work with it to know what it can and cannot do. There is a lot of research going on to overcome these shortcomings. Most of these approaches are in contrast with one another which makes it all the more exciting. With that being said, I can’t wait to see what the future in Artificial Intelligence research holds for us.
Cheers!
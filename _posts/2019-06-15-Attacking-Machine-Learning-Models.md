---
toc: false
layout: post
description: Let us evaluate the capabilities of Deep Learning.
categories: [Deep Learning]
title: Attacking Machine Learning Models
image: images/2019-06-15-Attacking-Machine-Learning-Models/adversarial.png
---
Machine Learning is an incredibly exciting technology. Many systems powered by Machine Learning are helping in making predictions and decisions for most businesses and organizations. The impact of such models is undeniable and significant. These models face many security issues nevertheless. It turns out such models could be fooled using some smartly crafted inputs. What’s worse is that crafting such inputs is not so hard at all. You can go ahead, hide your model and data. It’s still possible!


## The Implications!
Oh, the implications are of significance definitely. Imagine a self driving car being fooled by a modified sign board. All one needs to do is print the adversarial image of the sign on a paper and stick it over. This is just one example of exploiting such weakness and I will leave it to your imagination where situations far worse are possible!

![]({{ site.baseurl }}/images/2019-06-15-Attacking-Machine-Learning-Models/adversarial.png "Doesn’t look like anything to me!")

## Adversarial Attacks
Before we get any technical, here's an informal introduction to adversarial attacks. This write-up is in no way a rigorous review of this field and is written only to expose you to some aspects of adversarial attacks in machine learning. Hope this inspires you even just a little bit to explore more about this field.
Wew! With that being said, let’s dive in.

Adversarial attacks are basically when an attacker or an adversary uses adversarial examples to trick models into misclassifying them when such a misclassification is not expected of them.

> What are the reasons for such a vulnerability? How do we come up with adversarial examples? How can we defend our models against such attacks?

Before we seek answers to these questions, lets get over with some formalities!

Adversarial attacks can be classified based on what the attacker knows about the model and if the attacker wants to target the model to predict a particular class or not. More formally, there are black-box attacks where the attacker knows nothing about the architecture or the parameters of the model but has access to using it to make predictions. White-box attacks are just the opposite — attacker knows the model’s internals. If the attacker wants to target a particular class to be the output for the adversarial input, we call that a targeted attack and non-targeted otherwise.


## So, why does such a vulnerability exists?
First things first: this misclassification is not due to overfitting. Models which have high performance results on test sets are vulnerable as well! Adversarial examples fooling models basically implies that models are not robust to calculated noise. Small non-perceivable perturbations in the inputs are a challenge to the model. The reason for this is somewhat intuitive. I will try my best to explain this.
Let us consider the problem of image classification. Consider a hypercube of $$n$$ dimensions. All possible input images of size n exist in this hypercube. A classifier will “learn” to divide this hypercube into $$k$$ partitions where $$k$$ is the number of classes. Naturally, each class is a distribution on this hypercube and all the classes are mutually exclusive. In nature and reality, most of the points in the hypercube do not occur and hence are fake images. But, the classifier has learnt a mapping from all the points in the hypercube to a probability distribution over the classes. An adversarial image of image $$x$$ is image $$y$$, subject to $$\lvert x - y \rvert ≤ \epsilon $$ ($$\epsilon$$ is a small amount of noise), where $$y$$ is classified differently from $$x$$. Under these assumptions, we can see that adversarial examples always exist. The classifier will try to classify the input even if the input doesn’t occur in the natural distribution.
But, theoretically deep neural networks are able to represent functions that are resistant to adversarial examples. Remember universal approximation theorem?! So, the learning algorithms are the real culprit here. They simply are not told to be wary of adversarial examples.

![]({{ site.baseurl }}/images/2019-06-15-Attacking-Machine-Learning-Models/adv_meme.jpg "Source: Machine Learning at Berkeley")

## How to generate Adversarial Examples?
We are already past the hardest part. We will discuss few methods to generate adversarial examples below and the key idea here is to use the gradient information.
### Fast Gradient Sign Method
For a given example $$x$$, generate adversarial example $$x'$$ as follows:

$$x' = x + \epsilon * sign(\frac{\partial J}{\partial x})$$

grad() is the gradient function. $$sign(c)$$ returns $$-1$$ if $$c$$ is negative and $$+1$$ otherwise of the input. $$epsilon$$ is the amount of perturbation. $$J$$ is the cost function.
This can be intuitive once you notice that we are moving the image in the direction of increasing gradient in steps of size epsilon.
This is a one shot method to generate an adversarial example. Value of epsilon is a trade off between similarity to x and success of an adversarial attack using X.
### Basic Iterative Method
We extend the idea of above method and iteratively perform the update for X and clip the output pixel wise so as to keep final X within epsilon neighborhood.
X = Clip-epsilon( x + sign( grad( J(x, y), x ) ) )
Number of iterations is a hyper-parameter, that trades off between computational speed and a successful attack.
So far, we have discussed non-targeted and white box attacks. We will next look at a targeted attack.
### Targeted Fast Gradient Sign Method
We choose y-target and get a clean image x from which we would like to generate an adversarial example, X. Ideally, this image belongs to a class that is perceptually close to y-target but belongs to a different class.
X = Clip-epsilon( x - sign( grad( J( x, y-target ), x ) ) )
We now “descend” the gradient as indicated by the negative sign so as to get closer to y-target. This method can be extended as an iterative process as well.
We have discussed methods to generate targeted and non-targeted white-box attacks. What if the model is a black box and we do not know the gradient information? Turns out, the adversarial examples are usually not model/architecture specific. So, you can go ahead and create your own model, generate adversarial examples using your model and they will succeed in attacking a different model trained on the same task.

## What can we do to defend our models?
### Hide your gradients!
If you observe all the equations above, they need the gradient to compute the adversarial examples. So, if we try to hide these gradients, the model should be safe against attacks. This is not true though.
Masking the model’s gradients doesn’t really make the model more robust. Instead, it just makes the attack a little harder to perform, which could be either through a substitution model or randomly guessing adversarial points. Experiments showed that different models trained on similar tasks are vulnerable to similar adversarial examples.
### Be prepared with Adversarial Training
Aha! Since we can generate adversarial examples for a given task, what if we use them to train the model along with the regular dataset? It is shown to improve classification accuracies on adversarial examples. However, they are still vulnerable to black-box attacks. They improve defense but the idea to include most adversarial examples in training is unrealistic. Our journey in finding a practical and reasonable defense continues…
### Acknowledging Ignorance
What if we assign a “don’t know/null” class for the model and let the model predict this class for the images that it is not familiar with? Our hope is that the model would predict this class for adversarial examples.
![]({{ site.baseurl}}/images/2019-06-15-Attacking-Machine-Learning-Models/null_label.jpeg "How we assign null labels to examples that are perturbed with calculated noise.")
This method aims to block the transferability property of adversarial examples. This is easier said than done. I recommend training a model with such a class! How would you gather data for such a class? How many can you or should you gather? How many are enough? And, how practical is it to do something like that? To model such a formulation is not hard but the practicality of training such models is something I haven’t tried myself. However, this method is considered an effective defense method against adversarial attacks.

## Conclusion
This article is no way a rigorous write up on this field. I took the liberty to choose only a small set of methods and ideas to discuss here. I’m in no way saying these are superior to the ones that aren’t discussed here. In fact, I recommend you explore other proposed methods as well or maybe come up with one of your own! Machine Learning researchers got really creative and proposed a lot more methods to generate adversarial examples and to defend against such examples. They all have their arguments for the reasons behind such vulnerabilities but are unanimous in acknowledging the importance of this field. And finally, I hope you, dear reader, are little more curious than you were before about the field of adversarial attacks. Whether you develop machine learning systems or research on machine learning algorithms, I hope you are convinced that adversarial attacks are worthy to be considered in your work. Adios!

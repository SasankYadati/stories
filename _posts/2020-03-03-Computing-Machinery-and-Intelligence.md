---
toc: false
layout: post
description: Alan Turing, 1950.
categories: [Computation, Intelligence]
title: Computing Machinery and Intelligence
image: images/2020-03-03-Computing-Machinery-and-Intelligence/alan-turing.jpg
---
## The Imitation Game

> Can machines think?

This question begs one to define the words “machine” and “think”. Instead of defining them — which is seemingly easy, let’s replace the question with one that is very similar. Before that, we introduce the imitation game.

The game is played by three. A man, a woman and an interrogator. The interrogator is isolated from the other two and can ask each one of them questions, with a goal of identifying who the man and who the woman is. The man and woman, respond in a way so as to mislead the interrogator. We can assume the interrogator is oblivious to factors unconcerned with intellect such as voice, appearance and so forth.

![]({{ site.baseurl }}/images/2020-03-03-Computing-Machinery-and-Intelligence/imitation.gif)

Suppose, we replace one of the man and woman with a machine. Can the interrogator now identify them wrongly as often as they do otherwise?

## Critique of the New Problem
> Is this new question a worthy one to investigate?

The imitation game has the setting that prevents the investigator from seeing, touching or hearing the players. This setting provides the advantage of drawing a distinction between physical and intellectual capabilities of the players. The idea is to not penalize the machine for not being human-like except for when we compare intellect.

Some might argue that odds are too heavily against the machine. Because, for a person it might be easier to pretend as a man/woman more than as a machine. Slowness and inaccuracy can give it away. Nevertheless, if a machine can play the game well enough, it can convince that it’s not a machine as well as the human player can convince otherwise.

## The Machines Concerned in the Game
Even with the imitation game replacing our original question, we still have to define what a machine is. We wish to allow every kind of engineering technique and the possibility of the engineers not being able to describe the machine’s operations. To pin it down, we are interested in the kind of machines, which got us asking whether they can think, the digital computers.

One might ask why not perform the test with the existing digital computers. The short answer is that we are not looking whether all digital computers would fare well at the game. It’s not even whether the present digital computers would play well. We are only interested to know whether there are imaginary digital computers that would do well.

## Digital Computers
A digital computer consists mainly of 3 parts.
* Store
* Executive Unit
* Control

The store is a collection of information. The executive unit carries out various individual operations, which vary from machine to machine. The table of operations that the machine can perform are stored as part of the store. The control makes sure the instructions are obeyed in the right order. The information in store is usually stored in small packets of fixed size. Numbers are systematically assigned to the parts of store to identify packets.

There are digital computers being constructed at present just according to the principles we have described. If one desires to make a machine mimic the behavior of a human computer, all they have to do is describe formally what the human computer does in the form of an instruction table. We call the construction of instruction tables, programming.

An interesting variant can be the idea of a random element in a digital computer. It is not possible to determine whether a program involves a random element just by observing its behavior, simply because such effects can be produced — for example by making choices that depend on digits of pi.

When Charles Babbage planned the Analytical Engine, albeit incomplete, he shared the ideas of a digital computer. The fact that the Analytical Engine is equivalent to a digital computer but was completely mechanical tells us that the use of electricity cannot be of theoretical importance. The use of electricity in digital computers and brains is an implementation detail. Electricity is deemed useful in fast signalling and should be no surprise that it is used in computers and brains.


## Universality of Digital Computers
Digital computers are essentially discrete state machines. The states in which it can be are definite and discrete enough for all practical purposes.
Consider a discrete state machine, with a given initial state and input signals. It is possible to compute all the possible future states of this machine. This characteristic is reminiscent of [Laplace's Demon](https://www.stsci.edu/~lbradley/seminar/laplace.html) except that in case of a discrete state machine it’s much more practical.

![]({{ site.baseurl }}/images/2020-03-03-Computing-Machinery-and-Intelligence/state-machine.png "An example of a Discrete State Machine describing a Turnstile")

Although discrete, digital computers can occupy astronomical number of states. The machine in Manchester has about 2¹⁶⁵⁰⁰⁰ states. It’s storage capacity is about 165000. *I believe Turing was referring to [this](https://en.wikipedia.org/wiki/Manchester_Mark_1). Storage capacity can be thought as number of bits, as we know a bit encodes 2 states.*

Given the initial state and set of input signals, a digital computer is capable of computing all the possible future states. If the digital computer is sufficiently fast and has adequate storage capacity, it can mimic any discrete state machine. The two human players in the imitation game can be replaced by a discrete state machine and a digital computer, which mimics it, and the interrogator would not be able to tell them apart.

>This special property of digital computers, that they can mimic any discrete-state machine, is described by saying that they are universal machines.

The question can be restated as follows. Can we take a particular digital computer, give it adequate storage capacity, necessary improvements in speed and an appropriate program, and expect it to play satisfactorily in the imitation game against a human?

## Contrary Views on the Main Question
> I believe that in about fifty years’ time it will be possible, to programme computers, with a storage capacity of about 10⁹, to make them play the imitation game so well that an average interrogator will not have more than 70 per cent chance of making the right identification after five minutes of questioning.
>
> … Nevertheless I believe that at the end of the century the use of words and general educated opinion will have altered so much that one will be able to speak of machines thinking without expecting to be contradicted.

### Mathematical Objection
Gödel’s theorem is one of the results that describes the limitations of discrete state machines. It shows that in any sufficiently powerful logical system that is consistent, there will be statements that are true but cannot be proved within the system.
Gödel, Church and Turing independently came up with different proposals for an exact mathematical definition of [computable functions](https://en.wikipedia.org/wiki/Computable_function), and consequently, of [decidable sets](https://en.wikipedia.org/wiki/Recursive_set). These proposals, though, all turned out to be equivalent.
So for the sake of convenience we will refer to the latter work since it’s directly related to machines. The results of the work essentially imply that machines, even with infinite storage capacity, cannot give answers to certain questions. It will either give a wrong answer, or cannot arrive at an answer no matter how much time is allowed. The nature of these questions is that the answers Yes/No are appropriate.
The questions the machines will fail on are of this type, “Consider the machine specified as follows . . .Will this machine ever answer “Yes” to any question?” The dots are to be replaced by a formal description of some machine. Suppose the machine described is similar to the machine under interrogation, it can be shown that the answer is either wrong or unforthcoming. *For more information, check [undecidability](https://www.cs.rochester.edu/~nelson/courses/csc_173/computability/undecidable.html).*
The objection is that no such limitation exists for humans, albeit this statement has no proof.
> There would be no question of humans triumphing simultaneously over all machines. In short, then, there might be people cleverer than any given machine, but then again there might be other machines cleverer again, and so on.

### Other objections:
Turing also presents various arguments of the following nature:
* Thinking is a function of an immortal soul. God has given an immortal soul to every human, but not to any other animal or machines.
* Consciousness enables thinking and we cannot test for consciousness through the imitation game.
* Various disabilities of machines: machines can do all of that, but not X.
* Lady Lovelace’s objection that a machine can never do anything really new.
* The continuity of the nervous system prevents the machines, which are discrete in nature, to mimic its behaviour.
* Behaviour is informal and it is not possible to produce a set of rules purporting to describe what a man should do in every conceivable set of circumstances.
* Arguments from people, who believe in extrasensory perception.

## Learning Machines
> I have no very convincing arguments of a positive nature to support my views. If I had I should not have taken such pains to point out the fallacies in contrary views. Such evidence as I have I shall now give.

Human minds, most times, seem to be “sub-critical,” i.e., when an idea is presented to such a mind, it will on average give rise to less than one idea in reply. Other times, they seem to be super-critical, when presented with ideas give rise to a whole “theory” consisting of secondary, tertiary and more remote ideas. But this support isn’t good enough for the claims made early in the previous section.

> Can a machine be super-critical?

The problem is mainly programming. Engineering advances are necessary but insufficient. Storage capacity of about 10¹⁵ (estimated human brain’s storage capacity) should be more than sufficient and it should not require us to increase the operational speed. Our problem then is mainly to programme these machines to play the game.
We mainly see three components when we observe the growth of a child’s mind into an adult’s mind.
1. Initial state of mind, say, at birth
2. Education it has been subjected to
3. Other experiences it has been subjected to

Producing a program to simulate a child’s mind and subjecting it to necessary experience is just as appropriate as producing one that simulates an adult mind. The program and the experience are closely connected. This idea is in fact analogous to evolution, where the judge evaluating a machine’s progress corresponds to natural selection. However, this process is likely faster and more efficient than natural selection. The use of punishments and rewards, which are traditionally associated with teaching, can at best be a part of training process if there are “unemotional” channels of communicating the punishments and rewards.

How complex should the child machine be? Should it just be rudimentary and consistent with the general principles? Or should it have a complete system of logical inference? In the latter, system could be filled with well-established facts, conjectures, theorems, authority issued statements etcetera. The machine may produce its own propositions on top of it all may be by using scientific induction.

If the idea of a learning machine sounds paradoxical, it could help to understand that lifetime of some of the machine’s rules are short-lasting. They deem more useful because of their changeable nature than being enforcers of said constraints. The teacher of the learning machine will be mostly ignorant of the machine’s internals. We should be able to teach the machine to do something without being too detailed on how to do it. What may seem to us as random behaviour — owing to the deviation from deterministic behaviour, is presumably intelligent behaviour. The inclusion of randomness in a learning machine is useful especially when solving a problem with multiple solutions. It is unnecessary to keep track of the tried solutions. Since there are probably a lot of solutions for the learning problem, random process is better than systematic.

Hopefully, machines will soon compete with men intellectually. It could be by starting out on abstract tasks like playing chess (popular opinion) or it could be by providing the machine sensory equipment followed by a process similar to that of teaching a child. The right answer is unknown and both should be tried.

> ### We can only see a short distance ahead, but we can see plenty there that needs to be done.
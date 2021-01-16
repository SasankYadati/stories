---
toc: false
layout: post
description: Understand the basics of TensorFlow.
categories: [TensorFlow]
title: TensorFlow
image: images/2018-04-05-Tensorflow/comp_graph.jfif
---
## Introduction

TensorFlow is an open source library for machine intelligence developed by Google. It is a computational library with a wide range of functionality. However, its main purpose is to implement Machine Learning algorithms.
TensorFlow is extremely popular relative to other Deep Learning libraries due to many reasons. One of the most important reasons being its ability to facilitate both research and production. This was not possible with the other libraries. Researchers and developers had to use one language for research and prototyping and some other language to deploy their model into production. Needless to say, TensorFlow took good care of this.

> Research AND Production?! TensorFlow got it covered.

There are many other reasons for someone to choose TensorFlow over other libraries. Some of them include Python interface, TensorBoard (kick-ass visualizations!) and Auto Differentiation.

## The basics

Any TensorFlow program essentially contains 2 components : Computational Graph and Session.
Computational Graphs are a means to specify computations that need to be carried out in our model. They are directed graphs, where nodes represent operations and edges represent tensors and the direction in which they move (hence, the name TensorFlow!).
Once we define our graph, we can run it by creating a session. We can execute the whole graph or just a part of it. Session allocates memory for the graph and the variables.

(Note : TensorFlow has a new feature called Eager Execution which is more Python way of doing things. It is imperative in nature contrast to the graph-and-session approach, which is declarative.)

![]({{ site.baseurl }}/images/2018-04-05-Tensorflow/comp_graph.jfif "A Computational Graph. Nodes represent operations and edges represent data. Source: TensorFlow for Machine Intelligence")

In the above graph, you can see nodes corresponding to multiplication and addition operations. You can also see how data flows in the graph from one node to another. After defining such graph, we can run it (or parts of it) in a session.

## Tensors, Constants, Variables and Placeholders

```python
import tensorflow as tf
```

Tensors are best understood as a means of generalizing scalars, vectors and matrices. Scalars are 0-dimensional, vectors are 1-dimensional and matrices are 2-dimensional.

> Tensors are n-dimensional arrays.

Extending this idea, tensors are nothing but n-dimensional. If n is 0 they are scalars, if n is 1 they are vectors and so on. The rank of a tensor is nothing but the number of dimensions of the tensor.

Creating constants in TensorFlow is simple.

```python
# A is a 1D tensor constant
A = tf.constant([2,6], name="A_vector")
# B is a 2D tensor constant
B = tf.constant([[10, 11], [42, 33]], name="B_matrix")
```

You can create constants using various other operations like `tf.zeros(...)` , `tf.ones(...)` and `tf.random_normal(...)`.

Constants’ values cannot be changed and are stored in the graph’s definition. They are loaded every time you load the graph. Variables on the other hand, are mutable and are stored separately from the graph definition.

```python
# Variables can be created using tf.get_variable(...) function
tf.get_variable(
    name,
    shape=None,
    dtype=None,
    initializer=None,
    regularizer=None,
    trainable=True,
    collections=None,
    caching_device=None,
    partitioner=None,
    validate_shape=True,
    use_resource=None,
    custom_getter=None,
    constraint=None
)

# Let us create a variable "weights" of shape 10x10 filled with zeros.
weights = tf.get_variable("weights", shape=(10,10), initializer=tf.zeros_initializer())
```

> Constants are immutable and are stored in the graph definition. Variables are mutable and are stored separately from the graph.

Before using the variables you have to initialize them in a session. For this, we usually create a initializer operation and run this operation in a session. One operation is enough to initialize all variables, although you can initialize them individually.

```python
# Define variables
a = tf.get_variable(...)
b = tf.get_variable(...)
# Define an initializer operation
init_op = tf.global_variables_initializer()
# Create a session
with tf.Session() as sess:
  # Run the init operation
  sess.run(init_op)
  # Use variables
  sess.run(a)
  sess.run(b)
```

When we are defining our graph, we will not always know what values we need for certain computations. In order to define a computation without specifying the values, we use placeholders. It is similar to defining `F(x,y)` without specifying the values of `x` and `y` .

> Placeholders allow us to define computations without providing values.

Let us define `f(x,y) = x*y` where `x` and `y` are placeholders.

```python
# Define two placeholders
x = tf.placeholder(tf.float32, shape=[2,2])
y = tf.placeholder(tf.float32, shape=[2,2])
# Define f to be x*y
f = x*y
# Create a session
with tf.Session() as sess:
  x_value = [[1,2],[3,4]]
  y_value = [[5,6],[7,8]]
  # To compute f, we need to supply the values for the placeholders x and y
  f_value = sess.run(f,{x:x_value , y:y_value})
```

As you can see in the code above, we need to supply values for placeholders if we want to evaluate `f(x,y)`.

TensorFlow has many operations ranging from matrix inversion to advanced optimizations. We will cover basic operations by implementing a linear regression model.

## Linear Regression in TensorFlow

Linear Regression is basically finding a best fit line through a set of points. We will create two placeholders `x` and `y` whose values are later supplied in a session. We have weights `w` and bias `b` , whose optimal values need to be found by an optimizer. So, these will be variables. We will define our model `f` as `f(x) = w * x + b`.

> Have you ever fit a line through data? It’s liberating.

```python
x = tf.placeholder(tf.float32, shape=[500]) # 500 values for x
y = tf.placeholder(tf.float32, shape=[500]) # 500 values for y

w = tf.get_variable('w', shape=[1,1], initializer=tf.zeros_initializer()) # Variable w initialized with 0's
b = tf.get_variable('b', shape=[1,1], initializer=tf.zeros_initializer()) # Variable b initialized with 0's

init_op = tf.global_variables_initializer() # Variables initializer operation

f = w*x + b # Our model
```

Now, all that is left is to define a loss function and an optimizer. We will then run the optimizer operation in a session a few times and voila! We will have the model trained.

```python
# Define loss function as sum of squares
loss = tf.reduce_sum(tf.square(y-f))/500
# Define Gradient Descent optimizer with minimization of loss as objective
optimizer = tf.train.GradientDescentOptimizer(learning_rate=0.0003).minimize(loss)

## Generate random data for training
x_values = [random.randint(1,50) for _ in range(500)]
y_values = [(20+random.random())*x_val+(2+random.random()) for x_val in x_values]

## Create a session
with tf.Session() as sess:
  # Run the init operation
  sess.run(init_op)
  # 2000 Epochs
  for i in range(2000):
      # Run loss and optimizer operations
      c,_ = sess.run([loss,optimizer], {x:x_values,y:y_values})
      if(i%100==0): # Print loss every 100 epochs
          print("Epoch : {} , Loss : {}".format(i,c))
  # Finally, print optimized values of w and b
  print("w=".format(sess.run(w)))
  print("b=".format(sess.run(b)))
```
## Conclusion
I hope you have gained a good sense of how TensorFlow works! You pretty much know the basic constructs and can further build up to develop awesome applications. I wish to write a post on TensorBoard in the near future, covering the visualization aspects of TensorFlow. Until then!

---
layout: post
title: "Linear and Non-Linear ML Models"
date: 2022-05-27
categories: [data-science]
tags: [data-science]
usemathjax: true
---

## Linear Models

Recall Classification:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-12.31.41.png" alt="Classification Recall" style="width: 70%; height: auto;">
</div>

→ there are other possibilities than Gaussian, e.g. geometrically

### Parameterization

e.g. straight line (linear, 2D)

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-12.38.48.png" alt="Straight Line Parameterization" style="width: 70%; height: auto;">
</div>

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-12.40.09.png" alt="Linear Parameterization" style="width: 70%; height: auto;">
</div>

### How to find the Parameters?

→ we "draw" a line between the examples

→ many optimization methods to get better parameters

Minimize the error (the Loss function *L*):

* Loss function has to be differential

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-13.34.59.png" alt="Loss Function" style="width: 70%; height: auto;">
</div>

* logistic function: Values between 0 and 1 (pseudo probability)

two parameters, many possible solutions

→ solution in vector spaces

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-13.40.33.png" alt="Vector Space Solution" style="width: 70%; height: auto;">
</div>

* each point is a possible solution
* we can compute the gradient at each point, the direction of the gradient to the parameters with minimal errors

→ **Gradient Descent ALgorithm**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-14-at-13.48.51.png" alt="Gradient Descent Algorithm" style="width: 70%; height: auto;">
</div>

Lamda (Step 3) is the step size or learning rate, usually quite small scalar like 0.001

* with a higher step size, we get a faster solution, but may be less accurate

! pay attention if the algorithm is convex, otherwise a local minima could be calculated!

### How long to repeat?

Different possibilities:

* pre set number of iterations
* loss limit
* loss not changing

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.23.16.png" alt="Gradient Descent Iterations" style="width: 70%; height: auto;">
</div>

**Summary:**

1. Parameterization
2. Define Loss function
3. Optimize Parameters until satisfaction

### Multi class problems

→ one vector per class, summarized to matrix

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.32.03.png" alt="Multi-class Matrix" style="width: 70%; height: auto;">
</div>

Optimization problem is almost the same:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.33.17.png" alt="Multi-class Optimization" style="width: 70%; height: auto;">
</div>

Change *Loss* to *SOFTMAX* function to normalize sum aver all probabilities to one:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.34.25.png" alt="Softmax Function" style="width: 70%; height: auto;">
</div>

Use "one-hot" coding of y

* instead of giving a single probability, give a probability for each class
* Loss function returns now a vector

Different possibilities:

* one non-linear, complex function
* multiple linear functions (ensemble learning)

### Ensemble Learning (Random Forests)

* many weak models decide together (by voting)
* Easy to implement and to parallelize
* Does not tend to overfit
* Build in Feature-Selection→ doesn't only show us what is chased, but also why

### Decision Trees

* base classifier for Random Forests
* normally, decision trees aren't good, because they tend to simply memorize decisions→ recombination from different forests

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.53.14.png" alt="Decision Trees" style="width: 70%; height: auto;">
</div>

* we need a splitting function that will produce (almost) pure class labels

**Top Down Training:**

Assume ***k*** classes and data of dimension ***d***

Fill tree with ALL training samples from the root down In each node: compute probability for all class labels in node *n*

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-19-at-14.58.57-1.png" alt="Node Training" style="width: 70%; height: auto;">
</div>

Compute **node purity** based on class probabilities

Node purity: How clear is the node if it would be the last one

Split node along one dimension such that purity of children is increasing (**optimization**)

Entropy (a way to measure impurity):

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-20-at-14.40.57.png" alt="Entropy Formula" style="width: 70%; height: auto;">
</div>

Gini index:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-20-at-14.41.28.png" alt="Gini Index" style="width: 70%; height: auto;">
</div>

...

Split optimization (Simple Line search) examples

...

But we train multiple trees with the same data, how to avoid memorization?

we get randomness from:

* we select random variables→ trees are not the same
* Bootstrapping data→ not every tree gets the same data

### Regression

not every prediction is discrete (Class X, Class Y, ...)

→ some are continuous (like costs in a taxi)

→ fitting function instead of separation function

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.25.42.png" alt="Regression Fitting" style="width: 70%; height: auto;">
</div>

You can still use the same framework:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-20-at-15.04.47.png" alt="Regression Framework" style="width: 70%; height: auto;">
</div>

Simply need new loss function in the optimization

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.21.27.png" alt="Regression Loss Function" style="width: 70%; height: auto;">
</div>

**Measurements**

* least square error:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.22.22.png" alt="Least Square Error" style="width: 70%; height: auto;">
</div>

* many other measures possible, e.g. L1 (Histogram intersection)

**Regression with Random Forests:**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.32.58.png" alt="Regression with Random Forests" style="width: 70%; height: auto;">
</div>

we need a new splitting function (we don't have purity)

→ goal: reduce "data spread" in node

→ use simple statistical measure like "mean square error"

## Non-linear models I

### Need for non-linear models

Linear models are very limited, for example the "X-Or" Problem

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.47.26.png" alt="X-Or Problem" style="width: 70%; height: auto;">
</div>

### How to add non-linearity?

Three canonical ways:

* extracting non-linear features (already learned)

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.51.23.png" alt="Non-linear Features" style="width: 70%; height: auto;">
</div>

* use ensembles of linear models (like random forest)

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.53.52.png" alt="Ensembles of Linear Models" style="width: 70%; height: auto;">
</div>

* use non-linear functions → e.g. a polynom (Polynom Classifier)→ we can parameterize the polynomial degree and the parameters before the variables

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-09.55.32.png" alt="Polynomial Classifier" style="width: 70%; height: auto;">
</div>

### Add non-linearity to our simple classifier

**Step 1: add a simple element-wise non-linear mapping**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-10.26.59.png" alt="Element-wise Non-linear Mapping" style="width: 70%; height: auto;">
</div>

the non-linear mapping can be anything which can be done to every element, like square, root, ...

What are good choices for these functions?

* Properties
  * between 0 and 1 → pseudo probability interpretation
  * stable range of output → gradient optimization
* Common choices
  * Sigmoid function
  * Tanh
  * ...

**Step 2: concatenate several of these operations**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-22-at-10.41.43.png" alt="Concatenating Operations" style="width: 70%; height: auto;">
</div>

→ we combine several transformations:

**X** → Matrix/Vector Mult operation → Element wise non-linear operation → Matrix/Vector Mult operation ......... → **f (x)**

Note: if the W is large enough, we theoretical need only two concatenations to approximate any smooth function

**Then we need a Loss-function**

problem didn't change

→ same approach as in the linear case

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-09.43.48.png" alt="Loss Function for Non-linear Classifier" style="width: 70%; height: auto;">
</div>

* the parameters are set in W (Matrix/Vector Mult operation)
* non-linear operations are preset, they don't have to change

→ optimization problem is the same as by linear

### Problem: Overfitting

prevent already during optimization problem

→ adding regularization to the Loss function

**L2 regularization:**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-09.55.02.png" alt="L2 Regularization" style="width: 70%; height: auto;">
</div>

* all parameters to be learned in square
* Lambda (Scalar hyper parameter) sets how strong complexity is "punished"

**L1 regularization:**

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-09.55.54.png" alt="L1 Regularization" style="width: 70%; height: auto;">
</div>

**→ Regularization will punish higher parameter values**

→ smoother model

→ training errors allowed

### Neuronal Networks

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-10.16.38.png" alt="Neuronal Networks" style="width: 70%; height: auto;">
</div>

* inputs from other neurons
* every input has a (learnable) weight→ the more the input is activated, the stronger is the connection
* weighted sum is a neuron with sums up all incoming signals with their weights and gives it to a non-linear function which decides if the sum is big enough to "fire" (signalling)→ if yes, signal goes to the other neurons

Comparison to our previous non-linear model

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-10.25.13.png" alt="Comparison to Non-linear Model" style="width: 70%; height: auto;">
</div>

* Inputs are our X
* Input = 1 is our constant offset (our b in Wx + b)

Connect multiple neurons

A simple Neuronal Network:

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-10.27.58.png" alt="Simple Neuronal Network" style="width: 70%; height: auto;">
</div>

* our w turns into W

A deeper (fully connected) Neuronal Network

<div style="text-align:center">
  <img src="/wp-content/uploads/2022/05/Screenshot-2022-04-23-at-10.30.03.png" alt="Deeper Neuronal Network" style="width: 70%; height: auto;">
</div>

* multiple Layers (5 Layers in this example)
* "fully connected" means all outputs of a layer are connected to all coming layers

## Code Exercises

(Link to Github)

[Week5_Classification_solution.ipynb](https://github.com/HuberAdrian/DataScience-Lectures/blob/main/Week_5/Week5_Classification_solution.ipynb)
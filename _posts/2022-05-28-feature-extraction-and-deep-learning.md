---
layout: post
title: "Feature Extraction and Deep Learning"
date: 2022-05-28
categories: [data-science]
usemathjax: true
---

## Feature Extraction

### Recall Supervised Classification

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-27-at-14.55.07.png" alt="Supervised Classification diagram" style="width: 70%; height: auto;">
</div>

- the chosen vector space representation aligns the chosen model and how we make a classification
- earlier, we took pixel by pixel and write it in the vector space

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-27-at-14.56.25.png" alt="Vector space representation" style="width: 70%; height: auto;">
</div>

Problem: If we took a slightly other camera angle, there is still a coffee mug, but it's a whole different point in the space

→ Classification could be wrong

Different solutions:

- if we have a picture of every possible camera angle, we could evaluate more correctly → what if the size of the coffee mug differs?
- feature engineering "preparation", so our model can evaluate correctly

## Feature Engineering

**Solution: Shallow Learning**

Unstructured data —> Feature Engineering (mathematical operator) —> "mathematical finger print" (feature space)

Properties:

- preserves information semantic classes have in common, throws away the rest
- the mathematical finger print doesn't change much when e.g. the camera angle varies (called invariant or robust)
- Reduces the dimensionality of the problem

Drawbacks:

- good feature extraction is hard to find (high manual workload)
- feature extraction is very data specific

### Invariant Theory

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-28-at-11.48.33.png" alt="Invariant Theory" style="width: 70%; height: auto;">
</div>

- transformations can be anything, even don't have to be mathematically

→ we want to define invariance:

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-28-at-11.57.05.png" alt="Invariance definition" style="width: 70%; height: auto;">
</div>

- given are two data points that are equivalent under transformation
- feature extraction T
- we need completeness (transformation backwards), otherwise the trivial solution T(x) = 0 would be valid (we don't need to know how "much" they were transformed, but which class they are assign)

→ in praxis, these is nearly impossible to reach

→ we "weaken" the invariance

separability: we don't demand invariance for all, but for our training samples

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-28-at-12.09.02.png" alt="Separability" style="width: 70%; height: auto;">
</div>

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-04-28-at-12.09.21.png" alt="Separability example" style="width: 70%; height: auto;">
</div>

### Discussion

**Feature extraction vs learning algorithms:**

**I. if we had perfect features, learning would be trivial  
II. if we had perfect classifiers, we would not need features**

Features are usually used to introduce prior knowledge about the structure of the data and variances to the learning algorithm.

There isn't the perfect feature, most often you need clustering of different approaches.

**In practice:**

- Good features are hard to find
- Often based on complex mathematical functions
- Depend on the application (domain knowledge needed!)

**Generic Approaches:**

**Invariance by differentiation**: set properties into relation / normalization  
**Invariance by integration**: compute average properties

**Motivation**

- Very high dimensional representations require a lot of data to fill this huge space (curse of dimensionality)
- Danger of overfitting is higher if space is only sparsely sampled

→ **We would like to "compress" our data (with steerable loss) to a lower dimensional representation**

**Feature Reduction: PCA Recall:**

- Co-VarianceMatrix (Week3)
- EigenValueDecomposition (Week2)

Combining both concepts for dimension reduction via **Principal Component Analysis (PCA)**

## Feature Reduction: PCA

**PCA Algorithm in a nutshell**

1. Compute Co-Variance Matrix of the data

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-01-at-23.14.03.png" alt="Covariance matrix formula" style="width: 70%; height: auto;">
</div>

where E[X] is the expected value (mean)

2. Compute Eigen Vectors and Values of K[xx]
3. Sort Eigen Values
4. Select cut-off value
5. New basis: project to Eigen vectors New dimension: #Eigen values selected

## Deep Learning

### Intro

- On an implementational level, deep Learning are very large neuronal networks
- also called 3rd generation of neuronal networks
- we still are in machine Learning, there still isn't a strong KI

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-08.26.23.png" alt="History of neural networks" style="width: 70%; height: auto;">
</div>

- Modern architectures have evolved very far from the original perceptron → in a pure Deep Learning lectures, we would go from left to right, but we focus on the modern models

### Deep Learning as a blackbox

- is a subset of ML algorithms
- our blackbox model is still valid

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-08.39.38.png" alt="Blackbox model" style="width: 70%; height: auto;">
</div>

**What is different?**

Before:

- most ML algorithms are limited to tight input/output domains e.g. image to vector, always scalar output
- Pre- and post-processing needed to solve more complex problems!

Now:

- capacity of learned mapping is better → natively allows structured (tensor) in- and output 
- "End to End" learning: Feature extraction is difficult, can we make this step learnable? (Shallow Learning) → but still 2 steps, even if these steps are connected → "End to End" learning, learn decision space and function in one optimization problem

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-08.54.19.png" alt="Content creation example" style="width: 70%; height: auto;">
</div>

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-08.54.49.png" alt="End to End learning" style="width: 70%; height: auto;">
</div>

### Opening the blackbox model

(brief intro)

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-09.59.11.png" alt="Opening the blackbox" style="width: 70%; height: auto;">
</div>

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-09.59.53.png" alt="Neural network layers" style="width: 70%; height: auto;">
</div>

- we don't have one big function, rather we partition the problem in other functions
- Only constraint: **partially differentiable** (for training)
- Depending on application and data some have learnable parameters, others are static
- In/Output are **tensors**
- later we can't make this easy assignment, because steps are mixed

Simplest Example of DNN: **Multi Layer Perceptron (MLP)**

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-14.20.02.png" alt="Multi Layer Perceptron" style="width: 70%; height: auto;">
</div>

More complex deep DNN example:

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-10.22.54.png" alt="Complex DNN example" style="width: 70%; height: auto;">
</div>

## Training of Neural Networks

**Training of DNNs is an optimization problem:** (example for supervised learning)

**1. Run data samples through graph → "forward feed"**

**2. Get result *y'***

**3. Define differentiable "loss function" to measure "difference" between prediction and true label**

**4. Optimization objective: minimize *loss***

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-10.26.09.png" alt="Optimization objective" style="width: 70%; height: auto;">
</div>

Optimization Problem:

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-10.27.00.png" alt="Optimization problem" style="width: 70%; height: auto;">
</div>

- J is our Loss function

Problem: Non CONVEX optimization problem in a very high dimensional space

→ we don't know if the solution is the best one (could be local minima)

→ NP-HARD PROBLEM

→ numeric and stochastic solution

### How to get the nested gradients?

→ With Back Propagation algorithm

1. feed forward and compute activation
2. compute error gradient between **true Y** and **predicted Y'**

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-11.29.21.png" alt="Error gradient computation" style="width: 70%; height: auto;">
</div>

3. compute derivative by layer

→ chain rule (we calculate backwards each gradient with the chain rule)

4. update all weights with small step in gradient direction

BUT: Using all of the training data to compute the gradient is computational infeasible

Instead: Monte Carlo approach: select random batch (small set of training data) per iteration to compute the gradient → **SGD**

### Stochastic Gradient Descent (SGD)

we use random to escape from possible local minima and to calculate gradients without running over all data

→ non-smooth convergence

→ many iterations needed (also called epochs)

→ need additional parameters

- Step size (learning rate)
- Batch size
- ...

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-11.45.23.png" alt="SGD visualization" style="width: 70%; height: auto;">
</div>

### Pitfalls of DNN training

1. Optimization Algorithms have many hyper parameters (that have great effect on the outcome)
2. Optimization is not deterministic (local minima, random initialization)
3. Optimization is very compute intensive
4. DNN training is likely to overfit

→ regularization

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-12.03.13.png" alt="Regularization" style="width: 70%; height: auto;">
</div>

5. Needs a lot of training data to learn the underlying distributions

- **not only many data points, also good sampling**
- **data annotation (for supervised DL)**

→ especially in 3 to 5, progress in hardware and data are the core drivers

## Basic Types of Deep Neuronal Network Architectures

### Basic Architecture of Multi Layer Perceptron (2nd Generation Neuronal Networks):

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-14.20.02-1.png" alt="Multi Layer Perceptron" style="width: 70%; height: auto;">
</div>

Where are the Neurons?

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-14.23.31.png" alt="Neurons in MLP" style="width: 70%; height: auto;">
</div>

→ How do we implement the feature extraction?

→ we have to look at the operators

### Convolutional Neuronal Networks (CNN)

- Most prominent type of DNN (LSTMs are catching up). Responsible for many practical breakthroughs
- Able to capture locality at multiple scales. Works well for data with locally embedded structures, e.g. images, videos, audio, graphs ... even text
- Learns Filters which are applied via convolution (End-to-end optimization)

Typical Design: (AlexNet)

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-02-at-15.13.28.png" alt="AlexNet design" style="width: 70%; height: auto;">
</div>

- New Conv operators

---

### Exkurs: Convolution

- is a mathematical operation between two functions

(here over time series [t])

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-11.10.05.png" alt="Convolution formula" style="width: 70%; height: auto;">
</div>

(wikipedia example animation [here](https://en.wikipedia.org/wiki/File:Convolution_of_box_signal_with_itself2.gif))

→ we have discrete functions, often multi dimensional, e.g. image in 2D

→ we have to adapt

Convolutional Filters

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-11.21.29.png" alt="Convolutional filters" style="width: 70%; height: auto;">
</div>

- f is the image
- g is the filter
- image is much larger than the filter

→ We "sum of an element-wise multiplication over a sliding window"

- = filter is moved over the image

Example:

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-11.30.26.png" alt="Convolution example" style="width: 70%; height: auto;">
</div>

- we don't select a filter (Convolution Kernel), we learn which filter fits best for our problem
- we have a "filter bank", we choose which fits our problem the best

---

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-11.49.07.png" alt="Convolution stride" style="width: 70%; height: auto;">
</div>

- Stride: step size in which we move

**Capturing image statistics of natural scenes**

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-11.51.51.png" alt="Natural image statistics" style="width: 70%; height: auto;">
</div>

- at the lowest level, pictures are edges

## Recurrent Neural Networks

- Networks for sequence learning
- typical applications: text analysis, translation (sequence to sequence), audio, sensor data → time series, well logs, ...

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-12.41.19.png" alt="Recurrent Neural Networks" style="width: 70%; height: auto;">
</div>

- s1, s2, ... sn are Input sequence
- h1, h2, ... hn are "hidden" vectors, coding the current state in the sequence → hn can be used, e.g. as input for classification
- Recurrent DNN, usually LSTM or GRU, but more complex DNN possible
- RNN predicts next sequence element

## Generative Adversarial Neuronal Networks (GAN)

<div style="text-align:center">
<img src="/wp-content/uploads/2022/05/Screenshot-2022-05-03-at-14.40.23.png" alt="Generative Adversarial Networks" style="width: 70%; height: auto;">
</div>

In a Nutshell, Generative Adversarial Nets are:

- No classification or Regression, instead we reproduce data (probabilities)
- Groups of DNNs (at least two)
- Working against each other → Generator gets a negative gradient if the Discriminator knows if the image was real or fake
- Min parts
  - Discriminator Network
  - Generator Network

## Code Exercises

(Links to Github)

[Intro_to_keras_for_engineers_week7.ipynb](https://github.com/HuberAdrian/DataScience-Lectures/blob/main/Week_7/Intro_to_keras_for_engineers_week7.ipynb)

[Week7_CNNs_solution.ipynb](https://github.com/HuberAdrian/DataScience-Lectures/blob/main/Week_7/Week7_CNNs_solution.ipynb)
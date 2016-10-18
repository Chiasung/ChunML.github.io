---
title: "Machine Learning Part 6: Logistic Regression"
categories:
  - Tutorial
tags:
  - machine-learning
  - logistic-regression
  - classification
  - essential
---

<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript">

Hello there, I am back with you today. In the 6th post on Machine Learning tutorials series, I will tell you about Logistic Regression, a very important and must-know algorithm. Before I go any further, there is one thing I want you to be clear at first. The algorithm's name, Logistic Regression, is somehow confusing a little bit, but we are not dealing with a regression problem, but a **classification problem**.

But what is the difference between regression problems and classification problems? - You may ask. I am not a statistical expert, and you may not want any detailed academic explanations, so I will make it simply like below.

A regression problem is where you have a **continuous** dataset of label \\(y\\), and your goal is to make predictions for unlabeled data. Because \\(y\\) is continuous, it can take any value between a specific range. Concretely, if our problem's output range is \\(1 ~ 10\\), then \\(y\\) can be any value between that range, such as \\(1.2, 2.5\\) or even \\(4.23424324\\), etc. A regression problem's graph will mostly look like the graph I showed you in [Linear Regression](https://chunml.github.io/ChunML.github.io/tutorial/Linear-Regression/) tutorial:

![Update 4](/images/tutorials/linear-regression/7.jpg)

A classification problem, as you may guess, is where our labels \\(y\\) can only take a particular value, or we can say that \\(y\\) is a discrete dataset. For example, if we want to solve a spam mail detecting problem, obviously we will have only two labels which is either *spam* or *non-spam*. Another example, you are a magician who is trying to guess the suit of a randomly picked card, so you only have four choices among Hearts, Diamonds, Clubs and Spades, right? So we are now dealing with a different problem from the one we did before. Our graph will now look like this:

![Graph_1](/images/tutorials/logistic-regression/graph_1.png)

Okay, so I hope you know can see the difference between a regression problem and a classification problem. Let's see how we will do to deal with a classification problem. To make it easily for you to understand, it is better that we should now consider a two-class classification problem like above.

You still remember how Machine Learning actually works? It is important for any Machine Learning algorithms to have a way to compute the Predictions from the feature data \\(X\\) which we called Activation Functions. In the case of Linear Regression, the activation function is just as simple as below:

$$
h_\theta(X) = \theta_0 + \theta_1X_1 + \theta_2X_2 + \dots + \theta_nX_n
$$

As you can see, the function above is suitable for regression problems, as it doesn't apply any restriction onto the output. Obviously, this function won't work well with our classification problem. But we can also see that, Logistic Regression is somehow similar to Linear Regression (that is why there is *Regression* in its name), so we may be able to solve the Logistic Regression if we somehow find a way to restrict the output value of the function above.

One simple way we can think about is, to use a threshold value. The idea is like below:

$$
h_\theta(X^{(i)}) = \cases{ 1 & \text{if } h_\theta(X^{(i)}) \ge 0.5 \cr 0 & \text{if } h_\theta(X^{(i)}) \lt 0.5}
$$

And we will obtain a graph like this:

![Graph_2](/images/tutorials/logistic-regression/graph_2.png)

Seems OK, huh? At least we can ensure that the activation function now only outputs \\(0\\) or \\(1\\). But in fact, using a threshold directly on regression's activation function is not a good idea at all. The reason is, now we have a sharp change in our graph, which means that the value of \\(y\\) will change immediately in an unpredictable way, which results in a bad Model in the end.

So now we know what to do next. We need an activation function which not only restricts the output value but also contains no sharp change. That shouldn't be a big problem, in fact, we have quite a lot of functions which can satisfy both conditions. And the one which is mostly used is **Sigmoid** function, which has the form as below:

$$
g(z)=\frac{1}{1+e^{-z}}
$$

And the graph of sigmoid function looks like this:

![Graph_3](/images/tutorials/logistic-regression/graph_3.png)

Perfect, right? That is exactly what we need. So how are we supposed to apply this to our case. It's very simple, we just do like below:

$$
z = \theta^TX = \theta_0 + \theta_1X_1 + \theta_2X_2 + \dots + \theta_nX_n
h_\theta(X) = g(z) = \frac{1}{1+e^{-z}} = \frac{1}{1+e^{-\theta^TX}}
$$

So with a function which doesn't contain any sharp change, we can now use a threshold value to restrict the output value to be either \\(0\\) or \\(1\\). Let say we choose \\(thresh = 0.5\\). Then our sigmoid function's output will become like this:

$$
g(z) = \cases{ 1 & \text{if } z \ge 0 \cr 0 & \text{if } z \lt 0}
$$

From \\(e^{-0} = 1\\), you can prove the result above very easily. So what if we want a result in terms of \\(\theta\\) and \\(X\\)? Since \\(z = \theta^TX\\), we can obtain the same result like below:

$$
h_\theta(X) = \cases{ 1 & \text{if } \theta^TX \ge 0 \cr 0 & \text{if } \theta^TX \lt 0}
$$

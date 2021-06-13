## Basics

### Hyperplane: 

In 'mathematics', a hyperplane H is a linear subspace of a vector space V such that the basis of H has cardinality one less than the cardinality of the basis for V.  In other words, if V is an n-dimensional vector space than H is an (n-1)-dimensional subspace.  

In 'machine learning', a hyperplane is a linear (often after transforming the space using a nonlinear kernel to lend a linear analysis) subspace that divides the data set into two regions for binary classification.  If the dimensionality of the data set is greater than 2, this may be performed multiple times to achieve a multi-way classification.

### Loss function:

Loss function/cost function is an (objective) function is used to define how bad a model does its job. An optimization problem tries to minimize the loss/cost. If the objective function is the negative of the loss/cost function, the function is called reward/utility function, in this case, we need to seek to maximize the reward/utility.

* [SVM](https://github.com/JYL123/Notes/blob/master/svm.md)
* [GAN](https://github.com/JYL123/Notes/blob/master/gan.md)

### Distribution
A `distribution` is a mathematical representation of every possible value of our parameter and how likely we are to observe each one. 

Instead of just representing the values of a parameter and how likely each one is to be the true value, a `Bayesian` thinks of a distribution as describing our beliefs about a parameter.

`Markov Chain Monte Carlo Methods (MCMC)` allow us to estimate the shape of a posterior distribution in case we can’t compute it directly. `Monte Carlo simulations` are just a way of estimating a fixed parameter by repeatedly generating random numbers. By taking the random numbers generated and doing some computation on them. Monte Carlo simulations provide an approximation of a parameter where calculating it directly is impossible or prohibitively expensive. `Markov chains` are simply sequences of events that are probabilistically related to one another. Each event comes from a set of outcomes, and each outcome determines which outcome occurs next, according to a fixed set of probabilities. An important feature of Markov chains is that they are memoryless: everything that you would possibly need to predict the next event is available in the current state, and no new information comes from knowing the history of events. This is known as `Markov Property`.

To begin, MCMC methods pick a random parameter value to consider. The simulation will continue to generate random values (**this is the Monte Carlo part**), but subject to some rule for determining what makes a good parameter value. The trick is that, for a pair of parameter values, it is possible to compute which is a better parameter value, by computing how likely each value is to explain the data, given our prior beliefs.f a randomly generated parameter value is better than the last one, it is added to the chain of parameter values with a certain probability determined by how much better it is (**this is the Markov chain part**).

reference: https://towardsdatascience.com/a-zero-math-introduction-to-markov-chain-monte-carlo-methods-dcba889e0c50

### Matplotlib
```
In [4]: import matplotlib.pyplot as plt                                                                                                                              In [5]: import matplotlib.image as mpimg                                                                                                                            
In [6]: import numpy as np                                                                                   
```
`pyplot` is Matplotlib's imperative-style plotting interface. This interface maintains global state, and is very useful for quickly and easily experimenting with various plot settings. 

```
img = mpimg.imread('/Users/ljy/Desktop/stinkbug.png')
print(img)
```
loading image with `imread`


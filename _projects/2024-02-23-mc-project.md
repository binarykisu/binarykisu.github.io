---
layout: project
title: "University Project: Random Number Generating approaches to Monte Carlo methods"
date: 2024-02-23
excerpt: "This project combines the von Neumann rejection method with the inversion method to improve upon it."
tags: [project, university, statistics, monte-carlo, data-analysis]
feature: /assets/img/project-feature.png
comments: false
---


## Introduction

When working on a project having something to do with data analysis or data visualization, we usually need to generate some random numbers to plot some distribution. 
These random numbers are usually uniformly distirbuted between 0 and 1. However, sometimes it is better to have the random numbers distributed according to some function, if we get to decide (or are aware of) its shape beforehand.
- For example, when doing natural science experiments, the peaks in spectra often have a Gaussian or Lorentzian shape, and the decay of a radioactive sample follows an exponential function.

Two approaches to generating these _non-uniform_ random numbers are known as the **inversion method** and the **von Neumann rejection method**. 

- The inversion method is the analytical approach, because we consider the distribution of random numbers as a function, $f(x)$ (where $x>0$ for all values $x$.
Then, by integrating this function, $$\int_{-\infty}^{\infty}f(x)dx = 1$$ we get the cumulative distribution function (CDF),

$$
F(x) = \int_{-\infty}^{x}f(t)dt.
$$


Stick with me here. After we've found this function, we simply take its inverse to get non-uniformly distributed random numbers, $x$. In other words, 

$$
s = F(x) \Leftrightarrow x = F^{-1}(s).
$$


- The other method, known as the von Neumann (hit-and-miss) rejection method, rescues us from evil functions that cannot be integrated or inverted (or would take an eternity).
This approach is entirely numerical and works for any finite-valued function in a finite interval. Let's consider a normalized, arbitrary function $f(x)$ defined betwewen the interval $x \in [a, b]$.
Now, if we let $X$ be some number which is $\geq f(x)$ for any/every value $x$ in the interval. Then, we can generate uniformly-distributed randoom numbers $x$ between $[a, b]$ and compare them to uniformly-distributed
random numbers $y$ between $(0, Y)$. More specifically, check if $y > f(x)$. If so, we can count this as a _miss_, and values $y<= f(x)$ are counted as _hits_. We keep the $x$ values that are "hits", and those are our randomly generated numbers.

## Goals 

Why explain all of this? Well, this project takes a slightly different approach by combining both methods together! 
The idea is that, if we know the shape of some function, then we can find a function which is always larger than the one being generated, but not by too much. 
Then, we can use the analytical approach to get random numbers for the larger function, and _then_ use the hit-and-miss method to have significantly fewer misses than the traditional hit-and-miss method. 
This means we get rid of the cons of the hit-and-miss method but also avoid the limitations of the analytical method!

## Steps

Okay, let's break down the steps we need to follow to carry out such a project.

1. Find the inverse of the function,

$$
f(x) = \frac{4}{x^2 + 4}.
$$


This is done by 

$$
F(u) = \int_{-10}f(x)dx.
$$


Some math later, we get 

$$
F^{-1}(u) = 2 \tan \left[ x \left[ \tan^{-1} \left( 5 \right) - \tan^{-1} \left( -5 \right) \right] + \tan^{-1} \left( -5 \right) \right].
$$


2. Then, generate a random distributiono following $f(x)$ by generating uniformly-distributed random numbers $u$ in the interval [0, 1] and set $x = F^{-1}(u)$. 

3. Now it's time to work with the combined analytical + rejection method. Introduce a "mask" function $g(x)$ that will reduce the number of "misses", increasing the efficiency of our method. This is done by:
   - Generating a normally distributed number $x$ with the Box-Muller method in the interval $[-10,10]$ (the Box-Mueller method is used to generate a Gaussian “mask” distribution function).
   - Generating a uniformly distributed random number $y$ between $0$ and $A * \text{gaussian}(x)$.
   - $x$ is a "hit" if $y < f(x)$.
   - Let $A = 14.1$ (some constant found by trial-and-error).

## Results

We've finally made it to the results part!

Here's an example of what the hit-and-miss method might look like on its own:

![Figure of f(x) and the "mask" function g(x) as a square](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_analytical_approaches/Figure_4.png?raw=true)

It turns out that by doing this combined method, the "hits" are around $30$% more efficient! This is because we have acieved the goal of $g(x)$ being larger than $f(x)$ for all $x$ values, but not too much larger.

![Figure of our combined hit-and-miss method](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_analytical_approaches/Figure_3.png?raw=true)

This figure above is just a rough estimate of what we should expect. This next figure shows the actual results found by following the steps listed above. 

![Figure comparing the combined hit-and-miss method versus just the analytical method](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_analytical_approaches/Figure_1.png?raw=true)

In this figure, I have plotted function $f(x)$ and "mask" function $g(x)$ as a sort of guidelines showing how well each method performs when trying to model the $f(x)$ distribution. The blue historgram bars are what we get when following the analytical method by itself, and the orange histogram shows what we get using the combined method. As you can see, the orange histogram performs better ($\approx 30$%). 

Thanks for sticking around, and feel free to check my [GitHub](https://github.com/binarykisu/university_projects/tree/main/monte_carlo_projects/mc_analytical_approaches) page for all of the code I wrote. I hope you learned something cool! 


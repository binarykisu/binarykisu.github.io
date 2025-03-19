---
layout: project
title: "University Project #1"
date: 2024-02-18
excerpt: "This project is about the Inverse transform and Breit-Wigner distribution. It was completed during a Statistical Methods course."
tags: [university, statistics, breit-wigner]
comments: false
---

## Introduction

The Breit-Wigner (BW) distribution describes the energy distribution of an unstable quantum state, 

$$
\frac{dN}{dE} \propto \frac{(\Gamma_s)^2}{(E - E_s)^2 + (\Gamma_s/ 2)^2},
$$

where $E_s$ and $\Gamma_s$ are the mean energy and uncertainty on the mean energy of the state. $\Gamma_s$ is inversely proportional to the lifetime of the state.

## Generating the BW distribution

The BW distribution function is of interest because it can be found by taking the inverse Fourier transform of a uniform distribution of data. 

This is done by using a function such as $E(r)$, which gives the desired p.d.f. $f(E)$ can be evaluated using $r$ values that are uniformly distributed between $0$ and $1$. The probability to obtain a value of $r$ in $[r, r + dr]$ is given by $g(r)dr$. This is equivalent to the probability to obtain the energy, $E$ in $[E(r), E(r) + dE(r)]$, which is $f(E)$. This can be obtained by finding $E(r)$ and, therefore, the cumulative distribution function $F(E(r))$. 

Solving for $E(r)$,

$$
E(r) = \frac{\Gamma_s}{2} \tan{((r-1/2)\pi)} + E_s.
$$


This gives values of energy distributed like the Breit-Wigner distribution for when $r=[0,1]$.

## The goal

This goal for this project is to first generate random numbers according to a BW distribution with $E_s = 25$ and $\Gamma_s=5$ (the units here are arbitrary) and plot them into a histogram. Then, the central part of the generated distribution is fitted with a Gaussian distribution function. We can compare the obtained mean $\mu$ with the original $E_s$ and the obtained standard deviation $\sigma$ with the original $\Gamma_s$.

## Results

![BW distribution](https://raw.githubusercontent.com/binarykisu/university_assignments/main/statistical_methods_projects/breit-wigner_distribution/bw_dist.png)

Pretty cool, right?

Furthermore, the values I obtained for $\mu$ and $\sigma$ were $25.062$ and $1.599$, respectively. Comparing these with $E_s = 25$ and $\Gamma_s=5$, we can see that it wasn't too far off. This project is also available to view in [GitHub](https://github.com/binarykisu/university_projects/tree/main/statistical_methods_projects/breit-wigner_distribution), where the relevant code is included.

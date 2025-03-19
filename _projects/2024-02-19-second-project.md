---
layout: project
title: "University Project #2"
date: 2024-02-19
excerpt: "This project is about using the Maximum likelihood function with binned data."
tags: [project, university, statistics, maximum likelihood, data analysis]
feature: /assets/img/project-feature.png
comments: false
---

## Introduction

This project centers around an experiment much like the one conducted by physicist Jean Perrin, who received the Nobel Prize in Physics in 1926 for his pioneering work on atoms. 
Perrin's experiment involved the observation of molecular clusters suspended in a liquid medium, bringing valuable insights into the fundamental properties of matter and the discovery of Avogadro's number. 
His experiment can now be replicated and extended through modern computational techniques!

## Goal

The goal with this project is that, by analyzing data collected from observations of molecular clusters at different heights, one can estimate key parameters such as the Boltzmann constant or the number of clusters at some reference height. 
There will be three main parts:

**Part one**:
- Determine the Boltzmann constant, $k$ with the maximum likelihood method by maximizing $ln L(k)$ using some given data (will be shown in the next part).
- Estimate the uncertainty on the value $k$.
- Plot the results.

**Part two**:
- Use the log likelihood formula to determine values for both $k$ and $\nu_0$, along with their uncertainties.
  - This should be done using binned maximum likelihood method with the same data as from before.

**Part three**:
- Once we have the $k$ value, we can use it to determine Avogadro's number and its uncertainty.

## Formulas and data

Molecular clusters: 
- Radius: $r = 0.52 \mu m$
- Density: $1.063 g/cm^3$
- Thickness: $\approx 1 \mu m$

Photographs taken with microscope:
- Height, $z$ ($\mu m$): $\rightarrow$ Number of clusters, $n$:
  - $0$ $\rightarrow$ $1880$
  - $6$ $\rightarrow$ $940$
  - $12$ $\rightarrow$ $530$
  - $18$ $\rightarrow$ $305$

Gravitational potential energy of a spherical cluster of mastic molecules in water: $4 \pi r^3 \Delta\rho g z / 3 $
- Density difference between mastic and water: $\Delta\rho = \rho_{mastic} − \rho_{water}$
- Speed of acceleration/gravity: $g = 9.80 m/s^2$
- Probability for cluster to be in energy state, $E \propto e^{-E/kT}$
  - $k$ is the Boltzmann constant and $T= 293 K$ is the absolute temperature

Observed number $n$ at height $z$: 

$$
\nu(z) = \nu_0 e^{-4 \pi r^3 \Delta \rho g z / 3 k T}, \text{where } \nu_0 = \nu (z=0)
$$


Maximum likelihood method for binned data: 
$$
\ln{L}(\nu_0, k) = \sum_{i=1}^{N=4} (n_i \ln{\nu_i} - \nu_i)
$$


Avogadro's number can then be found using the relation: $N_A = R/k$ 

Gas constant: $R = 8.314 J/mol·K$

_Note: Remember that all units need to be converted into SI units and the density difference needs to be determined!_

## Results

**Part one**:
- By letting $\nu_0 = 1880$, the optimal value for $k$ was found to be: $k = 1.22 \pm 0.03 \cdot 10^{-23} J/K$.
  - The uncertainty is included in the value, but it is $2.52 \cdot 10^{-25}$.

**Part two**:
- Now, $\nu_0$ and $k$ are free parameters.
- From this part, I got $k = 1.24 \pm 0.03 \cdot 10^{-23} J/K$ and $\nu_0 = 1844.94 \pm 4$.
- The uncertainty of $k$ and $\nu_0$ are $3.00 \cdot 10^{-26}$ and $3.93$, respectively.

**Part three**:
- With all of this information, Avogadro's constant is easy to find:
  - $N_A = 6.72 \pm 0.16 \cdot 10^{23}$
  - The uncertainty is $1.63 \cdot 10^{21}$

The figures below will hopefully provide some much-needed visual aid.

![Figure one: parameter estimation](https://raw.githubusercontent.com/binarykisu/university_assignments/blob/main/statistical_methods_projects/maximum_likelihood/Figure_1.png)

![Figure 2: Parameter estimation including confidence of 1 standard deviation](https://raw.githubusercontent.com/binarykisu/university_assignments/blob/main/statistical_methods_projects/maximum_likelihood/Figure_2.png)

I hope you enjoyed this project! The code can be found on my [GitHub](https://github.com/binarykisu/university_projects/tree/main/statistical_methods_projects/maximum_likelihood) if you are interested.



---
layout: project
title: "University Project: Pearson's chi-square test"
date: 2024-02-20
excerpt: "This project tests whether two distributions are compatible with each other."
tags: [project, university, statistics, chi-square, data analysis]
feature: /assets/img/project-feature.png
comments: false
---


## Introduction

Particle physics experiments often involve analyzing data to uncover new particles or phenomena beyond the known standard model. 
Pearson's $\chi^2$ test can be used to test whether two distributions are compatible with each other, and can validate simulations against real data to ensure their accuracy and reliability.

The $\chi^2$ statistic is defined as:

$$
\chi^2 = \sum_{i=1}^{N_{bins}} \frac{(n_{i,data} - n_{i,MC})^2}{n_{i,MC}}, 
‎‎$$


where $n_{data}$ are the Poisson distributed measurements (histogram bin contents).

## Goal

The aim for this project is to employ the $\chi^2$ test to compare mass measurements obtained from real data with those simulated from two different background models. 
The first test will be to see if data can be described by only the first background (from `MC1_mass.txt`), and similarly by only the second background (from `MC2_mass.txt`).

A few bins have some small values, so one doesn’t expect for the test statistic to exactly follow the theoretical $\chi^2$ distribution. 
Therefore, the second test will be to try to determine the true distribution assuming the two hypotheses, `MC1_mass` and `MC2_mass`.

Then, the third test will be to find constant $a$ so that the combination $a * \text{MC1} + (1−a) * \text{MC2}$ best models the data using the cumulative $\chi^2$ distribution and pseudoexperiments.

## Results

For the first test:
- The $\chi^2$ values obtained by comparing the real data against background 1 and background 2 are $\chi_1^2 = 483.74$ (for MC1) and $\chi_1^2 = 28.14$ (for MC2), respectively.
- The probability (P-values) tells us how probable it is to get an equally (or more improbable) result from random data distributed as the theory. These values can be found by integrating the $\chi^2$ distribution with $n=20$ degrees of freedom from the obtained $\chi^2$ value to infinity.
  - The obtained P-values are $P_1 = 0$ for background 1 and $P_2 = 0.106$ for background 2.
- These resulting values allow us to conclude that MC1 is not the only background (due to the small P-value). However, MC2 may be compatible.

For the second test:
- Pseudoexperiments were performed by generating simulated data based on the Poisson Monte Carlo distribution with the means given by the simulated mass data for backgrounds 1 and 2. It generates more usable $\chi^2$ distribution values for both theories.
  The P-value is obtained as the ratio of pseudoexperiment $\chi^2$ values that are higher than the $\chi^2$ values we got for each background (from the first test) over the total number of pseudoexperiments.
- The resulting P-values are $P_{pseudo,1} = 0.001$ for MC1 and $P_{pseudo,2} = 0.103$ for MC2.
- The compatibility of the MC1 background is nonexistent again, and the MC2 background is good again.

Here is the figure which best shows what we've figured out so far:

![Figure 1](https://github.com/binarykisu/university_projects/blob/main/statistical_methods_projects/pearsons_chi-squared_test/Figure_1.png?raw=true)

 Finally, for the third test:
 - The value for $a$ and the best modeled $\chi^2$ value is found by varying the value of a constant, $a$ (representing the amount of background 1 appearing in the sample), between 0 and 1 and finding which value results in the smallest value for $\chi^2$.
 - The value for $a$ was found to be $a = 0.161$ and the corresponding $\chi^2$ value is  $\chi^2 = 14.75$.
 - The P-value based on the $\chi^2$ value is $P = 0.791$ and the P-value based on pseudoexperiments is $P =  0.743$.
 - From these results, the data can be fully explained by the combination of backgrounds with $\approx 16%$ of MC1 and $\approx 84%$ of MC2.

Here is the second figure, showing the results found from the third test:

![Figure 2](https://github.com/binarykisu/university_projects/blob/main/statistical_methods_projects/pearsons_chi-squared_test/Figure_2.png?raw=true)

That's all for this project. Check out the original datasets and code from my [GitHub](https://github.com/binarykisu/university_projects/tree/main/statistical_methods_projects/pearsons_chi-squared_test)!

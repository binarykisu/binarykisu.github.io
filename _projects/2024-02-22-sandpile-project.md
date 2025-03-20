---
layout: project
title: "University Project: Sandpile algorithm"
date: 2024-02-22
excerpt: "This project explores cellular automata and self-organised critical phenomena. A common example from nature is the sandpile inside of an hourglass."
tags: [project, university, statistics, sandpile-algorithm, data-analysis,]
feature: /assets/img/project-feature.png
comments: false
---


## Introduction

One of the most commonly examples of a _self-organized critical phenomenon_ is a sand pile. 

What is a self-organized critical phenomenon, you might ask?

It can generally be explained as a large-scale or complex event which seems to occur very rarely/randomly (i.e. earthquakes, avalanches, forest fires, etc.).
- Some of these can indeed occur randomly, but they could also be triggered by self-organized ciriticality.
- A system is considered to be critical if the number of events, $N(s), follows a power law: $N(s) \propto s^{- \alpha}$

## Goal 

The goal for this project is to create an algorithm that considers grains of sand falling on a flat square with open edges.
- The first grains of sand land and remain at their positions. But what happens as the grains start to pile on top of one another?
   - Steep, unstable slopes will collapse in small "sand avalanches"!
- The avalanches stabilize the sand, and it will eventually reach a steady-state shape (a pile with exactly a $45\degree$ angle) close to that of a cone.
   - This system is critical because, one the steady-state is reached, there will be avalanches of all sizes (even as big as the system itseslf)!
   - The system is also self-organized, because nothing (such as temperature or pressure) is needed to make the system enter its steady-state configuration.

_Note: There are many other well-explained and thorough sandpile algorithms out there, but this was my first go at it._

## Steps to follow

By following the steps/rules for cellular automata, this system can be created without too much difficulty. Here are the steps that I followed:

Cosider a one-dimensional system with $L$ sites $1,\dots,L$. Let the height of each site be $h(i)$.
1. Add a grain to the lef-most site: $h(i) = h(i) + 1$.

  2. For all sites $i$, if $h(i) - h(i + 1) > 1$, mark the site for toppling.

  3. Topple all marked sites to the right using $h(i) = h(i) - 1$ and $h(i + 1) = h(i + 1) + 1$.

  4. Set $h(L + 1) = 0$, i.e. grains beyond $L$ are lost forever.

  5. If any sites were toppled, return to step 2.

6. Return to step 1.

Note that the sand will continue to topple until a steady configuration is reached at each time step.

Now, the system can become more interesting by making a few changes. This is desireable because, after the system has reached a steady state, all avalanches will be exacttly of size $L$, and 
all other added particles will leave the system at the edge.

- Step 2 $\rightarrow$ Step 2: For all sites $i$, mark the site for toppling if $h(i) − h(i + 1) > 2$.
- Step 3 $\rightarrow$ Step 3: Topple all marked sites _two_ steps to the right using $h(i) = h(i) − 2$ and $h(i + 1) = h(i + 1) + 1$, $h(i + 2) = h(i + 2) + 1$.

Now, the system will exhibit the power-law dependency.

7. Allow toppling to occur both to the left and right, and dropping grains randomly everywhere along the interval $[1, L]$.

8. If the number of grains is more than $2$ larger than both left or right, choose one of the topple directions randomly, and then topple only $2$ grains.

## Results

I feel like I got this program to run quite well, and while I chose to not create an animated plot which updates as the grains of sand are dropped, I did create a visual text output in the console/terminal which 
sort-of does the same thing.

Adding the first grain:

![Figure 1: The first grain has been added to the grid.](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_sandpile/Figure%201.png?raw=true)

After many iterations (_Remember: the size of the grid and number of iterations can be chosen_), here is an example of what it looks like for the sandpile to have an avalanche:
- As you can see, this pile is looking pretty tall..

 ![Figure 2: A pile that is getting tall, and about to topple over.](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_sandpile/Figure%202.png?raw=true)

- Another grain is added to this same pile! It will now topple over.

 ![Figure 3: The pile topples over to the right.](https://github.com/binarykisu/university_projects/blob/main/monte_carlo_projects/mc_sandpile/Figure%203.png?raw=true)

- As you can see, the states of the piles are now more stable.

Who knew sand could be so interesting?? This project's code can be found on [GitHub](https://github.com/binarykisu/university_projects/tree/main/monte_carlo_projects/mc_sandpile).

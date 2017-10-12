---
title: 'Shiny app: Distributions of random variables'
author: Matthew Leonawicz
date: '2017-10-12'
slug: shiny-app-distributions-of-random-variables
categories:
  - R
tags:
  - Shiny
  - random variables
  - probability
  - distributions
  - plotmath
  - source code
header:
  caption: ''
  image: '../img/post/rvdist.png'
---

There is a new version of my [Distributions of Random Variables](https://uasnap.shinyapps.io/rvdist/) Shiny app available.
This is a cleaned up modern revision of my original 2013 app series involving random variable probability distributions.
The primary change is a switch to `ggplot2` from base graphics. I have added this app to my [shiny-apps](https://github.com/ua-snap/shiny-apps) GitHub repository so the source code is available, including a script containing all those pesky `plotmath` expressions.

<p align="center"><img src="/img/post/rvdist.png"/></p>

The app draws and plots samples from various well known discrete and continuous probability distributions, all of which are available in base R with the single exception of the Pareto distribution. To include this distribution, I used the `VGAM` package. The plots include an overlay of the formula for the selected probability mass or density function.

Available discrete distributions:

* Bernoulli
* Binomial
* Uniform
* Geometric
* Hypergeometric
* Negative Binomial
* Poisson

Available continuous distributions:

* Beta
* Cauchy
* Chi-squared
* Exponential
* F
* Gamma
* Laplace (Double Exponential)
* Logistic
* Log-Normal
* Normal
* Pareto
* t
* Uniform
* Weibull

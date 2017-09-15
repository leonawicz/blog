---
title: 'R animation: global climate change'
author: Matthew Leonawicz
date: '2016-09-29'
slug: r-animation-global-climate-change
categories:
  - R
tags:
  - visualization
  - animation
  - climate change
  - mapmate
header:
  caption: ''
  image: '../img/post/global_climate_change.jpg'
---

I have posted a new R data animation video. It's an example animation of modeled historical and projected global temperature change from 1850 - 2100. The data prep, analysis, full processing and generation of all sets of still frames for each layer in the video are done using R.

<div style="text-align:center;">
<iframe src="https://www.youtube.com/embed/xhqEkyJDBho?ecver=2" width="640" height="360" frameborder="0" allowfullscreen></iframe>
</div>

Typically an ensemble of models would be used but this video is just to demonstrate a basic animation using one climate model, both with a monthly time series and a monthly 10-year moving average time series. If wondering about the y-axis range, the animation shows anomalies, or delta change, from the climate model's historical baseline monthly average temperatures using a given climatology window.

In a later video I will use annual and seasonal averages, which will display a smoother signal than monthly series.

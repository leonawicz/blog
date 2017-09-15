---
title: 'R animation: global SNAP Shiny app users'
author: Matthew Leonawicz
date: '2016-03-25'
slug: r-animation-global-snap-shiny-app-users
categories:
  - R
tags:
  - visualization
  - animation
  - mapmate
  - Shiny
header:
  caption: ''
  image: '../img/post/apptraffic_bkgd.png'
---

For the blog readers, just a quick heads up that I have posted a new R data animation to YouTube. A complete post will follow, but for now here is the video. It displays the social network of SNAP Shiny app users over about the past year and a half using great circle trajectories on a rotating 3D Earth. It's best in 1080p, but still somewhat degraded for streaming. I'll post the raw source video later as well, which is crystal clear.

<div style="text-align:center;">
<iframe src="https://www.youtube.com/embed/uQYR91qixgo?ecver=2" width="640" height="360" frameborder="0" allowfullscreen></iframe>
</div>

I used geolocation data from Google Analytics. I routed all the traffic randomly through either Fairbanks, AK or Denver, CO to complete the network since those two places best describe where my apps come from. It's great to see how many people connect to the apps and from where; too many people to plot as a single static graphic without some of the essence of the data being lost.

As usual, the still frames of the rotating globe, its surface texture, country boundaries and great circle paths are all made in R. It's basically a series of plots made with ggplot2.

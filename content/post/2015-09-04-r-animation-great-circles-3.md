---
title: 'R animation: great circles 3, final draft'
author: Matthew Leonawicz
date: '2015-09-04'
slug: r-animation-great-circles-3
categories:
  - R
tags:
  - statistics
  - visualization
  - animation
  - great circles
  - mapmate
header:
  caption: ''
  image: '../img/post/datavis_r_geonet3.jpg'
---

Here is the final draft of my great circle arcs R animation. I made this back in January shortly after my first two drafts, but am only now getting around to sharing it, which is a typical representation of how seldom I can make time for blogging. But given the recent spike in interest (thanks to <a href="http://urbandemographics.blogspot.co.uk/2015/08/data-visualization-with-r-geographic.html" target="_blank">Urban Demographics</a> for sharing my work) in the first, and roughest, draft, I am motivated to finally share something better.

As with <a href="http://blog.snap.uaf.edu/2015/03/04/animated-great-circles-1-flat-map-to-3d-earth/" title="Animated great circles 1: flat map to 3D Earth">DRAFT 1</a> and <a href="http://blog.snap.uaf.edu/2015/04/16/animated-great-circles-2-smoother-lines/" title="Animated great circles 2: smoother lines">DRAFT 2</a>, the YouTube video upload is of significantly reduced quality compared to the original render. As I've said in the previous posts, it's really not even worth watching on YouTube.

A much higher quality <a href="https://www.snap.uaf.edu/webshared/leonawicz/video/geonet_seq3.zip">source video is available here</a>. It can be downloaded (~365 MB) and viewed locally using a standard video player such as VLC. Here is a screenshot taken from source as an example:

<a href="/img/post/datavis_r_geonet3.jpg"><img src="/img/post/datavis_r_geonet3.jpg?w=774" alt="datavis_R_geonet3" width="774" height="424" class="aligncenter size-large" /></a>

The previous posts describe the issues with video streaming sites compressing videos for steaming and how this will not noticeably degrade most videos, but my great circle animations (particularly this one) have many tiny rapidly moving lines and subtle color and transparency changes; i.e., the perfect candidate videos for being severely degraded by re-encoding, with too much information being tossed out from frame to frame for streaming purposes. In fact, despite being my final draft, this video may ironically display more poorly on YouTube since it contains so many more elements in motion and frame-to-frame pixel changes than my first two drafts, while being far superior in quality when viewing the source video.

I am quite pleasantly surprised at the video quality on YouTube (1080p, full screen mode) at the beginning of the video. Perhaps this is because there are only 1,000 lines at first and they do not move quite as fast as in my previous videos. Furthermore, being shorter in length, their movement on the screen involves fewer pixel changes from frame to frame. There may be occasional stutter or moments of blurriness during streaming but overall not too bad with a good connection. As I expected, however, later in the video as I increment the number of great circle pathways simultaneously on the screen to over 10,000, the quality degrades significantly.

Here is the YouTube version if you must:

<div style="text-align:center;">
<iframe src="https://www.youtube.com/embed/yoyIUMvIP3Q?ecver=2" width="640" height="360" allowfullscreen></iframe>
</div>

In addition to my great circle path traversal animation, this video also incorporates a layer of my gridded path traversal in places. See <a href="http://blog.snap.uaf.edu/2015/02/06/animated-gridded-paths-in-r/">Animated gridded paths in R</a> for a description and video example of this process.

<a href="http://blog.snap.uaf.edu/2015/04/14/animated-paths-in-r-toy-example/" title="Animated paths in R: toy example">This post</a> explains one way to animate basic path traversal in R using a toy code example. Please read this before inquiring about source code. It explains how the basic concept is easy to implement for your data and provides template code, but the resources and computing environment I used to produce the frames for these videos makes the specific code I used not reproducible.

There is nothing special about the code that will make it magically perfectly scalable. That's where you have to provide your own ingenuity to deal with your data. For example, few people are going to want to use or have access to the <code>Rmpi</code> package on a multi-node Linux cluster to speed up the process. Depending on your data, you would have to find your own ways of dealing with the sheer resource overhead you may create. Believe it or not, the gridded paths can be much more resource intensive (RAM, CPUs, and/or time, pick your poison) to produce quality animations than great circles. This is because sometimes displaying movement of line segments along gridded paths requires segments which are defined by longer vectors of more closely spaced points in order to "turn corners" nicely.

Also, recall from previous posts that I am using R to make still frames and I then dump the image sequence onto a timeline in a movie editing program to render the video. There are R packages like <code>animation</code> which can abstract the entire process for you, but it isn't meant for something as large as this video. Besides, it just makes sense to use R for statistically and mathematically defined data plotting and animation sequences and use a video rendering program for finishing touches and rendering to mp4 format. Do what makes the most sense with each piece of software.

Lastly, credit obviously to John Tukey for the "Tukey tally" 30-point countdown visual I made for the beginning of the video. While perhaps not the most interesting, that code is short, simple, and shareable so I will just dump it here:

```r
# Tukey tally plot sequence
tukeyTally <- function(i, ...){
  stopifnot(as.numeric(i) && i %in% 1:10)
  par(mai=c(0,0,0,0))
  plot(0, 0, type="n", axes=F, xlab="", ylab="", xlim=c(0, 1), ylim=c(0, 1))
  m <- matrix(c(0,1,1,0,1,1,0,0), nrow=4)

  if(i>=5) segments(m[1,1], m[1,2], m[2,1], m[2,2], ...)
  if(i>=6) segments(m[2,1], m[2,2], m[3,1], m[3,2], ...)
  if(i>=7) segments(m[4,1], m[4,2], m[3,1], m[3,2], ...)
  if(i>=8) segments(m[1,1], m[1,2], m[4,1], m[4,2], ...)
  if(i>=9) segments(m[1,1], m[1,2], m[3,1], m[3,2], ...)
  if(i==10) segments(m[4,1], m[4,2], m[2,1], m[2,2], ...)

  points(m[1,1], m[1,2], ...)
  if(i>=2) points(m[2,1], m[2,2], ...)
  if(i>=3) points(m[3,1], m[3,2], ...)
  if(i>=4) points(m[4,1], m[4,2], ...)
}

dir.create(outDir <- "C:/leonawicz/GlobalNetworks/plots/frames/tukey_ticker_10to1", showWarnings=FALSE)
for(i in 1:10){
  png(paste0(outDir, "/tukey_ticker_10to1_frame", 10-i, ".png"), bg="transparent")
  tukeyTally(i, lwd=10,  pch=19, cex=4, col="greenyellow")
  dev.off()
}
```

You may be wondering how this can be a "final" draft. The obvious next step is to reproduce this video projected onto a 3D rotating earth, right!? Believe me, I have thought about it. That would take a good deal more work. As I explained in the post for the first draft, the only one to feature great circle lines on a spinning globe, resource issues makes it orders of magnitude more challenging, and this 2D flat map video is already far more complex than the original draft. Perhaps later I will take this on. In the meantime enjoy the video.

---
title: apputils 0.5.0 released
author: Matthew Leonawicz
date: '2017-10-24'
slug: apputils-0-5-0-released
categories:
  - R
tags:
  - Shiny
  - statistics
  - visualization
  - package
  - apps
header:
  caption: ''
  image: '../img/post/apputils.png'
---

Version 0.5.0 of the [apputils](https://github.com/leonawicz/apputils) R package has been released on GitHub.
Complete documentation is available at the [apputils website](https://leonawicz.github.io/apputils).

The key updates are:

* Added `exApp` for running Shiny app package examples.
* Ported custom icons demo app to `apputils`.
* Included all current custom icons in example app, adding the newer linear model themed icons.
* Added package css for `infoBox` override.
* Added introduction vignette content for stat boxes with package icons.

You can now call `exApp("icons")` to view the stat box icons examples locally.
Available icons are grouped into three categories.

### Icons representing common statistics

<p align="center"><img src="/img/post/apputils_vbox1.png"/></p>

### Icons representing delta change or trends

<p align="center"><img src="/img/post/apputils_vbox2.png"/></p>

### Icons related to fitting statistical models

<p align="center"><img src="/img/post/apputils_vbox3.png"/></p>

These are the recent updates to `apputils`. However, the package offers other helpful utilities such as convenient functions for:

* app citation
* a showcase widget for displaying and linking to other related apps
* an author/contact info widget
* dashboard sidebar footer logo
* collapsible FAQ widget
* integration with `rintrojs` and `shinytoastr`.

These utilities involve relatively canned styles of presentation so they are not universally suitable for all users and use cases, but they offer convenience when applicable. An example app that uses several utilities from `apputils` is my recent work in progress, the SNAP [Climate Analytics](https://uasnap.shinyapps.io/climdist/) app.

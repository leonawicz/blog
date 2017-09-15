---
title: Custom images for Shiny dashboard valueBox icons
author: Matthew Leonawicz
date: '2017-01-11'
slug: custom-images-for-shiny-dashboard-valuebox-icons
categories:
  - R
tags:
  - Shiny
  - visualization
  - source code
header:
  caption: ''
  image: '../img/post/valueboxes1.png'
---

The `shinydashboard` package provides functions like `valueBox` that conveniently display basic information like summary statistics. In addition to presenting a value and subtitle on a colored background, an icon may be included as well. However, the icon must come from either the Font Awesome or Glyphicon icon libraries and cannot be image files.

I've <a href="https://gist.github.com/leonawicz/0fab3796b02a62b7f3bd0c02a171f0b7">provided a gist</a> that shows how to achieve the use of custom icons with local image files stored in an app's `www/` directory. It involves overriding a couple functions in `shiny` and `shinydashboard` and adding a small bit of custom CSS. Ideally, functionality could be included in future versions of these two packages to allow this in a more robust and complete fashion. But for now, here is a way to do it yourself for value boxes.

<a href="/img/post/valueboxes1.png"><img src="/img/post/valueboxes1.png" alt="valueboxes1" width="599" height="351" class="aligncenter size-full" /></a>

The gist above includes the `app.R` file to run the <a href="https://uasnap.shinyapps.io/customiconsdemo/">Custom Icons Shiny app demo</a> and the `override.R` file which I have it `source` separately. The gist also includes an `icons.R` script to generate some statistics and probability themed icons from R. This is interesting and fun on its own. This is not needed to run the app, but the icons are of course needed. If you build the app locally you will have to run this script to generate the images and place them in your `www/` folder. The live app demo contains them already.

I've included both light and dark examples using icons that can be used to generally represent a distribution, mean, standard deviation, minimum, maximum, median or interquartile range. Note that `app.R` adds some custom CSS; it is not sufficient to override the definitions of `icon` and `valueBox` alone. I placed it inline for to reduce the number of required files, but it could alternatively be loaded from a file using `includeCSS`.

This overriding functionality is only for `valueBox` widgets and the way in which a local image file is passed to `icon` is with a named list where the available names are `src` (required, image file name) and `width` (optional, defaults to `'100%'`). It is restrictive but demonstrates potential to use image files in place of icon library options without too much code refactoring.

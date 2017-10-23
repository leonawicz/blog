---
title: 'Climate explorer update: monthly data and delta change'
author: Matthew Leonawicz
date: '2017-10-23'
slug: climate-explorer-update-monthly-data-and-delta-change
categories:
  - R
tags:
  - climate science
  - climate change
  - Shiny
  - statistics
  - visualization
  - distributions
  - anomalies
  - projections
header:
  caption: ''
  image: '../img/post/climdist_data.png'
---

The SNAP [Climate Analytics](https://uasnap.shinyapps.io/climdist/) Shiny app has been updated.
Previously, the app included seasonally and annually aggregated data.
With the recent inclusion of monthly data, the number of conditional spatio-temporal climate probability distributions has now increased from a base set of about 13 million unique distributions to over 46 million. The `Seasonal` dropdown menu now offers annual average, 3-month seasonals, and individual months.

This other major change is the ability to convert figures and statistics to reflect projected delta change (anomalies) in comparison with a historical climatology period.
The new option can be found in the `Additional settings` modal.

<p align="center"><img src="/img/post/climdist_climatology.png"/></p>

In this example, the data selection is as shown here.

<p align="center"><img src="/img/post/climdist_data.png"/></p>

By default, raw climate values are shown, e.g., a time series of temperature values.
This is unchanged from before.

<p align="center"><img src="/img/post/climdist_ts1.png"/></p>

When the delta change option is checked, plots and statistics update to reflect change vs. historical baseline average.
Climatologies use CRU 4.0 data. The period can range anywhere from 1950 - 2009, defaulting the the 1980 - 2009 30-year climatology.
Climatologies are unique to each geographic region and seasonal period.

<p align="center"><img src="/img/post/climdist_ts2.png"/></p>

As you can see above, some comparisons of change over time are easier to glean from the plot when viewing delta change instead of raw values.
Also note that temperature deltas or anomalies are differential whereas change in precipitation is proportional.

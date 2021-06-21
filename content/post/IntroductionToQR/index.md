---
title: Extreme event analysis using quantile regression
subtitle: 

# Summary for listings and search engines
summary: Gentle introduction to using quantile regression to understand changes in distributions and extreme events using R and environmental datasets.

# Link this post with a project
projects: ["Quantile Regression"]

# Date published
date: "2021-06-21T00:00:00Z"

# Date updated
lastmod: ""

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Image credit: [**IPCC**](https://archive.ipcc.ch/ipccreports/tar/wg1/fig2-32.htm)'
  focal_point: ""
  placement: 2
  preview_only: false

authors:
- admin

tags:
- Extreme Event Analysis
- Statistics

# categories:
# - Demo
# - 教程
---

Climate change will increase the frequency and severity of extreme events like heatwaves, cyclones, and droughts. Unfortunately, *modeling extreme events is hard*. First, you need a lot of data. Second, most statistical models are not designed for extreme events. Third, extreme event models that do exist can have a high barrier to entry. Here I'll discuss a model I have found very helpful in my research to tackle these challenges: quantile regression.

## Why quantile regression?

1. Flexibly explore different parts of the target distribution (e.g. the tails)
2. Detect changes in mean, variability, and skew 
3. Utilizes the full dataset
4. Easy implementation thanks to _quantreg_ package in R

The opening graphic above from the IPCC demonstrates one use case of quantile regression. A shift in the distribution of, say, temperatures to warmer conditions will lead to far more extreme events (left). Most standard statistical methods are well suited to analyzing such changes in the mean. But, what happens when there are changes in variability (right), or changes in the mean and variability combined? Standard linear regression would report zero trend, from which you might falsely assume there is not trend in extreme events and thus underestimate your climate risk.

 





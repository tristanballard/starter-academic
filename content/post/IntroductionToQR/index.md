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

Climate change will increase the frequency and severity of extreme events. Unfortunately, **modeling extreme events is hard**. First, you need a lot of data. Second, most statistical models are not designed for extreme events. Third, extreme event models that do exist can have a high barrier to entry. Here I'll discuss a model I have found very helpful in my research to tackle these challenges: quantile regression.

## Why quantile regression?

1. Flexibly explore different parts of the target distribution (e.g. the tails)
2. Detect changes in mean, variability, and skew 
3. Utilize the full dataset
4. Robust to outliers
5. Easy implementation thanks to _quantreg_ package in R

The opening graphic above from the IPCC demonstrates one use case of quantile regression. A shift in the distribution of temperatures to warmer conditions will lead to far more extreme events (left). Most standard statistical methods are well suited to analyzing such changes in the mean. But, what happens when there are changes in variability (right)? Standard linear regression would report no trend in the mean, from which you might assume there is no trend in extreme events, hugely underestimating your climate risk.

## Detecting changes in distribution shapes

Let's walk through a few examples of shifts in the shape of the distribution, what they mean for extreme events, and how you would measure them with respect to different quantile trends.

Here I will consider trends in the 10th, 50th (median), and 90th percentiles. I have seen other climate scientists use the 5th and 95th percentiles, which look at trends in even more rare events, with the word of caution that your dataset should increase in size as you explore more and more extreme quantiles. 

The first scenario is a simple shift in the mean/median (a). This is the default assumption of most trend analyses I have seen in climate sciences. For shifts towards warmer weather, this means more hot extremes and fewer cold extremes. The 10th, 50th, and 90th percentile trends are all positive and roughly equal to each other. Easy!

{{< figure src="./qr_distributions.png" title="A caption" lightbox="true" >}}

The second scenario is...



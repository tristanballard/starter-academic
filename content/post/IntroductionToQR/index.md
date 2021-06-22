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

Climate change will increase the frequency and severity of extreme events. Unfortunately, **modeling extreme events is hard**. First, you need a lot of data. Second, most statistical models are not designed for extreme events. Third, those extreme event models that do exist have a high barrier to entry. Here I'll discuss a model I have found very helpful in my research to tackle these challenges: quantile regression.

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

{{< figure src="./qr_distributions_a.png" title="For simple shifts in the mean/median, linear regression would have served just fine." lightbox="true" >}}

The first scenario is a simple shift in the mean/median (a). This is the default assumption of most trend analyses I have seen in climate sciences. For shifts towards warmer weather, this means more hot extremes and fewer cold extremes. The 10th, 50th, and 90th percentile trends are all positive and roughly equal to each other. Easy!

{{< figure src="./qr_distributions_b.png" title="Increases in variability can greatly exacerbate extreme event risk when accompanying other shifts in the distribution." lightbox="true" >}}

The second scenario portrays a shift in the median towards warmer conditions along with an increase in variability. This would be the worst case if we are considering temperatures, with an essentially completely new thermal regime having a far greater likelihood of extreme warm temperatures. Here the 90th percentile trend exceeds the 50th, which itself exceeds the 10th.  

{{< figure src="./qr_distributions_c.png" title="In some cases, one tail of the distribution can experience huge changes while the median and other tail change little. Linear regression would struggle to accurately portray changing risk in this setting too. " lightbox="true" >}}

The third scenario portrays a shift in the median towards warmer conditions along with an increase in variability and a change in skew. Skewness can essentially be though of as a measure of distribution symmetry. Skewness is particularly relevant when the starting distributions are not normal, such as with precipitation and tropical cyclone (hurricane) speeds. In the scenario depicted above, subtle changes in the median belie massive increases in the risk of hot extremes. The expansion of variability here is driven primarily by increases in hot extremes.

## Application to river temperatures
As part of my PhD, I was interested in how rivers and streams have already responded to climate change. I conducted a trend analysis using quantile regression at 149 rivers across the U.S. utilizing daily water temperature data provided by the U.S. Geological Survey. 

In short, we found that 84% of rivers have already experienced warming in median water temperatures, and 77% of rivers indicate a significant change in variability. Nearly half of rivers show warming of the 90th percentile during summer months, suggesting increasing risk from extreme heat events. Warming of median and extreme temperatures can have important ecological consequences, such as by altering habitat suitability and exceeding species’ thermal thresholds.

{{< figure src="./demo_site_rt.png" title="Water temperatures at a river in Virginia indicate shifts towards warmer temperatures with a contraction of variability driven by decreases in cold extremes." lightbox="true" >}}

This river indicates a decrease in variability driven primarily by warming of the 10th percentiles, i.e. a decrease in cold extremes. Such an analysis provides a much more detailed picture of change in these systems than a typical linear regression. Moreover, we can pinpoint the driver of the changes in variability, something that methods like trends in standard deviation would fail to provide. 

## Final thoughts
I have found quantile regression tremendously useful in my work and look forward to its continued adoption in industry and academic research. I only scratched the surface in this post by demonstrating univariate quantile regression between temperature and time. As with linear regression, additional covariates can be incorporated to gain further insights into how different covariates interact to influence the response variable distribution and its extremes. A final caveat is that I did not touch on statistical significance testing of regression coefficients. The _quantreg_ package provides several options, and I typically use their bootstrap approach, but these can be complicated when investigating time series trends in the presence of autocorrelation.  
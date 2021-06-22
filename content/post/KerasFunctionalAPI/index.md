---
title: >-
  RiverHeatNet: Building a river temperature neural network with Keras functional API
subtitle: 

# Summary for listings and search engines
summary: I develop a framework to flexibly incorporate both time-varying and static variables into a river temperature model with over 4 million observations.  

# Link this post with a project
projects: ["Deep Learning"]

# Date published
date: "2021-06-22T00:00:00Z"

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
- Deep Learning
- Statistics

# categories:
# - Demo
# - 教程
---

## Motivation
I set out to develop a model for predicting river temperatures so that I can estimate how they will change in the future and under different sustainability scenarios. The dataset I collected consists of over 4.1 million temperature measurements across 1,210 rivers. Input variables like air temperature and precipitation are of the same time series structure as the output, but I also have information about each of the rivers like elevation and ecosystem type that I know are relevant and would like to incorporate.

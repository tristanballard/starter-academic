---
title: RiverHeatNet: Building a river temperature neural network with Keras functional API
subtitle: 

# Summary for listings and search engines
summary: I develop a framework to flexibly incorporate both time-varying and static variables into a river temperature model with over 4 million observations.  

# Link this post with a project
projects: ["Deep Learning"]

# Date published
date: "2021-06-21T12:00:00Z"

# Date updated
lastmod: ""

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'Network Architecture'
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

**The modeling challenge is that the predicted variable, water temperature, is a time series, while the input variables are a mixture of time series and static variables.**  Previous studies using artificial neural networks (ANNs) sidestepped this challenge by ignoring the time series structure of the data. Instead, I developed a model that flexibly incorporates both time series inputs and static inputs to predict a time series output using the Keras functional API.

There are a few options for tackling this variable mismatch:

1. Use an ANN and ignore the time series nature. Fast but ultimately lower accuracy since it leaves out so much useful information. This is what most if not all prior neural networks developed for river temperatures have done. 
2. Use a recurrent neural network with the static variables converted to time series, repeating the same values at every time step. Woefully computationally inefficient.
3. Combine the best aspects of 1 and 2

## Keras Functional API
Thanks to the Keras functional API, it is remarkably easy to combine recurrent neural network layers with standard, fully connected ANN layers. The functional API can build all of the same models as the sequential API but has much greater flexibility to incorporate different inputs. The functional API can also be used to build models with multiple outputs such as combined classification and regression tasks (e.g. this image is a cat predicted to be 4.3 years old).

## Model Architecture
#### LSTM Layers
I feed all input variables that are time series into separate long short-term memory (LSTM) cells. LSTMs, first proposed in 1997 by Sepp Hochreiter and Jürgen Schmidhuber, are a type of recurrent neural network commonly used in time series applications. LSTMS are capable of taking the input, storing it for as long as needed, and extracting its value later. As a result, they have been very suuccessful in tasks with long-term patterns like speech recognition and long texts. A commonly used alternative is the gated recurrent unit (GRU), which can be easily swapped in the API.

``` r
airTLayer <- airTInput %>% 
  layer_lstm(units = 7, dropout = 0.15, recurrent_dropout = 0.15)
```

The _units_ argument determines the dimensionality of the output space. I set it to 7 days. The input data are organized such that the 'lookback' period is 7 days as well, meaning that the model can only see data from the previous week when trying to fit today's value. I chose the lookback period based on a literature review, where we have little reason to believe river temperatures from more than a week prior will give useful information about todays temperature. The output dimension of 7 days is a tuneable hyperparameter and does not need to match the lookback period. 

The two dropout specifications impose a moderate regularization effect to help mitigate overfitting. How does it work? Simply put, during each forward or backward pass of the algorithm, 15% of the nodes are randomly ignored. This 15% level is also a tuneable hyperparameter. 

#### Fully connected layers


## Final thoughts
I have used the Keras functional API in both R and Python, and the syntax is nearly identical. This makes deployment and migration between languages a breeze.
---
layout: post
title:  "Time Series Modelling - ARIMA"
description: "Note on the ARIMA model for time series forecasting"
---

Arima is a simple method for forecasting time series using only lagged values. The statsmodels library contains an implementation of ARIMA for python (https://www.statsmodels.org/stable/generated/statsmodels.tsa.arima_model.ARIMA.html). 

ARIMA us made up of three components:

#### Auto Regressive (AR) 

An autoregression model forecasts a variable using a linear combination of its previous values. It is therefore a regression of the the variable *against itself*. So in an AR model:

$$\begin{equation} y_{t} = c + \sum_{i=1}^{p}\theta_{i}y_{t-i} + \varepsilon_{t} \tag{1} \end{equation}$$

where $$c$$ is some constant, $$\theta$$ is the regression coefficients and $$\varepsilon_{t}$$ is white noise. The $$p$$ term is the number of previous values to take, which is known as the order of the AR model. E.g. an AR(2) model would be a model that uses the previous 2 values. 

#### Moving Average (MA)

A moving average model is similar to the AR model, but it uses the past forecast errors rather than the past actual values. So in an MA model:

$$\begin{equation} y_{t} = c + \sum_{i=1}^{q}\phi_{i}\varepsilon_{t-i} + \varepsilon_{t} \tag{2} \end{equation}$$

where $$c$$ is some constant, $$\phi$$ is the regression coefficient and $$\varepsilon$$ is the error. The $$q$$ term is the number of previous error values to take, which again is known as the order of the model. An MA model should not be confused with moving average *smoothing* models. 

AR and MA models can be combined into an ARMA(p, q) model. 

#### I (Integrated)

Integrated simply refers to the differencing applied to the time series. Differencing is done by computing the differences between consecutive observations, e.g. for a series [2, 3, 5, 3, 4] the first order differenced series would be [1, 2, 2, 1]. The order of differencing is denoted by *d*.

Differencing is often necessary in order to make a series **stationary** (i.e. mean and standard deviation is not a function of time), which is a requirement for an ARIMA model. 

#### ARIMA

An ARIMA(p, d, q) model is the combination of the above three components: 

$$\begin{equation}  y'_{t} = c + \sum_{i=1}^{p}\theta_{i}y'_{t-i} + \sum_{i=1}^{q}\phi_{i}\varepsilon_{t-i} +  \varepsilon_{t} \tag{3} \end{equation}$$

where $$y'$$ is the time series $$y$$ differenced by order $$d$$. 
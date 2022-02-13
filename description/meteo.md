---
layout: default
title: Processing meteo data
parent: Description
nav_order: 2
permalink: /des/meteo
---

# Processing and regionalisation of meteorological input data

under construction

<!-- openAMUNDSEN simulates the processes for each model grid cell individually and is developed to use meteorological forcing from different sources. The standard application is to provide meteorological station data (point measurements). openAMUNDSEN provides a set of procedures suited specifically for topographically complex terrain to regionalise the point data to the model grid.

## Required meteorological input data

- air temperature
- precipitation
- global radiation
- wind speed
- relative humidity

## optional input data
- incoming longwave radiation


## Regionalisation of station data

### Regression-based approach including interpolation of the residuals

For each model time step,
- a regression analysis between observations and the associated station elevation is performed to derive an elevation-dependent trend function.
- the derived function is applied upon a digital elevation model to create a trend field for a given meteorological variable (e.g., temperature as a function of elevation).
- the residuals for all station locations are calculated by subtracting the calculated regression value for the station elevation from the actual measurement for the current time step.
- the residuals from the station locations (raster cells) are then interpolated to the grid using Inverse Distance Weighting (IDW) method.
- the interpolated residual field is finally added to the trend field, which results in elevation- and distance-dependent interpolated field ensuring a reproduction of the measured values at the station locations.





### Monthly altitudinal gradients

## Directly use gridded input

An option to directly read and use gridded meteorological data is currently in development.

## Choose and configure method in openAMUNDSEN -->

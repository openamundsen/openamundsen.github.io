---
layout: page
title: Description
has_children: true
nav_order: 3
permalink: /des/
---


# Model description

openAMUNDSEN is a modular snow and hydroclimatological modeling framework written in Python.

<p align="center">
  <img src="https://user-images.githubusercontent.com/17546246/115751189-3afe4c00-a399-11eb-8bfa-87d0a86c2119.gif" />
</p>

## Overview

openAMUNDSEN is a fully distributed model, designed primarily for resolving the mass and energy
balance of snow and ice covered surfaces in mountain regions.
Typically, it is applied in areas ranging from the point scale to the regional scale (i.e., up to
some hundreds to thousands of square kilometers), using a spatial resolution of 10–100 m and a
temporal resolution of 1–3 h, however its potential applications are very versatile.

Main features include:

* Spatial interpolation of scattered meteorological point measurements using a combined lapse
  rate – inverse distance weighting scheme
* Calculation of solar radiation taking into account terrain slope and orientation, hill shading
  and atmospheric transmission losses and gains due to scattering, absorption, and reflections
* Adjustment of precipitation using several correction functions for wind-induced undercatch and
  redistribution of snow using terrain-based parameterizations
* Simulation of the snow and ice mass and energy balance using either a multilayer scheme or a
  bulk-layering scheme using separate layers for new snow, old snow, firn and ice
* Modification of the meteorological variables for inside-canopy conditions in forested areas and
  calculation of forest snow processes (interception, sublimation and melt unload)
* Calculation of snowmelt using the surface energy balance or a temperature index/enhanced
  temperature index method
* Calculation of evapotranspiration for snow-free surfaces using the FAO Penman-Monteith method
* Usage of arbitrary timesteps (e.g. 10 minutes, daily) while resampling forcing data to the
  desired time resolution if necessary
* Flexible output of time series including arbitrary model variables for selected point locations in
  NetCDF or CSV format
* Flexible output of gridded model variables, either for specific dates or periodically (e.g., daily
  or monthly), optionally aggregated to averages or sums in NetCDF, GeoTIFF or ASCII Grid format
* Live view window for displaying the model state in real time

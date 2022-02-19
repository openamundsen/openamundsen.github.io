---
layout: default
title: Processing meteo data
parent: Description
nav_order: 2
permalink: /des/meteo
---

# Processing and regionalisation of meteorological input data

openAMUNDSEN simulates the processes for each model grid cell individually and is developed to use meteorological forcing from different sources. The standard application is to provide meteorological station data (point measurements). An option to directly read and use gridded meteorological data is currently in development.

    Required meteorological input data:
      - air temperature
      - precipitation
      - global radiation
      - wind speed
      - relative humidity

    Optional meteorological input data:
      - incoming longwave radiation

## Regionalisation of station data

openAMUNDSEN provides a set of procedures suited specifically for topographically complex terrain to regionalise the point data to the model grid.


### Regression-based approach including interpolation of the residuals (`regression`)

For each model time step,
- a regression analysis between observations and the associated station elevation is performed to derive an elevation-dependent trend function.
- the derived function is applied upon a digital elevation model to create a trend field for a given meteorological variable (e.g., temperature as a function of elevation).
- the residuals for all station locations are calculated by subtracting the calculated regression value for the station elevation from the actual measurement for the current time step.
- the residuals from the station locations (raster cells) are interpolated to the grid using Inverse Distance Weighting (IDW) method.
- the interpolated residual field is added to the trend field, which results in elevation- and distance-dependent interpolated field ensuring a reproduction of the measured values at the station locations.



### Monthly altitudinal gradients (`fixed`/`fractional`)

This method uses prescribed monthly altitudinal gradients either in absolute (`fixed`) or fractional (`fractional`) values. Fractional values are useful for precipitation gradients.


## Choose and configure method in openAMUNDSEN

The following example shows the options for choosing and configureing the regionalisation methods for each meteorological variable individually:

```yaml
meteo:
  # Spatial interpolation parameters
  interpolation:
    temperature:
      trend_method: fixed # use fixed monthly temperature lapse rates
      extrapolate: true
      lapse_rate: # (°C m-1)
        - -0.0026 # J
        - -0.0035 # F
        - -0.0047 # M
        - -0.0053 # A
        - -0.0052 # M
        - -0.0053 # J
        - -0.0049 # J
        - -0.0047 # A
        - -0.0042 # S
        - -0.0033 # O
        - -0.0035 # N
        - -0.0031 # D

    precipitation:
      trend_method: fractional # use fixed monthly fractional precipitation gradients
      extrapolate: true
      lapse_rate: # (m-1)
        - 0.00048 # J
        - 0.00046 # F
        - 0.00041 # M
        - 0.00033 # A
        - 0.00028 # M
        - 0.00025 # J
        - 0.00024 # J
        - 0.00025 # A
        - 0.00028 # S
        - 0.00033 # O
        - 0.00041 # N
        - 0.00046 # D

    humidity:
      trend_method: fixed # use fixed monthly dew point temperature lapse rates
      extrapolate: true
      lapse_rate:
        - -0.0044 # J
        - -0.0046 # F
        - -0.0049 # M
        - -0.0048 # A
        - -0.0046 # M
        - -0.0047 # J
        - -0.0043 # J
        - -0.0042 # A
        - -0.0045 # S
        - -0.0044 # O
        - -0.0047 # N
        - -0.0046 # D

    cloudiness:
      day_method: clear_sky_fraction # use the ratio of measured vs. potential shortwave radiation to calculate cloudiness
      night_method: humidity
                                # "constant" keep the last cloudiness value of the day during nighttime
    wind_speed:
      trend_method: regression
      extrapolate: false

  # Precipitation phase determination parameters
  precipitation_phase:
    method: wet_bulb_temp # use wet-bulb temperature for precipitation phase determination
    threshold_temp: 273.65 # threshold temperature (K) in which 50% of precipitation falls as snow
    temp_range: 1. # temperature range in which mixed precipitation can occur

  measurement_height:
    temperature: 2 # temperature measurement height (m)
    wind: 10 # wind measurement height (m)

  stability_correction: false # adjust turbulent fluxes for atmospheric stability
  stability_adjustment_parameter: 5. # adjustment parameter for atmospheric stability correction
```

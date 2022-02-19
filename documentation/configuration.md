---
layout: default
title: Configuration
parent: Documentation
nav_order: 3
permalink: /doc/configuration
---

# Configuration

The configuration of an openAMUNDSEN model run can either be read in from a
[YAML](https://en.wikipedia.org/wiki/YAML) file or be passed directly as a dictionary from within
Python.

Only few configuration parameters (`domain`, `start_date`, `end_date`, `resolution`, `timezone` and
the input data directories) are mandatory, for all other parameters default values are used
otherwise. The different options for the process modules are described at the respective sections in the [model description](/des/). A detailed documentation of all model parameters will be available soon (in the meantime, the available parameters and their default values can be looked up in [configschema.yml](https://github.com/openamundsen/openamundsen/blob/main/openamundsen/data/configschema.yml).

This is an example of a YAML configuration file:

```yaml
domain: rofental # name of the model domain (corresponding to the domain part of the spatial input data filenames)
start_date: "2020-10-01"
end_date: "2021-03-31"
resolution: 50  # spatial resolution (m)
timestep: H  # temporal resolution as a pandas-compatible frequency string (e.g., "H", "3H", "D")
crs: "epsg:32632"  # CRS of the input grids
timezone: 1  # timezone of the model domain (difference to UTC in h)
results_dir: results  # directory for storing the model outputs

# Input data configuration
input_data:
  grids:
    dir: input/grid  # location of the input grids (DEM, ROI etc.)
  meteo:
    dir: input/meteo  # location of the meteorological input data
    format: csv  # input format (CSV or NetCDF)
    crs: "epsg:4326"  # CRS of the station coordinates (when using CSV)

# Output data configuration
output_data:
  # Time series (point) outputs configuration
  timeseries:
    # List of points to be written
    points:
      - x: 642579 # x coordinate in the domain CRS
        y: 5193069 # y coordinate in the domain CRS
        name: testpoint # point name (optional)

    add_default_variables: true # write default point output variables
    variables: # optional additional output variables not written by default
      - var: surface.turbulent_exchange_coeff

  # Configuration for gridded outputs
  grids:
    format: netcdf # "netcdf", "ascii", "geotiff" or "memory"
    variables:
      - var: meteo.precip # internal variable name
        name: precip_month # NetCDF output variable name
        freq: M # write frequency (if not specified, write every timestep)
        agg: sum # aggregation function ("sum", "mean" or empty)
      - var: snow.melt
        freq: M
        agg: sum
      - var: snow.swe
        freq: D

meteo:
  # Spatial interpolation parameters
  interpolation:
    temperature:
      trend_method: fixed # use fixed monthly temperature lapse rates

    precipitation:
      trend_method: fractional # use fixed monthly fractional precipitation gradients
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

  # Precipitation phase determination parameters
  precipitation_phase:
    method: wet_bulb_temp # use wet-bulb temperature for precipitation phase determination
    threshold_temp: 273.65 # threshold temperature (K) in which 50% of precipitation falls as snow
    temp_range: 1. # temperature range in which mixed precipitation can occur

  # Parameters for adjusting precipitation for wind-induced undercatch and snow redistribution
  precipitation_correction:
    - method: wmo
      gauge: hellmann

snow:
  model: multilayer # snow scheme ("multilayer" or "cryolayers")

  # Number of layers and minimum thicknesses (m) when using the multilayer model
  min_thickness:
    - 0.1
    - 0.2
    - 0.4

  albedo:
    min: 0.55 # minimum snow albedo
    max: 0.85 # maximum snow albedo
    cold_snow_decay_timescale: 480 # albedo decay timescale for cold (T < 0 °C) snow (h)
    melting_snow_decay_timescale: 200 # albedo decay timescale for melting snow (h)
    refresh_snowfall: 0.5 # snowfall amount for resetting albedo to the maximum value (kg m-2 h-1)
```

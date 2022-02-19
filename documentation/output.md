---
layout: default
title: Output data
parent: Documentation
nav_order: 5
permalink: /doc/output
---

# Output data

The model output is configured in the configuration file. It generally consist of gridded data and/or time series of chosen model variables. The data format, variable names, output frequency, and aggregation functions are fully customizable. File formats are `netcdf`,`geotiff`,`ascii`, and `csv`.

## Gridded output data

The following part of an example configuration file demonstrates the options for gridded output.


```yaml
# Output data configuration
output_data:
  # Configuration for gridded outputs
  grids:
    format: ascii # output format (ascii, geotiff or netcdf)
    variables:
      # Temperature (monthly mean)
      - var: meteo.temp # internal variable name
        name: temp_month # NetCDF output variable name
        freq: M # write frequency (if not specified, write every timestep)
        agg: mean # aggregation function ("sum", "mean" or empty)

      # Precipitation (monthly sum)
      - var: meteo.precip # internal variable name
        name: precip_month # NetCDF output variable name
        freq: M # write frequency (if not specified, write every timestep)
        agg: sum  # aggregation function ("sum", "mean" or empty)

      # SWE (monthly mean)
      - var: snow.swe
        name: swe_month
        freq: M
        agg: mean

      # Snow depth (monthly mean)
      - var: snow.depth
        name: snowdepth_month
        freq: M
        agg: mean

      # SWE (certain dates)
      - var: snow.swe
        name: swe_dates
        dates:
        - 2020-04-11 12:00
        - 2020-06-02 12:00

      # Snow depth (certain dates)
      - var: snow.depth
        name: snowdepth_dates
        dates:
        - 2020-04-11 12:00
        - 2020-06-02 12:00

      # Snowmelt (monthly sum)
      - var: snow.melt
        name: snowmelt_month
        freq: M
        agg: sum

       # SWE (daily)
       - var: snow.swe
         freq: D

       - var: snow.depth
         freq: D

      # Evapotranspiration (monthly sum)
      - var: evapotranspiration.evapotranspiration
        freq: M
        agg: sum
```

## Time-series (point) output data

The following part of an example configuration file demonstrates the options for time series output. By default, time series are written at the locations of the meteorological input stations.

```yaml
# Output data configuration
output_data:
  # Time series (point) outputs configuration
  timeseries:
    format: csv # output format (csv or netcdf)
    points:
      - x: 638139
        y: 5181920
      - x: 642579
        y: 5193069
        name: testpoint
      - x: 637235
        y: 5192569

    add_default_variables: true
    variables:
      - var: evapotranspiration.evapotranspiration
```

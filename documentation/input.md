---
layout: default
title: Input data
parent: Documentation
nav_order: 2
permalink: /doc/input
---

# Input data

Required input data for running the model is at the least:

- a digital elevation model (DEM) as an [Arc/Info ASCII
  Grid](https://en.wikipedia.org/wiki/Esri_grid) (.asc) file in a projected coordinate reference
  system, with the same spatial resolution in which the model should be run,
- and time series of the meteorological variables air temperature, precipitation, relative humidity,
  global radiation and wind speed in NetCDF or CSV format.

## Spatial input data

Mandatory:
- `dem_{domain}_{resolution}.asc`: digital elevation model

Optional:
- `roi_{domain}_{resolution}.asc`: region of interest
- `lc_{domain}_{resolution}.asc`: land cover
- `soil_{domain}_{resolution}.asc`: soil data

All input grids have to be provided as [Arc/Info ASCII
  Grid files](https://en.wikipedia.org/wiki/Esri_grid) (.asc)in the exact same format, reference system, extent, and spatial resolution.


#### Digital elevation model (`dem_{domain}_{resolution}.asc`)

A DEM as an [Arc/Info ASCIIGrid](https://en.wikipedia.org/wiki/Esri_grid) (.asc) file in a projected coordinate reference system, with the same spatial resolution in which the model should be run has to be provided. The DEM file must be named `dem_{domain}_{resolution}.asc`, where `{domain}` refers to the (freely selectable) name of the respective model domain, and `{resolution}` to the spatial resolution in m.

#### Region of interest (`roi_{domain}_{resolution}.asc`)

Optionally, a region of interest (ROI) file can be additionally supplied defining a subset of the
DEM area in which the model should be applied. All model calculations are then only performed for the pixels which are marked as 1 in the ROI file. Accordingly, the ROI file (if available) is named `roi_{domain}_{resolution}.asc`.

#### Land cover (`lc_{domain}_{resolution}.asc`)

If either the [canopy](/des/canopy) or the [evapotranspiration module](/des/evapotranspiration) is enabled, land cover classes have to be provided as a grid input file named `lc_{domain}_{resolution}.asc`. The according parameters are defined in [land_cover_class_params.yml](https://github.com/openamundsen/openamundsen/blob/main/openamundsen/data/land_cover_class_params.yml).

#### Soil data (`soil_{domain}_{resolution}.asc`)

When using the [evapotranspiration module](/des/evapotranspiration) a grid containing soil texture classes has to be provided (`soil_{domain}_{resolution}.asc`). The soil texture classes are listed in [soiltexture.py](https://github.com/openamundsen/openamundsen/blob/main/openamundsen/modules/evapotranspiration/soiltexture.py). The according parameters are defined in [evapotranspiration.py](https://github.com/openamundsen/openamundsen/blob/main/openamundsen/modules/evapotranspiration/evapotranspiration.py).


## Meteorological input data

Meteorological input time series must be provided in the same or higher temporal resolution in which
the model should be run.
For each point location, a CSV or NetCDF file covering the entire time series must be provided.

### CSV input

When using CSV as input format, the input files should have one or more of the following columns
(columns for variables not available can be omitted):

* `date`: timestamp as a
  [`pd.to_datetime`](https://pandas.pydata.org/docs/reference/api/pandas.to_datetime.html)-compatible
  string (e.g. `YYYY-MM-DD HH:MM`)
* `temp`: air temperature (K)
* `precip`: precipitation sum (kg m<sup>-2</sup>)
* `rel_hum`: relative humidity (%)
* `sw_in`: global radiation (W m<sup>-2</sup>)
* `wind_speed`: wind speed (m s<sup>-1</sup>)

Additionally, a `stations.csv` file containing the metadata of the point locations must be provided
containing the following columns:

* `id`: station ID, corresponding to the filename of the respective data file
* `name`: station name
* `x`: longitude or projected x coordinate
* `y`: latitude or projected y coordinate
* `alt`: altitude (m)

### NetCDF input

When using NetCDF as input format, for each station a NetCDF file containing the meteorological time
series and the station metadata is read in (i.e., no additional metadata file is required in this
case).
The NetCDF files are expected to conform to the following schema (unavailable variables can be
omitted):

```
netcdf dummy {
dimensions:
        time = UNLIMITED ;
variables:
        double alt ;
                alt:_FillValue = NaN ;
                alt:standard_name = "surface_altitude" ;
                alt:units = "m" ;
        float hurs(time) ;
                hurs:_FillValue = NaNf ;
                hurs:standard_name = "relative_humidity" ;
                hurs:units = "%" ;
        double lat ;
                lat:_FillValue = NaN ;
                lat:standard_name = "latitude" ;
                lat:units = "degree_north" ;
        double lon ;
                lon:_FillValue = NaN ;
                lon:standard_name = "longitude" ;
                lon:units = "degree_east" ;
        float pr(time) ;
                pr:_FillValue = NaNf ;
                pr:standard_name = "precipitation_flux" ;
                pr:units = "kg m-2 s-1" ;
        float rsds(time) ;
                rsds:_FillValue = NaNf ;
                rsds:standard_name = "surface_downwelling_shortwave_flux_in_air" ;
                rsds:units = "W m-2" ;
        float tas(time) ;
                tas:_FillValue = NaNf ;
                tas:standard_name = "air_temperature" ;
                tas:units = "K" ;
        int64 time(time) ;
                time:standard_name = "time" ;
                time:units = "hours since 1999-01-01 00:00:00" ;
                time:calendar = "proleptic_gregorian" ;
        float wss(time) ;
                wss:_FillValue = NaNf ;
                wss:standard_name = "wind_speed" ;
                wss:units = "m s-1" ;

// global attributes:
                :Conventions = "CF-1.6" ;
                :station_name = "dummy" ;
}
```

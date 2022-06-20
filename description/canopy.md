---
layout: default
title: Inside canopy
parent: Description
nav_order: 6
permalink: /des/canopy
---


# Simulating inside-canopy micrometeorology and snow processes (interception, sublimation, melt unload)

The processes affecting a snow cover beneath a forest canopy are distinct from those in the open: on one hand, the meteorological conditions relevant for the energy transfer at the snow surface beneath the canopy are different, and on the other hand, a certain amount of precipitation is retained in the interception storage of stems, branches and needles. Snow that is intercepted in the canopy can melt, fall down, or sublimate into the air masses above the canopy. This latter process leads to a reduction of precipitation accumulated and stored in the ground snowpack.

To simulate these processes openAMUNDSEN extracts vegetation- and season-dependent values of leaf areas index (LAI) from the given land cover which is provided as a grid input file (see [Spatial Input data](/doc/input)). The according land cover class parameters are defined in [land_cover_class_params.yml](https://github.com/openamundsen/openamundsen/blob/main/openamundsen/data/land_cover_class_params.yml).

## Inside-canopy micrometeorology

Forest canopies generally lead to a reduction of global radiation, precipitation and wind speed, whereas humidity and long-wave radiation are increased and the diurnal temperature cycle is attenuated. In openAMUNDSEN, the micrometeorological conditions for the ground beneath a forest canopy are derived from the interpolated measurements (if all stations are located in the open) by applying a set of modifications for solar and thermal radiation, temperature, humidity and wind speed. The modifications are based on the effective Leaf Area Index (LAI) of the forest.

## Snow-forest interaction

In openAMUNDSEN, the processes of snow-forest interaction of interception, i.e. sublimation, unloading by melt, and exceeding the canopy snow–holding capacity are calculated as a function of LAI. Liquid precipitation is assumed to fall through the canopy and is added to the ground snow cover.

## Choose and configure method in openAMUNDSEN

```yaml
canopy:
    enabled: true
    extinction_coefficient: 0.71
    temperature_scaling_coefficient: 0.8
    canopy_flow_index_coefficient: 0.9
    spherical_ice_particle_radius: 500.e-6
    kinematic_air_viscosity: 1.3e-5
    max_interception_storage_coefficient: 4.4
    exposure_coefficient_coefficient: 0.010
    degree_day_factor: 5.
```

## References
- Strasser, U., Warscher, M., and Liston, G. E. (2011): Modeling Snow-Canopy Processes on an Idealized Mountain. Journal of Hydrometeorology, 12(4), 663–677, [https://doi.org/10.1175/2011JHM1344.1](https://doi.org/10.1175/2011JHM1344.1).

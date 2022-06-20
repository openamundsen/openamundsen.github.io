---
layout: default
title: Evapotranspiration
parent: Description
nav_order: 8
permalink: /des/evapotranspiration
---

# Calculating evapotranspiration using the FAO Penman-Monteith method

Evapotranspiration from snow-free surfaces is simulated using the FAO Penman-Monteith approach (Allen et al. 1998).


## Choose and configure method in openAMUNDSEN

```yaml
evapotranspiration:
    enabled: true
    min_crop_coefficient: 0.175
    grass_albedo: 0.23
    grass_emissivity: 0.985
    sealed_albedo: 0.4
    sealed_emissivity: 0.92
    mean_wind_speed: 2.
    mean_min_humidity: 45.
    surface_soil_layer_evaporation_depth: 0.125
```

## References
- Allen, R. G., Pereira, L. S., Raes, D., and Smith, M. (1998): Crop evapotranspiration – Guidelines for computing crop water requirements, Tech. rep., [https://www.fao.org/3/x0490e/x0490e00.htm](https://www.fao.org/3/x0490e/x0490e00.htm).

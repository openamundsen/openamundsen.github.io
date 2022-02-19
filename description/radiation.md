---
layout: default
title: Radiation modeling
parent: Description
nav_order: 3
permalink: /des/radiation
---

# Short- and long-wave radiative flux modeling

## Incoming short-wave radiation
Incoming short-wave radiation strongly varies in time and space depending on terrain position and atmospheric state. To regionalise point measurements, openAMUNDSEN calculates potential global radiation for each grid cell based on position of the sun, orographic shadows, local aspect and slope, atmospheric composition (aerosols, water vapour content), multiple reflections between snow and clouds as well as from snow covered neighbouring slopes. Calculated potential global radiation is then compared to observed global radiation to determine cloud coverage. In the final step, cloud coverage is regionalised using the methods described in [Processing meteo data](/des/meteo), and actual incoming short-wave radiation is calculated from potential global radiation and cloud coverage for each model grid cell.

## Outgoing / reflected short-wave radiation
Reflected short wave radiation depends on surface albedo, i.e. the ability to reflect incoming short-wave radiation. Snow albedo varies with snow characteristics like grain size, density and snow impurity. In openAMUNDSEN, it is modelled using an ageing-curve approach.

## Incoming long-wave radiation
Incoming long-wave radiation from the atmosphere is a function of atmospheric composition and temperature and is determined using the the Stefan-Boltzmann law. Atmospheric emissivity thereby depends on water vapour content in clear sky conditions and cloud cover in overcast situations. Additionally, openAMUNDSEN accounts for long-wave radiation from the neighbouring slopes.

## Outgoing / emitted long-wave radiation
Outgoing long-wave radiation is calculated following the Stephan-Boltzmann law with the emissivity of snow and modelled snow surface temperature.

## Choose and configure method in openAMUNDSEN

The radiation model is a mandatory module and is therefore enabled by default. Several model parameters can be adjusted.

```yaml
meteo:
  # Radiation parameters
  radiation:
    snow_emissivity: 0.99
    cloud_emissivity: 0.976
    rock_emission_factor: 0.01
    ozone_layer_thickness: 0.0035
    atmospheric_visibility: 25000.
    single_scattering_albedo: 0.9
    clear_sky_albedo: 0.0685
    num_shadow_sweeps: 1
```



## References

- Corripio, J. G. (2003). Vectorial algebra algorithms for calculating	terrain parameters from DEMs and solar radiation modelling in mountainous terrain. International Journal of Geographical Information Science, 17(1), 1–23. https://doi.org/10.1080/13658810210157796

- Essery, R., Morin, S., Lejeune, Y., & B Ménard, C. (2013). A comparison of 1701 snow models using observations from an alpine site. Advances in Water Resources, 55, 131–148. https://doi.org/10.1016/j.advwatres.2012.07.013

- Greuell, W., Knap, W. H., & Smeets, P. C. (1997). Elevational changes in meteorological variables along a midlatitude glacier during summer. Journal of Geophysical Research, 102(D22), 25941–25954.	https://doi.org/10.1029/97JD02083

- Hanzer, F., Helfricht, K., Marke, T., & Strasser, U. (2016). Multilevel spatiotemporal validation of snow/ice mass balance and runoff modeling in glacierized catchments. The Cryosphere, 10(4), 1859–1881. https://doi.org/10.5194/tc-10-1859-2016

- Liston, G. E., & Elder, K. (2006). A Meteorological Distribution System for High-Resolution Terrestrial Modeling (MicroMet). Journal of Hydrometeorology, 7(2), 217–234. https://doi.org/10.1175/JHM486.1

- Prata, A. J. (1996). A new long-wave formula for estimating downward clear-sky radiation at the surface. Quarterly Journal of the Royal Meteorological Society, 122(533), 1127–1151. doi:10.1002/qj.49712253306

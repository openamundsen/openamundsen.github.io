---
layout: default
title: Snow and energy balance
parent: Description
nav_order: 5
permalink: /des/energy
---

# Calculating snow processes and the energy balance of snow

Generally, the energy balance of a snowpack can be expressed as:

		Q + H + E + P + G = C + M

		Q = net radiation
		H = sensible heat flux
		E = latent heat flux
		P = advective heat flux caused by precipitation
		G = ground heat flux
		C = energy transferred to temperature changes within the snowpack
		M = energy transferred to snow melt


## Snow layering schemes and energy balance

Two different layering schemes ("Cryolayers" / "Multilayer") are implemented in the model. The energy balance calculation depends on the selected layering scheme.

### Snow layering scheme "Cryolayers"

"Cryolayers" is a bulk-layering scheme using separate layers for new snow, old snow, firn and ice. When using this scheme, the snowpack is taken as one layer to solve its energy balance. If air temperature rises above 0° C the model assumes that melting processes are possible and checks for a positive surface energy balance. If the surface energy balance is positive, melting processes occur where the melt amount is determined by the simulated available excess energy. If the air temperature is below 0°C, an iterative procedure to compute the snow surface temperature needed for closing the energy balance is applied. In this procedure, the snow surface temperature is altered until the residual energy balance passes zero.

### Snow layering scheme "Multilayer"

"Multilayer" is a scheme that divides the snowpack in distinct layers to calculate heat fluxes within the snow pack (Essery 2015). To solve the energy balance within this scheme, in a first step, melt is assumed to be zero for the surface temperature change of every timestep. If the energy balance results in a surface temperature above 0 °C, snow is melting. The temperature increment has to be recalculated assuming that all of the snow melts. If this results in a surface temperature below 0 °C, snow melts only partially during the timestep (Essery 2015).

## Snow albedo

Snow albedo strongly varies in space and time depending on snow characteristics like grain size, density and snow impurity. In openAMUNDSEN, it is modelled using two different approaches for albedo ageing and refreshing.

### Albedo ageing

Both approaches use an exponential ageing curve which is linked to either air temperature (Hanzer et al., 2016) or snow surface temperature (Essery et al., 2013) and is adjusted to melting or cold snow conditions. Melting conditions are assumed if temperature (air or snow surface) is greater or equals 0° C. Cold snow conditions are asssumed for temperatures below 0° C.

### Albedo refreshing
Snowfall leads to a "refreshing" of the snow surface and an abruptly increasing albedo. The method by Hanzer et al. (2016) uses a threshold of solid precipitation per timestep (default: 0.5 kg/m²) to reset the value of snow albedo to its predefined maximum. Essery et al. (2013) introduce a method, where snow albedo is continuously increasing towards the predefined maximum.


## Fresh snow density and snow compaction

Fresh snow density is calculated using wet bulb temperature according to Anderson (1976). If the temperature is below -15° C, fresh snow density is assumed to be 50 kg/m³. If the temperature is higher than -15° C an exponential function is applied (see Koivusalo et al. 2001).
Snow compaction is calculated using one of the approaches described in the following.

### Method proposed by Anderson (1976)

This method calculates compaction for each snow layer depending on overlying snowmasses and by determining equilibrium metamorphism. Details about the approach and the implemented parameters are described in Koivusalo et al. (2001).

### Empirical approach (Essery 2015)

The empirical approach follows the method described in Essery (2015). Assumptions are made for maximum density of snow for below 0° C and for melting conditions (default values: 300 kg/m³ for cold snow and 500 kg/m³ for melting snow). The timescale for compaction is an adjustable parameter (default value: 200 h). The increase of density for every timestep is calculated as a fraction of the compaction timescale multiplied with the difference of maximum density and the density of the last timestep. This method can only be applied when using the "Multilayer" snow layering scheme.

## Liquid water content

The model simulates liquid water content (LWC) and potential refreezing within the snowpack. Following either Braun (1984) or Essery (2015), the parameter maximum LWC is defined as mass fraction of SWE or as a fraction of pore volume that can be filled with liquid water (volumetric water content). If the maximum LWC is reached during snowmelt, runoff at the bottom of a snow layer occurs and drains to the snow layer underneath, or - for the bottom snow layer - into the upper soil layer respectively.


## Choose and configure methods in openAMUNDSEN

### "Cryolayers" scheme

```yaml
# Snow parameters
snow:
  model: cryolayers # snow scheme (multilayer or cryolayers)
  thermal_conductivity: 0.24 # snow thermal conductivity (W m-1 K-1)
  roughness_length: 0.01 # roughness length of snow-covered ground (m)
  measurement_height_adjustment: false # adjust the temperature measurement height for snow depth
  snow_cover_fraction_depth_scale: 1.e-6 # snow cover fraction depth scale (m)
  cryolayers:
    cold_holding_capacity: 0.05 # cold holding capacity (as a fraction of the layer SWE) and refreezing factor for the cold content approach by Braun (1984)
    refreezing_factor: 1. # fraction of available energy that is used for building up cold content and refreezing liquid water
    surface_heat_flux: -2. # surface heat flux for snow-covered conditions (W m-2)
    transition:
      old_snow: 200. # new snow -> old snow transition (density, kg m-3)
      firn: 10 # old snow -> firn transition (calendar month)
      ice: 900. # firn -> ice transition (density, kg m-3)
```  

### "Multilayer" scheme

```yaml
# Snow parameters
snow:
  model: multilayer # snow scheme (multilayer or cryolayers)
  thermal_conductivity: 0.24 # snow thermal conductivity (W m-1 K-1)
  roughness_length: 0.01 # roughness length of snow-covered ground (m)
  measurement_height_adjustment: false # adjust the temperature measurement height for snow depth
  snow_cover_fraction_depth_scale: 1.e-6 # snow cover fraction depth scale (m)
```  


### General snow and energy-balance related model parameters

```yaml
# Snow parameters
snow:
  # Albedo parameters
  albedo:
    method: snow_age
    min: 0.55 # minimum snow albedo
    max: 0.85 # maximum snow albedo
    firn: 0.4 # firn albedo (constant)
    ice: 0.2 # ice albedo (constant)
    cold_snow_decay_timescale: 480 # albedo decay timescale for cold (T < 0 °C) snow (h)
    melting_snow_decay_timescale: 200 # albedo decay timescale for melting snow (h)
    decay_timescale_determination_temperature: surface # use surface temperature to distinguish between cold and melting snow
    refresh_snowfall: 0.5 # snowfall amount for resetting albedo to the maximum value (kg m-2 h-1)
    refresh_method: binary # binary or continuous

  # Snow compaction parameters
  compaction:
    method: anderson # anderson or empirical

    # Parameters for method "empirical"
    timescale: 200 # snow compaction timescale (h)
    max_cold_density: 300 # maximum density for cold (T < 0 °C) snow (kg m-3)
    max_melting_density: 500 # maximum density for melting snow (kg m-3)

  # Liquid water content parameters
  liquid_water_content:
    method: pore_volume_fraction # pore_volume_fraction or mass_fraction
    max: 0.03 # maximum liquid water content as a fraction of the total pore volume or mass

  # Melt parameters
  melt:
    method: energy_balance # melt method (energy_balance, temperature_index or enhanced_temperature_index)
    threshold_temp: 273.15 # threshold temperature for the temperature index methods (K)
    degree_day_factor: 1.2 # degree day factor for the temperature index methods (kg m-2 d-1 K-1)
    albedo_factor: 0.1 # albedo factor for the enhanced temperature index method (m2 kg m-2 W-1 d-1)

```

## References

- Anderson, E. A. (1976): A point energy and mass balance model of a snow cover (NOAA Technical Report NWS 19, pp. 1–172). NOAA. https://repository.library.noaa.gov/view/noaa/6392

- Braun, L. N. (1984): Simulation of snowmelt-runoff in lowland and lower alpine regions of Switzerland. Dissertation. Zürich. https://doi.org/10.3929/ethz-a-000334295

- Essery, R., Morin, S., Lejeune, Y. and Ménard C. B. (2013): A comparison of 1701 snow models using observations from an alpine site. Advances in Water Resources 55:131-148.

- Essery, R. (2015): A factorial snowpack model (FSM 1.0). Geoscientific Model Development, 8(12), 3867–3876, [https://doi.org/10.5194/gmd-8-3867-2015](https://doi.org/10.5194/gmd-8-3867-2015).

- Hanzer, F., Helfricht, K., Marke, T. and Strasser, U. (2016): Multi-level spatiotemporal validation of snow/ice mass balance and runoff modeling in glacierized catchments. The Cryosphere, 10, 1859-1881, https://doi.org/10.5194/tc-10-1859-2016.

- Koivusalo, H., Heikinheimo, M., & Karvonen, T. (2001). Test of a simple two-layer parameterisation to simulate the energy balance and temperature of a snow pack. Theoretical and Applied Climatology, 70(1–4), 65–79. https://doi.org/10.1007/s007040170006

- Strasser, U. (2008): Modelling of the mountain snow cover in the Berchtesgaden National Park, Tech. Rep. 55, Berchtesgaden National Park, Berchtesgaden.

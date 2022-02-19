---
layout: default
title: Energy and mass balance
parent: Description
nav_order: 5
permalink: /des/energy
---

# Calculating the energy and mass balance of snow and ice

Generally, the energy balance of a snowpack can be expressed as:

		Q + H + E + P + G = C + M

		Q = net radiation
		H = sensible heat flux
		E = latent heat flux
		P = advective heat flux caused by precipitation
		G = ground heat flux
		C = energy transferred to temperature changes within the snowpack
		M = energy transferred to snow melt


## Energy balance in openAMUNDSEN

Two different layering schemes ("Cryolayers" / "Multilayer") are implemented in the model. The energy balance calculation depends on the selected layering scheme.

### Snow layering scheme "Cryolayers"

 "Cryolayers" is a bulk-layering scheme using separate layers for new snow, old snow, firn and ice. When using this scheme, the snowpack is taken as one layer to solve its energy balance. If air temperature rises above 0° C the model assumes that melting processes are possible and checks for a positive surface energy balance. If the surface energy balance is positive, melting processes occur where the melt amount is determined by the simulated available excess energy. If the air temperature is below 0°C, an iterative procedure to compute the snow surface temperature needed for closing the energy balance is applied. In this procedure, the snow surface temperature is altered until the residual energy balance passes zero.

### Snow layering scheme "Multilayer"

"Multilayer" is a scheme that divides the snowpack in distinct layers to calculate heat fluxes within the snow pack (Essery 2015). To solve the energy balance within this scheme, in a first step, melt is assumed to be 0 for the surface temperature change of every timestep. If the energy balance results in a surface temperature above 0° C, snow is melting. The temperature increment has to be recalculated assuming that all of the snow melts. If this results in a surface temperature below 0°C, snow melts only partially during the timestep (Essery 2015).


## Choose and configure method in openAMUNDSEN

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

- Essery, R. (2015). A factorial snowpack model (FSM 1.0). Geoscientific Model Development, 8(12), 3867–3876. https://doi.org/10.5194/gmd-8-3867-2015

- Strasser, U. (2008). Modelling of the mountain snow cover in the Berchtesgaden National Park, Tech. Rep. 55, Berchtesgaden National Park, Berchtesgaden.

---
layout: default
title: Model structure
parent: Description
nav_order: 1
permalink: /des/structure
---

# General model structure

openAMUNDSEN is a fully distributed model, designed primarily for resolving the mass and energy balance of snow and ice covered surfaces in mountain regions. Its modular architecture allows for creating simulations of different complexity and using different methods.

The general model structure for a simulation is:

    - Model initialization (once)
      - Read input files
      - Analyze terrain
    - Model run (each time step)
      - Interpolate meteo variables
      - Calculate derived meteo variables
      - Calculate irradiance
      - Calculate snow-vegetation interaction
      - Calculate snow processes
      - Calculate evapotranspiration
      - Calculate runoff
    - Write results


<p align="center">
    <img src="/description/model_structure.png" />
</p>

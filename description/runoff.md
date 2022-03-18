---
layout: default
title: Runoff
parent: Description
nav_order: 9
permalink: /des/runoff
---

# Simulating catchment runoff and streamflow

## Distributed catchment runoff

Pixel runoff in each time step is calculated in the model by calculating and solving the water balance.

## Runoff concentration

For runoff concentration, a linear reservoir cascade approach (Nash 1960) following Asztalos et al. (2007) is used.

Runoff originating from rainfall and from meltwater released from glaciers and the snowpack is thereby cumulated in each time step and catchment and routed through four parallel linear reservoir cascades for unglacierized areas, bare ice areas, firn-covered areas on glaciers, and snow-covered areas on glaciers. A constant fraction of the inflow into the snow, firn, and ice reservoirs, as well as a fraction of the inflow into the unglacierized reservoir, is diverted into an additional soil reservoir. The parameters of the linear reservoir model are determined by calibration separately for each catchment. (Hanzer et al. 2016)

The runoff concentration module is coupled to openAMUNDSEN as an external python routine which will be published here soon.

## References

- Asztalos, J., Kirnbauer, R., Escher-Vetter, H., and Braun, L. (2007): A distributed energy balance snowmelt model as a component of a flood forecasting system for the Inn river, in: Alpine Snow Workshop, Munich, 9–17.

- Hanzer, F., Helfricht, K., Marke, T., and Strasser, U. (2016): Multilevel spatiotemporal validation of snow/ice mass balance and runoff modeling in glacierized catchments, The Cryosphere, 10, 1859–1881, [https://doi.org/10.5194/tc-10-1859-2016](https://doi.org/10.5194/tc-10-1859-2016).

- Nash, J. E. (1960): A unit hydrograph study, with particular reference to British catchments, Proc. Inst. Civ. Eng., 17, 249–282, [https://doi.org/10.1680/iicep.1960.11649](https://doi.org/10.1680/iicep.1960.11649).

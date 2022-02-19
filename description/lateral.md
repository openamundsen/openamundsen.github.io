---
layout: default
title: Lateral snow redistribution
parent: Description
nav_order: 7
permalink: /des/lateral
---

# Simulating of lateral snow redistribution processes

## Wind-driven snow redistribution

A terrain-based parameterization to account for wind-driven snow redistribution is implemented in openAMUNDSEN. It is a static approach based on topographic openness that applies a redistribution factor on the interpolated solid precipitation field. Details are described in Hanzer et al. (2016).

## Choose and configure method in openAMUNDSEN

```yaml
precipitation_correction:
  - method: srf
```

<!-- ## Gravitation-driven snow redistribution -->


## References

- Hanzer, F., Helfricht, K., Marke, T., and Strasser, U.: Multilevel spatiotemporal validation of snow/ice mass balance and runoff modeling in glacierized catchments, The Cryosphere, 10, 1859–1881, https://doi.org/10.5194/tc-10-1859-2016, 2016.

- Warscher, M., Strasser, U., Kraller, G., Marke, T., Franz, H., and
Kunstmann, H.: Performance of complex snow cover descriptions in a distributed hydrological model system: A case study for the high Alpine terrain of the Berchtesgaden Alps, Water Resour. Res., 49, 2619–2637, 2013.

- Yokoyama, R., Shirasawa, M., and Pike, R. J.: Visualizing topography by openness: a new application of image processing to digital elevation models, Photogram. Eng. Remote Sens., 68, 257–266, 2002.

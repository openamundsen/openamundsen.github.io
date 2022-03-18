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
```

## References
- Allen, R. G., Pereira, L. S., Raes, D., and Smith, M. (1998): Crop evapotranspiration – Guidelines for computing crop water requirements, Tech. rep., [https://www.fao.org/3/x0490e/x0490e00.htm](https://www.fao.org/3/x0490e/x0490e00.htm).

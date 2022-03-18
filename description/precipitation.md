---
layout: default
title: Precipitation correction
parent: Description
nav_order: 4
permalink: /des/precipitation
---

# Correction of precipitation undercatch

Precipitation measurements are vital input for every hydrological model. Particularly measuring solid precipitation in complex alpine terrain is prone to large errors which typically results in an undercatch of precipitation. High wind speeds can cause an undercatch of snowfall up to 50 % (Kochendorfer et al. 2017) when using typical precipitation gauges / pluviometers.

## Approaches implemented in the model
Three different approaches are implemented in openAMUNDSEN to correct for the undercatch of solid precipitation:

- Constant snow correction factor
- WMO approach (Goodison et al. 1998)
- Method proposed by Kochendorfer et al. 2017

### Constant correction factor for snowfall
A basic method to correct for undercatch is a simple, linear scaling of precipitation. The fracture of snowfall (i.e. solid precipitation) is multiplied by a defined, constant factor (e.g. 1.25 for 25% of added solid precipitation).

### WMO approach (Goodison et al. 1998)

The WMO approach uses different transfer functions for different type of gauges to scale solid precipitation using measured meteorological conditions (i.e. temperature and/or wind speed).
This approach provides functions for following gauge types/setups:

    - nipher
    - tretyakov
    - us_shielded
    - us_unshielded
    - hellmann


### Method proposed by Kochendorfer et al. 2017

The method introduced by Kochendorfer et al. estimates undercatch regardless of precipitation phase. This method also uses transfer functions for different measuring setups and takes wind speed and temperature into account. In contrast to the WMO method, the transfer functions were derived from different windshields used for the same gauge (3-wire T200B, Geonor Inc., Oslo, Norway), as well as from a unshielded gauge.

Supported measuring setups are:

    - unshielded
    - single alter
    - double alter
    - small DFIR
    - Belfort double-Alter

## Choose and configure method in openAMUNDSEN

- Constant correction factor for snowfall

```yaml
meteo:
# Parameters for adjusting precipitation for wind-induced undercatch and snow redistribution
  precipitation_correction:
    - method: constant_scf
      scf: 1.25
```  

- Method proposed by Kochendorfer et al. 2017

```yaml
meteo:
# Parameters for adjusting precipitation for wind-induced undercatch and snow redistribution
  precipitation_correction:
    - method: kochendorfer # use the Kochendorfer et al. (2017) transfer functions
      gauge: us_un # gauge-specific transfer function to use according to Kochendorfer et al. (2017, Table 3)
```  

- WMO approach (Goodison et al. 1998)

```yaml
meteo:
# Parameters for adjusting precipitation for wind-induced undercatch and snow redistribution
  precipitation_correction:
    - method: wmo
      gauge: hellmann
```  


## References

- Goodison, B. E., Louie, P., and Yang, D. (1998): WMO solid precipitation measurement intercomparison (World Meteorological Organization, p. 212). World Meteorological Organization, [https://library.wmo.int/doc_num.php?explnum_id=9694](https://library.wmo.int/doc_num.php?explnum_id=9694).

- Kochendorfer, J., Rasmussen, R., Wolff, M., Baker, B., Hall, M. E., Meyers, T., Landolt, S., Jachcik, A., Isaksen, K., Brækkan, R., and Leeper, R. (2017): The quantification and correction of wind-induced precipitation measurement errors. Hydrology and Earth System Sciences, 21(4), 1973–1989, [https://doi.org/10.5194/hess-21-1973-2017](https://doi.org/10.5194/hess-21-1973-2017).

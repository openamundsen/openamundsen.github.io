---
layout: default
title: Radiation modeling
parent: Description
nav_order: 3
permalink: /des/meteo
---

# Short- and longwave radiative flux modeling

under construction


<!-- Short- and longwave radiative flux modeling

The radiation balance of snow is the factor, that contributes the most to the energy balance of the snow pack and consists of following terms:

	- sw_in:	incoming short wave radiation
	- sw_out:	reflected short wave radiation
	- lw_in:	incoming long wave radiation
	- lw_out	emmited long wave radiation


	Qradiation = SW_in - SW_out + LW_in - LW_out

		- evtl. klassische Abbildung mit Zusammensetzung der Strahlung?

SW_in
The incoming short wave radiation of a point strongly varies in space and time and therefore is challenging to interpolate. openAMUNDSEN calculates a potential radiation for each grid cell, taking the position of the sun, orographic shadows, local aspect and slope, the atmospheric composition (aerosols, water content...) and reflections between snow and clouds as well as reflections from snow covered neighbouring slopes into account. In order to assume cloud cover, the potential radiation is compared to observed radiation measurements. Cloud cover is then interpolated using the regression based approach.


		- hier evtl. Video von Uli -

SW_out
The reflected short wave radiation depends on the snow surface albedo, i.e. the ability to reflect incoming short wave radiation. The albedo varies with snow characteristics like grain size, density and snow impurity. In openAMUNDSEN snow albedo is modelled along a aging curve approach.

(	a = amin + aadd *e-kn  

	amin = 	minimum snow albedo
	aadd = 	additive Albedo
	k =	recession coefficient
	n = 	number of days since last significant snowfall (>0.5mm/h)
)

LW_in
Incoming longwave radiation is calculated as a function of temperature dependent on the Stefan-Boltzmann law. openAMUNDSEN accounts for longwave radiation from the atmosphere as well as from neighboring slopes. The atmospheric emessivity thereby depends on water vapour content in clear sky conditions and cloud cover in overcast conditions.

LW_out
Outgoing longwave radiation is calculated following the Stephan Boltzmann law once again, using snow emissivity (0.99) and snow surface tepmerature to solve the equation.



	References

	Bernard Bourges. Improvement in solar declination computation. Solar
       	Energy, 1985, 35(4), pp.367-369.

	Corripio, J. G. (2002). Modelling the energy balance of high
       	altitude glacierised basins in the Central Andes. PhD thesis, University of
       	Edinburgh.

	Corripio, J. G. (2003). Vectorial algebra algorithms for calculating
       	terrain parameters from DEMs and solar radiation modelling in mountainous
       	terrain. International Journal of Geographical Information Science, 17(1),
      	1–23. https://doi.org/10.1080/13658810210157796

	J. W. Spencer, "Fourier series representation of the position of the
       	sun" in Search 2 (5), p. 172 (1971)

	Snow Hydrology: Summary Report of the Snow Investigations. Published
       	by the North Pacific Division, Corps of Engineers, U.S. Army, Portland,
       	Oregon, 1956.  437 pages, 70 pages of plates, maps and figs., 27 cm.
       	https://doi.org/10.3189/S0022143000024503

	Hanzer, F., Helfricht, K., Marke, T., & Strasser, U. (2016).
       	Multilevel spatiotemporal validation of snow/ice mass balance and runoff
       	modeling in glacierized catchments. The Cryosphere, 10(4), 1859–1881.
       	https://doi.org/10.5194/tc-10-1859-2016

	Essery, R., Morin, S., Lejeune, Y., & B Ménard, C. (2013). A
       	comparison of 1701 snow models using observations from an alpine site.
       	Advances in Water Resources, 55, 131–148.
       	https://doi.org/10.1016/j.advwatres.2012.07.013

	Dutra, E., Balsamo, G., Viterbo, P., Miranda, P., Beljaars, A.,
       	Schär, C., & Elder, K. (2009). New snow scheme in HTESSEL: description and
       	offline validation. ECMWF. https://doi.org/10.21957/98x9mrv1y

	Prata, A. J. (1996). A new long-wave formula for estimating downward
       	clear-sky radiation at the surface. Quarterly Journal of the Royal
       	Meteorological Society, 122(533), 1127–1151. doi:10.1002/qj.49712253306

	Liston, G. E., & Elder, K. (2006). A Meteorological Distribution
      	System for High-Resolution Terrestrial Modeling (MicroMet). Journal of
       	Hydrometeorology, 7(2), 217–234. https://doi.org/10.1175/JHM486.1

	Greuell, W., Knap, W. H., & Smeets, P. C. (1997). Elevational
       	changes in meteorological variables along a midlatitude glacier during
       	summer. Journal of Geophysical Research, 102(D22), 25941–25954.
       	https://doi.org/10.1029/97JD02083 -->

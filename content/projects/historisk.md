+++
title = 'Historisk'
date = 2023-09-01
draft = false
+++

FireSight provides tailored geospatial analysis of bushfire conditions. This
requires the development of custom geospatial software to help perform the
analysis of environmental conditions ranging across historical weather, future
forecasts and fire spread analysis. Given my previous experience with Python,
and the toolset already available in QGIS, creating a plugin was the logical
choice.

![](/projects/lfmc.png)

The tasks that the tools can perform include:
* Historical analysis for fire danger indexes to determine annual exceedance thresholds
* Discovery of historical extreme weather dates for chosen areas
* Weather extraction to formats suitable for fire simulation
* Analysing fire simulation output for dangerous ignitions
* Scanning historical weather for suitable burn conditions to determine the
  suitability of prescribed conditions

**Tech Stack**
* Python 3.8
* QGIS 3.26
* GDALXarray
* Pandas
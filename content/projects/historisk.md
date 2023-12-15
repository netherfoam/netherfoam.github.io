+++
title = 'Historisk'
date = 2023-09-01
draft = false
+++

## Background

FireSight provides tailored geospatial analysis of bushfire conditions. This
requires the development of custom geospatial software to help perform the
analysis of environmental conditions ranging across historical weather, future
forecasts and fire spread analysis.

![](/projects/lfmc.png)

## Historisk QGIS Plugin

The Historisk QGIS plugin was created to provide tools inside QGIS which allow
FireSight to perform a number of tasks, including:

### Historical Fire Danger Index Analysis
Given the historical Forest Fire Danger Index (`FFDI`) for the past 30 years of
data, provided by the Bureau of Meteorology, this tool builds a raster of an
annual exceedance threshold value across the years. This lets FireSight determine
what historical extreme fire weather days to use for customer simulations.

### Discovering Historical Extreme Weather Days
Given a high FFDI value, this algorithm determines which days exceed that value
by the smallest amount. These are the days that are chosen for simulation.

### Extracting Historical Weather for Simulation
Weather is provided by the Bureau of Meteorology in a given format. The relevant
days must be extracted and converted into NetCDF format, while remaining
compatible with the simulation software which doesn't support the modern NetCDF
schema.

### Dangerous Ignitions
Given the output of simulations, determine which ignitions caused the most area
to be burnt, and create an impact frequency raster of those ignitions. This
shows where the worst fires are starting and where they're burning.

### Impact Ignitions
Given a bounding area of interest, a high density town for example, determine
where ignitions are that intersect with the town and cause a high probability
of house loss.

### Historical Burn Condition Analysis
Customers will have areas that are burned at intervals to reduce the risk of
bushfire. They have prescribed ranges for weather conditions, usually a
combination of relative humidity, temperature, wind direction and speed. This
tool takes the parameters and filters days from historical weather at a location
to determine the frequency that suitable days occur, and the parameters that are
most commonly excluding days from being suitable. This made use of a dynamic
decision tree to speed performance, tweaking the order of checks to increase the
speed of the algorithm when scanning a significant quantity of rasters.

##

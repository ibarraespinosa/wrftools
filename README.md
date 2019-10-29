---
title: "wrftools"
author: "Sergio Ibarra-Espinosa"
date: "October 29, 2019"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## wrftools

This package does 3 things

1. help you to define domains
2. extract data as points of spatial features and bricks
3. returns st_bbox from wrf files

I'm not an expert in WRF but i need to use it. One of the very frustating and
tricky part was to make a correct namelist.wps. Hours and hours trying to
get the perfect domains. This functions solves this part while providing
a dynamic maps for actually viewing where are your domains. 

## Install
```{r eval = FALSE}
remotes::install_github("atmoschem/wrftools")
```

## wrf_domains (bug for mid latitudes, good for low latitude regions)

wrf_domains returns a list of:

1. the map
2. the sf object

The arguments of wrf_domains are the same arguments of namelist.wps.
It include default values but you can change them accordingly.

```{r}
library(wrftools)
a <- wrf_domains()
a[[1]] # leaflet
```

![](https://i.imgur.com/7giwGp6.png)



## xtractor

(inspired in NCL from DCA/IAG/USP)

Which returns data.frame ready for ggplot2. The class of Time is POSIXct

* NOW SUPPORTS MANY POINTS*

```{r eval = FALSE}
data(cetesb)
#use your wrfout
wrf <- "wrfoA.nc"
t2 = c("T2", "o3", "no", "no2", "PM10", "PM2_5_DRY")
df <- xtractor(atmos = wrf, vars = t2, points = cetesb,
stations = cetesb$Station)
```

![](https://i.imgur.com/cXJZ1nI.png)

and raster bricks

```{r eval = FALSE}
library(cptcity)
r <- xtractor(atmos = wrf, vars = t2, points = cetesb[1, ], return_list = T)
#  A list with raster and data.frame
sp::spplot(r[[1]][[2]], "layer.60",
           scales = list(draw = T), col.regions = cpt(1224))
```

![](https://i.imgur.com/j4d5ei5.png)


## Contributing

If you see any errors and know how to improve the function, or add new functions
write an issue and a pull request, please. I will be ver grateful, for sure,
100%.

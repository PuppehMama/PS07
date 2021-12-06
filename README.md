California State Map Outline
================

## R Code to map the state of California and its capital

The capital is Sacramento

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.0     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   1.4.0     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(sf)
```

    ## Linking to GEOS 3.8.1, GDAL 3.2.1, PROJ 7.2.1

``` r
library(maps)
```

    ## 
    ## Attaching package: 'maps'

    ## The following object is masked from 'package:purrr':
    ## 
    ##     map

``` r
USA_map <-  maps::map("state", plot = FALSE, fill = TRUE)

USA_sf <- USA_map %>% 
  st_as_sf(crs = 4326)

CA_sf <- USA_sf %>%
  filter(ID == "california")

CA_capital <- tibble(
  name = c("Sacramento"),
  lat = c(38.5816), 
  lon = c(-121.4944)
)

CA_capital_sf <- CA_capital %>%
  st_as_sf(coords = c("lon", "lat"), crs = 4326)
```

## ggplot Code

Creates the map

``` r
ggplot() +
  geom_sf(data = CA_sf) +
  geom_sf(data = CA_capital_sf, aes(col = name), size = 3) +
  labs(title="California State", x= "Longitude", y= "Latitude", color= "Capital")
```

![](README_files/figure-gfm/ggplot-1.png)<!-- -->

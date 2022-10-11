# Understanding-the-relation-between-High-Paying-and-IT-jobs-with-the-median-rent-in-Bay-Area-CA
## set your working directory for export and import

setwd("/Users/swarn/Desktop/LAB 5")

## Package setup

pkgs <- c("tidyverse", "tidycensus", "spdep", "mapview", 
          "leafsync", "tmap", "tmaptools", "remotes", "sf", "shiny", "shinyjs")

install.packages(pkgs)
remotes::install_github("walkerke/crsuggest")

## Set your Census API key if need be
library(tidycensus)
census_api_key("671c46c68c7be71e877cd3eeb315bbd0acd627fc")
readRenviron("~/.Renviron")


---------------------------------------------------------------------


## ----tidycensus-geometry-------------------------------------------------------------------------------
library(tidycensus)
options(tigris_use_cache = TRUE)


ca_medianrent <- get_acs(geography = "county", 
                      variables = c(medrent = "B25064_001"), 
                      state = "CA")

ca_medianrent <- get_acs(geography = "county", 
                     variables = c(medrent = "B25064_001"), 
                     state = "CA", 
                     geometry = TRUE)

## ----show-geometry-------------------------------------------------------------------------------------
ca_medianrent


## ----plot-geometry-------------------------------------------------------------------------------------
plot(ca_medianrent["estimate"])



## ----geom-sf-------------------------------------------------------------------------------------------
library(tidyverse)

ca_map <- ggplot(ca_medianrent, aes(fill = estimate)) + 
  geom_sf()


## ----plot-geom-sf--------------------------------------------------------------------------------------
ca_map


## ----get-santa-clara-data---------------------------------------------------------------------------------

sf_rent <- get_acs(
  geography = "tract",
  state = "CA",)



##SF Rent map
sf_rent <- get_acs(
  geography = "tract",
  state = "CA",
  county = "San Francisco",
  variables = c(medrent = "B25064_001"),
  geometry = TRUE
)


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(sf_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

sf_rent <- filter(sf_rent, 
                   variable == "medrent")

tm_shape(sf_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(sf_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(sf_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of San Francisco") + 
  tm_layout(title = "Median Rent Of San Francisco\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(sf_rent, zcol = "estimate")

m1 <- mapview(sf_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(sf_rent, "sfdata/sfrent.shp")

##Alameda Rent
Al_rent <- get_acs(
  geography = "tract",
  state = "CA",
  county = "Alameda",
  variables = c(medrent = "B25064_001"),
  geometry = TRUE
)


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(Al_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

sf_rent <- filter(Al_rent, 
                  variable == "medrent")

tm_shape(Al_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(Al_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(sf_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of Alameda") + 
  tm_layout(title = "Median Rent Of Alameda\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(Al_rent, zcol = "estimate")

m1 <- mapview(Al_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(Al_rent, "sfdata/alamedarent.shp")

##Contra Costa Rent
cc_rent <- get_acs(
  geography = "tract",
  state = "CA",
  county = "Contra Costa",
  variables = c(medrent = "B25064_001"),
  geometry = TRUE
)


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(cc_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

cc_rent <- filter(cc_rent, 
                  variable == "medrent")

tm_shape(cc_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(cc_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(cc_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of Contra Costa") + 
  tm_layout(title = "Median Rent Of Contra Costa\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(cc_rent, zcol = "estimate")

m1 <- mapview(cc_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(cc_rent, "sfdata/contracostarent1.shp")

##Santa Clara rent
  
sc_rent <- get_acs(
    geography = "tract",
    state = "CA",
    county = "Santa Clara",
    variables = c(medrent = "B25064_001"),
    geometry = TRUE
  )


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(sc_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

cc_rent <- filter(sc_rent, 
                  variable == "medrent")

tm_shape(sc_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(sc_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(cc_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of Santa Clara") + 
  tm_layout(title = "Median Rent Of Santa Clara\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(sc_rent, zcol = "estimate")

m1 <- mapview(sc_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(sc_rent, "sfdata/santaclararent.shp")

##Marin County rent

mc_rent <- get_acs(
  geography = "tract",
  state = "CA",
  county = "Marin",
  variables = c(medrent = "B25064_001"),
  geometry = TRUE
)


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(mc_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

mc_rent <- filter(mc_rent, 
                  variable == "medrent")

tm_shape(mc_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(mc_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(mc_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of Marin County") + 
  tm_layout(title = "Median Rent Of Marin County\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(mc_rent, zcol = "estimate")

m1 <- mapview(mc_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(mc_rent, "sfdata/marincountyrent.shp")

##San Mateo rent

sm_rent <- get_acs(
  geography = "tract",
  state = "CA",
  county = "San Mateo",
  variables = c(medrent = "B25064_001"),
  geometry = TRUE
)


## ----glimpse-sc-data-----------------------------------------------------------------------------
glimpse(sm_rent)


## ----polygons-map, echo = FALSE------------------------------------------------------------------------
library(tmap)

cc_rent <- filter(sm_rent, 
                  variable == "medrent")

tm_shape(sm_rent) + 
  tm_polygons() 


## ----choropleth-show, echo = FALSE---------------------------------------------------------------------
tm_shape(sm_rent) + 
  tm_polygons(col = "estimate")


## ----custom-choropleth-show, echo = FALSE--------------------------------------------------------------
tm_shape(cc_rent, 
         projection = sf::st_crs(26915)) + 
  tm_polygons(col = "estimate",
              style = "quantile",
              n = 5,
              palette = "Greens",
              title = "Median Rent Of San Mateo County") + 
  tm_layout(title = "Median Rent Of San Mateo County\nby Census tract",
            frame = FALSE,
            legend.outside = TRUE)


## ---- eval = FALSE-------------------------------------------------------------------------------------
library(mapview)

mapview(sm_rent, zcol = "estimate")

m1 <- mapview(sm_rent, zcol = "estimate")


## ----write-shp, eval = FALSE---------------------------------------------------------------------------
library(sf)

st_write(sm_rent, "sfdata/sanmateorent.shp")



# Using DiSARM API from R tutorial

The DiSARM API uses JSON as a standard for inputs and outputs, i.e. data have to be sent to the DiSARM API as JSON and will be returned as JSON. Some functions accept URLs to JSON files. In which case, the JSON input can contain the URL.

Handling JSON objects in R is most easily done using lists. As an example walkthrough, let’s use the `fn-covariate-extractor` function which allows users to pass in a GeoJSON of points, specify the required bioclimatic layers, and receive back the same GeoJSON with values of those layers attached. As specified in the function [SPECS file](https://github.com/disarm-platform/fn-covariate-extractor/blob/master/SPECS.md), the function requires a JSON object with 2 fields:

* `points` {GeoJSON Points FeatureCollection} Points at which to

  extract covariate values

* `layer_names` {Array of string} array: list of layer names to

  include

First we have to create a list object containing everything required for the function. As specified in SPECS, `points` has to be a GeoJSON. R doesn’t handle GeoJSON natively, but there are functions in the `geojsonio` package to make this conversion simple. Let’s work through an example using some dummy data from Swaziland. We are going to handle spatial data using the `sf` package. See [here](https://github.com/r-spatial/sf/blob/master/README.md) for more info on this package.

```r
library(sf)
library(geojsonio)

points_sf <- st_read("https://www.dropbox.com/s/i7r4ws1hziy45m6/test_points.geojson?dl=1")
```

```text
## Reading layer `OGRGeoJSON' from data source `https://www.dropbox.com/s/i7r4ws1hziy45m6/test_points.geojson?dl=1' using driver `GeoJSON'
## Simple feature collection with 4 features and 11 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 31.22881 ymin: -27.06899 xmax: 31.84315 ymax: -26.08659
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
```

```r
input_data_list <- list(
      points = geojson_list(points_sf),
      layer_names = c("elev_m", "dist_to_water_m")
    )
```

We have now created a list of the JSON object we are going to send to the function, which includes `points` as a `geo_list` class object. This replicates the JSON structure of a GeoJSON. Now let’s use the `POST` function from the `httr` package to send it to the function.

```r
library(httr)

response <-
      httr::POST(
        url = "https://<OPENFAAS_GATEWAY_URL>/function/fn-covariate-extractor",
        body = as.json(input_data_list),
        content_type_json(),
        timeout(90)
      )
```

Let’s take a look at the response. If the function runs successfully, The API will return a JSON object with `result` property which contains the result specific to the function.

```r
# Get status code (200 is good)      
response$status_code
```

```text
## [1] 200
```

```r
# Get contents of the response
response_content <- content(response)
```

In this case, as the API is returning a GeoJSON object, when you inspect the contents of the result in R, it is converted to a list. To convert it to something useful, you should first convert the list to a JSON string and then use the `sf` package to convert into an `sf` object.

```r
points_sf <- st_read(as.json(response_content$result))
points_sf
```

```text
## Simple feature collection with 4 features and 11 fields
## geometry type:  POINT
## dimension:      XY
## bbox:           xmin: 31.22881 ymin: -27.06899 xmax: 31.84315 ymax: -26.0866
## epsg (SRID):    4326
## proj4string:    +proj=longlat +datum=WGS84 +no_defs
##   GID_0    NAME_0   GID_1     NAME_1   TYPE_1 ENGTYPE_1 HASC_1
## 1   SWZ Swaziland SWZ.1_1     Hhohho District  District  SZ.HH
## 2   SWZ Swaziland SWZ.2_1    Lubombo District  District  SZ.LU
## 3   SWZ Swaziland SWZ.3_1    Manzini District  District  SZ.MA
## 4   SWZ Swaziland SWZ.4_1 Shiselweni District  District  SZ.SH
##   extracted_pop  VARNAME_1 elev_m dist_to_water_m
## 1        357593        { }    570             898
## 2        264585        { }    268            1737
## 3        405114        { }    645            2286
## 4        264529 Shiselwini    675            1821
##                     geometry
## 1  POINT (31.3261 -26.08659)
## 2  POINT (31.84315 -26.5465)
## 3 POINT (31.22881 -26.55188)
## 4 POINT (31.42339 -27.06899)
```

You can now continue to work with the `sf` objects, for example plotting points colored by elevation in leaflet

```text
library(leaflet)

col_pal <- colorNumeric(topo.colors(4), points_sf$elev_m)
leaflet() %>% addProviderTiles("CartoDB.Positron") %>%
  addCircleMarkers(data = points_sf, col = col_pal(points_sf$elev_m)) %>% 
  addLegend(pal = col_pal, values =points_sf$elev_m, title = "Elevation (m)")
```

![](https://raw.githubusercontent.com/disarm-platform/docs/master/images/elev_m_sazi_points.png)


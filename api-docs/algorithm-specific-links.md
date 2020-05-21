# Algorithm-specific links

_Please see the note on_ [_Availability of live algorithms API_]()\_\_

Below is a list of algorithms and functions available via the DiSARM API. For each function, there are links to the specifications \(SPECS.md file\), which provides information on the inputs required to run each function, as well as the outputs returned by each function. For each function, we also provide a links to a simple UI to run the function and the function/UI repositories on GitHub.

If you bump into any issues on any of the functions, please log an issue on the function repository \(if you know how\) or email [hugh.sturrock@ucsf.edu](mailto:hugh.sturrock@ucsf.edu).

## Buildings Clusterer

This algorithm clusters buildings into groups. The user can specify the minimum and maximum number of builidngs per cluster, as well as the maximum distance between any two buildings in a cluster. It is also possible to ensure that no clusters intersect lines \(e.g. roads, rivers or admin boundaries\).

[Specs](https://github.com/disarm-platform/fn-dbscan-clusterer/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-dbscan-clusterer) \| [Algorithm Repo](https://github.com/disarm-platform/fn-dbscan-clusterer) \| [UI Repo](https://github.com/disarm-platform/ui-dbscan-clusterer)

## Raster extractor

This function allows users to extract values of a supplied raster using supplied polygons or points.

[Specs](https://github.com/disarm-platform/fn-raster-vector-summary-stats/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-raster-vector-summary-stats/) \| [Algorithm Repo](https://github.com/disarm-platform/fn-raster-vector-summary-stats) \| [UI Repo](https://github.com/disarm-platform/ui-raster-vector-summary-stats/)

## Covariate extractor

This function allows users to obtain values of select bioclimatic/environmental layers \(bioclim, elevation, distance to water\) from supplied polygons or points.

[Specs](https://github.com/disarm-platform/fn-covariate-extractor/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-covariate-extractor/) \| [Algorithm Repo](https://github.com/disarm-platform/fn-covariate-extractor) \| [UI Repo](https://github.com/disarm-platform/ui-covariate-extractor/)

## Village finder

This function allows users to obtain estimated locations of settlements from WorldPop data for select countries.

[Specs](https://github.com/disarm-platform/fn-village-finder/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-village-finder/) \| [Algorithm Repo](https://github.com/disarm-platform/fn-village-finder) \| [UI Repo](https://github.com/disarm-platform/ui-village-finder/)


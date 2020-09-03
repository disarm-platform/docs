# Existing DiSARM algorithms

Below is a list of algorithms and functions that were created for the DiSARM API. For each function, there are links to the specifications \(`SPECS.md` file\), which provides information on the inputs required to run each function, as well as the outputs returned by each function. For each function, we also provide a link to a simple UI to run the function as well as links to the function/UI repositories on GitHub.

To use these algorithms, you will need run them as a container. The simplest way to do this is on your local machine \(see [Running algorithms](using-the-api/) for more information\). Alternatively, you can deploy the container on a remote server and call the algorithm using an HTTP request. The section 'Managing and example infrastructure' provides an overview of the approach taken by the DiSARM project using OpenFaaS. If you want to create your own containerized function, refer to the [Creating and deploying functions](creating-and-deploying-functions/) section.

## Buildings Clusterer

This algorithm clusters buildings into groups. The user can specify the minimum and maximum number of buildings per cluster, as well as the maximum distance between any two buildings in a cluster. It is also possible to ensure that no clusters intersect lines \(e.g. roads, rivers or admin boundaries\).

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

## Prevalence predictor

This function allows users to predict prevalence of a \(binomial\) outcome at specific locations given georeferenced set of point prevalence data. Includes an option to obtain optimal locations of further sites to survey.

[Specs](https://github.com/disarm-platform/fn-prevalence-predictor-mgcv/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ntd-shiny-points/) \| [Algorithm Repo](https://github.com/disarm-platform/fn-prevalence-predictor-mgcv) \| [UI Repo](https://github.com/disarm-platform/ntd-shiny-points)


# API docs

The API provides access to DiSARM algorithms, functions and models. Each algorithm can be accessed headless (i.e. via http request without an interface) or via a simple user interface (UI). See Algorithm-specific docs for a list of each algorithm available and links to the UIs and source code.

## General instructions

The simplest example of a synchronous request with parameters would be something like:

```text
curl --request 'POST' \
    --data '{"delay_s":0.5}'  \
    https://faas.srv.disarm.io/function/longrun
```

There are detailed instructions for running the functions in [development](https://github.com/disarm-platform/functions-for-openfaas/wiki/Running-deployed-functions-for-development-and-testing) \(e.g. using [`curl`](https://curl.haxx.se)) and in [production](https://github.com/disarm-platform/functions-for-openfaas/wiki/Running-deployed-functions-in-production) \(e.g. from Python\). For more general instructions and background information, see [the project wiki](https://github.com/disarm-platform/functions-for-openfaas/wiki).

Note: [HTTPie](https://httpie.org) might be a useful alternative command line client for HTTP requests.

## Algorithm-specific docs

Below is a list of alorithms and functions available via the DiSARM API. For each function, there are links to the specifications \(SPECS.md file\), which provides info on how to run the function via an HTTP request, as well as links to a simple UI to run the function and the function repository on GitHub.

If you bump into any issues on any of the functions, please log an issue on the function repository \(if you know how\) or email [hugh.sturrock@ucsf.edu](mailto:hugh.sturrock@ucsf.edu).

### Buildings Clusterer

This algorithm clusters buildings into groups. The user can specify the minimum and maximum number of builidngs per cluster, as well as the maximum distance between any two buildings in a cluster. It is also possible to ensure that no clusters intersect lines \(e.g. roads, rivers or admin boundaries\).

[Docs](https://github.com/disarm-platform/fn-dbscan-clusterer/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-dbscan-clusterer) \| [Repo](https://github.com/disarm-platform/fn-dbscan-clusterer)

### Raster extractor

This function allows users to extract values of a raster using polygons or points.

[Docs](https://github.com/disarm-platform/fn-raster-vector-summary-stats/blob/master/SPECS.md) \| [UI](https://disarm.shinyapps.io/ui-raster-vector-summary-stats/) \| [Repo](https://github.com/disarm-platform/fn-raster-vector-summary-stats)


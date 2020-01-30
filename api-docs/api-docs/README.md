# Managing an example API infrastructure

## Aim and background

The DiSARM project has developed a number of algorithms to support disease control efforts. Most of these algorithms have been written in a way that allows them to be 'deployed' on servers accessible via an API. This allows them to be used via an HTTP request and therefore provides a mechanism to integrate them into user interfaces and other pipelines.

For the duration of the DiSARM project, we will host our deployed versions on our own servers for demonstration purposes. Each algorithm can be accessed headless \(i.e. via http request without an interface\) or via a simple user interface \(UI\). See [Algorithm-specific docs](../algorithm-specific-links.md) for a list of each algorithm available and links to the UIs and source code.

The algorithms will be taken offline once the project is complete. However, all algorithms can be easily deployed on other servers and we provide documentation on how to do this \(see [Deploying an algorithm](https://docs.disarm.io/api-docs/creating-and-deploying-functions/deploying)\).

If you are interested in deploying your own algorithm, refer to the [Creating and deploying functions](https://docs.disarm.io/api-docs/creating-and-deploying-functions) page which provides documentation on how to structure your function and how to use our scripts/templates to deploy to your own server. Documentation is only provided for deploying algorithms written in python or R.

## Components

**Functions**: It's basically an OpenFaaS server. It runs on Google Cloud Platform, in a Docker Swarm across 2 nodes. We documented our configuration in [config-faas-cluster](https://github.com/disarm-platform/config-faas-cluster).

**Caching files:** Most of the functions we use are shutdown when not in use, and restarted when needed. Besides user-provided data, there's often a need for additional data files for the algorithm to run. There's no _persistence_ of data within the function, so in order to avoid excessive network requests, and reliance on partner data servers, we cache requests for large data files, using [Squid](http://www.squid-cache.org/).

**Files:** we also have a need for some cached data files, usually that we've created or pre-processed ourselves. We use Google Cloud Storage to store the files. In order to allow caching, we configured a process to run every time a file is uploaded, which sets the correct cache headers on the files.


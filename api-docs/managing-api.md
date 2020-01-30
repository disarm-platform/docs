# Managing an example API infrastructure

For the time being, some notes on how we're managing the DiSARM API infrastructure. The hosted functions will be retired when the project closes, so these docs are to record what we did, some problems we encountered, and how we solved them.

## Aim and background

We created a way to provided hosted functions during the life of the project. This provides both a demonstration of the approach, as well as a way for partners to test algorithms running in production.

## Components

**Functions**: It's basically an OpenFaaS server. It runs on Google Cloud Platform, in a Docker Swarm across 2 nodes. We documented our configuration in [config-faas-cluster](https://github.com/disarm-platform/config-faas-cluster).

**Caching files:** Most of the functions we use are shutdown when not in use, and restarted when needed. Besides user-provided data, there's often a need for additional data files for the algorithm to run. There's no _persistence_ of data within the function, so in order to avoid excessive network requests, and reliance on partner data servers, we cache requests for large data files, using [Squid](http://www.squid-cache.org/).

**Files:** we also have a need for some cached data files, usually that we've created or pre-processed ourselves. We use Google Cloud Storage to store the files. In order to allow caching, we configured a process to run every time a file is uploaded, which sets the correct cache headers on the files.




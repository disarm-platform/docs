# DiSARM API \(Algorithms-as-a-service\)

The DiSARM project has developed a number of algorithms to support disease control efforts. Most of these algorithms have been written in a way that allows them to be deployed on servers accessible on-demand via an API. This allows them to be called over the web via an HTTP request and therefore provides a mechanism to integrate them into user interfaces and other pipelines. For example, the Google directions API allows users to find the optimal route between two or more points. This algorithm can be accessed directly using code, or indirectly via Google maps. There are a number of other algorithm APIs that provide other functionality, from identifying contents of images to converting addresses to latitude/longitudes. 

The potential benefits of this so called 'algorithms-as-a-service' \(AaaS\) approach are substantial, primarily by reducing the barrier to adoption of complex algorithms from requiring very specialised high-level human expertise, to requiring more widely-available web-development skills. See [Value of algorithms-as-a-service](why-deploy-an-algorithm.md) for more.

This documentation is primarily aimed at modelers and algorithm developers who want to learn how to deploy functions as an API service, as well as those on the software side who are interested in integrating these into interfaces, dashboards and other software. Our [Creating and deploying functions](https://docs.disarm.io/api-docs/creating-and-deploying-functions) page provides documentation on how to structure your function and how to use our scripts/templates to deploy to your own servers. Documentation is only provided for deploying algorithms written in Python or R.

The DiSARM project has also developed own our algorithms as part of work supporting malaria and neglected tropical disease control efforts. 
For the duration of the DiSARM project, we will host our deployed versions on our own servers for demonstration purposes. Each algorithm can be accessed headless \(i.e. via HTTP request without an interface\) or via a simple user interface \(UI\). See [Algorithm-specific docs](algorithm-specific-links.md) for a list of each algorithm available and links to the UIs and source code.

The algorithms will be taken offline once the project is complete. However, all algorithms can be easily deployed on other servers and we provide documentation on how to do this \(see [Deploying an algorithm](https://docs.disarm.io/api-docs/creating-and-deploying-functions/deploying)\).


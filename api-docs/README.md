# DiSARM API \(Algorithms via API\)

The DiSARM project has developed a number of algorithms to support disease control efforts. Most of these algorithms have been written in a way that allows them to be deployed on servers accessible via an API. This allows them to be used via an HTTP request and therefore provides a mechanism to integrate them into user interfaces and other pipelines.

The potential benefits of this approach are substantial, primarily by reducing the barrier to adoption of complex algorithms from requiring very specialised high-level human capital, to requiring more widely-available web-development skills. See [Why deploy an algorithm?](why-deploy-an-algorithm.md) for more.

For the duration of the DiSARM project, we will host our deployed versions on our own servers for demonstration purposes. Each algorithm can be accessed headless \(i.e. via HTTP request without an interface\) or via a simple user interface \(UI\). See [Algorithm-specific docs](algorithm-specific-links.md) for a list of each algorithm available and links to the UIs and source code.

The algorithms will be taken offline once the project is complete. However, all algorithms can be easily deployed on other servers and we provide documentation on how to do this \(see [Deploying an algorithm](https://docs.disarm.io/api-docs/creating-and-deploying-functions/deploying)\).

If you are interested in deploying your own algorithm, refer to the [Creating and deploying functions](https://docs.disarm.io/api-docs/creating-and-deploying-functions) page which provides documentation on how to structure your function and how to use our scripts/templates to deploy to your own server. Documentation is only provided for deploying algorithms written in Python or R.


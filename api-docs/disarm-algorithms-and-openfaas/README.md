# DiSARM algorithms and OpenFaas

We have been developing and testing DiSARM algorithms for deployment on [OpenFaas](https://www.openfaas.com/). It is a great platform, and has sped us up considerably in steps [2](../creating-and-deploying-functions/lifecycle-of-an-algorithm.md#2-re-write), [3](../creating-and-deploying-functions/lifecycle-of-an-algorithm.md#3-package) and [4](../creating-and-deploying-functions/lifecycle-of-an-algorithm.md#4-deploy) in the [lifecycle](../creating-and-deploying-functions/lifecycle-of-an-algorithm.md). OpenFaas is not the only approach to this, but any function _built_ with OpenFaas should then be much easier to deploy.

We've used 3 parts of OpenFaas:

1. The OpenFaas platform itself: for hosting and running deployed functions
2. The `watchdog` process handler: gets built into Docker images, to convert incoming HTTP requests into `STDIN` streams 
3. The `faas-cli` tool: scaffold new functions from templates, then build and deploy \(see [below](./)\)

## The `faas-cli`

The officials docs are at [https://docs.openfaas.com/cli/install/](https://docs.openfaas.com/cli/install/)

We've used these commands for _creating new functions_:

* `faas template pull https://github.com/disarm-platform/faas-templates.git`: retrieves our [custom templates](../creating-and-deploying-functions/scaffolding-from-a-template.md), and gets ready to create a new function from them
* `faas new --lang r-geospatial new-function-r`: scaffolds a new function from the `r-geospatial` template

We've used these commands for _building_. They assume the existence of a `stack.yml` file.

* `faas build`: builds a Docker image for the function. We've also found `faas build --shrinkwrap` can be useful to prepare the required files, but not actually build a container \(check in the `build` folder that gets created\)
* `faas push`: push the built image to Docker Hub
* `faas deploy`: get the built image running on your OpenFaas deployment

They can be combined and run at once with `faas up`.


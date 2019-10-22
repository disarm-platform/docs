# Creating and deploying a new algorithm to OpenFaas

## Pre-requisites

1. [OpenFaas CLI](https://docs.openfaas.com/cli/install/) installed localled
2. [Docker](https://docs.docker.com/install/) installed and running locally
3. OpenFaas gateway `username` and `password` details
4. Docker Hub account and login details
5. A fast internet connection

## Creating a new algorithm

1. Create a local copy of an existing repo (e.g. [Python sample](https://github.com/disarm-platform/faas-template-python-fn) or [R sample](https://github.com/disarm-platform/faas-template-r-fn)), in the correct language for the new algo. There isn't currently a better way to copy the wrapper code and structure.
2. Change at least these files:
   * `stack.yml`: this describes the Docker image, and the name the function will have when deployed \(don't want to over-write an existing algo\)
   * the `requirements.txt` or `install_packages.R` files \(or similar\): these are for installing dependencies, and without them, the image won't build
3. Ensure your function runs locally, ideally with some automated testing. Refer to the [Testing and debugging functions page](https://docs.disarm.io/api-docs/testing-and-debugging-functions) for more information. 

## Deploying

1. Login in Docker Hub with `docker login` - this lets you send the built Docker image somewhere more useful than local machine.
2. Login to the OpenFaas gateway with `faas login -u <GATEWAY_USER> -p <GATEWAY_PASSWORD> --gateway https://faas.srv.disarm.io`. If this doesn't work, you won't be able to stick the algorithm on the gateway.
3. From the top-level folder \(where `stack.yml` exists\), run `faas up` in the terminal. This combines three steps \(building, pushing and deploying\), and if successful is all you need to deploy the algorithm.

### Detail on deploy process

The OpenFaas CLI handles the process, but for info, the 3 main steps are:

1. `build`: create a local Docker image of the algorithm. Often requires a large \(few GB\) download the first time, to get the base images required and any packages installed. Subsequent builds of the same algorithm are usually faster.
2. `push`: pushes the built image to the Docker Hub image registry. It will be public by default. Can take a while first time, but subsequent pushes are usually faster.
3. `deploy`: tells the OpenFaas gateway to fetch the image you just pushed, and make it available on the gateway for use. Usually very quick. Relies on the content of `stack.yml` to determine which gateway to send it to, what to name it, and which image to use. 


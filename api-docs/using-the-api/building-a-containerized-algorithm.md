# Building a containerized algorithm

Stuff about faas build. Can mention faas build shrinkwrap as a tip, but isn;t really testing container



The simplest way to use a containerized algorithm, such as the existing DiSARM algorithms, is to run the container on your local machine and interact with it through port 8080. To do this you need to:  

1. Make sure [docker](https://docs.docker.com/get-docker/) is installed on your machine
2. Make sure the [`faas -cli`](https://docs.openfaas.com/cli/install/) is installed on your machine. We use some of OpenFaas' command line functions to help build and run containers.
3. If you are using an algorithm available as a GitHub repo, clone the repository to get hold of the necessary algorithm code. 
4. Build the container using the command line by navigating to the folder with the `stack.yml` file and running

```text
> faas build
```

This will built a container which will be named according to the `image` field of `stack.yml`. The first time you build a container it could take a while as it is obtaining all the necessary dependencies required to run the algorithm. 

Once built, you are ready to start and run the containerized algorithm. These are covered in the following sections.  


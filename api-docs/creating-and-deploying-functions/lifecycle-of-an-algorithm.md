# Lifecycle of an algorithm

Here we provide a brief overview of the process of building an API service. For a step-by-step guide, see the [following sections x y, and z](). When thinking about building an API service, we think about the problem in 4 steps:

1. **Write** an algorithm which solves a problem
2. **Re-write** the algorithm so it is more robust and reliable and more automated (i.e. able to provide useful results when supplied new data)
3. **Package** the algorithm to be accessed remotely by HTTP request and deployed simply via Docker
4. **Deploy** so it is accessible on a remote server, by HTTP request

## 1. Write

The first thing is to write some code to solve the problem. This can involve any or all of: developing a new algorithm or approach, writing code to implement an existing algorithm, gluing together existing algorithms and code, and so on. Depending on the problem and the way you're solving it, it can take a while to create something new, or can be very quick to pick an existing solution.

The initial output is usually brittle and regularly suffers from 'it-works-on-my-machine' errors. This is ok. To start with. Then we look at re-writing it.

There's no requirement to start this step in any particular way, but starting with a [templated function](lifecycle-of-an-algorithm.md) can simplify the later steps. The templates contain a number of files that simplify deployment. 

## 2. Re-write

We want to upgrade the original code to make it more robust and reliable. For example, if it references a local data file, we might instead place that somewhere on a remote server and write code to re-construct or retrieve it. We'll also want to include some validation of the incoming request parameters, to tell the user as early as possible they've supplied an invalid input.

We can add some automated _unit_ testing, for example, to make sure a function inside the code returns the expect values for a known input.

We'll also create a `test_req.json` file, which we try to ensure contains a simple but functioning example request, which we can use for `end-to-end` testing once the algorithm is deployed.

As with step 1, this step also does not _need_ to use any particular structure, but using a [templated function](lifecycle-of-an-algorithm.md) can simplify the next steps.

## 3. Package

To package and deploy functions, we have used two important tools. [Docker](https://www.docker.com/) and [OpenFaas](https://www.openfaas.com/). Docker is a tool that allows you to wrap all the required software and code into a 'container', which is essentially a mini computer environment with all the reuqired pieces for running a function. for example, you might have a function written in R that you want to deploy as an API. Using Docker, you could get hold of a copy of R and the required libraries and package them into a single 'container' which can then be run on a different machine without the need for that machine having R or dependent libraries. OpenFaas is a tool that allows us to deploy these containers on the web and be used over the web. Its not the only tool that can do this, but is open-source, widely used and well supported.

To package an algorithm, this can be as simple as running `faas build` form the command line if you started with a [templated function](lifecycle-of-an-algorithm.md). If not, you'll need to create a new [templated function](lifecycle-of-an-algorithm.md) and copy your code and related files into the new folder. Once they're copied across, you can also run `faas build`.

## 4. Deploy

You will need a running OpenFaas deployment, which you've logged-into using `faas login`.

Assuming you have a successful build from step 3, the deploy is simple to initiate: `faas up`. If this works, the command should output the URL of the hosted function. 

The following sections will take you through the process in more detail. 



# Creating a new algorithm

## Lifecycle of a algorithm
We think about a function having 4 steps, to bring from an idea to a remotely-deployed and accessible service.
1. **Write** an algorithm which solves a problem
2. **Re-write** the algorithm so it is more robust and reliable
3. **Package** the algorithm to be accessed remotely by HTTP request and deployed simply via Docker
4. **Deploy** so it is accessible on a remote server, by HTTP request

<img src="/Users/jonathan/Dv-DiSARM/docs/api-docs/creating-and-deploying-functions/3 steps.png" style="zoom:38%;" />

### 1. Write

The first thing is to actually solve the problem. This can involve any or all of developing a new algorithm or approach, writing code to implement an existing algorithm, gluing together existing algorithms and code, and so on. Depending on the problem and the way you're solving it, it can take a while to create something new, or can be very quick to pick an existing solution.

The initial output is usually brittle and regularly suffers from 'it-works-on-my-machine' errors. This is ok. To start with. Then we look at re-writing it.

There's no requirement to start this step in any particular way, but starting with a [templated function]() can simplify the later steps.

### 2. Re-write

We want to upgrade the original code to make it more robust and reliable. For example, if it references a local data file, we might instead place that somewhere on a remote server and write code to re-construct or retrieve it. We'll also want to include some validation of the incoming request parameters, to tell the user as early as possible they've given us invalid input.

We can add some automated _unit_ testing, for example, to make sure a function inside the code returns the expect values for a known input.

We'll also create a `test_req.json` file, which we try to ensure contains a simple but functioning example request, which we can use for `end-to-end` testing once the algorithm is deployed.

As with step 1, this step also does not _need_ to use any particular structure, but using a [templated function]() can simplify the next steps.

### 3. Package

If you started with a [templated function](), then this can be as simple as running `faas build`.

If not, you'll need to create a new [templated function]() and copy your code and related files into the new folder. Once they're copied across, you can also run `faas build`.

### 4. Deploy

Assuming you have a successful build from step 3, this step is simple to initiate: `faas up` .



## DiSARM algorithms and *OpenFaas*

We have been developing and testing DiSARM algorithms for deployment on OpenFaas. It is a great platform, and has speeded us up considerably in steps 2, 3 and 4 above. OpenFaas is not the only approach to this, but any function _built_ with OpenFaas should then be much easier to deploy.

We've used 3 parts of OpenFaas:
1. The OpenFaas platform itself: for hosting and running deployed functions
1. The `watchdog` process handler: gets built into Docker images, to convert incoming HTTP requests into `STDIN` streams 
1. The `faas-cli` tool: scaffold new functions from templates, then build and deploy (see [below](#faas-cli))

### `faas-cli`

The officials docs are at https://docs.openfaas.com/cli/install/

We've used these commands for *creating new functions*:

- `faas template pull https://github.com/disarm-platform/faas-templates.git`: retrieves our [custom templates](#scaffolding-from-a-template), and gets ready to create a new function from them
- `faas new --lang r-geospatial new-function-r`: scaffolds a new function from the `r-geospatial` template

We've used these commands for *building*. They assume the existence of a `stack.yml` file.

- `faas build`: builds a Docker image for the function. We've also found `faas build --shrinkwrap` can be useful to prepare the required files, but not actually build a container (check in the `build` folder that gets created)
- `faas push`: push the built image to Docker Hub
- `faas deploy`: get the built image running on your OpenFaas deployment

They can be combined and run at once with `faas up`.



## Scaffolding from a template

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. The instructions assume you want to use one of the DiSARM templates.

You will need `faas-cli` and Docker installed.

In your terminal:

1. Create and change into a new folder
1. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
1. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
1. Check the template builds with `faas build -f <function-name>`

This creates a basic function. Check the [editing `stack.yml` page](api-docs/creating-and-deploying-functions/editing-stack-yml.md) for instructions on editing this empty function to make it deployable on OpenFaas.

The folders and files created using our `python-geospatial` template will be something like: 

```
new-function-py
├── handler.py
├── preprocess_params.py
└── requirements.txt
```

and for `r-geospatial`:

```
new-function-r
├── function.R
├── install_packages.R
└── preprocess_params.R
```


## Basics of writing a function

Regardless of the language and dependencies, all functions use the same *basic* approach to data
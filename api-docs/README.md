# API docs

The API provides access to DiSARM algorithms, functions and models. Each algorithm can be accessed headless (i.e. via http request without an interface) or via a simple user interface (UI). See Algorithm-specific docs for a list of each algorithm available and links to the UIs and source code.

## Terms
We can deploy almost any function to the OpenFaas platform, so the following terms are used interchangeably: `functions`, `algorithms`, `models`, etc.

## General instructions

The simplest example of a synchronous request with parameters would be something like:

```text
curl --request 'POST' \
    --data '{"delay_s":0.5}'  \
    https://faas.srv.disarm.io/function/longrun
```

There are detailed instructions for running the functions in [development](../api-docs/Running-deployed-functions-for-development-and-testing.md) \(e.g. using [`curl`](https://curl.haxx.se)) and in [production](../api-docs/Running-deployed-functions-in-production) \(e.g. from Python\).

Note: [HTTPie](https://httpie.org) might be a useful alternative command line client for HTTP requests.

# Data
- Datasets [coming]
- [Structuring JSON](../api-docs/Structuring-JSON)

# Creating, deploying
- [Creating and deploying a new algorithm on DiSARM OpenFaas](../api-docs/Creating-and-deploying-a-new-algorithm-on-DiSARM-OpenFaas)
- [Versioning](../api-docs/Versioning-algos)

# Testing, debugging
- [Troubleshooting functions](../api-docs/Troubleshooting-functions)
- [Testing local function containers](../api-docs/Testing-a-function-locally)
- [Running for test/dev](../api-docs/Running-deployed-functions-for-development-and-testing)

# Using
- [Running in production](../api-docs/Running-deployed-functions-in-production)
- [Logging and monitoring](../api-docs/Logging,-monitoring)


# Infrastructure
- [DiSARM API Infrastructure](../api-docs/DiSARM-API-Infrastructure)
# API docs

The API provides access to DiSARM algorithms, functions and models. Each algorithm can be accessed headless (i.e. via http request without an interface) or via a simple user interface (UI). See Algorithm-specific docs for a list of each algorithm available and links to the UIs and source code.

## General instructions

The simplest example of a synchronous request with parameters would be something like:

```text
curl --request 'POST' \
    --data '{"delay_s":0.5}'  \
    https://faas.srv.disarm.io/function/longrun
```

There are detailed instructions for running the functions in [development](/api-docs/Running-deployed-functions-for-development-and-testing) \(e.g. using [`curl`](https://curl.haxx.se)) and in [production](/api-docs/Running-deployed-functions-in-production) \(e.g. from Python\). For more general instructions and background information, see [the project wiki](/api-docs).

Note: [HTTPie](https://httpie.org) might be a useful alternative command line client for HTTP requests.


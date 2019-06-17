# API docs

The API provides access to DiSARM algorithms, functions and models. Each algorithm can be accessed headless \(i.e. via http request without an interface\) or via a simple user interface \(UI\). See [Algorithm-specific docs](algorithm-specific-links.md) for a list of each algorithm available and links to the UIs and source code.

## Terms

We can deploy almost any function to the OpenFaas platform, so the following terms are used interchangeably: `functions`, `algorithms`, `models`, etc.

## General instructions

The simplest example of a synchronous request with parameters would be something like:

```text
curl --request 'POST' \
    --data '{"delay_s":0.5}'  \
    https://faas.srv.disarm.io/function/longrun
```

There are detailed instructions for running the functions in [development](testing-and-debugging-functions/running-deployed-functions-for-development-and-testing.md) \(e.g. using [`curl`](https://curl.haxx.se)\) and in [production](using-the-api/running-deployed-functions-in-production.md) \(e.g. from Python\).

Note: [HTTPie](https://httpie.org) might be a useful alternative command line client for HTTP requests.


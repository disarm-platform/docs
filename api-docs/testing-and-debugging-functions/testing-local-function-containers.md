# Testing local function containers

## What is this?

Instructions for testing the _container_, not the code. The container includes all the dependencies, etc. It would be neat to test this directly on a local installation of OpenFaas, but it doesn't look like that's too easy. So these instructions are for directly testing the container.

## Steps

This is easiest with two terminal windows side-by-side. You will need to navigate each to the root folder \(where `stack.yml` is found\).

You'll need [Docker installed](https://runnable.com/docker/install-docker-on-macos) locally, as well as the [faas-cli](https://docs.openfaas.com/cli/install/).

1. Start the container in the **first terminal window**:
   * You'll need the `image` name from `stack.yml`, something like `disarm/fn-covariate-extractor:0.0.2`
   * Run this command, substituting the `image` name:

     ```bash
     docker run -it --rm -p 8080:8080 -e read_timeout=600 -e write_timeout=600 -e exec_timeout=600 -e combine_output=false disarm/fn-covariate-extractor:0.0.2
     ```

   * This will get it running locally on port 8080 \(you might need to change the _first_ `8080` if there's a conflict on your machine\).
   * Should print a few lines and then wait. You can kill it by pressing CTRL+C in this terminal

     ```bash
       ❯ docker run -it -p 8080:8080 disarm/fn-covariate-extractor:0.0.2
       2019/03/04 06:54:53 Version: 0.9.14     SHA: a65df4795bc66147c41161c48bfd4c72f60c7434
       2019/03/04 06:54:53 Read/write timeout: 5s, 5s. Port: 8080
       2019/03/04 06:54:53 Writing lock-file to: /tmp/.lock
     ```
2. Second a request in the **second terminal window**:
   * In another terminal send an HTTP request to `localhost:8080` e.g. `curl --request 'POST' 'http://localhost:8080' --max-time 60 -d @fn-covariate-extractor/function/test_req.json`
   * This request should make the first terminal print out `2019/03/04 07:22:58 Forking fprocess.`
   * Assuming it doesn't timeout or crash, your second terminal should contain the successful response, while the first should contain some logging, or at least the error if it crashes.


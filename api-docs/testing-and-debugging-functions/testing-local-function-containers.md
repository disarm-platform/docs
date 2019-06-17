# Testing local function containers

## What is this?

Instructions for testing the _container_, not the code. The container includes all the dependencies, etc. It would be neat to test this directly on a local installation of OpenFaas, but it doesn't look like that's too easy. So these instructions are for directly testing the container.

## Steps

1. Open two terminal windows - side-by-side would be useful.
2. In first terminal, build the container: `faas build` from the top-level \(where `stack.yml` file exists\). You'll need [Docker installed](https://runnable.com/docker/install-docker-on-macos) locally, as well as the [`faas-cli`](https://docs.openfaas.com/cli/install/).
3. In the first terminal, start the container running:
   * from the previous step, check the built container name \(something like `Image: disarm/fn-covariate-extractor:0.0.2 built.` - take the `disarm/fn-covariate-extractor:0.0.2` part\)
   * Run this command: `docker run -it -p 8080:8080 disarm/fn-covariate-extractor:0.0.2`. This will get it running locally on port 8080 \(you might need to change the second 8080 if there's a conflict on your machine\).
   * Should print a few lines and then wait. You can kill it by pressing CTRL+C in this terminal 

     ```bash
       ❯ docker run -it -p 8080:8080 disarm/fn-covariate-extractor:0.0.2
       2019/03/04 06:54:53 Version: 0.9.14     SHA: a65df4795bc66147c41161c48bfd4c72f60c7434
       2019/03/04 06:54:53 Read/write timeout: 5s, 5s. Port: 8080
       2019/03/04 06:54:53 Writing lock-file to: /tmp/.lock
     ```
4. In the second terminal, send a request
   * In another terminal send an HTTP request to `localhost:8080` e.g. `curl --request 'POST' 'http://localhost:8080' -d --max-time 60 @fn-dbscan-clusterer/function/test_req.json`
   * This request should make the first terminal print out `2019/03/04 07:22:58 Forking fprocess.`
5. Assuming it doesn't timeout or crash, your second terminal should contain the successful response, while the first should contain some logging, or at least the error if it crashes.
6. Make sure you've not

## Editing the `Dockerfile`

If the function doesn't seem to be running properly, you might need to change the environment settings in the Dockerfile. It's 🧨really important - do not commit any changes to the `Dockerfile`, that will break the deployed version or introduce hard-to-spot bugs!

Add the following lines into the `Dockerfile`, towards the bottom, and the rebuild the image \(see step \#2 above\)

```text
ENV fprocess="Rscript index.R"

# Add lines below
ENV write_debug="false" # Writes out STDERR to the log
ENV combine_output='false' # Splits out the STDERR from STDOUT - important to keep the two separated, to see exactly what gets returned to the user.
ENV read_timeout=120 # In seconds, how long the function waits to receive input (not relevant on local machine)
ENV write_timeout=120 # In seconds, how long the function waits to send output (not relevant on local machine)
ENV exec_timeout=120 # In seconds, how long the function can run in total (incl waiting for input and sending output) before timing-out
# Add lines above

EXPOSE 8080
```


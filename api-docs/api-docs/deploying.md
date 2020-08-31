# Deploying an algorithm

There are two approaches, depending on whether or not a containerised version of the algorithm has already been built and published on Docker Hub. For all existing DiSARM algorithms, the relevant container is currently published on Docker Hub. Once deployed, the algorithms can be called as an API. Refer to the [Using the algorithms API](https://github.com/disarm-platform/docs/tree/02fce263d68abd9ef6e11bf3edbff02259ca297a/api-docs/creating-and-deploying-functions/api-docs/using-the-api/README.md) section for descriptions of different ways to call and use deployed algorithms.

Both approaches have the following prerequisites:

1. [Docker](https://docs.docker.com/install/) installed and running locally
2. An OpenFaaS gateway running at `<GATEWAY_URL>`. See [here](https://github.com/disarm-platform/config-faas-cluster) for details on how we set up an OpenFaas cluster. 
3. You have logged in to the OpenFaas gateway \([see below](deploying.md#required-logins)\)
4. `faas-cli` is installed \([docs](https://docs.openfaas.com/cli/install/)\).
5. The function code is available in a GitHub repo.

## Containerised version exists \(_tldr:_ `faas deploy`\)

**Prerequisite**: The container image exists in Docker Hub.

**Steps**:

1. Clone the repo with `git clone <repo>`.
2. `cd` into the folder with `cd <repo>`.
3. Edit the `stack.yml` file and change the value of `gateway` to `<GATEWAY_URL>` \(or override with `--gateway <GATEWAY_URL>` in next step\)
4. Deploy the function with `faas deploy`.

## No containerised version \(_tldr:_ `faas up`\)

**Prerequisite**: You have logged into Docker Hub \([see below](deploying.md#required-logins)\)

**Steps**:

1. Clone the repo with `git clone <repo>`.
2. `cd` into the folder with `cd <repo>`.
3. Edit the `stack.yml` file and change the value of `gateway` to `<GATEWAY_URL>` \(or override with `--gateway <GATEWAY_URL>` in next step\)
4. Deploy the function with `faas up`.

## Extra help

### Required logins

1. Login to the OpenFaas gateway with `faas login -u <GATEWAY_USER> -p <GATEWAY_PASSWORD> --gateway https://<OPENFAAS_GATEWAY_URL>`. If this doesn't work, you won't be able to stick the algorithm on the gateway.
2. Login in Docker Hub with `docker login` - this lets you send the built Docker image somewhere more useful than local machine.

### Detail on deploy process

The OpenFaas CLI handles the process, but for info, the 3 main steps are:

1. `build`: create a local Docker image of the algorithm. Often requires a large \(few GB\) download the first time, to get the base images required and any packages installed. Subsequent builds of the same algorithm are usually faster.
2. `push`: pushes the built image to the Docker Hub image registry. It will be public by default. Can take a while first time, but subsequent pushes are usually faster.
3. `deploy`: tells the OpenFaas gateway to fetch the image you just pushed, and make it available on the gateway for use. Usually very quick. Relies on the content of `stack.yml` to determine which gateway to send it to, what to name it, and which image to use. 


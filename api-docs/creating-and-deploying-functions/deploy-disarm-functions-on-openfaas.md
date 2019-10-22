# Deploying a diasarm function to OpenFaaS

There are two approaches, depending on whether or not a containerised version of the algorithm has already beeen built and published on Docker Hub.

Both approaches have the following prerequisites:

1. An OpenFaaS gateway running at `<GATEWAY_URL>`
2. You have logged in to the OpenFaas gateway
3. `faas-cli` is installed ([docs](https://docs.openfaas.com/cli/install/)).
2. The function code is available in a GitHub repo.

## Containerised version exists

### Prerequisite
The container image exists in Docker Hub.


### Steps
*TLDR:* use `faas deploy`

1. Clone the repo with `git clone <repo>`.
2. `cd` into the folder with `cd <repo>`.
3. Edit the `stack.yml` file and change the value of `gateway` to `<GATEWAY_URL>` (or override with `--gateway <GATEWAY_URL>` in next step)
4. Deploy the function with `faas deploy`.


## No containerised version

### Prerequisite
1. You have logged into Docker Hub.


### Steps
*TLDR:* use `faas up`

1. Clone the repo with `git clone <repo>`.
2. `cd` into the folder with `cd <repo>`.
3. Edit the `stack.yml` file and change the value of `gateway` to `<GATEWAY_URL>` (or override with `--gateway <GATEWAY_URL>` in next step)
4. Deploy the function with `faas up`.


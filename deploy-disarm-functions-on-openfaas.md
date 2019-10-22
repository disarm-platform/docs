# Deploying a diasarm function to OpenFaaS
These guide assumes that you have an OpenFaaS gateway running on the url `<http://faas_url.com>` and the function is in a git repo.
## Using `faas up`
### Prerequisites
1. `faas-cli` is installed.
2. You have logged in to the gateway.
3. Yo have logged into docker up.

### Steps
1. Clone the repo with `git clone https://github.com/disarm-platform/<function_name>.git`.
2. `cd` into the folder with `cd <function_name>`.
3. Edit the `stack.yml` file and change the value of `provider.gateway` to `<http://faas_url.com>`
4. Deploy the function with `faas up`.

## Using `faas deploy`
### Prerequisites
1. `faas-cli` is installed.
2. You have logged in to the gateway.
3. The container image exists in docker hub.

### Steps
1. Clone the repo with `git clone https://github.com/disarm-platform/<function_name>.git`.
2. `cd` into the folder with `cd <function_name>`.
3. Edit the `stack.yml` file and change the value of `provider.gateway` to `<http://faas_url.com>`
4. Deploy the function with `faas deploy`.

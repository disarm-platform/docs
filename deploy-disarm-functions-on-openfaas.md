# Deploying a diasarm function to OpenFaaS
These guide assumes that you have an OpenFaaS gateway running on the url `<http://faas_url.com>` and the function is in a git repo.

1. Clone the function repo with `git clone https://github.com/disarm-platform/<function_name>.git`

2. Change you working directory to the function folder with `cd <function_name>`
3. If you don't have `faas-cli` installed, install it with `curl -sSL https://cli.openfaas.com | sh`

4. Login to your OpenFaaS gateway with `faas login --gateway <http://faas_url.com> -u <Your Username> --password <Your password>`

5. Edit the `stack.yml` file and change the value of `provider.gateway` to `<http://faas_url.com>`
6. Deploy the function with `faas deploy`
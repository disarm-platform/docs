# Scaffolding from a template

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. Both templates include a very simple function which returns `TRUE`. The instructions assume you want to use either the R or Python version of the DiSARM templates.

You will need [`faas-cli`](https://docs.openfaas.com/cli/install/) and [Docker](https://docs.docker.com/engine/install/) installed.

In your terminal:

1. Create and change into a new folder
2. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
3. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
4. Rename `<function-name>.yml` to `stack.yml` (makes it easier to deploy later)
5. Rename `<function-name>` folder to `function/` (makes it easier to deploy later)
6. Edit the `stack.yml` file. Every function created for OpenFaas requires a configuration file in `yaml` format. The default for a new function is to name the configuration file the same as the function name you give \(e.g. `new-function.yml`\). Naming it `stack.yml` makes it easier for the OpenFaas CLI \(`faas` commands\) to find it. To make edits to the file, you can open in any text editor.

	There are 3 places to edit:

	* `gateway`: 
	   * edit to be the URL for the OpenFaas instance
	* `handler`:
	   * edit to be `./function`, this is required for our template code to work
	* `image`: 
	   * need to prefix with a Docker Hub org or repo you can write to
	   * optionally change the `latest` tag to a specific version number (e.g. 0.0.1)

	More information on editing the file can be found [in the official docs](https://docs.openfaas.com/reference/yaml/).

	Your `stack.yml` should then look like

	```yaml
	version: 1.0
	 provider:
	   name: openfaas
	   gateway: https://<OPENFAAS_GATEWAY_URL> # Changed from `http://127.0.0.1:8080
	 functions:
	   new-function:
	     lang: python
	     handler: ./function
	     image: <DOCKER_HUB_ORG>/new-function:0.0.1 # Changed from `new-function:latest`
	```

7. Once you've edited the stack.yml file, check the template builds without errors with `faas build`.

Once you've followed the steps above, the folders and files created will look like this if using our `python-geospatial` template:

```text
py-new-function
├── function
│  ├── handler.py
│  ├── preprocess_params.py
│  └── requirements.txt
└── stack.yml
```

and like this for `r-geospatial`:

```text
r-new-function
├── function
│  ├── function.R
│  ├── install_packages.R
│  └── preprocess_params.R
└── stack.yml
```

The python script `handler.py` and its analogue `function.R` are the scripts that contains the function. The default function in the template is very simple. This is the file you will need to edit to include your own function. The next sections walk you through how to do this. The `preprocess_params` script is where you can insert code to run checks on your incoming data before it is sent to the function. This is useful as it allows errors to be caught before calling the function itself. The `requirements.txt` and `install_packages.R` scripts should contain the libraries your function requires. If you have other scripts, such as those containing utility functions, you can include them in the `function` folder alongside these other files and source them from the highest level, e.g. `source('function/utils.R')`.
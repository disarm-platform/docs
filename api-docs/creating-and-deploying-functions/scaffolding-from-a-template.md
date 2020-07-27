# Scaffolding from a template

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. Both templates include a very simple function which returns `TRUE`. The instructions assume you want to use either the R or Python version of the DiSARM templates.

You will need [`faas-cli`](https://docs.openfaas.com/cli/install/) and [Docker](https://docs.docker.com/engine/install/) installed.

In your terminal:

1. Create and change into a new folder
2. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
3. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
4. Rename `<function-name>.yml` to `stack.yml`
5. Rename `<function-name>` folder to `function/`
6. Follow instructions to [edit `stack.yml`](editing-stack-yml.md)
7. Check the template builds with `faas build`

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


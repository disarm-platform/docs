# Scaffolding from a template

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. The instructions assume you want to use one of the DiSARM templates.

You will need `faas-cli` and Docker installed.

In your terminal:

1. Create and change into a new folder
2. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
3. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
4. Check the template builds with `faas build -f <function-name>.yml`

This creates a basic function. Check [editing `stack.yml`](editing-stack-yml.md) for instructions on editing this empty function to make it deployable on OpenFaas.

The folders and files created using our `python-geospatial` template will be something like:

```text
py-new-function
├── handler.py
├── preprocess_params.py
└── requirements.txt
```

and for `r-geospatial`:

```text
r-new-function
├── function.R
├── install_packages.R
└── preprocess_params.R
```


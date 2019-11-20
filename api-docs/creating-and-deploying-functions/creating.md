## Creating a new algorithm

You will need `faas-cli` and Docker installed

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. The instructions assume you want to use one of the DiSARM templates.

In your terminal:

1. Create and change into a new folder
1. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
1. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
1. Check the template builds with `faas build -f <function-name>`

This creates a basic function. Check the [editing `stack.yml` page](api-docs/creating-and-deploying-functions/editing-stack-yml.md) for instructions on editing this empty function to make it deployable on OpenFaas.

The folders and files created using our `python-geospatial` template will be something like: 

```
new-function-py
├── handler.py
├── preprocess_params.py
└── requirements.txt
```

and for `r-geospatial`:

```
new-function-r
├── function.R
├── install_packages.R
└── preprocess_params.R
```

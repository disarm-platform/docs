# Scaffolding from a template

New functions are based on templates. OpenFaas comes with some defaults e.g. for python. We've also built two templates for DiSARM, `python-geospatial` and `r-geospatial`. The instructions assume you want to use one of the DiSARM templates.

You will need `faas-cli` and Docker installed.

In your terminal:

1. Create and change into a new folder
2. Clone the templates with: `faas template pull https://github.com/disarm-platform/faas-templates.git`
3. Choose a name and create a new function with: `faas new --lang python-geospatial <function-name>`
4. Rename `<function-name>.yml` to `stack.yml`
5. Rename `<function-name>` folder to `function/`
6. Follow instructions to [edit `stack.yml`](editing-stack-yml.md)\`\`
7. Check the template builds with `faas build`

The folders and files created using our `python-geospatial` template will be something like:

```text
py-new-function
├── function
│  ├── handler.py
│  ├── preprocess_params.py
│  └── requirements.txt
└── stack.yml

```

and for `r-geospatial`:

```text
py-new-function
├── function
│  ├── function.R
│  ├── install_packages.R
│  └── preprocess_params.R
└── stack.yml

```


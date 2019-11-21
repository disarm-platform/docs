# Versioning algos

## Why version?

If you are actively developing an algorithm, you might find you want more than one version available. Before going further, it's worth checking that a new version is really needed: versions can be useful, but they add mental overhead in both use and maintenance. Be aware that running multiple versions of an algorithm might also result in slower server performance, depending on the way the OpenFaas server is configured. It can also be confusing for users to know which version to access. When possible, aim to keep a single version of an algorithm live, and make sure that any changes you make to it are 'backwards-compatible'

If you decide to have more than one version of an algorithm deployed at the same time, it is important to differentiate them in both the Docker image which is built and pushed to Docker Hub, _and_ also the way the function is deployed to OpenFaas, so they are accessed with different URLs.

## Pick a versioning scheme

You can version using any approach you want: e.g. `v1`, `v2`, etc, or `0.0.1`, `0.0.2`, etc, or `working-version`, `test-version`, etc.

## How to version?

You can always decide to make an entire new function and repository, following the instructions as if you are creating from scratch. When the changes are significant, this can be the right approach. For smaller changes, you will need to edit two things in the `stack.yml` file:

1. The _tag_ of the Docker image, so it is stored remotely with a version number.
2. The _name_ of the function as it is deployed to OpenFaas, so that multiple versions of an algorithm can be accessed through OpenFaas.

### Tagging the Docker image

You can add a _tag_ to a Docker image to specify different versions: e.g. `0.0.1`.

To do this, edit the `stack.yml` file, and change the `image` entry.

* from:

  ```yaml
  ...
  image: disarm/fn-covariate-extractor:0.0.3
  ...
  ```

* to:

  ```yaml
  ...
  image: disarm/fn-covariate-extractor:0.0.4
  ...
  ```

Do `faas build` then `faas push` to build the image and push it onto Docker Hub \(or `faas deploy` to build and push _and_ deploy\)

### Changing the function name

Edit the `stack.yml` file. Look for the entry under the `functions:` header: this is the name used to deploy to OpenFaas, and also what determines the URL to access the function once it is deployed.

To version the function this way, you just edit the name. Note that the name needs to produce a valid URL. For adding version numbers we've found that _underscores_ can be useful: for example, changing `new-function` to `new-function_v1`.

If you're using a semantic versioning scheme for the code and Docker tags \(e.g. `0.1.2`\), you might not need to add every part of the version to the function name, and could instead keep just the _major_ \(first\) part of the version: e.g. instead of `1.3.1` just call the function `my-function_v1`.

```yaml
version: 1.0
 provider:
   name: openfaas
   gateway: https://faas.srv.disarm.io # Changed from `http://127.0.0.1:8080
 functions:
   new-function:
     lang: python
     handler: ./new-function
     image: disarm/new-function:0.0.1 # Changed from `new-function:latest`
```


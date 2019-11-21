# Editing stack.yml

Every function created for OpenFaas requires a configuration file in `yaml` format. The default for a new function is to name the configuration file the same as the function name you give \(e.g. `new-function.yml`\). Naming it `stack.yml` makes it easier for the OpenFaas CLI \(`faas` commands\) to find it.

## Required edits

There are 3 places to edit:

1. `gateway`: 
   * edit to be the URL for the OpenFaas instance
2. `handler`:
   * edit to be `./function`, this is required for our template code to work
3. `image`: 
   * need to prefix with a Docker Hub org or repo you can write to
   * optionally change the `latest` tag to a specific version number

More information on editing the file can be found [in the official docs](https://docs.openfaas.com/reference/yaml/).

## Example of edited file

For example, create a new function with `faas new --lang python new-function` \(see [creating functions](https://github.com/disarm-platform/docs/tree/29b1a875dfd97b9332cd1eae0ce2ea4999205f52/api-docs/creating-and-deploying-functions/api-docs/creating-and-deploying-functions/creating.md)\).

1. Rename `new-function.yml` to `stack.yml`
2. Edit `stack.yml`:
   1. `gateway`: change to `https://faas.srv.disarm.io`
   2. `handler`: change to `./function`
   3. `image`: add Docker Hub org/username `new-function:latest` -&gt; `disarm/new-function:latest`

Your `stack.yml` should then look like

```yaml
version: 1.0
 provider:
   name: openfaas
   gateway: https://faas.srv.disarm.io # Changed from `http://127.0.0.1:8080
 functions:
   new-function:
     lang: python
     handler: ./function
     image: disarm/new-function:0.0.1 # Changed from `new-function:latest`
```


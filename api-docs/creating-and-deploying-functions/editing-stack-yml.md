Every function created for OpenFaas requires a `stack.yml` configuration file. Below we describe any changes that can be made by a user. More information can be found [in the official docs](https://docs.openfaas.com/reference/yaml/)

```yml
provider:
  name: faas # Don't change

  gateway: <GATEWAY_URL>
  # URL of the OpenFaas gateway you want to deploy to. 
  # Can be over-ridden with the `--gateway` flag when
  # deploying, e.g. `faas deploy --gateway 
  # gateway.example.com`

functions:
# Can contain config for multiple functions

  <FUNCTION_NAME>:
  # Name of function, set by e.g. `faas new ...`
    
    lang: <LANGUAGE>
    # The template language, e.g. `dockerfile`

    handler: <HANDLER_PATH>
    # The folder where the function's source code can be found
    
    image: <DOCKER_HUB_IMAGE>
    # The location for the built Docker image, e.g. on DockerHub
```


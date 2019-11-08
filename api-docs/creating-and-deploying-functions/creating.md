# Creating and deploying a new algorithm to OpenFaas


## Creating a new algorithm

If you want to create a new deployable function, following these steps.

1. Create a local copy of an existing repo (e.g. [Python sample](https://github.com/disarm-platform/faas-template-python-fn) or [R sample](https://github.com/disarm-platform/faas-template-r-fn)), in the correct language for the new algo.
2. Insert your function code in the relevant script.
3. Change at least these files:
   * `stack.yml`: this describes the Docker image, and the name the function will have when deployed \(don't want to over-write an existing algo\) (see [editing stack.yml](/api-docs/creating-and-deploying-functions/editing-stack-yml.md))
   * the `requirements.txt` or `install_packages.R` files \(or similar\): these are for installing dependencies, and without them, the image won't build
4. Ensure your function runs locally, ideally with some automated testing. Refer to the [Testing and debugging functions page](/api-docs/testing-and-debugging-functions) for more information. 

Note that the prerequisites for deploying might also be useful during the creation steps. See [here](/api-docs/creating-and-deploying-functions/deploying.md)



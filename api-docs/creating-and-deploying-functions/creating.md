# Creating and packaging an algorithm for OpenFaas

## Creating a new algorithm

1. Create a local copy of an existing repo \(e.g. [Python sample](https://github.com/disarm-platform/faas-template-python-fn) or [R sample](https://github.com/disarm-platform/faas-template-r-fn)\), in the correct language for the new algo.
2. Change at least these files:
   * `stack.yml`: this describes the Docker image, and the name the function will have when deployed \(don't want to over-write an existing algo\) \(see [editing stack.yml](editing-stack-yml.md)\)
   * the `requirements.txt` or `install_packages.R` files \(or similar\): these are for installing dependencies, and without them, the image won't build
3. Ensure your function runs locally, ideally with some automated testing. Refer to the [Testing and debugging functions page](../testing-and-debugging-functions/) for more information. 

Note that the prerequisites for deploying might also be useful during the creation steps. See [here](deploying.md)


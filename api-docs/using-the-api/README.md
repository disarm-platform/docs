# Using the algorithms API

_This page is intended to help developers, or public health officers with understanding of HTTP requests. For details on the user interfaces as a way to interact with algorithms, please see_ [_User interfaces_](using-user-interfaces-to-access-the-algorithms.md)_._

The major benefit of the API approach is being able to call the algorithms from any system that can send an [HTTP request](https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_message). This is often referred to as _integrating_ the API into another system. Integration will usually require basic technical skills, but these are very generic, transferable skills, and not tied to the algorithm.

From the developer's perspective, the basic procedure is to:

1. prepare a _request_, usually containing data from the source system
2. send the _request_ to the DiSARM API
3. wait for the processing to complete
4. receive the _response_, and do something with this 

We describe the detail of an integration example in [DHIS2 integration example](dhis2-integration-example.md).


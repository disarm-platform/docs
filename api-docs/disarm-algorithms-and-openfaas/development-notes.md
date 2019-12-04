# Development notes

## Timeouts

What we've learned:

* If we're finding lots of 502 errors, they seem to be related to timeouts
* Timeouts can \(must?\) be set on both the gateway and the function
* We think the read/write timeouts are 'cumulative' - i.e. must all be measured from the same zero.
* We've update the `openfaas-docker.yml` file for DiSARM to extend default timeouts of 5m up to 15m
* Without a timeout set explicitly on a function, it defaults to 5s


# Troubleshooting functions

Sometimes they just don't work... Here's what you can try.

1. Make sure the built container works fine on your local machine: not just the code, but the actual container. See the section on [Running containers](https://docs.disarm.io/api-docs/using-the-api).
2. Remove the function from OpenFaas and redeploy \(`faas rm` then `faas up` or `faas deploy`\). This will give you the best chance of figuring out if you have a reproducible problem. Just redeploying might not help.
3. There are debug logs for each container, but they’re turned off by default. If we turn them on, they log _all_ input and output, so we want to be careful about using them. Note: if you're working only with URLs for data files \(rather than serialising data into the requests\), it's easier when you log everything out.
4. If you are getting HTTP `502` errors, this might be caused by timeouts. Check the [OpenFaaS docs](https://docs.openfaas.com/deployment/troubleshooting/#timeouts) for the places where timeouts can be set.


# Troubleshooting functions

Sometimes they just don't work... Here's what you can try.

1. Make sure the built container works fine on your local machine: not just the code, but the actual container. See [testing functions locally](https://github.com/disarm-dev/functions-for-openfaas/wiki/Testing-a-function-locally).
1. Remove the function from OpenFaas and immediately redeploy (`faas up` or `faas deploy`). This will give you the best chance of figuring out if you have a reproducible problem. Just redeploying might not help.
3. There are debug logs for each container, but they’re turned off by default. If we turn them on, they log _all_ input and output, so we want to be careful about using them. Also, the log viewer in Portainer always has them out of date order, so only useful straight after removing+redploying (see #1 above). 
	- Note: if you're working only with URLs, then it's easier when you log everything out.
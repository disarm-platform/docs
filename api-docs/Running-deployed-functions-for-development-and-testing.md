# Running deployed functions for development and testing

You run a function by issuing an HTTP request. There are many ways to construct and send the request. In this page, we're going to work through a few different ways and tools to create and send testing requests. Correctly sending and handling requests inside [client applications](/api-docs/Running-deployed-functions-in-production.md) - i.e. the real users of the functions - is a separate topic!

In general you need a _URL_ and some _parameters_. The _URL_ refers to the function, while the _parameters_ describe the . All the DiSARM functions are designed to take _parameters_ sent as JSON. See [below](#JSON) for info on making and using JSON correctly.

### Synchronous vs asynchronous, scaling, etc

The normal simple requests described below use a _synchonrous_ approach: the request will start the function running, and the connection will stay open until the run is complete (either successfully or not). One problem with a synchronous request, especially a long-running one, is that if the connection drops, the run is discarded and the result lost.

An alternative to _synchronous_ requests is _asynchronous_ requests. With these, you must specify a 'return address', or somewhere the result can be sent, and once the run is complete, you go and check the 'return address' location. More details on this [are below](#advanced-requests-async).

Multiple requests to the same function at the same time are supposed to trigger an automatic scaling of the function containers, up to a specified maximum number of copies (defaults to 5). Additional requests will then either back-up, waiting for completion of the currently-running functions, or will return an error saying there's no function available.


### Timeouts

**Gateway and function timeouts**
We try to never let any function run forever - even (especially!) if it's crashing. There are timeouts set in many places to try to avoid this:
- There's a default timeout of 5 minutes set on the gateway itself: this is currently the maximum time any one function should be able to run for. 
- Each function might also have its own set of timeouts (for reading from client, for writing back to client, and for total execution time).
If the function exceeds these timeouts, you'll get 

### Responses

These are usually comprised of a _header_ and a _body_. The _header_ will always contain a [status code](https://httpstatuses.com). We want it to be `200` - which indicates a success. If it fails, we'll expect it to give back a `4xx` or `5xx` type of error - watching these can help figure out what's going wrong.

We try to make sure that if the function fails, it's able to send back a useful response. For normal synchronous calls (using the `/function` endpoint), a successful function run will return a `200` status code.

### Notes on examples
- The examples below use [httpie](https://httpie.org): you'll need to install it, but it's easier to use than `curl`, and defaults to printing headers and better-formatted response. Some examples of [curl](#examples-using-curl) are given at the bottom.
- The commands below starting with a `$` are to type/paste straight into a terminal (without the first `$`).

## Tools to help constructing and sending requests

We strongly recommend getting one of the desktop tools. They make it easiest to create the requests, and also to save and re-use the requests.

### Desktop tools
- [Insomnia](https://insomnia.rest/) - Free
- [Postman](https://www.getpostman.com/) - Free
- [Paw](https://paw.cloud) - Not free, but very powerful

### Command-line tools
- [httpie](https://httpie.org)
- [curl](https://curl.haxx.se)


## Sending a simple requests from command line

We'll use the `longrun` function, which is really only for testing use, and simply starts counting for a default of 10 seconds (configurable with a `delay_s` parameter):

### Simplest request

```bash
$ http POST https://faas.srv.disarm.io/function/longrun
```

### Simplest request with a single parameter

Adding a parameter to get it to wait only 1 second:

```bash
$ http POST https://faas.srv.disarm.io/function/longrun \
    'Content-Type':'application/json' \
    delay_s:=0.5
```

### Sending a request file using `cat`

If you have a valid JSON file which contains a complete request, you can send this 

```bash
$ cat req.json | http https://faas.srv.disarm.io/function/longrun
```

### Sending a request using `echo`

```bash
$ echo '{"delay_s": 0.5}' | http https://faas.srv.disarm.io/function/longrun
```

## JSON
JSON is a format for representing/saving/transmitting data. Writing valid JSON is not immediately straightforward. Also, files (especially large ones) can get hard to view and understand. 

### Watch out for
- **types**: a string of `"1"` is not the same as the numeric value of `1`.
- **punctuation**: the double-quote marks, square-braces, curly-braces and commas are ALL important
- **it's 'all-or-nothing'**: a final missing brace can invalidate the whole JSON, and make it hard for the linter to point you in the right direction

### Tools

- **Text editors:** Most text editors can handle JSON, and some way to 'pretty print' or format a valid JSON file. This is a useful way to create sample requests, as well as review result files.
- **Browser extensions**: search for something like [JSON Viewer](https://chrome.google.com/webstore/detail/json-viewer/gbmdgpbipfallnflgajpaliibnhdgobh) to view and explore JSON better in a browser
- **Online 'linters'**: 'linter' like [JSON Lint](https://jsonlint.com) can tell you straightaway if you're trying to send valid JSON or not (but not necessarily _where_ the problem is...)
- **Online viewers**: http://jsonviewer.stack.hu or similar can be useful ways to view and explore JSON
- **Command-line**: things like [`jq`](https://stedolan.github.io/jq), [`fx`](https://github.com/antonmedv/fx) or [`gron`](https://github.com/tomnomnom/gron) are very powerful and quick, but they're harder to use


## Examples using `curl`

For reference (and these might be out-of-date or not match the examples above)

Simplest request:
```bash
$ curl -X POST https://faas.srv.disarm.io/function/longrun
```

Simplest request with single parameter (also the `echo` example above)
```bash
$ curl -X POST" "https://faas.srv.disarm.io/function/longrun" \
    -H 'Content-Type: application/json' \
	-d '{"delay_s": 0.5}'
```

Use request from a file
```bash
curl -X POST https://faas.srv.disarm.io/function/longrun \
	--data-binary '@./req.json'
```

## Advanced requests (async)

The OpenFaas function gateway also lets us send requests _asynchronously_. There are 3 differences with the _synchronous_ approach used so far:
1. The endpoint used is different: `/async-function` instead of `/function`
2. You must provide a 'return address': this is sent as an additional `X-Callback-Url` header
3. The initial request will return `202 - Accepted` response very quickly, but no further information - you'll need to check the 'return address' you provided to see if there's a response.

### Async example

Using the [Pipedream](pipedream.com) service (see below for alternatives), we get `https://enkifhiljb74k.x.pipedream.net` as a URL we can use as our 'return address'. Adding that as a header, and changing the endpoint to `/async-function`, the request becomes:

```bash
http https://faas.srv.disarm.io/async-function/longrun \
	delay_s:=1 \
	X-Callback-Url:https://enkifhiljb74k.x.pipedream.net
```

This returns the following response:
```http
HTTP/1.1 202 Accepted
```

We can then check the Pipedream request viewer page https://pipedream.com/r/enkifhiljb74k/1I4vfdikddbaFst91yN5Y98NQW6 to see what's been posted.

### Failing functions

A function that runs and then fails won't post anything to the 'return address'. Since the initial request will always return `202 - Accepted`, you'll not be able to find out what happened, without checking the specific container logs (assuming the container is configure for debug logging!).

### Request-testing services

The following are all free ways to get an 'endpoint' you can use as the `X-Callback-Url` above.
- [Beeceptor](https://beeceptor.com) - simple and quick, but doesn't persist results when browser window closes
- [Pipedream](https://pipedream.com) - great, but sometimes weirdly erratic and slow to load the website initially, but stores responses for a while
- [http://req](https://httpreq.com) - newer, not so good as others, might need to reload page if can't see requests
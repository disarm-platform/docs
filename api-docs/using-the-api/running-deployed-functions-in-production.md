# Running deployed functions in production

The basics of how to call the functions in a live production setting. There are more details on the requests and how to use them for [testing and development](../testing-and-debugging-functions/running-deployed-functions-for-development-and-testing.md).

## Expect the unexpected

> Expect that any network request will fail

Make sure you can handle any network failures, that you display a message to the user, etc.

## Sending requests

You can send either _synchronous_ or _asynchronous_ requests. The first is simpler, but might fail with long-running requests. The second is more robust, but requires some extra steps to retrieve the result.

## Python

### Synchronous

Send a request and wait for the response:

```python
import requests
import json


response = requests.post(
    url="https://faas.srv.disarm.io/function/longrun",
    headers={
        "Content-Type": "application/json; charset=utf-8",
    },
    data=json.dumps({
        "delay_s": 0.5
    })
)
print('Response HTTP Status Code: {status_code}'.format(
  status_code=response.status_code))
print('Response HTTP Response Body: {content}'.format(
  content=response.content))
```

### Asynchronous

You'll need an endpoint to receive the eventual result - this needs to be publicly available and able to receive `POST` requests.

Send a request and ask for the result to be posted to `https://enng15e09rp2.x.pipedream.net`:

```python
import requests
import json


response = requests.post(
    url="https://faas.srv.disarm.io/async-function/longrun",
    headers={
        "X-Callback-Url": "https://enng15e09rp2.x.pipedream.net",
        "Content-Type": "application/json; charset=utf-8",
    },
    data=json.dumps({
        "delay_s": 0.5
    })
)
print('Response HTTP Status Code: {status_code}'.format(
    status_code=response.status_code))
```

## R

### Synchronous

Send a request and wait for the response:

```r
library(httr)
library(geojsonio)

    response <-
      httr::POST(
        url = "https://faas.srv.disarm.io/function/longrun",
        body = as.json(list(delay_s = 0.5)),
        content_type_json()
      )

# Get status code      
response$status_code

# Get contents of the response
content(response)
```


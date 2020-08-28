# Running containerized algorithms

## Running using a curl request

Once you have a container running and listening on port 8080, you can interact with it. The simplest way to do this is using a `curl` request from the command line. To do this, you will need to open a **second terminal window** and send an HTTP request to `localhost:8080` e.g. 

* ```bash
  curl --request 'POST' 'http://localhost:8080' --max-time 60 -d @function/test_req.json
  ```
* This request should make the first terminal print out something like `2020/03/04 07:22:58 Forking fprocess.`
* Assuming it doesn't timeout or crash, your second terminal should contain the successful response, while the first should contain some logging, or at least the error if it crashes.

## Running using code

Containerized algorithms can also be run from a script. For example, assuming you have started the container with an algorithm that requires a JSON with a single numeric field called `input_value` , in Python the code would be:

```python
import requests
import json


response = requests.post(
    url="http://localhost:8080",
    headers={
        "Content-Type": "application/json; charset=utf-8",
    },
    data=json.dumps({
        "input_value": 0.5
    })
)
print('Response HTTP Status Code: {status_code}'.format(
  status_code=response.status_code))
print('Response HTTP Response Body: {content}'.format(
  content=response.content))
```

Similarly, in R, the code would be:

```r
library(httr)
library(geojsonio)

    response <-
      httr::POST(
        url = "http://localhost:8080",
        body = as.json(list(input_value = 0.5)),
        content_type_json()
      )

# Get status code      
response$status_code

# Get contents of the response
content(response)
```


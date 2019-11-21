# Creating and packaging an algorithm in Python

\(Based on the R version, which is better\)

To create a function that you can deploy as an API using the DiSARM resources, the most important thing to understand is how to get data in and out of your function.

## Getting data in and out of your function

When working in Python, you can use a range of possible data formats and classes, including vectors, data frames, dics etc. etc. With deployed functions, you are much more restricted. OpenFaas uses something called _standard in_ and _standard out_. This essentially means a continuous string of values/characters. Fortunately, JSON can be streamed as standard in/out. If you are not familiar with JSON, it is essentially a text format, which can contain some structure.

For example, let's imagine you are writing a function which allows the user to pass in a vector of values in meters and get back the elevation in feet. The user would therefore have to pass in a JSON object with these values and would receive back a JSON object with the answers. You might therefore specify that the user pass in a JSON object with the field `meters` containing the values they want to convert. An example JSON might look like this:

```javascript
{
    "meters": 250
}
```

This JSON will be read into your function in a `dict` called `params`. i.e. you will be able to access these values inside the function as `params['meters']`. Let's open up the template function and make the necessary edits to return elevation in feet.

```python
def handler(params): 
  # run function and catch result
  result = params['meters'] * 3.28
  return result
```

Notice that in the above example, we are just returning the value in feet. If you want to name your output, or if we were returning multiple objects, these should be packaged in a named `dict`. For example, if we wanted the function to return both the feet and yards:

```python
def handler(params):
  # run function and catch result

  feet = params['meters'] * 3.28

  return(dict(feet = feet,
                yards = feet * 3))
```

This will return the following JSON to the user

```javascript
{
    "feet": 820.0,
    "yards": 2460
}
```

Now we have the core function written, we need to write some tests to handle erroneous inputs and to return useful error messages to the user. These tests should live in the `preprocess_params.py` file. Here is an example test and the corresponding error message. You may be able to think of many more

```python
def preprocess(params: dict):
  if params['meters'] is None:
       raise ValueError('Must provide a value for "meters"')
 
```

If your function requires any packages, you can include these in the `requirements.txt` file, and they will be installed as the image is being built.

Once you've finished your model, you can test the function. A good way to do this is to create a test request file. We use the convention `test_req.json` as a way to identify this file. This might look like:

```javascript
{
    "meters": 250
}
```

## Test your function

Create a `test_req.json` file. You can test the function from the command line, e.g.

```bash
cat test_req.json | Rscript main.R
```

You can also just feed the function raw JSON, e.g.

```bash
cat {"meters": } | Rscript main.R
```

This is a good way to test the error messages, e.g.

```bash
cat {"meters": "two hundred"} | Rscript main.R
```

Once you're confident the function is behaving properly, you can build and test the container. See [here](https://docs.disarm.io/api-docs/testing-and-debugging-functions/testing-local-function-containers) for instructions.


# Creating and packaging an algorithm in Python

## Getting data in and out of your function

When working in Python, you can use a range of possible data formats and classes, including vectors, data frames, `dict` etc. etc. The data coming in and out of the function needs to be serialisable to JSON. \(See the [basics of writing containerised functions](basics-of-writing-a-function.md) for more info\)

For example, let's imagine you are writing a function which allows the user to pass in a value in meters and get back the elevation in feet. The user would therefore have to pass in a JSON object with the value and would receive back a JSON object with the answers. You might therefore specify that the user pass in a JSON object with the field `meters` containing the values they want to convert. An example JSON might look like this:

```javascript
{
    "meters": 250
}
```

This JSON will be read into your function in a `dict` called `params`. i.e. you will be able to access it inside the function as `params['meters']`. Let's open up the template function and make the necessary edits to return elevation in feet.

```python
def run_function(params): 
  # run function and catch result
  result = params['meters'] * 3.28
  return result
```

Notice that in the above example, we are just returning the value in feet. If you want to name your output, or if we were returning multiple objects, these should be packaged in a named `dict`. For example, if we wanted the function to return both the feet and yards:

```python
def run_function(params):
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

The best way to test your function is to test it running in the container. This then mimics the environment others will interact with when running your function. To do this, follow the steps outlined in building, starting and running containerized algorithms in the 'Running algorithms' section.


# Creating a function in R

If you are not familiar with the basics of creating a function in R, you should check out Hadley Wickham's [guide](http://adv-r.had.co.nz/Functions.html#function-components). To create a function that you can deploy as an API using the DiSARM resources, the most important thing to understand is how to get data in and out of your function. 

## Getting data in/out of your function

When working in R, you can use a range of possible data formats and classes, including vectors, data frames, `sf` objects etc. etc. With deployed functions, you are much more restricted. OpenFaas uses something called *standard in* and *standard out*. This essentially means a continuous string of values/characters. Fortunately, JSON can be streamed as standard in/out. If you are not familiar with JSON, it is essentially a text format, which can contain some structure. 

For example, let's imagine you are writing a function which allows the user to pass in a vector of values in meters and get back the elevation in feet. The user would therefore have to pass in a JSON object with these values and would receive back a JSON object with the answers. You might therefore specify that the user pass in a JSON object with the field `meters` containing the values they want to convert. An example JSON might look like this:

```
{
    "meters": [250, 280, 290]
} 
```

This JSON will be read into your function in a `list` called `params`. i.e. you will be able to access these values inside the function as `params$meters` or more specifically `params[['meters']]`. Let's open up the template R function and make the necessary edits to return elevation in feet.

```
function(params) {
  # run function and catch result

  result = params[['meters']] * 3.28

  return(result)
}
```

Notice that in the above example, we are just returning the vector of values in feet. If you want to name your output, or if we were returning multiple objects, these should be packaged in a named list. For example, if we wanted the function to return both the feet and yards:

```
function(params) {
  # run function and catch result

  feet = params[['meters']] * 3.28

  return(list(feet = feet,
                yards = feet * 3))
}
```

This will return the following JSON to the user

```
{
    "feet": [820.0, 918.4, 951.2],
    "yards": [273.3333, 306.1333, 317.0667]
}
```

Now we have the core function written, we need to write some tests to handle erroneous inputs and to return useful error messages to the user. These tests should live in the `preprocess_params.r` file. Here is an example of two tests and the corresponding error messages. You may be able to think of many more

```
function(params) {
  # Individual check for each parameter
  if (is.null(params[['meters']])) {
    stop('Missing `meters` parameter')
  }
  if (!is.numeric(params[['meters']])) {
    stop('Parameter `number` is not numeric')
  }
}
```

If your function requires any packages, you can include these in the `install.packages.r` file. In this case, we don't need any functions beyond those available in base R so we can leave this file untouched.

Once you've finished your model, you can test the function. A good way to do this is to create a test request file. We use the convention `test_req.json` as a way to identify this file. This might look like:

```
{
    "meters": [250, 280, 290]
} 
```

## Test your function

Create a `test_req.json` file. You can test the function from the command line, e.g.

```
cat test_req.json | Rscript main.R
```

You can also just feed the function raw JSON, e.g.

```
cat {"meters": [250, 280, 290]} | Rscript main.R
```

This is a good way to test the error messages, e.g.

```
cat {"meters": [250, "two hundred", 290]} | Rscript main.R
```

Once you're confident the function is behaving properly, you can build and test the container. See [here](https://docs.disarm.io/api-docs/testing-and-debugging-functions/testing-local-function-containers) for instructions. 

## Dealing with spatial data

If your function requires spatial data (vector, raster) you can still pass these into your function using JSON. For example, let's imagine you are writing a function to identify which two points are closest to each other. You can specify that the user passes in a GeoJSON called `points` and the function will return a JSON with the indeces of those nearest each other. The first option is for `points` to be a URL to the GeoJSON, e.g.

```
{
    "points": "https://www.dropbox.com/s/18kw35g1su1iuus/three_test_points.json?dl=1"
}
```

Within your function, you can then use packages such `sf` to read this GeoJSON from URL into memory, e.g.

```
points <- st_read(params$points)
```

The second option is for the user to specify the GeoJSON, e.g.

```
{
        points: {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "properties": {},
          "geometry": {
            "type": "Point",
            "coordinates": [
              26.564941406249996,
              -17.329664329425047
            ]
          }
        },
        {
          "type": "Feature",
          "properties": {},
          "geometry": {
            "type": "Point",
            "coordinates": [
              23.4228515625,
              -19.797717490704724
            ]
          }
        },
        {
          "type": "Feature",
          "properties": {},
          "geometry": {
            "type": "Point",
            "coordinates": [
              26.510009765625,
              -18.28151823530889
            ]
          }
        }
      ]
    }
}
```

To read this into memory, you have to tell R it is JSON. e.g.

```
points <- st_read(as.json(params$points))
```

For raster data, we can use the same approach. The user can either pass in a URL to a raster file which can be read into memory with the `raster` function from the `raster ` package, e.g. if the name of the raster object to be passed in is called `input_raster`, our input JSON would look like this:

```
{
    "input_raster": "https://www.dropbox.com/s/mwjpdzxyu6csuss/swz_pop.tif?dl=1"
}
```

And then in R

```
r <- raster(params$input_raster)
```

## Getting GeoJSON out of your function

If you want your function to return a GeoJSON, you can use the `geojson_list` function when you return the object. This puts the spatial object into a format which can then be easily returned as JSON to the user. For example, let's write a function that take an input GeoJSON `points` and simply adds a new field called `new_field`:

```
function(params) {

    points <- st_read(params$points)

    points$new_field <- "I'm new"

    return(geojson_list(points))

}
```

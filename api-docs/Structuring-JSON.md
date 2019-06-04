# Structuring JSON

Users expect to handle JSON as an array of objects, not arrays of values. We'll need to make all our functions work with the first of these, for both _input_ and _output_. 

**GOOD**:

```json
[
  {
    "ID": 11,
    "value_1": 12,
    "value_2": 13
  },
  {
    "ID": 21,
    "value_1": 22,
    "value_2": 23
  }
]
```

**BAD**:

```json
{
  "ID": [
    11,
    21
  ],
  "value_1": [
    12,
    22
  ],
  "value_2": [
    13,
    23
  ]
}
```

Spatial vector data (points and polygons) are handled using GeoJSON FeatureCollections. GIS software and some online tools such as [geojson.io](geojson.io) can be used to create GeoJSON from shapefiles. Below is an example of a single point with 1 `country` attribute. 

```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {"country": "DRC"},
      "geometry": {
        "type": "Point",
        "coordinates": [
          23.203125,
          -7.01366792756663
        ]
      }
    }
  ]
}
```

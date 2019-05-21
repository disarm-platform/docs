# Structuring JSON

Users expect to handle JSON as an array of objects, not arrays of values. We'll need to make all our functions work with the first of these, for both _input_ and _output_. 

**GOOD**:

```json
[
  {
    "lat": 11,
    "lng": 12,
    "value": 13
  },
  {
    "lat": 21,
    "lng": 22,
    "value": 23
  }
]
```

**BAD**:

```json
{
  "lat": [
    11,
    21
  ],
  "lng": [
    12,
    22
  ],
  "value": [
    13,
    23
  ]
}
```



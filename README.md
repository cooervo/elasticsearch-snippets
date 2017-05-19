Elasticsearch snippets
===================
The urls is as follows: `host/index_name/type_name`
http://localhost:9200/nyc_visionzero/logs/_search

Get all `logs`(type name) that contain: "11/08/2016"
GET /nyc_visionzero/logs/_search
```
{
  "query":{
    "query_string": {
      "query": "11/08/2016"
    }
  }
}
```

Get all `logs`that `contributing_factor_vehicle`  = `Unsafe Speed`
```
GET /nyc_visionzero/logs/_search
{
  "query": {
    "term": {
      "contributing_factor_vehicle": "Unsafe Speed"
    }
  }
}
```

Same as above but with pagination:
```
GET /nyc_visionzero/logs/_search
{
  "from": 0,  // The offset from the first result you want to fetch
  "size": 1,  // PAGE SIZE 
  "query": {
    "term": {
      "contributing_factor_vehicle": "Unsafe Speed"
    }
  }
}
```
GET and sort by field `on_street_name` in desc order:
```
GET /nyc_visionzero/logs/_search
{
  "sort": [
    {
      "on_street_name":  "desc"
    }
  ],
  "query": {
    "term": {
      "contributing_factor_vehicle": "Unsafe Speed"
    }
  }
}
```

GET all in range date, and number_of_cyclist_killed > 0, only return fields:   `"latitude"`, `"number_of_cyclist_killed"`

``
{
  "query": {
    "bool": {
      "must": [
        {
          "range": {
            "date": {
              "gt": "18/05/2017",
              "lt": "19/05/2017"
            }
          }
        },
        {
          "range": {
            "number_of_cyclist_killed": {
              "gt": 0
            }
          }
        }
      ]
    }
  },
  "_source": ["latitude", "number_of_cyclist_killed"]
}
```


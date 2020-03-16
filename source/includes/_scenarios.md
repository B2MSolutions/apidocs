
# Scenarios

## Get devices within GPS coordinates

> Devices within 100 meters of GPS Point `51.667789, -1.310762`

```graphql
query {
  devices(filter: { field: "location.position", value: "51.667789, -1.310762 / 100m" }) {
    nodes {
      serialNumber
      group 
    }
  }
}
```

## List devices with pagination
Request the first & second page of devices

```graphql
query {
  devices(limit: 2) {
    nodes {
      id
      manufacturer
      model
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

> The above query returns JSON structured like this:

```json
{
  "data": {
    "devices": {
      "nodes": [
        {
          "id": "wsxcvhfdrtgbdertgt73d",
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 8.04
        },
        {
          "id": "bvghjiuhgvfr67890okjh",
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 12.88
        }
      ],
      "pageInfo": {
        "hasNextPage": true,
        "endCursor": "MTRkNTFkNWE1ZTJhMjUyZTliZTg2NTc3ZmMyNWIzMGI="
      }
    }
  }
}
```

This query demonstrates how to paginate through results from the API.

## List devices with pagination, next page
```graphql
query {
  devices(limit: 2 from: "MTRkNTFkNWE1ZTJhMjUyZTliZTg2NTc3ZmMyNWIzMGI=") {
    nodes {
      id
      manufacturer
      model
    }
    pageInfo {
      hasNextPage
      endCursor
    }
  }
}
```

> The above query returns JSON structured like this:

```json
{
  "data": {
    "devices": {
      "nodes": [
        {
          "id": "mnbvftyujbvfr678iu",
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 8.04
        },
        {
          "id": "hgjtyuiuy6trgd6782",
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 12.88
        }
      ],
      "pageInfo": {
        "hasNextPage": true,
        "endCursor": "ZDRlNjFkOWZkMDUxY2ZlNGViNThmMThiMTU5ZWI4OWE="
      }
    }
  }
}
```

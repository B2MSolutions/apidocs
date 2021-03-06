# Mutations

## Set Device Asset Tag

> `POST` https://graph.elemez.com/graphql

```graphql
mutation {
  setDeviceAssetTag(assetTag: "OXF-001" filter: { field: "serialNumber" value: "4GH78UJ1"}) {
    success
    updated
  }
}
```

> The above mutation returns JSON structured like this:

```json
{
  "data": {
    "setDeviceAssetTag": {
      "success": true,
      "updated": true
    }
  }
}
```

Set the `assetTag` of a single device. If multiple devices are matched based on the filter the mutation will fail.

### Input Fields
| Field      | Type              | Description                                         |
|------------|-------------------|-----------------------------------------------------|
| `assetTag` | `string`          | The asset tag string to be set on the device        |
| `filter`   | [Filter](#filter) | The query to run to find the device that is updated |

### Available Response Fields
| Field     | Type      | Description                                                                     |
|-----------|-----------|---------------------------------------------------------------------------------|
| `success` | `boolean` | Was the update successful                                                       |
| `updated` | `boolean` | Was an update performed; this will be `false` if the given assetTag is the same |

## Set Device Groups

> `POST` https://graph.elemez.com/graphql

```graphql
mutation {
  setDeviceGroups(
    filter: { field: "serialNumber" value: "SA78HY65" }
    groups: "uk,oxfordshire,oxford"
    operation: replace)
  {
    success
    updated
  }
}
```

> The above mutation returns JSON structured like this:

```json
{
  "data": {
    "setDeviceGroups": {
      "success": true,
      "updated": true
    }
  }
}
```

Add/Update/Clear/Replace Device groups.

### Input Fields
| Field       | Type                              | Description                                         |
|-------------|-----------------------------------|-----------------------------------------------------|
| `filter`    | [Filter](#filter)                 | The query to run to find the device that is updated |
| `groups`    | `string`                          | A comma separated list of groups                    |
| `operation` | [GroupOperation](#group-operation) | The operation to execute                            |

### Available Response Fields
| Field     | Type      | Description                                                                     |
|-----------|-----------|---------------------------------------------------------------------------------|
| `success` | `boolean` | Was the update successful                                                       |
| `updated` | `boolean` | Was an update performed; this will be `false` if the groups are unchanged by the operation |

## Add Home Location

> `POST` https://graph.elemez.com/graphql

```graphql
mutation {
  createHomeLocation(data: {
    name: "Heathrow Warehouse 1"
    addressLine1: "Heathrow Airport"
    addressLine2: "Hounslow"
    locality: "London"
    postalCode: "TW6 1EW"
    country: "United Kingdom"
    latitude: 51.470020
    longitude: -0.454296
    radius: 1000
  }) {
    success
    homeLocation {
      id
      position
    }
  }
}
```

> The above mutation returns JSON structured like this:

```json
{
  "data": {
    "createHomeLocation": {
      "success": true,
      "homeLocation": {
        "id": "heathrow warehouse 1",
        "position": "51.470020,-0.454296"
      }
    }
  }
}
```

Add a [HomeLocation](#home-locations) to Elemez for use with location metrics on a device.

### Input Fields
| Field          | Type     | Description                                                                |
|----------------|----------|----------------------------------------------------------------------------|
| `name`         | `string` | Friendly name                                                              |
| `addressLine1` | `string` | Address line 1                                                             |
| `addressLine2` | `string` | Address line 2                                                             |
| `locality`     | `string` | Locality                                                                   |
| `postalCode`   | `string` | Postal code                                                                |
| `country`      | `string` | Country                                                                    |
| `latitude`     | `float`  | Latitude                                                                   |
| `longitude`    | `float`  | Longitude                                                                  |
| `radius`       | `number` | The radius from the center point denoting the boundary of the homelocation |

### Available Response Fields
| Field          | Type                            | Description               |
|----------------|---------------------------------|---------------------------|
| `success`      | `boolean`                       | Was the update successful |
| `homeLocation` | [HomeLocation](#home-locations) | Home Location             |


## Set Device Home Location

> `POST` https://graph.elemez.com/graphql

```graphql
mutation {
  setDeviceHomeLocation(
  homeLocationId: "heathrow warehouse 1"
  filter: { field: "id" value: "6a20525fc89c" }) {
    success
    updated
  }
}
```

> The above mutation returns JSON structured like this:

```json
{
  "data": {
    "setDeviceHomeLocation": {
      "success": true,
      "updated": true
    }
  }
}
```

Set the [HomeLocation](#home-location) on an individual device

### Input Fields
| Field            | Type              | Description                              |
|------------------|-------------------|------------------------------------------|
| `filter`         | [Filter](#filter) | Filter to location the individual device |
| `homeLocationId` | `string`          | The `id` of the HomeLocation             |

### Available Response Fields
| Field     | Type      | Description                                                                     |
|-----------|-----------|---------------------------------------------------------------------------------|
| `success` | `boolean` | Was the update successful                                                       |
| `updated` | `boolean` | Was an update performed; this will be `false` if the given homeLocation is the same |

## Delete Device

> `POST` https://graph.elemez.com/graphql

```graphql
mutation {
  deleteDevice(
  filter: { field: "id" value: "6a20525fc89c" }) {
    success
  }
}
```

> The above mutation returns JSON structured like this:

```json
{
  "data": {
    "deleteDevice": {
      "success": true,
    }
  }
}
```

Delete device

### Input Fields
| Field            | Type              | Description                              |
|------------------|-------------------|------------------------------------------|
| `filter`         | [Filter](#filter) | Filter to location the individual device |

### Available Response Fields
| Field     | Type      | Description                                                                     |
|-----------|-----------|---------------------------------------------------------------------------------|
| `success` | `boolean` | Was the update successful                                                       |

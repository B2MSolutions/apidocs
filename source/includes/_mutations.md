# Mutations

## Set Device Asset Tag

Set the `assetTag` of a single device. If multiple devices are matched based on the filter the mutation will fail.

> `POST` https://api.elemez.com/graphql

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

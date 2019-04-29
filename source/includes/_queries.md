# Queries

## Devices

> `POST` https://api.elemez.com/graphql

```graphql
query {
  devices(limit: 2) {
    nodes {
      model
      manufacturer
      averageDischarge
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
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 8.04
        },
        {
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 12.88
        }
      ]
    }
  }
}
```

### Available Fields
| Field              | Type                                | Description                                                  |
| ---------          | --------                            | -----------                                                  |
| `id`               | `string`                            | unique device identifier                                     |
| `imei`             | `string`                            | the IMEI                                                     |
| `mac`              | `string`                            | Devics MAC Address                                           |
| `serialNumber`     | `string`                            | Devices Serial Number                                        |
| `model`            | `string`                            | Model numbel                                                 |
| `manufacturer`     | `string`                            | Manufacturer name                                            |
| `updated`          | [timestamp](#timestamp)             | Timestamp in milliseconds when device last send data         |
| `firstSeen`        | [timestamp](#timestamp)             | Timestamp in milliseconds when device was initially enrolled |
| `clientVersion`    | `number`                            | Elemez agent version code                                    |
| `group`            | `[string]`                          | Array of group names the device currently belongs to         |
| `averageDischarge` | `float`                             | The average discharge over the last 30 days                  |
| `location`         | [GPS](#gps)                         | GPS..                                                        |
| `smartBattery`     | [SmartBattery](#smart-batteries)     | Smart battery information                                    |
| `sim`              | [Sim](#sim)                         | Sim card details                                             |
| `batteryDischarge` | [DeviceDischarge](#devicedischarge) | Battery discharge information                                |
| `impactDetection`  | [ImpactDetection](#impactdetection) | Impact detection information |

## Smart Batteries

> `POST` https://api.elemez.com/graphql

```graphql
query {
  smartbatteries {
    nodes {
      partNumber
      capacityFactor
      device {
        manufacturer
        model
      } 
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
          "partNumber": "A7654",
          "capacityFactor": 0.94,
          "device": {
            "manufacturer": "Zebra Technologies",
            "model": "TC75x"
          }
        },
        {
          "partNumber": "A8871",
          "capacityFactor": 0.40,
          "device": {
            "manufacturer": "Zebra Technologies",
            "model": "TC75x"
          }
        }
      ]
    }
  }
}
```

### Available Fields
| Field             | Type                    | Description                                          |
| -----             | ----                    | -----------                                          |
| `id`              | `string`                | Unique smart battery ID                              |
| `partNumber`      | `string`                | The part number as given by the battery              |
| `serialNumber`    | `string`                | The battery serial number                            |
| `presentCapacity` | `number`                | The present capacity in `mah` of the battery         |
| `ratedCapacity`   | `number`                | The rated capacity in `mah` of the battery           |
| `capacityFactor`  | `float`                 | Health percentage based on `presentCapacity` and `ratedCapacity` |
| `manfactureDate`  | `string`                | The manufactured date as given by the battery        |
| `updated`         | [Timestamp](#timestamp) | When the smart battery last updated its information |
| `device`          | [Device](#devices)      | The device associated with the smart battery         |

## Groups

> `POST` https://api.elemez.com/graphql

```graphql
query {
  deviceStats {
    nodes {
      count
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
        { "name": "HUB-OX1" },
        { "name": "HUB-RG17" },
        { "name": "HUB-GL7" }
      ]
    }
  }
}
```

### Available Fields
| Field             | Type                    | Description                                          |
| -----             | ----                    | -----------                                          |
| `name`            | `string`                | Group name                                           |

## Device Stats

> `POST` https://api.elemez.com/graphql

```graphql
query {
  deviceStats(filter: { field: "group" value: "Oxfordshire" }) {
    nodes {
      count
    }
  }
}
```

> The above query returns JSON structured like this:

```json
{
  "data": {
    "deviceStats": {
      "nodes": [
        { "count": 12861 }
      ]
    }
  }
}
```

Returns the count of devices matched by the given query

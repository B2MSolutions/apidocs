# Queries

## Devices

> `POST` https://api.elemez.com/graphql

```graphql
query {
  devices(
    limit: 2 
    filter: { field: "deviceUserExperienceRebootStatus" value: "red" }
    sort: { field: "updated" order: desc }) {
    nodes {
      model
      manufacturer
      averageDischarge
      deviceUserExperienceRebootStatus
      smartBattery {
        serialNumber
        capacityFactor
        manufactureDate
      }
      location {
        position
        updated
      }
      sim {
        serialNumber
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
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 8.04,
          "deviceUserExperienceRebootStatus": "red",
          "smartBattery": {
            "serialNumber": "00937482B",
            "capacityFactory": 0.95
            "manufactureDate": "2018-01-05"
          },
          "location": {
            "position": "51.616181,-1.312273",
            "updated": 1557988946000
          },
          "sim": {
            "serialNumber": "164836990773694264"
          }
        },
        {
          "manufacturer": "Panasonic Corporation",
          "model": "FZ-G1",
          "averageDischarge": 12.88
          "deviceUserExperienceRebootStatus": "red",
          "smartBattery": {
            "serialNumber": "7843GJ3",
            "capacityFactory": 0.8
            "manufactureDate": "2017-06-02"
          },
          "location": {
            "position": "51.526214,-0.079549",
            "updated": 1557868921000
          },
          "sim": {
            "serialNumber": "985476129846787128"
          }
        }
      ]
    }
  }
}
```

### Available Fields
| Field                                 | Type                                 | Description                                                                                       |
| ---------                             | --------                             | -----------                                                                                       |
| `id`                                  | `string`                             | unique device identifier                                                                          |
| `imei`                                | `string`                             | the IMEI                                                                                          |
| `mac`                                 | `string`                             | Devics MAC Address                                                                                |
| `serialNumber`                        | `string`                             | Devices Serial Number                                                                             |
| `model`                               | `string`                             | Model numbel                                                                                      |
| `manufacturer`                        | `string`                             | Manufacturer name                                                                                 |
| `assetTag`                            | `string`                             | Asset tag                                                                                         |
| `updated`                             | [timestamp](#timestamp)              | Timestamp in milliseconds when device last send data                                              |
| `firstSeen`                           | [timestamp](#timestamp)              | Timestamp in milliseconds when device was initially enrolled                                      |
| `clientVersion`                       | `number`                             | Elemez agent version code                                                                         |
| `group`                               | `[string]`                           | Array of group names the device currently belongs to                                              |
| `averageDischarge`                    | `float`                              | The average discharge over the last 30 days                                                       |
| `location`                            | [GPS](#gps)                          | Last known location of the device                                                                 |
| `smartBattery`                        | [SmartBattery](#smart-batteries)     | First smart battery's information                                                                 |
| `smartBatteries`                      | \[[SmartBattery](#smart-batteries)\] | All available smart battery information                                                           |
| `sim`                                 | [Sim](#sim)                          | Sim card details                                                                                  |
| `batteryDischarge`                    | [DeviceDischarge](#devicedischarge)  | Battery discharge information                                                                     |
| `impactDetection`                     | [ImpactDetection](#impactdetection)  | Impact detection information                                                                      |
| `homeLocation`                        | [HomeLocation](#home-locations)      | Configured home location                                                                          |
| `customFields`                        | [CustomFields](#custom-fields)       | Custom field processing                                                                           |
| `deviceStatus`                        | [Status](#status)                    | Rollup of all status fields                                                                       |
| `deviceLocationStatus`                | [Status](#status)                    | Rollup of location status fields                                                                  |
| `deviceLocationDistanceStatus`        | [Status](#status)                    | Distance status based on configured distance outside from home location radius                    |
| `deviceLocationTimeStatus`            | [Status](#status)                    | Time status based on configured time outside home location radius                                 |
| `deviceUtilisationStatus`             | [Status](#status)                    | Rollup of utilisation status fields                                                               |
| `deviceUtilisationIdleStatus`         | [Status](#status)                    | Status of device if it is idle for more than the idle configuration threshold                     |
| `deviceUtilisationOutOfContactStatus` | [Status](#status)                    | Status of device if it is out-of-contact for more than the out-of-contact configuration threshold |
| `deviceUserExperienceStatus`          | [Status](#status)                    | Rollup of user experience status fields                                                           |
| `deviceUserExperienceRebootStatus`    | [Status](#status)                    | Status if reboot count is greater than the configured threshold                                   |
| `deviceUserExperienceLowPowerStatus`  | [Status](#status)                    | Status if low power event count is greater than the configured threshold                          |

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
    "smartbatteries": {
      "nodes": [
        {
          "partNumber": "A7654",
          "capacityFactor": 0.94,
          "batteryStatus": "green",
          "device": {
            "manufacturer": "Zebra Technologies",
            "model": "TC75x"
          }
        },
        {
          "partNumber": "A8871",
          "capacityFactor": 0.40,
          "batteryStatus": "red",
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
| Field             | Type                    | Description                                                        |
| -----             | ----                    | -----------                                                        |
| `id`              | `string`                | Unique smart battery ID                                            |
| `partNumber`      | `string`                | The part number as given by the battery                            |
| `serialNumber`    | `string`                | The battery serial number                                          |
| `presentCapacity` | `number`                | The present capacity in `mah` of the battery                       |
| `ratedCapacity`   | `number`                | The rated capacity in `mah` of the battery                         |
| `capacityFactor`  | `float`                 | Health percentage based on `presentCapacity` and `ratedCapacity`   |
| `manfactureDate`  | `string`                | The manufactured date as given by the battery                      |
| `batteryStatus`   | [Status](#status)       | Status based on the batteries health against configured thresholds |
| `updated`         | [Timestamp](#timestamp) | When the smart battery last updated its information                |
| `device`          | [Device](#devices)      | The device associated with the smart battery                       |

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
    "groups": {
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


## Home Locations
> `POST` https://api.elemez.com/graphql

```graphql
query {
  homeLocations {
    nodes {
      id
      name
      latitude
      longitude
      position
      radius
    }
  }
}
```

> The above query returns JSON structured like this:

```json
{
  "data": {
    "homeLocations": {
      "nodes": [
        {
          "id": "didcot",
          "name": "Didcot, Oxfordshire",
          "latitude": 51.608,
          "longitude": -1.2448,
          "position": "51.608, -1.2448",
          "radius": 500
        },
        {
          "id": "london",
          "name": "London",
          "latitude": 51.5074,
          "longitude": -0.1278,
          "position": "51.5074, -0.1278",
          "radius": 100
        },
        {
          "id": "melbourne",
          "name": "Melbourne",
          "latitude": -37.8136,
          "longitude": 144.9631,
          "position": "-37.8136, 144.9631",
          "radius": 100
        }
      ]
    }
  }
}
```

Returns a list of configured home locations

### Available Fields
| Field       | Type        | Description                                                                          |
| -----       | ----        | -----------                                                                          |
| `id`        | `string`    | Unique identifier                                                                    |
| `name`      | `string`    | Home location friendly name                                                          |
| `latitude`  | `float`     | Latitude                                                                             |
| `longitude` | `float`     | Longitude                                                                            |
| `position`  | `gps point` | Concatenated latitude &amp; longitide. `51.61492, -1.311916`                         |
| `radius`    | `number`    | Radius around the gps point in meters that defines the boundary of the home location |

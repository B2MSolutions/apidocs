# Queries

## Devices

> `POST` https://graph.elemez.com/graphql

```graphql
query {
  devices(
    limit: 2
    filter: { field: "deviceStatus" value: "red" }
    sort: { field: "updated" order: desc }) {
    nodes {
      model
      manufacturer
      averageDischarge
      deviceStatus
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
          "deviceStatus": "red",
          "smartBattery": {
            "serialNumber": "00937482B",
            "capacityFactory": 0.95,
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
          "averageDischarge": 12.88,
          "deviceStatus": "red",
          "smartBattery": {
            "serialNumber": "7843GJ3",
            "capacityFactory": 0.8,
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
| `mac`                                 | `string`                             | Device's MAC Address                                                                                |
| `serialNumber`                        | `string`                             | Device's Serial Number                                                                             |
| `model`                               | `string`                             | Model number                                                                                      |
| `manufacturer`                        | `string`                             | Manufacturer name                                                                                 |
| `assetTag`                            | `string`                             | Asset tag                                                                                         |
| `updated`                             | [timestamp](#timestamp)              | Timestamp in milliseconds when device last send data                                              |
| `firstSeen`                           | [timestamp](#timestamp)              | Timestamp in milliseconds when device was initially enrolled                                      |
| `clientVersion`                       | `number`                             | Elemez agent version code                                                                         |
| `group`                               | `[string]`                           | Array of group names the device currently belongs to                                              |
| `averageDischarge`                    | `float`                              | The average discharge over the last 30 days                                                       |
| `averageDischargeStatus`              | [Status](#status)                    | The average discharge status                                                                      |
| `location`                            | [GPS](#gps)                          | Last known location of the device                                                                 |
| `smartBattery`                        | [SmartBattery](#smart-batteries)     | First smart battery's information                                                                 |
| `smartBatteries`                      | \[[SmartBattery](#smart-batteries)\] | All available smart battery information                                                           |
| `sim`                                 | [Sim](#sim)                          | Sim card details                                                                                  |
| `batteryDischarge`                    | [DeviceDischarge](#devicedischarge)  | Battery discharge information                                                                     |
| `homeLocation`                        | [HomeLocation](#home-locations)      | Configured home location                                                                          |
| `customFields`                        | [CustomFields](#custom-fields)       | Custom field processing                                                                           |
| `deviceStatus`                        | [Status](#status)                    | Rollup of all status fields                                                                       |

## Smart Batteries

> `POST` https://graph.elemez.com/graphql

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

## Custom Events

> `POST` https://graph.elemez.com/graphql

```graphql
query {
  customEvents(
    limit: 2
    filter: { field: "name" value: "boot_time" })
    nodes {
    utc
    device {
      serialNumber
    }
    customFields {
      name
      value
    }
  }
}
```

> The above query returns JSON structured like this:

```json
{
  "data": {
    "customEvents": {
      "nodes": [
        {
          "utc": "1563173408750",
          "device": {
            "serialNumber": "JKU876556G"
          },
          "customFields": [
            {
              "name": "bootDuration",
              "value": "99522"
            }
          ]
        },
        {
          "utc": "1563141948679",
          "device": {
            "serialNumber": "998JUHY765"
          },
          "customFields": [
            {
              "name": "bootDuration",
              "value": "99422"
            }
          ]
        }
      ]
    }
  }
}
```

### Available Fields
| Field          | Type                                    | Description                              |
| ---------      | --------                                | -----------                              |
| `id`           | `string`                                | unique device identifier                 |
| `source`       | `string`                                | Event source                             |
| `sender`       | `string`                                | Event sender                             |
| `type`         | `string`                                | Event type                               |
| `name`         | `string`                                | Event name                               |
| `utc`          | [Timestamp](#timestamp)                 | When the event was created               |
| `received`     | [Timestamp](#timestamp)                 | When Elemez received the event           |
| `raised`       | [Timestamp](#timestamp)                 | When the event was raised on the device  |
| `deviceInfo`   | [DeviceInfo](#device-info)               | Searchable & sortable device information |
| `device`       | [Device](#device)                       | The associated device                    |
| `customFields` | [CustomEventField](#custom-event-field) | Custom fields associated with the event  |

## Groups

> `POST` https://graph.elemez.com/graphql

```graphql
query {
  groups {
    nodes {
      name
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

> `POST` https://graph.elemez.com/graphql

```graphql
query {
  devicesStats(filter: { field: "group" value: "Oxfordshire" }) {
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
    "devicesStats": {
      "nodes": [
        { "count": 12861 }
      ]
    }
  }
}
```

Returns the count of devices matched by the given query

### Available Fields
| Field   | Type     | Description              |
| -----   | ----     | -----------              |
| `count` | `number` | Count of matched records |

## Smart Battery Stats

> `POST` https://graph.elemez.com/graphql

```graphql
query {
  smartBatteriesStats(filter: { field: "deviceInfo.group" value: "Oxfordshire" }) {
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
    "smartBatteriesStats": {
      "nodes": [
        { "count": 12861 }
      ]
    }
  }
}
```

Returns the count of devices matched by the given query

### Available Fields
| Field   | Type     | Description              |
| -----   | ----     | -----------              |
| `count` | `number` | Count of matched records |

## Home Locations
> `POST` https://graph.elemez.com/graphql

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
          "name": "Didcot",
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
| `position`  | `gps point` | Concatenated latitude &amp; longitude. `51.61492, -1.311916`                         |
| `radius`    | `number`    | Radius around the gps point in meters that defines the boundary of the home location |

## Device Events
> `POST` https://graph.elemez.com/graphql

```graphql
query {
    deviceEvents(
        filter: { field: "group" value: "Oxfordshire" }
    ) {
        nodes {
            name
            category
            utc
            local
            deviceInfo {
                id
                serialNumber
                assetTag
                group
                homeLocationId
            }
        }
        applicationInfo {
            name
            version
        }
        oldBatteryInfo {
            serialNumber
        }
        newBatteryInfo {
            serialNumber
        }
    }
}
```


> The above query returns JSON structured like this:

```json
{
    "data": {
        "deviceEvents": {
            "nodes": [
                {
                    "category": "application",
                    "name": "applicationInstalled",
                    "utc": 1605006049000,
                    "local": 1604998849000,
                    "deviceInfo": {
                        "id": "8f138afdfde8fea7186dd2af006bb9d0",
                        "serialNumber": "ABC123",
                        "assetTag": "DLE9901",
                        "group": [ "oxfordshire" ],
                        "homeLocationId": "oxfordshire"
                    },
                    "applicationInfo": {
                        "name": "Microsoft Teams",
                        "version": "12.2.5.12222"
                    }
                },
                {
                    "category": "battery",
                    "name": "batteryChanged",
                    "utc": 1605006049000,
                    "local": 1604998849000,
                    "deviceInfo": {
                        "id": "8f138afdfde8fea7186dd2af006bb9d0",
                        "serialNumber": "ABC123",
                        "assetTag": "DLE9901",
                        "group": [ "oxfordshire" ],
                        "homeLocationId": "oxfordshire"
                    },
                    "oldBatteryInfo": {
                        "serialNumber": "JJD99877"
                    },
                    "newBatteryInfo": {
                        "serialNumber": "XXP99921"
                    }
                }
            ]
        }
    }
}
```

Returns a list of Events generated from a device

| Field            | Type                                 | Related Event Name                                                   | values                                                | Description                               |
| --               | --                                   | -                                                                    | -                                                     | -                                         |
| `category`       | `string`                             | n/a                                                                  | [EventCategories](#device-event-categories-amp-names) | A top level category for the event        |
| `name`           | `string`                             | n/a                                                                  | [EventNames](#device-event-categories-amp-names)      | Event name                                |
| `deviceInfo`     | [DeviceInfo](#device-info)           | n/a                                                                  | n/a                                                   | Searchable & sortable device information  |
| `local`          | [Timestamp](#timestamp)              | n/a                                                                  | n/a                                                   | Event generation time - Device local time |
| `utc`            | [Timestamp](#timestamp)              | n/a                                                                  | n/a                                                   | Event generation time - UTC time          |
| `applicationInfo` | [ApplicationInfo](#application-info) | `applicationInstalled` `applicationUpdated` `applicationUninstalled` | n/a                                                   | Application info                          |
| `oldBatteryInfo` | [BatteryInfo](#battery-info)         | `batteryChanged`                                                     | n/a                                                   | Removed battery information               |
| `newBatteryInfo` | [BatteryInfo](#battery-info)         | `batteryChanged`                                                     | n/a                                                   | Inserted battery information              |


## Device Events Stats
> `POST` https://graph.elemez.com/graphql

```graphql
query {
    deviceEventsStats(filter: [
        { field: "name" value: "deviceRebooted" }
        { field: "local" value: "1606241092000" operator: gte }
    ]
    ) {
        count
    }
}
```

> The above query returns JSON structured like this:

```json
{
    "data": {
        "deviceEventsStats": {
            "nodes": [
                { "count": 6 }
            ]
        }
    }
}
```

Returns the count of events matched by the given query.
See [Device Events Stats Grouped](#device-events-stats-grouped) for more advanced usage of [Device Events](#device-events).

### Available Fields
| Field   | Type     | Description              |
| -----   | ----     | -----------              |
| `count` | `number` | Count of matched records |


## Device Events Stats Grouped
> `POST` https://graph.elemez.com/graphql

```graphql
query {
    deviceEventsStats(filter: [
        { field: "name" value: "deviceRebooted" }
        { field: "local" value: "1606241092000" operator: gte }
      ]
    group: [
        { field: "deviceInfo.serialNumber" }
        { field: "deviceInfo.group" }
      ]
    ) {
        count
        keys {
            field
            value
        }
    }
}
```

> The above query returns JSON structured like this:

```json
{
    "data": {
        "deviceEventsStats": {
            "nodes": [
                {
                    "count": 2,
                    "keys": [
                        {
                            "field": "deviceInfo.serialNumber",
                            "value": "887hgd53dd"
                        },
                        {
                            "field": "deviceInfo.group",
                            "value": "warehouse"
                        }
                    ]
                },
                {
                    "count": 4,
                    "keys": [
                        {
                            "field": "deviceInfo.serialNumber",
                            "value": "2932peor3"
                        },
                        {
                            "field": "deviceInfo.group",
                            "value": "warehouse"
                        }
                    ]
                }
            ]
        }
    }
}
```

Returns the counts per grouping provided.
Eg: If a the standard [Device Events Stats](#device-events-stats) query returns `6` devices based on the query, the addition of the `group` parameter allows
the counts to be grouped by this field.

In the examples case we have grouped by the `deviceInfo.serialNumber` and `deviceInfo.group` field so you will receive the `deviceRebooted` count per `deviceInfo.serialNumber` and `deviceInfo.group`.

Grouping is limited to 2 `group` definitions.

### Available Fields
| Field   | Type                | Description                 |
| -----   | ----                | -----------                 |
| `count` | `number`            | Count of matched records    |
| `keys`  | [Keys](#stats-keys) | Event Stats Grouping values |

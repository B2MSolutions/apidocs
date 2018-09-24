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

Some information about the devices query here...

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
| `smartBattery`     | [SmartBattery](#smartbattery)       | Smart battery information                                    |
| `sim`              | [Sim](#sim)                         | Sim card details                                             |
| `batteryDischarge` | [DeviceDischarge](#devicedischarge) | Battery discharge information                                |

[Device](#device)

## Smart Batteries

### Available Fields
| Field             | Type                    | Description                                          |
| -----             | ----                    | -----------                                          |
| `id`              | `string`                | Unique smart battery ID                              |
| `partNumber`      | `string`                | The part number as given by the battery              |
| `serialNumber`    | `string`                | The battery serial number                            |
| `persentCapacity` | `number`                | The present capacity in `mah` of the battery         |
| `ratedCapacity`   | `number`                | The rated capacity in `mah` of the battery           |
| `manfactureDate`  | `string`                | The manufactured date as given by the battery        |
| `updated`         | [Timestamp](#timestamp) | When the smart battery laste updated its information |
| `device`          | [Device](#devices)      | The device associated with the smart battery         |

## Groups

## Device Stats

## Ping

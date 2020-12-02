# Types

## Timestamp
Unix Timestamp in milliseconds returned as a number

## Status

Elemez status value returned as `red` `yellow` `green`

## GPS
| Field       | Type                    | Description                                                  |
| -----       | ----                    | -----------                                                  |
| `latitude`  | `float`                 | Latitude                                                     |
| `longitude` | `float`                 | Longitude                                                    |
| `position`  | `gps point`             | Concatenated latitude &amp; longitide. `51.61492, -1.311916` |
| `accuracy`  | `number`                | Accuracy in meters of the given coordinates                  |
| `time`      | [Timestamp](#timestamp) | When the GPS coordinates where collected                     |
| `source`    | `string`                | Method of collection eg: `gps` `cellular` `fused`            |
| `utc`       | [Timestamp](#timestamp) | When the GPS coordinates were sent to the server             |

## DeviceDischarge
| Field     | Type     | Description                   |
| -----     | ----     | -----------                   |
| `date`    | `string` | `YYYY-MM-DD` date format      |
| `average` | `number` | The devices average discharge |

## Sim
| Field          | Type              | Description                             |
| -----          | ----              | -----------                             |
| `serialNumber` | `string`          | The Sim card serial number              |
| `device`       | [Device](#device) | The device associated with the sim card |

## ImpactDetection

| Field            | Type                                    | Description                                  |
| -----            | ----                                    | -----------                                  |
| `count`          | `number`                                | Total number of drops                        |
| `lastOccurrence` | [Timestamp](#timestamp)                 | Last occurrence of a drop or forceful impact |
| `drops`          | [ImpactInformation](#impactinformation) | Information on the drop count                |


## ImpactInformation
| Field           | Type                    | Description              |
| -----           | ----                    | -----------              |
| `count`         | `number`                | Total number detected    |
| `lastOccurrence` | [Timestamp](#timestamp) | Last occurrence timestamp |

## PageInfo
| Field         | Type      | Description                                                    |
|---------------|-----------|----------------------------------------------------------------|
| `hasNextPage` | `boolean` | Is there another page in the pagination series                 |
| `endCursor`   | `string`  | The identifier for the `after` query parameter when paginating |

## Operator
| Operator  | Description               |
| --        | --                        |
| `eq`      | Equal                     |
| `lt`      | Less than                 |
| `lte`     | Less than or Equal        |
| `gt`      | Greater than              |
| `gte`     | Greater than or Equal     |
| `not_eq`  | Not equal                 |
| `not_lt`  | Not less than             |
| `not_lte` | Not less than or equal    |
| `not_gt`  | Not greater than          |
| `not_gte` | Not greater than or equal |

## Custom Fields
| Field     | Type                    | Description                     |
|-----------|-------------------------|---------------------------------|
| `name`    | `string`                | Name                            |
| `value`   | `string\|number`        | Value                           |
| `updated` | [Timestamp](#timestamp) | Last updated time of the metric |

## Custom Event Field
| Field   | Type     | Description             |
| --      | --       | --                      |
| `name`  | `string` | Custom event field name |
| `value` | `any`    | Custom event value      |

## Device Info
| Field            | Type       | Description                                          |
| ---------------- | ---------- | ---------------------------------------------------- |
| `serialNumber`   | `string`   | Devices Serial Number                                |
| `model`          | `string`   | Model numbel                                         |
| `manufacturer`   | `string`   | Manufacturer name                                    |
| `assetTag`       | `string`   | Asset tag                                            |
| `group`          | `[string]` | Array of group names the device currently belongs to |
| `homeLocationId` | `string`   | Configured home location Id                          |

## Group Operation
| Field     | Description                                                  |
|-----------|--------------------------------------------------------------|
| `add`     | Append the provided groups to the existing list of group     |
| `remove`  | Remove the provided groups from the exisiting list of groups |
| `clear`   | Remove all group - this ignores the `groups` string provided |
| `replace` | Replace the existing groups with the provided set            |

## Device Event Categories & Names
| Category      | Names                                                                                  |
| --            | --                                                                                     |
| `application` | `applicationinstalled`, `applicationupdated`, `applicationuninstalled`                 |
| `battery`     | `batterychanged`                                                                       |
| `device`      | `devicerebooted`, `deviceonpower`, `deviceoffpower`, `devicelowpower`, `devicedropped` |
| `time`        | `timeerror`, `timerecovery`                                                            |

## Stats Keys
| Field   | Type     | Description |
| --      | --       | --          |
| `name`  | `string` | Field name  |
| `value` | `any`    | Field value |

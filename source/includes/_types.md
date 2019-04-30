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

| Field            | Type                                    | Description                                 |
| -----            | ----                                    | -----------                                 |
| `count`          | `number`                                | Total number of drops                       |
| `lastOccurance`  | [Timestamp](#timestamp)                 | Last occurance of a drop or forceful impact |
| `drops`          | [ImpactInformation](#impactinformation) | Information on the drop count               |
| `forcefulImpact` | [ImpactInformation](#impactinformation) | Information on forceful impacts             |


## ImpactInformation
| Field           | Type                    | Description              |
| -----           | ----                    | -----------              |
| `count`         | `number`                | Total number detected    |
| `lastOccurance` | [Timestamp](#timestamp) | Last occurance timestamp |

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

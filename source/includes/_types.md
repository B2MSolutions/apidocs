# Types

## Timestamp
Unix Timestamp in milliseconds returned as a number

## GPS
| Field       | Type                    | Description                                                   |
| -----       | ----                    | -----------                                                   |
| `latitude`  | `float`                 | Latitude                                                      |
| `longitude` | `float`                 | Longitude                                                     |
| `position`  | `gps point`             | Concatenated latitude &amp; longitide. `51.61492, -1.311916`  |
| `accuracy`  | `number`                | Accuracy in meters of the given coordinates                   |
| `time`      | [Timestamp](#timestamp) | When the GPS coordinates where collected                      |
| `source`    | `string`                | Method of collection eg: `gps` `cellular` `fused`             |
| `utc`       | [Timestamp](#timestamp) | When the GPS coordinates were sent to the server              |

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

## PageInfo
| Field | Type | Description
|------|-----|------
|`hasNextPage`|`boolean`|Is there another page in the pagination series
|`endCursor`|`string`|The identifier for the `after` query parameter when paginating



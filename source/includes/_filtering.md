# Filter

## Input Fields
| Field   | Type                | Description                         |
| --      | --                  | --                                  |
| `field` | `string`            | Field name as defined in the object |
| `value` | `string/[string]`   | File value                          |

> Exact Match; get devices in the `group` `uk`

```graphql
{
  devices(filter: { field: "group" value: "uk" }) {
    nodes {
      serialNumber
      model
      group
    }
  }
}
```

> OR; get devices in the `group` `uk` OR `france`

```graphql
{
  devices(filter: { field: "group" value: ["uk", "france"] }) {
    nodes {
      serialNumber
      model
      group
    }
  }
}
```

> AND; get devices in the `group` `uk` AND `model` `TC75`

```graphql
{
  devices(filter: [{field: "group" value: "uk" }, { field: "model" value: "TC75"}]) {
    nodes {
      serialNumber
      model
      group
    }
  }
}
```

> Operators; get devices with `averageDischarge` greater than or equal `30%`

```graphql
{
  devices(filter: { field: "averageDischarge" value: "0.3" operator: gte }) {
    nodes {
      serialNumber
      model
      group
    }
  }
}
```

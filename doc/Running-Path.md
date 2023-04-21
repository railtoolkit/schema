# Running Path Schema

------------

# Specification

## Preamble

| Attributes           | Necessity | Description |
| -------------------- | --------- | ----------- |
| `schema`             | required  | Identifier of the JSON schema. |
| `schema_version`     | required  | Version of the JSON schema. |
| `paths`              | required  | An array of [paths](#Attributes-in-paths). |

## Attributes in "paths"

All attributes for paths are collected under the array `paths: -` in alphabetical order:
| Attributes                | Necessity | Description |
| ------------------------- | --------- | ----------- |
| `characteristic_sections` | required  | An array of triplets with a station in meter, speed limit in kilometers per hour, and resistance in permil. |
| `id`                      | required  | Identifier of the path. |
| `name`                    | required  | Name of the path. |
| `points_of_interest`      | optional  | An array of triplets with a station in meter, a name for the point, and if the point applies to the `front` or `rear` of a train. |
| `UUID`                    | optional  | The unique identifier of the path. |

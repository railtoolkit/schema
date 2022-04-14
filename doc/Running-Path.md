# Running Path Schema

------------

# Specification

All attributes for a train are collected under the mapping `path` in alphabetical order:
| Attributes                | Necessity | Description |
| ------------------------- | --------- | ----------- |
| `characteristic_sections` | required  | An array of triplets with a station in meter, speed limit in kilometers per hour, and resistance in permil. |
| `id`                      | required  | Identifier of the path. |
| `name`                    | required  | Name of the path. |
| `points_of_interest`      | optional  | An array of triplets with a station in meter, a name for the point, and if the point applies to the `front` or `rear` of a train. |
| `UUID`                    | optional  | The unique identifier of the path. |

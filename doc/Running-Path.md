# Running Path Schema

------------

# Specification

## Preamble

| Attributes           | Necessity | Description                                            |
| -------------------- | --------- | ------------------------------------------------------ |
| `schema`             | required  | Identifier of the JSON schema.                         |
| `schema_version`     | required  | Version of the JSON schema.                            |
| `paths`              | required  | An array of at least one [path](#Attributes-in-paths). |

## Attributes in "paths"

All attributes for paths are collected under the array `paths: -` in alphabetical order:
| Attributes                | Necessity | Description                                                                    |
| ------------------------- | --------- | ------------------------------------------------------------------------------ |
| `characteristic_sections` | required  | An array of [characteristic sections](#Attributes-in-characteristic_sections). |
| `id`                      | required  | Identifier of the path.                                                        |
| `description`             | optional  | Description of the path.                                                       |
| `points_of_interest`      | optional  | An array of [points of interest](#Attributes-in-points_of_interest).           |

## Attributes in "characteristic_sections"

All attributes for a characteristic section are collected under the array `characteristic_sections: -` sorted in ascending or descending order:

| Attributes   | Necessity    | Description                        |
| ------------ | ------------ | ---------------------------------- |
| `position`   | required     | mileage in meter                   |
| `speed`      | optional[^1] | speed limit in kilometers per hour |
| `resistance` | optional[^1] | resistance in permil               |

[^1]: At least one optional attribute must be present.

## Attributes in "points_of_interest"
All attributes for a point of interest (poi) are collected under the array `points_of_interest: -` sorted in ascending or descending order:

| Attributes   | Necessity | Description                                                       |
| ------------ | --------- | ------------------------------------------------------------------|
| `position`   | required  | mileage in meter                                                  |
| `id`         | required  | Identifier of the point                                           |
| `description`| optional  | Description of the point                                          |
| `groups`     | optional  | Array of group names this point belongs to                        |
| `measure`    | required  | measurement applies to the `front`, `middle` or `rear` of a train |

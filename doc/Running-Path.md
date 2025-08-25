# Running Path Schema

------------

# Specification

## Preamble

| Attributes           | Data Type | Necessity | Description                                            |
| -------------------- | --------- | --------- | ------------------------------------------------------ |
| `schema`             | string    | required  | Identifier of the JSON schema.                         |
| `schema_version`     | string    | required  | Version of the JSON schema.                            |
| `paths`              | array     | required  | An array of at least one[^1] [path](#Attributes-in-paths). |

[^1]: At least one item in `paths` should be present. For scaffolding purposes, `paths` can be empty.

## Attributes in "paths"

All attributes for a path are collected under the array `paths: -` in alphabetical order:

| Attributes               | Data Type | Necessity | Description |
| ------------------------ | --------- | --------- | ----------- |
| `id`                     | string    | required  | Identifier of the running path. |
| `description`            | string    | optional  | Description of the running path. |
| `characteristic_sections`| array     | required  | An array of [characteristic sections](#Attributes-in-characteristic_sections). |
| `points_of_interest`     | array     | optional  | An array of [points of interest](#Attributes-in-points_of_interest). |

## Attributes in "characteristic_sections"

Characteristic sections are sections of a running path within which properties, such as permitted speed or track resistances, do not change.

| Attributes           | Data Type | Necessity | Description |
| -------------------- | --------- | --------- | ----------- |
| `position`           | number    | required  | Position along the path (m) |
| `speed`              | number    | optional[^2] | Maximum permitted speed (km/h) |
| `resistance`         | number    | optional[^2] | Track resistance (‰) |

[^2]: At least one of attributes `speed` or `resistance` must be present.

## Attributes in "points_of_interest"

Points of interest mark specific locations along the path where measurements or observations should be taken.

| Attributes           | Data Type | Necessity | Description |
| -------------------- | --------- | --------- | ----------- |
| `position`           | number    | required  | Position along the path (m) |
| `id`                 | string    | required  | Identifier of the point of interest |
| `description`        | string    | optional  | Description of the point of interest |
| `groups`             | array     | optional  | Groups this point belongs to; an array of unique string identifiers |
| `measure`            | enum      | required  | Position on train to measure; values: `front`, `middle`, or `rear` |

# Units

The schema uses common railway units for all numerical values:

| Quantity         | Unit | Description |
|------------------|------|-------------|
| Position         | m    | Meters |
| Speed            | km/h | Kilometers per hour |
| Resistance       | ‰    | Per mille (mm/m) |

# Example
An example file showing a running path with block sections, signals, and platforms can be found in [running-path.example.yaml](running-path.example.yaml). The example includes various points of interest such as platform tracks, route signals, and clearing points, each with specific positions and descriptions. Below is a visual representation of the YAML structure:

![Running Path Example](running-path.example.png)

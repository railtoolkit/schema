# Rolling Stock Schema

------------

# Specification

## Preamble

| Attributes           | Necessity    | Description |
| -------------------- | ------------ | ----------- |
| `schema`             | required     | Identifier of the JSON schema. |
| `schema_version`     | required     | Version of the JSON schema. |
| `trains`             | optional[^1] | An array of [trains](#Attributes-in-trains). |
| `vehicles`           | optional[^1] | An array of [vehicles](#Attributes-in-vehicles). |

[^1]: At least one of attributes `trains` or `vehicles` must be present.

## Attributes in "trains"

All attributes for a train are collected under the array `trains: -` in alphabetical order:

| Attributes           | Necessity | Description |
| -------------------- | --------- | ----------- |
| `id`                 | required  | Identifier of the train. |
| `name`               | required  | Name of the train. |
| `UUID`               | optional  | The unique identifier of the train. |
| `formation`          | required  | A Collection of vehicles that form the train referenced by vehicle `id`. |

## Attributes in "vehicles"

All attributes for a vehicle are collected under the array `vehicles: -` in alphabetical order:

| Attributes           | Necessity | Description |
| -------------------- | --------- | ----------- |
| `air_resistance`     | optional  | Coefficient for air resistance in permil. |
| `base_resistance`    | optional  | Coefficient for basic resistance  in permil. |
| `id`                 | required  | Identifier of the vehicle. |
| `length`             | required  | The length of the vehicle in meter. |
| `load_limit`         | optional  | The maximum permitted load of the vehicle in metric ton. |
| `mass_traction`      | optional  | The mass on the powered axles of the vehicle in metric ton. |
| `mass`               | required  | The empty mass (dead weight) of the vehicle in metric ton. |
| `name`               | required  | Name of the vehicle. |
| `picture`            | optional  | A [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) with a picture for humans. | 
| `power_type`         | optional  | Type of propulsion; values: `diesel`, `electric`, or `steam`. |
| `rolling_resistance` | optional  | Coefficient for resistance of rolling axles in permil. |
| `rotation_mass`      | optional  | Factor for rotating mass; larger then 1. |
| `speed_limit`        | optional  | Maximum permitted speed in kilometers per hour. |
| `tractive_effort`    | optional  | Tractive effort as pairs of speed in kilometers per hour and tractive force in newton. |
| `UUID`               | optional  | The unique identifier for a vehicle. |
| `vehicle_type`       | required  | Type of vehicle; values: `traction unit`, `freight`, `passenger`, or `multiple unit`. |


# Rolling Stock Schema

------------

# Specification

## Preamble

| Attributes           | Necessity    | Description |
| -------------------- | ------------ | ----------- |
| `schema`             | required     | Identifier of the JSON schema. |
| `schema_version`     | required     | Version of the JSON schema. |
| `model_fidelity`     | optional     | Level of detail for train dynamics modeling. Values: `simplified_characteristics`, `effort_tables`, or `physical_model`. Defaults to `effort_tables` if not specified. |
| `trains`             | optional[^1] | An array of [trains](#Attributes-in-trains). |
| `vehicles`           | optional[^1] | An array of [vehicles](#Attributes-in-vehicles). |

[^1]: At least one of attributes `trains` or `vehicles` must be present.

### Model Fidelity Rationale

The `model_fidelity` attribute allows for different levels of detail in train dynamics modeling, each serving different use cases:

- `simplified_characteristics`: Uses basic acceleration and deceleration parameters. Suitable for high-level planning and simple simulations where detailed dynamics are not required. Parametersare definied in `trains`.
  
- `effort_tables`: Uses lookup tables for tractive and braking effort over speed. Appropriate when measured or manufacturer-provided performance data is available and precise force calculations are needed. Parameters are defined in `vehicles`.
  
- `physical_model`: Uses physical parameters and formulas. Best suited for accurate simulations where component-level behavior and physical effects need to be considered. Parameters are defined in `vehicles`.

A file may contain more than one level of fidelity. Even though, the fidelity levels are mutually exclusive - only values from the selected fidelity level will be used in calculations, even if data for other levels is present in the file. The attribute `model_fidelity` can be used as switch to select the level of fidelity to be used.

## Attributes in "trains"

All attributes for a train are collected under the array `trains: -` in alphabetical order:

| Attributes                  | Necessity    | Description |
| -------------------------- | ------------ | ----------- |
| `id`                       | required     | Identifier of the train. |
| `description`              | optional     | Description of the train. |
| `train_type`               | optional     | Type of train service. See [Train Types](#train-types) below. |
| `formation`                | optional[^2] | A Collection of vehicles that form the train referenced by vehicle `id`. |
| `simplified_characteristics`| optional[^2] | Basic motion parameters when using `simplified_characteristics` model fidelity. |

[^2]: At least one of attributes `formation` or `simplified_characteristics` must be present, depending on the selected `model_fidelity`.

### Train Types

The `train_type` attribute categorizes trains into three main groups:

#### 1. Passenger Trains
- `long_distance` - Fast, long-distance trains with few stops (e.g., ICE, TGV)
- `regional` - Medium speed trains for mid-range distances (e.g., RE, RB)
- `suburban` - Short-distance trains with frequent stops (e.g., S-Bahn)
- `metro` - Urban trains with high frequency (e.g., Metro, Trams)

#### 2. Freight Trains
- `intermodal` - Container transport trains with medium speed
- `heavy_freight` - High axle load trains for bulk cargo (e.g., coal, ore)
- `block_freight` - Single cargo type trains with direct routes

#### 3. Special Trains
- `shunting` - Low speed trains for wagon formation
- `maintenance` - Infrastructure maintenance trains
- `construction` - Construction site supply trains
- `emergency` - Fire, rescue, and emergency response trains
- `snow_removal` - Seasonal service trains

### Attributes in "simplified_characteristics"

When using `model_fidelity: "simplified_characteristics"`, the following attributes define the basic motion parameters of a train:

| Attributes           | Necessity | Description |
| -------------------- | --------- | ----------- |
| `speed_limit`        | required  | Maximum permitted speed in kilometers per hour. |
| `length`            | required  | Total length of the train in meters. |
| `acceleration`      | required  | Constant acceleration rate in meters per second squared. |
| `deceleration`      | required  | Constant service braking rate in meters per second squared (negative value). |
| `coasting`          | optional  | Deceleration rate when coasting in meters per second squared (negative value). Defaults to 0 if not specified. |

These simplified characteristics are used when detailed vehicle dynamics are not required or available. They provide a basic but efficient way to model train movement for high-level planning and simple simulations.

## Attributes in "vehicles"

All attributes for a vehicle are collected under the array `vehicles: -` in alphabetical order:

| Attributes           | Necessity | Description |
| -------------------- | --------- | ----------- |
| `air_resistance`     | optional  | Coefficient for air resistance in permil. |
| `base_resistance`    | optional  | Coefficient for basic resistance in permil. |
| `description`        | optional  | Description of the vehicle. |
| `id`                 | required  | Identifier of the vehicle. |
| `length`             | required  | The length of the vehicle in meter. |
| `load_limit`         | optional  | The maximum permitted load of the vehicle in metric ton. |
| `mass_traction`      | optional  | The mass on the powered axles of the vehicle in metric ton. |
| `mass`               | required  | The empty mass (dead weight) of the vehicle in metric ton. |
| `picture`            | optional  | A [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) with a picture for humans. | 
| `power_type`         | optional  | Type of propulsion; values: `hydraulic`, `electric`, `steam`, or `misc`. |
| `rolling_resistance` | optional  | Coefficient for resistance of rolling axles in permil. |
| `rotation_mass`      | optional  | Factor for rotating mass; larger or equal to 1. |
| `speed_limit`        | optional  | Maximum permitted speed in kilometers per hour. |
| `tractive_effort`    | optional  | Tractive effort as pairs of speed in kilometers per hour and tractive force in newton. Must contain at least 3 unique pairs. |
| `vehicle_type`       | required  | Type of vehicle; values: `traction unit`, `freight`, `passenger`, `multiple unit`, or `non-revenue`. |


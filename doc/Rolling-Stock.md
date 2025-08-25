# Rolling Stock Schema

------------

# Specification

## Preamble

| Attributes           | Data Type    | Necessity    | Description |
| -------------------- | ------------ | ------------ | ----------- |
| `schema`             | string       | required     | Identifier of the JSON schema. |
| `schema_version`     | string       | required     | Version of the JSON schema (current version `2024.07`). |
| `model_fidelity`     | string       | required     | Level of detail for train dynamics modeling. Values: `simplified`, `detailed`. |
| `trains`             | array        | optional[^1] | A list of [trains](#Attributes-in-trains). |
| `vehicles`           | array        | optional[^1] | A list of [vehicles](#Attributes-in-vehicles). |

[^1]: At least one of attributes `trains` or `vehicles` must be present.

### Model Fidelity Rationale

The `model_fidelity` attribute specifies the level of detail for train dynamics modeling:

- `simplified`: Uses basic acceleration and deceleration parameters. Suitable for high-level planning and simple simulations where detailed dynamics are not required. Parameters are defined in `trains.simplified_characteristics`.
  
- `detailed`: Uses detailed vehicle parameters including physical properties and effort tables. Appropriate for precise simulations where accurate force calculations are needed. Parameters are defined in `vehicles`.

A file may contain data for both fidelity levels, but only values from the selected level will be used in calculations. The attribute `model_fidelity` acts as a switch to select which level of detail to use, ensuring that the appropriate parameters are applied based on the chosen fidelity level.

The `model_fidelity` attribute is not only used at the top level but also plays a crucial role in lower-level objects such as `resistance`, `traction`, and `brakes`. This allows for varying levels of detail in the modeling of these components, ensuring that the appropriate parameters are applied based on the selected fidelity level.

## Attributes in "trains"

All attributes for a train are collected under `trains: -` in alphabetical order:

| Attributes                   | Data Type    | Necessity    | Description |
| ---------------------------- | ------------ | ------------ | ----------- |
| `id`                         | string       | required     | Identifier of the train. |
| `description`                | string       | optional     | Description of the train. |
| `train_type`                 | string       | optional     | Type of train service. See [Train Types](#train-types) below. |
| `simplified_characteristics` | object       | optional[^2] | Basic motion parameters when using `simplified_characteristics` model fidelity. See [Simplified Characteristics](#simplified-characteristics) below. |
| `formation`                  | array        | optional[^2] | A Collection of vehicles that form the train referenced by vehicle `id`. Front and rear end of the train are defined by the first and last vehicle in the array. |
| `loading_factor`             | array        | optional     | Ratio (between 0 and 1) of the actual load to the maximum load capacity of the train. Using the `load_limit` attribute of the vehicles in the `formation` array. |

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

### Simplified Characteristics

When using `model_fidelity: "simplified"`, the following attributes define the basic motion parameters of a train:

| Attributes                   | Data Type    | Necessity | Description |
| ---------------------------- | ------------ | --------- | ----------- |
| `speed_limit`                | number       | required  | Maximum permitted speed (km/h) |
| `length`                     | number       | required  | Total length of the train (m) |
| `acceleration`               | number       | required  | Constant acceleration rate (m/s²) |
| `deceleration`               | number       | required  | Constant service braking rate (m/s²) (negative value) |
| `emergency_deceleration`     | number       | optional  | Emergency braking rate (m/s²) (negative value). If not specified, defaults to the value of `deceleration` |
| `coasting`                   | number       | optional  | Deceleration rate when coasting (m/s²) (negative value). Defaults to 0 if not specified |
These simplified characteristics are used when detailed vehicle dynamics are not required or available. They provide a basic but efficient way to model train movement for high-level planning and simple simulations.

## Attributes in "vehicles"

All attributes for a vehicle are collected under `vehicles: -` in alphabetical order:

| Attributes           | Data Type    | Necessity | Description |
| -------------------- | ------------ | --------- | ----------- |
| `id`                 | string       | required  | Identifier of the vehicle |
| `vehicle_type`       | string       | required  | Type of vehicle; values: `traction_unit`, `freight`, `passenger`, `multiple_unit`, or `non-revenue` |
| `mass`               | number       | required  | Empty mass (dead weight) (t)|
| `length`             | number       | required  | Length of the vehicle (m) |
| `load_limit`         | number       | optional  | Maximum permitted load (t), Defaults to 0 if not specified |
| `speed_limit`        | number       | optional  | Maximum permitted speed (km/h) |
| `description`        | string       | optional  | Description of the vehicle |
| `power_type`         | string       | optional  | Type of propulsion; values: `hydraulic`, `electric`, `steam`, or `misc` |
| `mass_traction`      | number       | optional  | Mass on powered axles (t), Defaults to 0 if not specified |
| `picture`            | string       | optional  | A [URI](https://en.wikipedia.org/wiki/Uniform_Resource_Identifier) with a picture for humans | 
| `resistance`         | object       | optional  | Vehicle resistance characteristics. See [Resistance Configuration](#resistance-configuration) below. |
| `traction`           | object       | optional  | Traction characteristics. See [Traction Configuration](#traction-configuration) below. |
| `brakes`             | object       | optional  | Braking system configuration. See [Brakes Configuration](#brakes-configuration) below. In a Train formation, at least one vehicle must have a `brakes` object. |Data Type

### Resistance Configuration

The `resistance` object defines the vehicle's resistance characteristics:

| Attributes           | Data Type    | Necessity     | Description |
| -------------------- | ------------ | ------------- | ----------- |
| `model_fidelity`     | string       | required      | Type of resistance model; values: `table` or `calculated`. |
| `rotation_mass`      | number       | optional[^3]  | Factor for rotating mass (-), greater or equal to 1. |
| `base_resistance`    | number       | optional[^3]  | Basic resistance coefficient (‰). |
| `rolling_resistance` | number       | optional[^3]  | Rolling resistance coefficient (-). |
| `air_resistance`     | number       | optional[^3]  | Air resistance coefficient (-). |
| `resistance_effort`  | array        | optional[^4]  | [List of speed-force pairs](#list-of-speed-force-pairs) defining resistance. |

[^3]: Required when using `model_fidelity: "calculated"`
[^4]: Required when using `model_fidelity: "table"`

### Traction Configuration

The `traction` object defines the vehicle's traction characteristics:

| Attributes              | Data Type    | Necessity     | Description |
| ----------------------- | ------------ | ------------- | ----------- |
| `model_fidelity`        | string       | required      | Type of traction model; values: `table` or `calculated`. |
| `rated_power`           | number       | optional[^5]  | Rated power of the vehicle (kW). |
| `initial_tractive_force`| number       | optional[^5]  | Initial tractive force (kN). |
| `tractive_effort`       | array        | optional[^6]  | [List of speed-force pairs](#list-of-speed-force-pairs) defining tractive effort. |

[^5]: Required when using `model_fidelity: "calculated"`
[^6]: Required when using `model_fidelity: "table"`

### Brakes Configuration

The `brakes` object defines the vehicle's braking characteristics:

| Attributes              | Data Type    | Necessity | Description |
| ----------------------- | ------------ | --------- | ----------- |
| `model_fidelity`        | string       | required  | Type of brake model; values: `force`, `one-part-deceleration`, `two-part-deceleration`, `three-part-deceleration` |
| `deceleration`          | number       | optional[^7]  | Final/maximum braking deceleration (m/s²). Negative value. |
| `emergency_deceleration`| number       | optional      | Maximum emergency braking deceleration (m/s²). Negative value. If not specified, defaults to the value of `deceleration`|
| `reaction_time`         | number       | optional[^8]  | Time between need recognition and control activation (s) |
| `response_time`         | number       | optional[^9]  | Time to reach 5% of final braking deceleration (s) |
| `threshold_time`        | number       | optional[^9]  | Time to develop from 5% to 95% of final deceleration (s) |
| `eddy_current_brake`    | object       | optional[^10] | Eddy current brake characteristics |
| `electrodynamic_brake`  | object       | optional[^10] | Electrodynamic brake characteristics |
| `friction_brake`        | object       | optional[^10] | Friction brake characteristics |

[^7]: Required when using `model_fidelity: "one-part-deceleration"`, `model_fidelity: "two-part-deceleration"`, or `model_fidelity: "three-part-deceleration"`
[^8]: Required when using `model_fidelity: "two-part-deceleration"` or `model_fidelity: "three-part-deceleration"`
[^9]: Required when using `model_fidelity: "three-part-deceleration"`
[^10]: Only used when using `model_fidelity: "force"`, at least one of `eddy_current_brake`, `electrodynamic_brake`, or `friction_brake` is required for `model_fidelity: "force"`

The braking system can include one or more of these brake types:

- `eddy_current_brake`
  | Attributes              | Data Type    | Necessity     | Description |
  | ----------------------- | ------------ | ------------- | ----------- |
  | `model_fidelity`        | string       | required      | Type of eddy current brake model; values: `table` or `calculated`. |
  | `min_speed`             | number       | optional[^11] | Minimum speed for the brake to engage (km/h). Minimum value is 0. |
  | `max_brake_effort`      | number       | optional[^11] | Maximum brake effort (kN). Minimum value is 0. |
  | `power`                 | number       | optional[^11] | Power of the brake (kW). Minimum value is 0. |
  | `brake_effort`          | array        | optional[^12] | [List of speed-force pairs](#list-of-speed-force-pairs) defining brake effort |

- `electrodynamic_brake`
  | Attributes              | Data Type    | Necessity     | Description |
  | ----------------------- | ------------ | ------------- | ----------- |
  | `model_fidelity`        | string       | required      | Type of electrodynamic brake model; values: `table` or `calculated`. |
  | `max_brake_force`       | number       | optional[^11] | Maximum brake force (kN). Minimum value is 0. |
  | `speed_control_range`   | number       | optional[^11] | Speed range for control (km/h). Minimum value is 0. |
  | `speed_power_limit`     | number       | optional[^11] | Speed limit for power (km/h). Minimum value is 0. |
  | `speed_field_weakening` | number       | optional[^11] | Field weakening speed (km/h). Minimum value is 0. |
  | `brake_effort`          | array        | optional[^12] | [List of speed-force pairs](#list-of-speed-force-pairs) defining brake effort |

- `friction_brake`
  | Attributes              | Data Type    | Necessity     | Description |
  | ----------------------- | ------------ | ------------- | ----------- |
  | `model_fidelity`        | string       | required      | Type of friction brake model; values: `table` or `calculated`. |
  | `service_brake_effort`  | number       | optional[^11] | Full service brake force (kN). Minimum value is 0. |
  | `emergency_brake_effort`| number       | optional[^11] | Full emergency brake force (kN). Minimum value is 0. |
  | `brake_regime`          | string       | optional[^11] | Brake regime type; values: `P`, `G`, or `R` |
  | `brake_effort`          | array        | optional[^12] | [List of speed-force pairs](#list-of-speed-force-pairs) defining brake effort |

[^11]: Required when using `model_fidelity: "calculated"`
[^12]: Required when using `model_fidelity: "table"`

### List of speed-force pairs 

| Attributes              | Data Type    | Necessity     | Description |
| ----------------------- | ------------ | ------------- | ----------- |
| `speed`                 | number       | required      | Speed at which the brake effort is applied (km/h) |
| `force`                 | number       | required      | Brake force applied at the specified speed (kN) |

# Units

The schema uses common railway units for all numerical values:

| Quantity         | Unit | Description |
|------------------|------|-------------|
| Speed            | km/h | Kilometers per hour |
| Mass             | t    | Metric tons |
| Length           | m    | Meters |
| Time             | s    | Seconds |
| Force            | kN   | Kilonewton |
| Power            | kW   | Kilowatt |
| Acceleration     | m/s² | Meters per second squared |
| Resistance       | ‰    | Per mille (mm/m) |
| Unit-less        | -    | Dimensionless values |

# Examples

An example file showing a train with model_fidelity `simplified` vehicle dynamics can be found in [rolling-stock.example.simplified.yaml](rolling-stock.example.simplified.yaml).

An example file showing a train with model_fidelity `detailed` vehicle dynamics can be found in [rolling-stock.example.detailed.yaml](rolling-stock.example.detailed.yaml). The example includes various vehicle types with different characteristics, including resistance, traction, and braking systems.

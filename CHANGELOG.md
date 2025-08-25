# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Calendar Versioning](https://calver.org) with YYYY.0M.

Categories: Added, Changed, Deprecated, Removed, Fixed, and Security.

## [Unreleased]

### Added
* running path:
  * added `description` attribute (see Issue #5)
  * added `track` to characteristic sections for grouping track sections
  * added `groups` array to points_of_interest for categorizing points
  * added comprehensive test suite with valid and invalid test cases
  * added example file with block sections and signals
* rolling stock:
  * added `description` attribute to trains and vehicles (see Issue #5)
  * added `hydraulic` and `misc` to power_type options
  * added `non-revenue` to vehicle_type options
  * added complete schema for `simplified_characteristics` with required fields and constraints
  * added `coasting` parameter to simplified characteristics
  * added `emergency_deceleration` to simplified characteristics
  * added `model_fidelity` attribute on different levels
  * added comprehensive brake model configuration with multiple fidelity levels
  * added detailed brake types: eddy_current_brake, electrodynamic_brake, and friction_brake
  * added brake timing parameters: reaction_time, response_time, threshold_time
  * added new train types: snow_removal, construction, emergency
  * added comprehensive documentation for all attributes and model fidelity levels

### Changed
* running path:
  * running path arrays now contain named attributes (see Issue #4)
  * characteristic sections now require at least one of `speed`, `resistance`, or `track` attributes
  * measures for `points_of_interest` can now take three values: "front", "middle", and "rear"
* rolling stock:
  * changed tractive_effort to require at least 3 unique pairs
  * changed rotation_mass description to specify >= 1
  * changed train requirements to need either `formation` or `simplified_characteristics`
  * changed `train_type` to include comprehensive list of train service types
  * changed brake modeling to support multiple fidelity levels
  * changed model_fidelity to be required at top level and component levels
  * refined train_type categories into passenger, freight, and special groups
  * improved documentation with detailed explanations of model fidelity rationale

### Removed
* running path:
  * removed `name` attribute (see Issue #5)
  * removed `UUID` attribute (see Issue #5)
* rolling stock:
  * removed `name` attribute from trains and vehicles (see Issue #5)
  * removed `UUID` attribute from trains and vehicles (see Issue #5)
  * removed `diesel` from power_type options

## Version [2022.05]

### Added
  * added tests for continuous integration
  * added schema and schema version (see Issue #1)

### Changed
  * renamed `vehicle` into `vehicles` and changed type to array (see Issue #2)
  * renamed `train` into `trains` and changed type to array (see Issue #2)
  * renamed `path` into `paths` and changed type to array (see Issue #2)

## Version [2022.04]

### Added
  * initial rolling-stock schema
  * initial running-path Schema

[Unreleased]: https://github.com/railtoolkit/schema/compare/2022.05...main
[2022.05]: https://github.com/railtoolkit/schema/compare/2022.04...2022.05
[2022.04]: https://github.com/railtoolkit/schema/releases/tag/2022.04
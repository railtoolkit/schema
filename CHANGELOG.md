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

### Changed
* running path:
  * running path arrays now contain named attributes (see Issue #4)
  * characteristic sections now require at least one of `speed`, `resistance`, or `track` attributes
  * measures for `points_of_interest` can now take three values: "front", "middle", and "rear"

### Removed
* running path:
  * removed `name` attribute (see Issue #5)
  * removed `UUID` attribute (see Issue #5)

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
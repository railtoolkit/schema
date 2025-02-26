# RailToolKit/schema

[![License: ISC][license-img]][license-url] [![DOI][zenodo-img]][zenodo-url] [![Build Status][ci-img]][ci-url] [![All Contributors][Contributors-img]][Contributors-url]

------------

## About

The RailToolkit/schema provides JSON schemas for railway operations data, offering a lightweight alternative to RailML. It focuses on two main aspects:

1. Rolling Stock Schema
   - Defines train and vehicle characteristics
   - Supports both simplified and detailed modeling approaches
   - Includes parameters like speed, mass, resistance, and tractive effort

2. Running Path Schema
   - Describes railway paths with speed limits and track resistance
   - Supports points of interest (signals, platforms, etc.)
   - Enables precise position-based path descriptions

The schemas use standardized railway units and can be validated using standard JSON schema tools. They are designed to support railway simulation and planning tools while maintaining simplicity and ease of use.

## Prerequisite

You will need a validator to validate the schema against data. This package provides a helper script that uses the [Ajv JSON schema validator](https://ajv.js.org).
Ajv requires to have [node](https://nodejs.org/) installed.
  
```bash
$ node --version # test if node is installed
```

## Usage

You will need the schema and some data. The repo contains among others the rolling-stock schema and example data:
```bash
$ git clone https://github.com/railtoolkit/schema.git && cd schema
```

Install all project dependencies:
```bash
$ npm install
```

You can validate if the data follows the schema:
```bash
$ npm run validate:rolling-stock doc/rolling-stock.example.yaml
$ npm run validate:running-path doc/running-path.example.yaml
```

## Testing

The repository includes comprehensive test suites for both schemas:

```bash
$ npm run test          # Run all tests
$ npm run test:stock    # Run rolling-stock tests only
$ npm run test:paths    # Run running-path tests only
```

Each test suite includes:
- Example file validation
- Valid test cases
- Invalid test cases

## Documentation

### Sub schemas

See 
* [Rolling-Stock.md](doc/Rolling-Stock.md) and 
* [Running-Path.md](doc/Running-Path.md)

for information about the used attributes in the sub schemas.

### Units

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


## Contributors

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/kaat0"><img src="https://avatars.githubusercontent.com/u/142348?v=4?s=100" width="100px;" alt="Martin Scheidt"/><br /><sub><b>Martin Scheidt</b></sub></a><br /><a href="#code-kaat0" title="Code">💻</a> <a href="#doc-kaat0" title="Documentation">📖</a> <a href="#example-kaat0" title="Examples">💡</a> <a href="#test-kaat0" title="Tests">⚠️</a> <a href="#research-kaat0" title="Research">🔬</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/gwehrle"><img src="https://avatars.githubusercontent.com/u/171450664?v=4?s=100" width="100px;" alt="Gregor Wehrle"/><br /><sub><b>Gregor Wehrle</b></sub></a><br /><a href="#bug-gwehrle" title="Bug reports">🐛</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/JonathanSchoener"><img src="https://avatars.githubusercontent.com/u/118694515?v=4?s=100" width="100px;" alt="JonathanSchoener"/><br /><sub><b>JonathanSchoener</b></sub></a><br /><a href="#research-JonathanSchoener" title="Research">🔬</a></td>
    </tr>
  </tbody>
</table>
<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->
<!-- ALL-CONTRIBUTORS-LIST:END -->

See [CONTRIBUTING.md](CONTRIBUTING.md) file if you are interested to contribute.

------------

# License
  
  [![Open Source Initiative Approved License logo](https://149753425.v2.pressablecdn.com/wp-content/uploads/2009/06/OSIApproved_100X125.png "Open Source Initiative Approved License logo")](https://opensource.org)

  Copyright (c) 2022 - 2025, Martin Scheidt (orcid.org/0000-0002-9384-8945) (ISC License)

  Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

  THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.

[license-img]: https://img.shields.io/badge/license-ISC-green.svg
[license-url]: https://opensource.org/licenses/ISC

[ci-img]: https://github.com/railtoolkit/schema/actions/workflows/testing.yaml/badge.svg?branch=main
[ci-url]: https://github.com/railtoolkit/schema/actions/workflows/testing.yaml?query=branch%3Amain

[zenodo-img]: https://zenodo.org/badge/DOI/10.5281/zenodo.6462039.svg
[zenodo-url]: https://doi.org/10.5281/zenodo.6462039

[Contributors-img]: https://img.shields.io/github/all-contributors/railtoolkit/schema?color=ee8449&style=flat-square
[Contributors-url]: #Contributors

# RailToolKit Schema

[![License: ISC][license-img]][license-url] [![DOI][zenodo-img]][zenodo-url] [![Build Status][ci-img]][ci-url] [![All Contributors][Contributors-img]][Contributors-url]

------------

## About

  This repo collects the descriptions of the structure and the validation constraints of tools in the railtoolkit in JSON schemas. It is, therefore, an alternative to [RailML](https://www.railml.org/). The JSON schemas enable the validation of YAML files in [TrainRun.jl](https://github.com/railtoolkit/TrainRun.jl.git) and [rolling-stock](https://github.com/railtoolkit/rolling-stock.git).

## Prerequisite

  You will need a validator to validate the schema against data. This example uses the [Ajv JSON schema validator](https://ajv.js.org).
  ```bash
  $ npm install -g ajv-cli && npm install -g ajv-formats
  ```

## Usage

  You will need the schema and some data. The repo contains among others the rolling-stock schema and example data:
  ```bash
  $ git clone https://github.com/railtoolkit/schema.git && cd schema
  ```

  You can now validate if the data follows the schema:
  ```bash
  $ ajv --spec=draft2020 -c ajv-formats -s src/rolling-stock.json -d doc/rolling-stock.example.yaml
  ```
  This will return:
  ```bash
  $ doc/rolling-stock.example.yaml valid
  ```
  Or:
  ```bash
  $ ajv --spec=draft2020 -c ajv-formats -s src/running-path.json -d doc/running-path.example.yaml
  ```
  This will return:
  ```bash
  $ doc/running-path.example.yaml valid
  ```

## Documentation

  see [Rolling-Stock.md](https://github.com/railtoolkit/schema/blob/main/doc/Rolling-Stock.md) and [Running-Path.md](https://github.com/railtoolkit/schema/blob/main/doc/Running-Path.md) for information about the used attributes.

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

See [CONTRIBUTING.md](https://github.com/railtoolkit/schema/blob/main/CONTRIBUTING.md) file if you are interested to contribute.

------------

# License
  
  [![Open Source Initiative Approved License logo](https://149753425.v2.pressablecdn.com/wp-content/uploads/2009/06/OSIApproved_100X125.png "Open Source Initiative Approved License logo")](https://opensource.org)

  Copyright (c) 2022, Martin Scheidt \<m.scheidt@tu-bs.de\> (ISC License)

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

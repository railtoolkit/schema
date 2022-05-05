# RailToolKit Schema

[![License: ISC](https://img.shields.io/badge/license-ISC-green.svg)](https://opensource.org/licenses/ISC) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.6462039.svg)](https://doi.org/10.5281/zenodo.6462039) [![continuous integration test](https://github.com/railtoolkit/schema/actions/workflows/testing.yaml/badge.svg)](https://github.com/railtoolkit/schema/actions/workflows/testing.yaml)

------------

# About

  This repo collects the descriptions of the structure and the validation constraints of tools in the railtoolkit in JSON schemas. It is, therefore, an alternative to [RailML](https://www.railml.org/). The JSON schemas enable the validation of YAML files in [TrainRun.jl](https://github.com/railtoolkit/TrainRun.jl.git) and [rolling-stock](https://github.com/railtoolkit/rolling-stock.git).

# Prerequisite

  You will need a validator to validate the schema against data. This example uses the [Ajv JSON schema validator](https://ajv.js.org).
  ```bash
  $ npm install -g ajv-cli && npm install -g ajv-formats
  ```

# Usage

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

# Documentation

  see [Rolling-Stock.md](https://github.com/railtoolkit/schema/blob/main/doc/Rolling-Stock.md) and [Running-Path.md](https://github.com/railtoolkit/schema/blob/main/doc/Running-Path.md) for information about the used attributes.

# Contributing

  see [CONTRIBUTING.md](https://github.com/railtoolkit/schema/blob/main/CONTRIBUTING.md) file

# Roadmap

  * include breaking model in rolling-stock schema

------------

# License
  
  [![Open Source Initiative Approved License logo](https://opensource.org/files/OSIApproved_100X125.png "Open Source Initiative Approved License logo")](https://opensource.org)

  Copyright (c) 2022, Martin Scheidt \<m.scheidt@tu-bs.de\> (ISC License)

  Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

  THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
[![tests](https://github.com/richlawson/ddev-pinecone/actions/workflows/tests.yml/badge.svg)](https://github.com/richlawson/ddev-pinecone/actions/workflows/tests.yml) ![project is maintained](https://img.shields.io/maintenance/yes/2025.svg)

## What is this?

This repository allows you to quickly install [Pinecone](https://www.pinecone.io/) into a [DDEV](https://ddev.readthedocs.io) project using `ddev get richlawson/ddev-pinecone`.

## Installation

For DDEV v1.23.5 or above run:
```sh
ddev add-on install richlawson/ddev-pinecone && ddev restart
```

For earlier versions of DDEV run:

```sh
ddev add-on install richlawson/ddev-pinecone && ddev restart
```
## Explanation

This Pinecone recipe for [DDEV](https://ddev.readthedocs.io) installs a [`.ddev/docker-compose.pinecone.yaml`](docker-compose.pinecone.yaml) using the [Pinecone Local Docker image with indexes](https://docs.pinecone.io/guides/operations/local-development#start-with-indexes).

## Interacting with Pinecone

* The Pinecone service will provide a serverless environment at port 5080.
* The Pinecone service will provide an index at port 5081.
* Configure your application to access the Pinecone index on the host:port `pinecone:5081`.

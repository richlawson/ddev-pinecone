# Archived
While this project will allow you to run Pinecone locally there are currently some incompatibilities with local Drupal indexing.

Since Pinecone can't be used in a non-cloud environment with the current tooling available, I'm archiving this project for now.

## What is this?

This repository allows you to quickly install [Pinecone](https://www.pinecone.io/) into a [DDEV](https://ddev.readthedocs.io) project using `ddev add-on install richlawson/ddev-pinecone`.

## Installation

For DDEV v1.23.5 or above run:
```sh
ddev add-on install richlawson/ddev-pinecone && ddev restart
```

For earlier versions of DDEV run:

```sh
ddev get richlawson/ddev-pinecone && ddev restart
```
## Explanation

This Pinecone recipe for [DDEV](https://ddev.readthedocs.io) installs a [`.ddev/docker-compose.pinecone.yaml`](docker-compose.pinecone.yaml) using the [Pinecone Local Docker image with indexes](https://docs.pinecone.io/guides/operations/local-development#start-with-indexes).

## Interacting with Pinecone

* The Pinecone service will provide a serverless environment at port `5080`.
* Create an index using cURL, which becomes available at port `5082` (the serverless configuration seems necessary even for the locally-hosted docker container):
```
curl -X POST "http://$PINECONE_LOCAL_HOST/indexes" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -H "X-Pinecone-API-Version: 2025-01" \
    -d '{
            "name": "dense-index",
            "vector_type": "dense",
            "dimension": 2,
            "metric": "cosine",
            "spec": {
                "serverless": {
                    "cloud": "aws",
                    "region": "us-east-1"
                }
            },
            "tags": {
                "environment": "development"
            },
            "deletion_protection": "disabled"
        }'
```
* Configure your application to access the Pinecone index on the host:port (`(https://${PROJNAME}.ddev.site:5082`, for example).

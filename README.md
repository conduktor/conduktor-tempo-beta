# Conduktor Tempo - private beta

You will need a private beta secret key to run this application.

During the private beta, Conduktor Tempo is accessible via a docker image. It requires a postgres instance.

## Running the application

- Option 1- Docker compose (app + postgres)

Perfect to test locally.

**To reach a kafka started on the host, you should use `host.docker.internal` instead of localhost**

Get the docker-compose.yml file in this repository, update the secret key with the one provided by your account manager, then just run

`docker-compose up`

To make sure you always have the latest version, use instead

`docker-compose pull && docker-compose up`

To stop the application, run

`docker-compose down`

- Option 2- Docker image

Use this if you want to deploy the application.

We provide the following image :

`ghcr.io/conduktor/tempo-beta:latest`

It will require a few env var :

- DB_HOST : host of the postgres db
- DB_PORT : port of the postgres db
- DB_DATABASE: name of the Postgres database
- DB_USER: the Postgres user
- DB_PASSWORD: the Postgres user password
- PORT : port of the http api
- GRPC_PORT : port of the grpc api, used by the CI runner
- ENV: must be "private_beta" to allow using the secret key

## Running the CI runner

The CI runner is currently available as a simple docker container. We'll provide more packaging options in a close future.

We provide the following image :

`ghcr.io/conduktor/tempo-ci-beta:latest`

You can find an example github action leveraging the runner in this repository.

You will need to provide a scenario_id (copied in the UI), and the host and port where the main application is reachable.

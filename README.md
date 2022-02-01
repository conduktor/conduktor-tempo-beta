# Conduktor Tempo - private beta

***Warning** : Due to some deep database changes, next release (0.5.0, planned for the 01 or 02 feb) will trigger a reset of the scenarios. From there we'll do our maximum to ensure backward compatibility and avoid any data lost.*


## Running the application

During the private beta, Conduktor Tempo is accessible via a docker image. You will need a secret key to run this application.

It also requires a postgres instance (included in Option 1).

> The default _Playground_ workspace and test case requires you to configure your cluster and create a "my-topic" topic before use

### Option 1- Docker compose (app + postgres)

---

**The simplest way to get started !**

Get the docker-compose.yml file in this repository, update the BETA_KEY env with the key provided by your account manager, then :

- To just start the app (not checking for new versions), run

`docker-compose up`

- To update or to make sure you're running the latest version, use

`docker-compose pull && docker-compose up`

- To stop the application, run

`docker-compose down`

Tempo will be available on http://localhost:8080 by default. You can change the port by changing the HTTP_PORT env var in the docker-compose file.

> Notes : To reach a kafka started on the host, you should use `host.docker.internal` instead of localhost

### Option 2- Docker image

---

We provide the following image :

`conduktorbeta/tempo-beta:latest`

It will require a few environment variables :

- DB_HOST : host of the postgres db
- DB_PORT : port of the postgres db
- DB_DATABASE: name of the Postgres database
- DB_USER: the Postgres user
- DB_PASSWORD: the Postgres user password
- HTTP_PORT : port of the http api, used to reach Tempo from your browser
- GRPC_PORT : port of the grpc api, used by the CI runner
- BETA_KEY: the secret key provided by your account manager

## Running the CI runner

The CI runner is currently available as a simple docker container. We'll provide more packaging options in a close future.

We provide the following image :

`conduktorbeta/tempo-ci:latest`

You can find an example github action leveraging the runner in this repository.

You will need to provide a scenario_id (copied in the UI), and the host and port where the main application is reachable.

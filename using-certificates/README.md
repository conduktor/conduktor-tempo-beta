## Using certificate stores

Tempo doesn't provide a way to load certificates via the UI right now. However it can be done easily using docker volumes.

The docker-compose file in this folder is configured to mount the local `./mount` folder to the `/data/tempo` folder inside the container.

Just drop your keystores/truststores in the `mount` folder and start the docker compose.

Then you can simply reference these files in the Additional properties of your cluster, eg
`ssl.keystore.location` = `/data/tempo/client.keystore.p12`

> _Note_ : make sure the mounted files allow Read access, for example using `chmod 644 ./filename`

Importing certificates in the CI runner can require a few more steps to prevent exposing them in version control, depending on the CI backend used.
We'll provide a github action soon. If you need another integration, please reach out so we can prioritize accordingly !

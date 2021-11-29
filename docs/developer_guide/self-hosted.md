# Self-Hosting Backend

## No Data Loss

Our number one design principle is to never have data loss.

All accounts of data loss will be documented publicly on our [GitHub Discussions](https://github.com/athensresearch/athens/discussions/categories/post-mortems).

Our last (and only) account of data loss was in February 2021 on our local-only version of Athens, before we made a public release, posted by a developer contributor.

When the self-hosted backend was in `alpha`, we had known issues of data loss, crashing, and freezing because the distributed events system being incomplete. We discovered and solved these issues internally as a team. We did not invite others to use this build during this period.

Now we are in `beta`, meaning we are ready to open up Athens for beta testers. We don't have known issues with data loss, crashing, and freezing anymore, and the first implementation of the distributed events system is complete. That said, we need to open this up to beta at this point because we need more real-world testing in a variety of contexts beyond our own team of six to go from `beta` to `stable`.

We invite feedback on anything and everything, don't be shy! We've created two new Discord channels, 2.0.0-beta and data loss at **2.0.0-beta-feedback** and **#data-loss**, respectively. [Join us on Discord!](https://discord.gg/avzDmq3nah)

## Client

To connect to an Athens server, you must know its remote address (an IP address, URL, or localhost) and its password. Skip to [server](#server) to setup a server first if you haven't yet.

You can connect to the backend through the DB Picker. Open the DB Picker with the button in the top left:

![db-picker-button](https://user-images.githubusercontent.com/8952138/142514926-f61c4070-f3b5-4ded-b8a4-2219c410a64d.png)

Go the **Join** tab and add the database name (give whatever name you want, it is only stored on the client), the remote address (which you can get from the server administrator), and the password (leave empty if no password). Then press the **Join** button.

![join-tab](https://user-images.githubusercontent.com/8952138/142514744-c87d95b9-ee6d-4f39-839f-75d2f8f1c5f9.png)

If the address and password match, congrats! You should be in a collaborative, self-hosted Athens! Read more

## Server

You can run Athens in your local environment, [Docker](#docker), or [DigitalOcean](#digitalocean). Setup docs do not yet exist for AWS or GCP, but feel free to contribute and add these!

### Custom Config

The default configuration can be found in `config.edn`.
You can customize it through the `config_edn` environment variable.

Here's an example on how to configure the server password using `config_edn`.
```
config_edn: "{:password "YourServerPassword"}"
```
The `config_edn` will be merged to other configs via deep merging.


### Running Athens Self-Hosted Server

Run the following commands in two different terminals:

``` shell
docker-compose up fluree
yarn server
```

The first command starts the Fluree database using docker to persist data.
If you set `:in-memory? false` in `dev/clj/config.edn` no data is persisted and this command is not needed.

The second command will start HTTP server on port 3010, unless you've modified `dev/clj/config.edn`.

Also nREPL server is started on port 8877, unless you've modified `dev/clj/config.edn`.


### Developing Athens Self-Hosted Server

Start REPL:

``` shell
yarn server:repl
```

Start the system:

``` clojure
(dev)
(start)
```

Same way you can start the system after `cider-jack-in`.

After starting HTTP & nREPL servers are running on default ports or changes in `config.edn`.

**Resetting the system**

``` clojure
(reset)
```

**Clean the Fluree DB**

Stop the Self-Hosted server. [ctrl+c] if using `yarn server` or [ctrl+d] if repl.
By default Fluree DB is stored in `./athens-data/fluree`, remove this folder,
start the server and Bob's your unkle.


## Docker

You can create an Athens server without installing anything else via docker compose.

At any point, if any of the services fails to launch or something seems broken, you have two options to debug.

1. You can run `docker-compose ps`  to see all running services. You should see that services `fluree`, `athens`, and `nginx` are "up" and/or "healthy". ![docker-ps-output](https://user-images.githubusercontent.com/8952138/142656719-21c54b94-8f50-4091-9044-a72bac1988a2.png)
2. Additionally, you can use `docker-compose logs SERVICE_NAME` to inspect what the problem is further.

Pick a [release](https://github.com/athensresearch/athens/releases) you'd like to use and download the `docker-compose.yml`. For example, for `v2.0.0-beta.3`:

```sh
curl -L -o docker-compose.yml https://github.com/athensresearch/athens/releases/download/v2.0.0-beta.3/docker-compose.yml
```
On Linux, `fluree` fails to launch if it does not have enough permissions for the `./athens-data` folder. The current workaround for this is to manually create the data folder and give all users of the machine read and write access. This is not a long-term workaround, and we will have more constrained permissions before Athens RTC is available for general release.

If you are on Mac, you can skip this workaround.
```
mkdir -p ./athens-data/fluree
chmod -R 777 ./athens-data/fluree
```

Then, start Docker Compose!

```
docker-compose up --detach
```

If you want to configure a password, you can override the app configuration via an environment variable:

```sh
CONFIG_EDN="{:password \"YourServerPassword\"}" docker-compose up
```

or via an `.env` file located in the same directory as the downloaded `docker-compose.yml`:

```sh
# .env
CONFIG_EDN="{:password \"YourServerPassword\"}"
```

Currently, the only server config we have is for the password. If you update the password, then clients that previously logged in will not have access unless. They must update the password on their end to get back in.

### Updating Docker
To update your deployment, curl the new `docker-compose.yml` file and restart docker-compose entirely:

```
# curl a new version of Athens described by docker-compose
curl -L -o docker-compose.yml https://github.com/athensresearch/athens/releases/download/v2.0.0-beta.3/docker-compose.yml

# restart docker-compose
docker-compose down
docker-compose pull
docker-compose up --detach
```


## DigitalOcean

Athens the team has tested the backend beta server on DigitalOcean the most, and not as much yet on other cloud providers like AWS or GCP.

A minimum of 4gb of memory is needed.

![image](https://user-images.githubusercontent.com/8952138/141150237-dce5f183-f25c-4a9b-9526-dcc310c09a44.png)

Use marketplace docker image: `docker 19.03.12 on Ubuntu 20.04` which has docker and docker-compose pre-installed.

![digital-ocean-docker-image](https://user-images.githubusercontent.com/8952138/141150155-7be8bce5-1804-431c-9cd0-4cf11e9c8d87.jpg)

If you resize your droplet image and have trouble opening the console, just wait a few minutes and refresh the Digital Ocean dashboard.

Once your droplet has been created, open the console to ssh to the server, follow the instructions in [Docker](#docker) to start the server, and copy and paste the IP address to your Athens client to connect to the server (and add a password if you configured one).

![digital-ocean-console-and-ip-address](https://user-images.githubusercontent.com/8952138/141150925-9f8df004-faa0-4fbe-9875-c276d60c5118.jpg)



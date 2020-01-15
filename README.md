# Logging HQ
This repository contains documentation and baseline setup of a Loki + Grafana service which serves as a centralized logging component of the Prior Art Archive.

The repository is driven by docker and involves the following:

1. An instance of [Loki](https://grafana.com/oss/loki/) which handles the collection of logs.
2. (SOON) An instance of [Grafana](https://grafana.com/) which handles the rendering of the logs.

## Setup
We're using [Docker](https://www.docker.com/) and `docker-compose` which will let you set up your own Prometheus server to make improvements and modifications to this repository.

To run the project locally:

```
docker-compose up
```

You can verify that Loki is running by checking [http://localhost:3100/ready](http://localhost:3100/ready).

## Building and Deploying

The project is run on [AWS ECS], which means in order to actually deploy you will need to [install the ecs-cli](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html).

You will also need read access to the following services:

1. [Our Docker organization](https://hub.docker.com/u/priorartarchive): `priorartarchive`
2. An AWS account with permission to interact with ECS

Once you've done that, this is how you would deploy a new version:

```
> docker-compose build
> docker-compose push
> ecs-cli compose service down --cluster prior-art-archive-logging
> ecs-cli compose service up --cluster prior-art-archive-logging
```

Note that `prior-art-archive-logging` can be whatever name you have set up.
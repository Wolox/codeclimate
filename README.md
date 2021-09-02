# Wolox Code Climate CLI

This is a fork from the [Codeclimate CLI](https://github.com/wolox/codeclimate).

## Overview

`codeclimate` is a command line interface for the Code Climate analysis
platform. It allows you to run Code Climate engines on your local machine inside
of Docker containers.

## Prerequisites

The Code Climate CLI is distributed and run as a
[Docker](https://www.docker.com) image. The engines that perform the actual
analyses are also Docker images. To support this, you must have Docker installed
and running locally. We also require that the Docker daemon supports connections
on the default Unix socket `/var/run/docker.sock`.

On macOS, we recommend using [Docker for Mac](https://docs.docker.com/docker-for-mac/).

### Usage

The above packages pull the docker image and install a shell script wrapper.
In some cases you may want to run the docker image directly.

To pull the docker image:

```console
docker pull codeclimate/codeclimate
```

To invoke the CLI via Docker:

```console
docker run \
  --env CODECLIMATE_CODE="${process.env.HOST_PATH}/projects/${repoName}" \
  --volume "${process.env.HOST_PATH}/projects/${repoName}":/code \
  --volume /var/run/docker.sock:/var/run/docker.sock \
  --volume /tmp/cc:/tmp/cc wolox/codeclimate \
  > "./projects/${repoName}/code_quality.json"

docker run \
  --interactive --tty --rm \
  --env CODECLIMATE_CODE="$PWD" \ # Path where the code to be checked is in the host
  --volume "$PWD":/code \ # Host code path --> container code path
  --volume /var/run/docker.sock:/var/run/docker.sock \
  --volume /tmp/cc:/tmp/cc \
  wolox/codeclimate
```

## Copyright

See [LICENSE](LICENSE)

# Docker Electrum-LTC

Docker image for [Electrum-LTC](https://electrum-ltc.org/).

## Build

```sh
git clone https://github.com/nickjer/dockerfiles
cd dockerfiles/electrum-ltc
docker build --force-rm -t nickjer/electrum-ltc .
```

## Usage

```sh
# First make the directory that will hold config files
mkdir ${HOME}/electrum-ltc

# Run the docker image
docker run --rm -i -t \
  -v "/etc/localtime:/etc/localtime:ro" \
  -v "/tmp/.X11-unix:/tmp/.X11-unix:ro" \
  -v "${HOME}/electrum-ltc:/data" \
  -e "DISPLAY=${DISPLAY}" \
  -u "$(id -u):$(id -g)" \
  nickjer/electrum-ltc
```

### Docker Compose

It is recommended to use [Docker Compose](https://docs.docker.com/compose/). An
example `docker-compose.yml` is seen as:

```yaml
version: "2"
services:
  ssr:
    image: "nickjer/electrum-ltc"
    volumes:
      - "/etc/localtime:/etc/localtime:ro"
      - "/tmp/.X11-unix:/tmp/.X11-unix:ro"
      - "${HOME}/electrum-ltc:/data"
    environment:
      DISPLAY: "${DISPLAY}"
    user: "1000:1000"
```

Then run:

```sh
docker-compose run --rm electrum-ltc
```

## How it Works?

### GUI Display

The options:

```sh
...
  -v "/tmp/.X11-unix:/tmp/.X11-unix:ro" \
  -e "DISPLAY=${DISPLAY}"
```

are necessary to get the GUI running in your display.

### Save Configuration

I create a directory:

```sh
mkdir ${HOME}/electrum-ltc
```

and mount this to the `/data` directory in the container for all the output:

```sh
...
  -v "${HOME}/electrum-ltc:/data"
```

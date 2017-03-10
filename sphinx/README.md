# Sphinx

Docker image for Sphinx.

## Build

You can build with:

```sh
docker build --force-rm -t <user>/sphinx:devel .
```

## Run

I recommend `docker-compose`. An example config file is:

```yaml
version: '2'
services:
  sphinx:
    image: "nickjer/sphinx:devel"
    volumes:
      - "${PWD}:/doc"
    working_dir: "/doc"
    user: "1000:1000"
```

Then run:

```sh
docker-compose run --rm sphinx <cmd>
```

For example:

```sh
docker-compose run --rm sphinx sphinx-quickstart
docker-compose run --rm sphinx make html
```

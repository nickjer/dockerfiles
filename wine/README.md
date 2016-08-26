# Wine

Super simple docker with wine.

## Build

You can build with:

```sh
docker build -t <user>/wine:devel .
```

## Run

I recommend `docker-compose`. An example config file is:

```yaml
version: '2'
services:
  wine:
    image: "<user>/wine:devel"
    volumes:
      - "/etc/localtime:/etc/localtime:ro"
      - "/tmp/.X11-unix:/tmp/.X11-unix"
      - "${HOME}/.wine:/wine"
    environment:
      WINEPREFIX: "/wine/prefix"
      WINEARCH: "win32"
      DISPLAY: "${DISPLAY}"
      HOME: "/wine"
    user: "1000"
```

You will need to create the directory ahead of time if you don't want `root`
owning it:

```sh
mkdir ${HOME}/.wine
```

You will also need to confirm the user id you want to run as is `1000`:

```sh
id -u
```

otherwise change it in the `docker-compose.yml` file.

Create the service:

```sh
docker-compose create wine
```

To initially set up your environment I recommend overriding the entry point
with `bash` and building it how you like:

```sh
docker-compose run --rm --entrypoint=/bin/bash wine
# wine wineboot --init
# winetricks
```

Then you can run your code as such:

```sh
docker-compose run --rm wine notepad.exe
```

or copy the `*.exe` to `${HOME}/.wine` and run it like...

```sh
docker-compose run --rm wine /wine/my-prog.exe
```

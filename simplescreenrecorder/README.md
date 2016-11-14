# SimpleScreenRecorder

Docker image for SimpleScreenRecorder.

## Build

You can build with:

```sh
docker build -t <user>/simplescreenrecorder:devel .
```

## Run

I recommend `docker-compose`. An example config file is:

```yaml
version: '2'
services:
  simplescreenrecorder:
    image: "nickjer/simplescreenrecorder:devel"
    volumes:
      - "/etc/localtime:/etc/localtime:ro"
      - "/tmp/.X11-unix:/tmp/.X11-unix:ro"
      - "/run/user/1000/pulse/native:/pulse/socket:ro"
      - "${HOME}/.config/pulse/cookie:/pulse/cookie:ro"
      - "${HOME}/.simplescreenrecorder:/home/simplescreenrecorder"
      - "${HOME}/Videos:/data"
    devices:
      - "/dev/snd:/dev/snd"
    environment:
      DISPLAY: "${DISPLAY}"
      HOME: "/home/simplescreenrecorder"
      PULSE_SERVER: "/pulse/socket"
      PULSE_COOKIE: "/pulse/cookie"
    working_dir: "/home/simplescreenrecorder"
    user: "1000:1000"
    pid: "host"
    ipc: "host"
```

In order for the display to work you must have:

```yaml
    volumes:
      - "/tmp/.X11-unix:/tmp/.X11-unix:ro"
    environment:
      DISPLAY: "${DISPLAY}"
    user: "1000:1000"
    ipc: "host"
```

This will run as you the user and connect to your X11 display. The `ipc: "host"`
is needed for the QT shared memory.

In order for sound to be recorded we will need to add ALSA:

```yaml
    devices:
      - "/dev/snd:/dev/snd"
```

as well as PulseAudio:

```yaml
    volumes:
      - "/run/user/1000/pulse/native:/pulse/socket:ro"
      - "${HOME}/.config/pulse/cookie:/pulse/cookie:ro"
    environment:
      PULSE_SERVER: "/pulse/socket"
      PULSE_COOKIE: "/pulse/cookie"
    pid: "host"
```

This will connect to the PulseAudio socket with your cookie for authorization.
The `pid: "host"` is needed so it can find the host PulseAudio server PID. This
may be overkill, but it works.

I also set a home directory so we can save any configurations we set:

```yaml
    volumes:
      - "${HOME}/.simplescreenrecorder:/home/simplescreenrecorder"
    environment:
      HOME: "/home/simplescreenrecorder"
    working_dir: "/home/simplescreenrecorder"
```

Last but not least, I set up a directory to store my video recordings:

```yaml
    volumes:
      - "${HOME}/Videos:/data"
```

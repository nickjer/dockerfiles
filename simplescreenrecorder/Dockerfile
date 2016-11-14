FROM ubuntu:xenial

# Add ppa:maarten-baert/simplescreenrecorder
RUN printf "deb http://ppa.launchpad.net/maarten-baert/simplescreenrecorder/ubuntu xenial main\ndeb-src http://ppa.launchpad.net/maarten-baert/simplescreenrecorder/ubuntu xenial main" > /etc/apt/sources.list.d/simplescreenrecorder.list && \
  apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 4DEDB3E05F043CA185176AC0409C8B51283EC8CD

# Install latest development version of wine
RUN apt-get update && \
  apt-get install --install-recommends -y simplescreenrecorder

ENTRYPOINT [ "simplescreenrecorder" ]

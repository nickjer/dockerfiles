FROM ubuntu:xenial

# Add ppa:wine/wine-builds
RUN printf "deb http://ppa.launchpad.net/wine/wine-builds/ubuntu xenial main\ndeb-src http://ppa.launchpad.net/wine/wine-builds/ubuntu xenial main" > /etc/apt/sources.list.d/wine.list && \
  apt-key adv --keyserver hkp://p80.pool.sks-keyservers.net:80 --recv-keys B59525092DF44DD0CE1D5D47E61A24DF77C899CB

# Install latest development version of wine
RUN dpkg --add-architecture i386 && \
  apt-get update && \
  apt-get install --install-recommends -y winehq-devel

# Install latest winetricks
RUN apt-get update && \
  apt-get install --no-install-recommends -y \
  cabextract \
  zenity \
  ca-certificates \
  curl && \
  curl https://raw.githubusercontent.com/Winetricks/winetricks/master/src/winetricks > /usr/local/bin/winetricks && \
  chmod +x /usr/local/bin/winetricks

ENTRYPOINT [ "wine" ]
